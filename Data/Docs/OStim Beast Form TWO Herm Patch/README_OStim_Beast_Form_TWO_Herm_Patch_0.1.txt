OStim Beast Form TWO Herm Patch 0.1
Optional add-on for TWO's herm / urta player werewolf
By That Guy (Coronerra)

Skyrim SE / AE · ESL-flagged optional addon · player-only


PLEASE READ: TESTING AND SUPPORT
================================
I am not going to test this myself. If you use TWO's herm or urta
werewolf, please test it and report any problems in the support section
of the OStim Beast Form Merged page on LoversLab:
https://www.loverslab.com/files/file/52768-ostim-beast-form-merged/

GitHub: https://github.com/Coronerra/OStim-Beast-Form-TWO-Herm-Patch


WHAT THIS IS
============
A small optional patch that adds OStim support for TWO Extras' player herm
and urta werewolf. It sits on top of either:

  - OStim Beast Form Merged 0.6 + OStim Beast Form Merged TWO Patch 0.1, or
  - OStim Beast Form TWO Edition 0.2

It is not a new edition and not a replacement for those plugins. The
published Merged 0.6, TWO Edition 0.2, and TWO Patch 0.1 plugins are not
edited. All new forms live in this patch's own ESL.

This zip ships no TWO meshes, textures, TRIs, scripts, or other TWO
assets. You must already own TWO 4.1 (Frosferes) and have TWO Extras
installed. The plugin only looks up TWO Extras at runtime.


REQUIREMENTS
============
Required:
  - TWO 4.1 Core, plus TWO Extras (WerewolvesExtras.esp), which adds the
    "Toggle Herm Werewolf" spell (TWO_ToggleHermPlayer)
  - One of:
      OStim Beast Form Merged 0.6 + TWO Patch 0.1
      OStim Beast Form TWO Edition 0.2
  - OStim Standalone (already required by Beast Form)

If you use Growl with Merged + TWO Patch, also install TWO's
WerewolvesExtrasGrowl.esp (Extras Growl patch). That is what makes TWO's
own herm/urta skin swap work under Growl. This patch does not need it as
a master, but Growl users still need it for the body.

If TWO Extras is not installed, this patch still loads and does nothing.
Regular female werewolves are unchanged.


HERM VS URTA
============
TWO's "Toggle Herm Werewolf" spell cycles a global (TWO_PlayerHermVal):

  0 = default female werewolf body (no penis) — this patch stays off
  1 = herm  — TWO swaps in its herm werewolf skin
  2 = urta  — TWO swaps in its urta werewolf skin

This patch treats herm and urta the same for OStim: both are a
female-sex player werewolf who also has a penis. The visual difference
between herm and urta is entirely TWO's, via TWO's own SkinSwap. This
patch does not touch that skin and does not ship those bodies.


WHAT IT DOES
============
TWO's herm/urta actor is still flagged as female, with no penis flag, so
OStim's Female werewolf property (penis: false) would win and male-
werewolf-role scenes would not be offered. This patch:

  1. Detects TWO Extras at runtime (Game.GetFormFromFile /
     GetModByName). WerewolvesExtras.esp is not a master.

  2. When the player is in werewolf form and the herm global is 1 or 2,
     adds a hidden ability from this plugin. A new OStim actor-property
     file matches that ability:

       type Werewolf
       sex  male   (so OStim.HasSchlong / IsFemale follow the penis;
                    AppearsFemale is still the actor's female sex)
       penis, testicles, vagina, breast, nipple, anus, mouth, hand, foot
       all true

  3. The condition perk's level is 50. OStim picks the highest perk
     level when more than one actor property of the same type matches.
     Beast Form's Female/Male properties are level 19 (OCR uses 20), so
     the herm property is the one OStim uses. The Female property is not
     edited or dispelled — it simply loses the priority check while the
     ability is on. Turning herm off (or reverting) removes the ability,
     and Female/Male behave as before.

  4. Aroused cock swap: OBL_Main only equips the addon when GetSex() is
     male. This patch equips the same existing addon for the herm/urta
     player, from whichever Beast Form plugin is loaded:
       Merged 0.6 + TWO Patch  — GT Softbody Addon_Dog_Black_Hard
       TWO Edition 0.2        — TWO's CanineRedHard path (already set
                                on that edition; this zip does not
                                include the mesh)
     It does not fight TWO's herm/urta body SkinSwap; it only adds the
     aroused addon the same way males get it. If OCreatures.esp is
     present, this patch steps aside and leaves the swap to OCR, the
     same way OBL_Main does.

  5. OCum Beast Load / Werewolf Shot: OCumBeastPie skips female-sex
     beasts. For the herm/urta player this patch runs the same male-
     style climax path by calling OCumBeastPie's public functions and
     the cum-shot event. The published script is not replaced.

  6. Player-only. TWO's herm global is driven by a player spell.
     Regular female werewolves (herm val 0, or Extras not installed)
     and NPC female werewolves are not changed.

