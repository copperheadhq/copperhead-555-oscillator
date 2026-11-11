# 3D models

Exported with KiCad 10.0.6 from `hardware/` at rev A (release commit `c822784`). Component bodies are generic KiCad library models, except SW1, which uses the EasyEDA model in `hardware/lib/ck_switches.3dshapes/`. They are not the exact manufacturer parts. Use them for fit, not for tolerance.

| File | For |
| --- | --- |
| `555-oscillator.step` | full model: tracks, pads, zones, silkscreen and mask |
| `555-oscillator-mechanical.step` | board and component bodies only; give this one to an enclosure designer |
| `555-oscillator.glb` | the full model for a web or Blender viewer |
| `555-oscillator.stl` | the assembled board as one mesh; GitHub previews it in 3D |
| `555-oscillator-board-only.stl` | bare outline with holes, for a fit-check print |

All parts are on the top side. J2 is a right-angle BNC whose barrel overhangs the right board edge; J1's USB-C opening faces the left edge. RV1 (25-turn trimmer, top adjust) and SW1 (top slide) are reached from above.
