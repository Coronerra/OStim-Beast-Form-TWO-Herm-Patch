># ⚠️ DEPRECIATED! ⚠️
> # GO TO (https://github.com/Coronerra/OStim-Beast-Form/)
>
> This project is no longer updated. **[OStim Beast Form Merged](https://github.com/Coronerra/OStim-Beast-Form-Merged)** replaces it: one download with one installer for Growl and TWO users, all on the TWO body. **Latest: [v0.8.1 release](https://github.com/Coronerra/OStim-Beast-Form-Merged/releases/tag/v0.8.1)** (always current: [latest release](https://github.com/Coronerra/OStim-Beast-Form-Merged/releases/latest)). Since 0.8 it is built for Lirael Atelier's [Werewolf and Vampire Lord OStim 0.2.3](https://www.patreon.com/LiraelAtelier/posts/werewolf-and-for-175434973), the recommended animation source.
>
> In the Merged installer, tick **Hermaphrodite patch (Fruta)**. It installs the same plugin, so remove this mod after installing Merged. I am still not going to test it myself; please report problems in the support section of the [OStim Beast Form Merged](https://www.loverslab.com/files/file/52768-ostim-beast-form-merged/) page on LoversLab. See [Updating](https://github.com/Coronerra/OStim-Beast-Form-Merged#updating).
>
> This repo and its old releases stay up for reference.

# OStim Beast Form TWO Herm Patch 0.1

> **Download:** [v0.1 release](https://github.com/Coronerra/OStim-Beast-Form-TWO-Herm-Patch/releases/tag/v0.1) → `OStim_Beast_Form_TWO_Herm_Patch_0.1.zip` (install with MO2).
> AI assistants: start with **[AI_CONTEXT.md](AI_CONTEXT.md)**. Build details: [BUILD_NOTES.md](BUILD_NOTES.md). License: [MIT for That Guy (Coronerra)'s work; third-party work belongs to its authors](LICENSE).

**Skyrim SE / AE · ESL-flagged optional add-on · player-only · for TWO's herm / urta player werewolf · by That Guy (Coronerra)**

---

## ⚠️ Testing and support

**I am not going to test this myself. If you use TWO's herm or urta werewolf, please test it and report any problems in the support section of the [OStim Beast Form Merged](https://www.loverslab.com/files/file/52768-ostim-beast-form-merged/) page on LoversLab.**

---

## Which download is for you?

This is an **optional add-on**. It does not replace anything. Pick your main setup first, then add this patch only if you use TWO Extras' herm or urta player werewolf.

| You use… | Get this |
|---|---|
| Growl + the HDT Werewolves / ABC look | **[OStim Beast Form Merged 0.6](https://github.com/Coronerra/OStim-Beast-Form-Merged)** ([v0.6 release](https://github.com/Coronerra/OStim-Beast-Form-Merged/releases/tag/v0.6)) on its own. This patch does not apply (it needs TWO). |
| Growl + Merged 0.6, with TWO 4.1 bodies | **Merged 0.6 + [Merged TWO Patch 0.1](https://github.com/Coronerra/OStim-Beast-Form-Merged-TWO-Patch)** ([v0.1 release](https://github.com/Coronerra/OStim-Beast-Form-Merged-TWO-Patch/releases/tag/v0.1)) |
| TWO 4.1, no Growl needed | **[OStim Beast Form - TWO Edition 0.2](https://github.com/Coronerra/OStim-Beast-Form-TWO)** ([v0.2 release](https://github.com/Coronerra/OStim-Beast-Form-TWO/releases/tag/v0.2)) |
| **Either TWO setup above, plus TWO Extras' herm or urta player werewolf** | **Add this patch (TWO Herm Patch 0.1)** on top. Optional. |

---

## What this is

A small optional patch that adds OStim support for **TWO Extras' player herm and urta werewolf**. It sits on top of either:

- **OStim Beast Form Merged 0.6 + OStim Beast Form Merged TWO Patch 0.1**, or
- **OStim Beast Form TWO Edition 0.2**

It is not a new edition and not a replacement for those plugins. The published Merged 0.6, TWO Edition 0.2 and TWO Patch 0.1 plugins are not edited. All new forms live in this patch's own ESL.

**This repository and its zip ship no TWO meshes, textures, TRIs, scripts or other TWO assets.** You must already own TWO 4.1 (Frosferes) and have TWO Extras installed. The plugin only looks up TWO Extras at runtime.

## Requirements

**Required**
- **TWO 4.1 Core, plus TWO Extras** (`WerewolvesExtras.esp`), which adds the "Toggle Herm Werewolf" spell (`TWO_ToggleHermPlayer`) and the herm / urta bodies.
- One of:
  - OStim Beast Form Merged 0.6 + Merged TWO Patch 0.1
  - OStim Beast Form TWO Edition 0.2
- OStim Standalone (already required by Beast Form).

**Growl users** (Merged + TWO Patch): also install TWO's **`WerewolvesExtrasGrowl.esp`** (the Extras-Growl patch). That is what makes TWO's own herm / urta skin swap work under Growl. This patch does not need it as a master, but Growl users still need it for the body.

The plugin's only master is `Skyrim.esm`. If TWO Extras is not installed, this patch still loads and does nothing. Regular female werewolves are unchanged.

## Herm vs urta

TWO's "Toggle Herm Werewolf" spell cycles a global (`TWO_PlayerHermVal`):

| Value | TWO look | This patch |
|---|---|---|
| 0 | default female werewolf body (no penis) | stays off |
| 1 | **herm**: TWO swaps in its herm werewolf skin | on |
| 2 | **urta**: TWO swaps in its urta werewolf skin | on |

This patch treats herm and urta the same for OStim: both are a female-sex player werewolf who also has a penis. The visual difference between them is entirely TWO's, through TWO's own skin swap. This patch does not touch that skin and does not ship those bodies.

## What it does

TWO's herm / urta actor is still flagged as female, with no penis flag, so OStim's Female werewolf property (penis: false) would win and male-werewolf-role scenes would not be offered. This patch:

1. **Detects TWO Extras at runtime** (`Game.GetFormFromFile` / `GetModByName`). `WerewolvesExtras.esp` is not a master.
2. **Adds an OStim actor property for herm / urta.** When the player is in werewolf form and the herm global is 1 or 2, it adds a hidden ability from this plugin. A new OStim actor-property file matches that ability: type `Werewolf`, sex `male` (so `OStim.HasSchlong` / `IsFemale` follow the penis; `AppearsFemale` still follows the actor's female sex), and penis, testicles, vagina, breast, nipple, anus, mouth, hand and foot all true.
3. **Wins the priority check cleanly.** The condition perk's level is 50. OStim picks the highest perk level when more than one actor property of the same type matches. Beast Form's Female/Male properties are level 19 (OCR uses 20), so the herm property is the one OStim uses. The Female property is not edited or dispelled; it just loses the priority check while the ability is on. Turning herm off (or reverting) removes the ability, and Female/Male behave as before.
4. **Aroused cock swap.** `OBL_Main` only equips the aroused addon when `GetSex()` is male. This patch equips the same existing addon for the herm / urta player, from whichever Beast Form plugin is loaded:
   - Merged 0.6 + TWO Patch: [GT Softbody](https://www.nexusmods.com/skyrimspecialedition/mods/152103) `Addon_Dog_Black_Hard`
   - TWO Edition 0.2: TWO's `CanineRedHard` path (already set on that edition; this zip does not include the mesh)

   It does not fight TWO's herm / urta body skin swap; it only adds the aroused addon the same way males get it. If `OCreatures.esp` is present, this patch steps aside and leaves the swap to OCR, the same way `OBL_Main` does.
5. **OCum Beast Load / Werewolf Shot.** `OCumBeastPie` skips female-sex beasts. For the herm / urta player this patch runs the same male-style climax path by calling `OCumBeastPie`'s public functions and the cum-shot event. The published script is not replaced.
6. **Player-only.** TWO's herm global is driven by a player spell. Regular female werewolves (herm value 0, or Extras not installed) and NPC female werewolves, including Aela, are not changed.

It reacts to events only (transform via `OnRaceSwitchComplete`, save load, and the herm toggle spell / effect), so the flags update if you cycle the spell while already transformed. No polling.

## Install (Mod Organizer 2)

1. Install TWO 4.1 Core and **TWO Extras** (and `WerewolvesExtrasGrowl.esp` if you use Growl).
2. Make sure one Beast Form setup is installed: Merged 0.6 + Merged TWO Patch 0.1, **or** TWO Edition 0.2. Never both.
3. Install `OStim_Beast_Form_TWO_Herm_Patch_0.1.zip` ("Install a new mod from archive").
4. Plugin order: put this plugin **after** Beast Form and TWO Extras. A typical order:
   ```
   Werewolves.esp                           (TWO Core)
   WerewolvesExtras.esp                     (TWO Extras, required)
   WerewolvesExtrasGrowl.esp                (only if you use Growl)
   OStim_Beast_Form_Merged.esp              (or OStim_Beast_Form_TWO.esp)
   OStim_Beast_Form_Merged_TWO_Patch.esp    (Merged path only)
   OStim_Beast_Form_TWO_Herm_Patch.esp      (this patch)
   ```
5. No Pandora / FNIS run is needed (no animations or behaviors are added).
6. In game, cast **"Toggle Herm Werewolf"** to pick herm or urta, then transform.

### OStim MCM
Leave **"Futas use male role"** on (that is the default). With this patch's actor property, OStim then treats the herm / urta player as having a schlong, so intended-sex-only still offers male-werewolf-role scenes as well as female-role ones. **"Futas use male orgasm"** (also on by default) is what you want for climax handling.

### Uninstall
Change back to human form, leave any scene, and save. Disable the plugin. The patch only adds a hidden ability, a perk, a quest and a magic effect of its own.

## Files in the zip

| File | What |
|---|---|
| `OStim_Beast_Form_TWO_Herm_Patch.esp` | ESL-flagged ESP, 4 records, master `Skyrim.esm` only |
| `Scripts\OBFHerm_Main.pex`, `Scripts\OBFHerm_PlayerAlias.pex` | Papyrus scripts |
| `Scripts\Source\` | Papyrus source |
| `SKSE\Plugins\OStim\actor properties\OBLWerewolfHerm.json` | OStim actor property for herm / urta |
| `Docs\OStim Beast Form TWO Herm Patch\` | README and static checks |

The same files are in [`Data/`](Data) in this repository.

## Known limits

- **Toggling herm / urta in the middle of a scene will not rewrite that scene.** Toggle before the scene starts.
- **If OCreatures (`OCreatures.esp`) is installed, OCR owns the aroused swap** and this patch steps aside for it.
- **No new animations.** Scenes that use a vagina and a penis at the same time don't exist for werewolves, so none are added.
- **Regular female werewolves are unchanged** (herm value 0, Aela, NPC female wolves) and still have no penis.
- Player-only.

## What to check in game (please report on LoversLab)

This was built against the published plugins and TWO Extras' scripts and FormIDs, and passed static checks ([STATIC_CHECKS_TWO_Herm_Patch_0.1.txt](Data/Docs/OStim%20Beast%20Form%20TWO%20Herm%20Patch/STATIC_CHECKS_TWO_Herm_Patch_0.1.txt)). **I am not going to test this myself. If you use TWO's herm or urta werewolf, please test it and report any problems in the support section of the [OStim Beast Form Merged](https://www.loverslab.com/files/file/52768-ostim-beast-form-merged/) page on LoversLab.** Worth checking:

1. Cast "Toggle Herm Werewolf", transform, and confirm male-werewolf-role scenes are offered (and female-role / receiving scenes still are, when the animation exists). Cycle the spell while already transformed; the flags should update before the next scene.
2. The aroused addon appears on the herm / urta player in a scene and comes off afterwards, without replacing TWO's herm / urta body skin.
3. Climax / cum shot on a herm / urta player in a werewolf scene, if you use OCum and Beast Load.
4. The default female werewolf (herm value 0) still behaves exactly as before, including no penis on Aela and other female wolves.
5. TWO Extras not installed: this plugin does nothing and the game is unchanged.

## Changelog

**0.1**
- First public release. Optional ESL. Soft-detects TWO Extras and Beast Form (Merged or TWO Edition). Herm / urta actor property, aroused addon, and Beast Load / cum shot for the player only.

## Permissions

- **This repository and its release ship none of TWO's meshes, textures, TRIs, plugins or scripts.** You must already own TWO 4.1 and TWO Extras (Frosferes, LoversLab). The scripts only look up TWO Extras' records at runtime.
- This patch is kept in **its own repository**, like the other TWO add-ons, so it can be removed without affecting the main [OStim Beast Form Merged](https://github.com/Coronerra/OStim-Beast-Form-Merged) project.
- That Guy (Coronerra)'s own work here (plugin records, scripts, actor property, docs) is MIT (see [LICENSE](LICENSE)). Third-party work belongs to its authors.

## Credits

- **Frosferes:** TWO - Total Werewolf Overhaul 4.1, including the Extras herm / urta feature and bodies. This patch contains none of those files.
- **OStim Standalone** and **OCum** authors: their work is used as-is and not modified here.
- Everyone credited in the [OStim Beast Form Merged README](https://github.com/Coronerra/OStim-Beast-Form-Merged).
- **That Guy (Coronerra):** OStim Beast Form, the Merged TWO Patch, the TWO Edition and this patch.