Events: transform (OnRaceSwitchComplete), save load, and the herm
toggle spell / effect, so the flags update if you cycle the spell
while already transformed. No polling.


LOAD ORDER
==========
Put this plugin after Beast Form and TWO Extras. A typical order:

  Werewolves.esp                    (TWO Core)
  WerewolvesExtras.esp              (TWO Extras — required)
  WerewolvesExtrasGrowl.esp         (only if you use Growl)
  OStim_Beast_Form_Merged.esp       (or OStim_Beast_Form_TWO.esp)
  OStim_Beast_Form_Merged_TWO_Patch.esp   (Merged path only)
  OStim_Beast_Form_TWO_Herm_Patch.esp     (this patch)

Do not run TWO Patch and TWO Edition together.


OSTIM MCM
=========
Leave "Futas use male role" on (that is the default). With this patch's
actor property, OStim then treats the herm/urta player as having a
schlong, so intended-sex-only still offers male-werewolf-role scenes as
well as female-role ones. "Futas use male orgasm" (also on by default)
is what you want for climax handling.


FILES
=====
  OStim_Beast_Form_TWO_Herm_Patch.esp
  Scripts\OBFHerm_Main.pex
  Scripts\OBFHerm_PlayerAlias.pex
  Scripts\Source\         (Papyrus source)
  SKSE\Plugins\OStim\actor properties\OBLWerewolfHerm.json
  Docs\OStim Beast Form TWO Herm Patch\


KNOWN LIMITS
============
  - Toggling herm/urta in the middle of a scene will not rewrite that
    scene. Toggle before the scene starts.
  - If OCreatures (OCreatures.esp) is installed, OCR owns the aroused
    swap and this patch steps aside for it.
  - No new animations. Scenes that use a vagina and a penis at the same
    time do not exist for werewolves, so none are added.
  - Regular female werewolves (herm val 0, Aela, NPC female wolves) are
    unchanged and still have no penis.
  - Player-only.


CREDIT AND PERMISSIONS
======================
  That Guy (Coronerra) — this patch (plugin, scripts, actor property).
  Frosferes — TWO 4.1, including the Extras herm/urta feature and bodies.
    This zip contains none of those files.
  OStim Standalone, OCum, and the published Beast Form / TWO Patch /
    TWO Edition work remain their authors' and are not modified here.

That Guy (Coronerra)'s own work here is MIT licensed (see the GitHub
repository). TWO and every other third-party mod belong to their
authors.


WHAT TO CHECK IN GAME (PLEASE REPORT ON LOVERSLAB)
==================================================
This was built against the published plugins and TWO Extras' scripts and
FormIDs. It passed static checks, but I am not going to test it in game
myself. If you use TWO's herm or urta werewolf, please check these and
report any problems in the LoversLab support section (link at the top):

  - Cast "Toggle Herm Werewolf", transform, and confirm male-werewolf-
    role scenes are offered (and female-role / receiving scenes still
    are, when the animation exists). Cycle the spell while already
    transformed; the flags should update before the next scene.
    Toggling in the middle of a scene will not rewrite that scene.
  - Aroused addon appears on the herm/urta player in a scene and comes
    off afterwards, without replacing TWO's herm/urta body skin.
  - Climax / cum shot on a herm/urta player in a werewolf scene, if you
    use OCum and Beast Load.
  - Default female werewolf (herm val 0) still behaves exactly as
    before, including no penis on Aela and other female wolves.
  - Extras not installed: this plugin does nothing and the game is
    unchanged.

Scenes that need both a vagina and a penis in use at the same time
would need new animations. This patch does not add any.


CHANGELOG
=========
0.1  First public release. Optional ESL. Soft-detect TWO Extras and
     Beast Form (Merged or TWO Edition). Herm/urta actor property,
     aroused addon, and Beast Load / cum shot for the player only.
