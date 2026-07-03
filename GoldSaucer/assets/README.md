# Bundled assets

## world_us.lgp (the self-contained world map)

`CraterBarrierPatcher` uses this file (deployed next to `GoldSaucer_GUI.exe` as
`assets/world_us.lgp`) instead of the builder's FF7 install, so every build ships
the same world-map edits no matter whose machine builds the mod. The barrier /
crater / field-51 / Highwind byte-patches are applied on top at build time.

If this file is absent, the patcher falls back to `<FF7 install>/data/wm/world_us.lgp`
and the mod will contain only vanilla `wm0.ev` (causing issues with Diamond WEAPON).

### Editing it

Future world-map changes go directly into this file: open it in ff7-landscaper,
make the edits, save, and commit it. Current contents: vanilla + the Diamond
map-boss scripts (touch -> `trigger_battle(980)` + `0xF29.1` cooldown;
`0xC1F.bit[1]` kill-gate on init/update/touch).

After editing, build once and check the log - a landscaper save recompiles
`wm0.ev` and shifts goto targets, so the byte-patch anchors in
`CraterBarrierPatcher.cpp` may need re-anchoring.
