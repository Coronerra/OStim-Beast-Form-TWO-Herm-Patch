# Build notes: OStim Beast Form TWO Herm Patch

## 0.1 (first public release)
- New ESL plugin, master `Skyrim.esm` only, 4 records (MGEF, SPEL, PERK, QUST). Written with a small Python record writer.
- Papyrus compiled with Caprica against vanilla, SKSE and OStim imports, plus small stubs for `OBL_Main`, `OCumBeastPie`, `OCumScript` and `MiscUtil` (so no Beast Form or OCum script is shipped or replaced).
- Actor property `OBLWerewolfHerm.json` points at perk 0x803 in this plugin.
- No animations or behaviours changed (no Pandora run needed). No meshes or textures.

Static checks (all pass): `Data/Docs/OStim Beast Form TWO Herm Patch/STATIC_CHECKS_TWO_Herm_Patch_0.1.txt`: ESL flag, masters, record list, VMAD script/property names, perk level and conditions, actor-property JSON, no TWO / mesh / texture / TRI files, no hard masters besides `Skyrim.esm`.

Release asset: `OStim_Beast_Form_TWO_Herm_Patch_0.1.zip`.
