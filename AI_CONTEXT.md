# AI_CONTEXT: how OStim Beast Form TWO Herm Patch works

For AI assistants, bots and modders. Everything written by That Guy (Coronerra) is MIT; third-party work belongs to its authors (see [LICENSE](LICENSE)). Read the main project's AI_CONTEXT first: [OStim-Beast-Form-Merged](https://github.com/Coronerra/OStim-Beast-Form-Merged/blob/main/AI_CONTEXT.md).

Support: the author does not test this patch himself. Problems go to the support section of the [OStim Beast Form Merged](https://www.loverslab.com/files/file/52768-ostim-beast-form-merged/) page on LoversLab.

## 1. Scope and sibling projects
- **This repo:** an optional ESL that makes OStim treat TWO Extras' herm / urta **player** werewolf as having a penis (plus vagina and breasts). Plugin `OStim_Beast_Form_TWO_Herm_Patch.esp`.
- Sits on **[OStim-Beast-Form-Merged](https://github.com/Coronerra/OStim-Beast-Form-Merged) 0.6 + [OStim-Beast-Form-Merged-TWO-Patch](https://github.com/Coronerra/OStim-Beast-Form-Merged-TWO-Patch) 0.1**, or on **[OStim-Beast-Form-TWO](https://github.com/Coronerra/OStim-Beast-Form-TWO) 0.2**. Never edits those plugins.
- Never add TWO files to this repo or its zip.

## 2. Repository layout
```
Data/OStim_Beast_Form_TWO_Herm_Patch.esp                     ESL, 4 records
Data/Scripts/*.pex, Data/Scripts/Source/*.psc                Papyrus
Data/SKSE/Plugins/OStim/actor properties/OBLWerewolfHerm.json
Data/Docs/OStim Beast Form TWO Herm Patch/                   README, static checks
BUILD_NOTES.md
```
The release zip is the contents of `Data/` plus the README at the zip root.

## 3. Plugin (ESL, master `Skyrim.esm` only)
| FormID | Type | EditorID | Content |
|---|---|---|---|
| xx000801 | MGEF | OBFHerm_ConditionEffect | condition marker effect |
| xx000802 | SPEL | OBFHerm_ConditionAbility | constant self ability carrying 801 |
| xx000803 | PERK | OBFHerm_WerewolfHermCondition | level 50; conditions: race `WerewolfBeastRace` (000CDD84) and HasMagicEffect 801 |
| xx000804 | QUST | OBFHerm_MainQuest | `OBFHerm_Main` + Player alias with `OBFHerm_PlayerAlias` |

Beast Form's Female/Male werewolf actor properties are perk level 19 (OCR 20); OStim picks the highest matching level, so 50 wins while the ability is on.

## 4. Runtime
- Soft-detects `WerewolvesExtras.esp` (`TWO_PlayerHermVal`, `TWO_ToggleHermPlayer`) via `Game.GetFormFromFile` / `GetModByName`.
- Herm value 1 (herm) or 2 (urta) while in werewolf form → add `OBFHerm_ConditionAbility`; otherwise remove it.
- Events only: `OnRaceSwitchComplete`, `OnPlayerLoadGame`, the toggle spell / effect (`OnSpellCast`, `OnMagicEffectApply`), and OStim mod events `ostim_thread_start` / `ostim_thread_end` / `ostim_actor_orgasm`. No polling.
- Aroused addon for the herm player via the loaded Beast Form plugin's existing swap path (Merged + TWO Patch: GT Softbody `Addon_Dog_Black_Hard`; TWO Edition: TWO `CanineRedHard`). Steps aside if `OCreatures.esp` is loaded.
- OCum: calls `OCumBeastPie`'s public functions and the cum-shot event for the herm player (that script skips female-sex beasts). The published script is not replaced.

## 5. Limits
Mid-scene toggles don't rewrite the running scene; no new dual-genital animations; regular / NPC female werewolves unchanged; player-only.

## 6. Rules for contributors
- Never add TWO, Growl, OStim, OCum or Beast Form files to this repo or its zip.
- Keep the FormIDs and the actor-property file name stable.
- Credit: That Guy (Coronerra); Frosferes for TWO and its Extras herm / urta feature.
