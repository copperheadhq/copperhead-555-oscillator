# Board statistics: 5-v-variable-frequency-555-oscillator

Rev A, release commit **c822784** (design at 6d0c6c8); board `hardware/5-v-variable-frequency-555-oscillator.kicad_pcb`. KiCad 10.0.6.
Counted on 2026-11-11 with `kicad-cli pcb export stats` and from the board file as committed (zones filled). DRC run with zones refilled on a copy; nothing in `hardware/` is written.

## Board

| Field | Value |
| --- | --- |
| Outline | 60 mm x 35 mm |
| Thickness | 1.6 mm |
| Copper layers | 2: F.Cu, B.Cu |
| Copper pours | GND on both layers: F.Cu 1852.3 mm², B.Cu 1986.9 mm² of copper (KiCad's count, pours with tracks and pads) |
| Mounting holes | 2, M3 (3.2 mm, non-plated) |
| Silkscreen | front only: labels and the copperhead identity block; back is blank |

## Components

| Type | Front | Back | Total |
| --- | --- | --- | --- |
| smd | 20 | 0 | 20 |
| tht | 3 | 0 | 3 |
| unspecified (test pads, mounting holes) | 7 | 0 | 7 |
| total | 30 | 0 | 30 |

| Field | Value |
| --- | --- |
| By reference prefix | C 6, D 3, H 2, J 3, R 7, RV 1, SW 1, TP 5, U 2 |
| Through-hole parts | J2 (BNC), J3 (header), RV1 (trimmer) |
| JLCPCB BOM (`fab/rev-a/`) | **none**: all 23 parts are UNVERIFIED, so rev A is released as a bare PCB |
| Placement file | 23 parts |
| Left out of the placement file | TP1 to TP5, H1, H2 |

## Assembly and drilling

| Pads | Count |
| --- | --- |
| smd | 69 |
| through_hole | 13 |
| npth | 4 |

| Holes | Size | Plated | From |
| --- | --- | --- | --- |
| 18 | 0.3 mm | yes | Via |
| 3 | 0.8 mm | yes | Pad (RV1) |
| 2 | 1.0 mm | yes | Pad (J3) |
| 2 | 0.89 mm | yes | Pad (J2 signal and ground pins) |
| 2 | 2.01 mm | yes | Pad (J2 mounting posts) |
| 2 | 0.6 x 1.7 mm slot | yes | Pad (J1 shell) |
| 2 | 0.6 x 1.4 mm slot | yes | Pad (J1 shell) |
| 2 | 0.65 mm | no | Pad (J1 locating pegs) |
| 2 | 3.2 mm | no | Pad (H1, H2) |

35 holes in all, as in the drill file.

## Routing

| Field | Value |
| --- | --- |
| Nets | 15 |
| Vias | 18, all through |
| Track segments | 68, all on F.Cu; B.Cu is a GND plane |
| Track length | F.Cu 184.7 mm |
| Default net class | 0.25 mm track, 0.2 mm clearance |
| Custom rule (`.kicad_dru`) | via drill at least 0.3 mm |

| Track width (mm) | Segments | Length (mm) |
| --- | --- | --- |
| 0.2 | 6 | 4.3 |
| 0.25 | 29 | 87.8 |
| 0.3 | 15 | 17.4 |
| 0.4 | 18 | 75.3 |

## Checks

| Check | Result |
| --- | --- |
| DRC (zones refilled, schematic parity, all severities) | 4 violations: hole_clearance inside the J1 USB-C library footprint, waived |
| Unconnected items | 0 |
| Schematic parity | 7 issues: TP1 to TP5, H1, H2 are excluded from the BOM on the board but not on their symbols (no copper effect) |
| ERC | 0 violations |
| Zone refill | changes nothing: the copper gerbers are identical before and after |

The full DRC report is [`fab/rev-a/drc.json`](../fab/rev-a/drc.json).
