# Project library

The one part KiCad 10 does not ship: the range switch SW1.

| Ref | Part | LCSC | Footprint | 3D model |
| --- | ---- | ---- | --------- | -------- |
| SW1 | C&K JS102011SCQN, SPDT top-slide, SMT | C221661 | `ck_switches.pretty/SW_SPDT_CK_JS102011SCQN.kicad_mod`, drawn for this project from the recommended PCB layout on sheet I-53 of the C&K JS Series datasheet (1.0 x 3.0 mm pads, 2.5 mm pitch) | `ck_switches.3dshapes/SW-SMD_JS102011SCQN.step`, fetched with easyeda2kicad from EasyEDA/LCSC, offset (0, +1.475, +0.625) mm on the footprint |

The 3D model is a vendor-community model for visual and enclosure checks, not a dimensional reference; the C&K datasheet is. `fp-lib-table` in `hardware/` points at this folder through `${KIPRJMOD}`.
