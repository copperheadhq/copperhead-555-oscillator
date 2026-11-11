# Design changelog

Append-only, newest first. One entry per committed copperhead run.

## 2026-11-11 — Move the whole front (F.SilkS) copperhead identity block 2.0 mm to the right (+x) and 1.0 mm down (+y), as one rigid group: the mark (ring and four ticks, centred at (121.5, 128.3)), the wordmark 'copperhead' (123.6, 128.3), '555 variable oscillator' (120.0, 130.7) and '5 V · 10 kHz–1 MHz · rev A' (120.0, 132.0). Keep sizes, strokes, justification and the left alignment unchanged. The person asked for it 'a bit down and to the right' in review; it stays inside the free area named in docs/BRIEF.md Design constraints. If DRC reports silk_edge_clearance or an overlap with J3, D3, H2 or its label at that offset, reduce the offset (prefer keeping the right shift, then shrink the down shift in 0.2 mm steps) and record the offset used. Do not change copper, tracks, vias, zones, footprints or any other label. Done when ERC and DRC are clean with no silk_over_copper, silk_overlap, silk_edge_clearance or text_height findings, and docs/LAYOUT.md's 'Front identity block' section shows the new positions.

- Change: fsilk-identity-block-shift-2r-1d
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean, DRC clean

## 2026-11-11 — front identity block shifted 2 mm right, 1 mm down

- Change: fsilk-identity-block-shift-2r-1d
- The F.SilkS identity block moved as one rigid group by (+2.0, +1.0) mm, at the person's review request ('a bit down and to the right'):
  - the mark (ring + 4 ticks) from (121.5, 128.3) to (123.5, 129.3);
  - `copperhead` from (123.6, 128.3) to (125.6, 129.3);
  - `555 variable oscillator` from (120.0, 130.7) to (122.0, 131.7);
  - `5 V · 10 kHz–1 MHz · rev A` from (120.0, 132.0) to (122.0, 133.0).
- The full offset was used: DRC showed no silkscreen findings, so no reduction was needed. Sizes, strokes, justification and left alignment are unchanged.
- No copper, track, via, zone, footprint or other label change. The schematic is untouched.
- Open: outputs/ gerbers are stale for silkscreen (DEVPLAN task 9).
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: DRC clean (0 unconnected, only the 4 waived J1 findings, no silk_over_copper/silk_overlap/silk_edge_clearance/text_height); ERC clean

## 2026-11-11 — Edit the front (F.SilkS) copperhead identity block, per the docs/BRIEF.md Design constraints line changed 2026-11-11: (1) delete the '2026-11' text; (2) left-align the block: the mark's left edge (ring plus left tick, now centred at (121.5, 128.3), about 3 mm across), the wordmark line and the two text lines '555 variable oscillator' and '5 V · 10 kHz–1 MHz · rev A' all start at the same x (the mark's left edge, about x 120). Make those two lines left-justified (justify left) at that x, keeping 0.8 mm height and 0.15 mm stroke; the wordmark 'copperhead' stays beside the mark, 1.0 mm. With the date gone, the two lines may move up slightly to sit evenly under the wordmark and further from the bottom edge. Keep everything off pads, test points, holes, J3, D3, H2 and its label, and clear of existing reference designators and labels. Do not change copper, tracks, vias, zones, footprints or any other label. Done when ERC and DRC are clean with no silk_over_copper, silk_overlap, silk_edge_clearance or text_height findings, and docs/LAYOUT.md's 'Front identity block' section shows the new positions and no date.

- Change: fsilk-identity-block-left-align-no-date
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean, DRC clean

## 2026-11-11 — front identity block: left-aligned, no date

- Change: fsilk-identity-block-left-align-no-date
- Per the BRIEF Design constraints line changed 2026-11-11:
  - deleted the F.SilkS text `2026-11`;
  - `555 variable oscillator` moved from (129, 130.9) centred to (120.0, 130.7), left-justified;
  - `5 V · 10 kHz–1 MHz · rev A` moved from (129, 132.2) centred to (120.0, 132.0), left-justified;
  - both stay 0.8 mm / 0.15 mm.
- x 120.0 is the mark's left edge. The mark at (121.5, 128.3) and the 1.0 mm `copperhead` wordmark at (123.6, 128.3) are unchanged.
- No copper, track, via, zone, footprint or other label change. The schematic is untouched.
- Open: outputs/ gerbers are stale for silkscreen (DEVPLAN task 9).
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: DRC clean (0 unconnected, only the 4 waived J1 findings, no silk_over_copper/silk_overlap/silk_edge_clearance/text_height); ERC clean; drift clean

## 2026-11-11 — Move the copperhead identity block from the bottom silkscreen (B.SilkS) to the top silkscreen (F.SilkS), per the docs/BRIEF.md Design constraints line changed 2026-11-11. Remove every B.SilkS item the change 'bottom identity block' (commit cb32fa5) added, so nothing of it remains on the back. On F.SilkS, not mirrored, draw the same content: the copperhead mark (a ring with four short ticks, about 3 mm across, from research/references/copperhead-branding/icon-transparent.svg) to the left of the lowercase wordmark 'copperhead', then '555 variable oscillator', '5 V · 10 kHz–1 MHz · rev A' and '2026-11'. Place it in the free area along the bottom board edge below RV1, U1 and TP4, to the right of D2/R6 and left of D3 and J3 (the person pointed at this area in the viewer). Keep every silk item off pads, test points and holes, and clear of the existing front labels and reference designators; text may be shrunk (not below 0.7 mm height, 0.15 mm stroke) or lines rearranged to fit, but not moved onto the back. Do not change copper, tracks, vias, zones, footprints or the other front labels. Done when ERC and DRC are clean with no silk_over_copper, silk_overlap or silk_edge_clearance findings, and docs/LAYOUT.md records the block on F.SilkS with its positions in place of the bottom block section.

- Change: fsilk-copperhead-identity-block
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean, DRC clean

## 2026-11-11 — copperhead identity block moved to the front silkscreen

- Change: fsilk-copperhead-identity-block
- Removed all 9 B.SilkS items of the bottom block (commit cb32fa5); B.SilkS is now empty.
- Added the same content on F.SilkS, not mirrored, in the bottom-edge strip below RV1/U1/TP4, between D2/R6 and D3/J3:
  - mark (3.0 mm ring + 4 ticks, 0.30 mm stroke) at (121.5, 128.3);
  - `copperhead` 1.0 mm, left-justified at (123.6, 128.3);
  - `555 variable oscillator` (129, 130.9), `5 V · 10 kHz–1 MHz · rev A` (129, 132.2), `2026-11` (129, 133.5), all 0.8 mm centred.
- 0.7 mm was tried for the two lower lines; DRC `text_height` (board minimum 0.8 mm) flagged it, so all lines are 0.8 mm.
- No copper, track, via, zone, footprint, refdes or other front label change. Schematic untouched.
- Open: outputs/ not re-exported (DEVPLAN task 9).
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: DRC clean (0 unconnected, only the 4 waived J1 findings, no silkscreen or text_height findings); ERC clean; drift clean

## 2026-11-11 — Add the copperhead identity block on the bottom silkscreen (B.SilkS), per docs/BRIEF.md Design constraints (line added 2026-11-11). Content, top to bottom: the copperhead mark (the fiducial: a ring with four short ticks at 0/90/180/270 degrees, geometry in research/references/copperhead-branding/icon-transparent.svg, drawn as B.SilkS graphic circle and lines, about 3 mm across) beside the lowercase wordmark 'copperhead'; then '555 variable oscillator'; then '5 V · 10 kHz–1 MHz · rev A'; then '2026-11'. All text on B.SilkS is mirrored as bottom-side text must be, so it reads correctly from the back. Place the block in the free central area of the 60 x 35 mm board, clear of the J1 (USB-C) and J2 (BNC) and J3 and SW1 through-hole pads, RV1 pads, the H1 and H2 mounting holes and all vias, with silk-to-pad and silk-to-edge clearance. Do not change the front silkscreen, copper, tracks, zones or any footprint. Done when ERC and DRC are clean with no silk_over_copper, silk_overlap or silk_edge_clearance findings, and docs/LAYOUT.md records the block and its position.

- Change: bsilk-copperhead-identity-block
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean, DRC clean

## 2026-11-11 — bottom-side copperhead identity block

- Change: bsilk-copperhead-identity-block
- Added B.SilkS board graphics per BRIEF Design constraints:
  - the copperhead mark, a 3.0 mm ring with four ticks, at (141.5, 102.3);
  - the mirrored texts `copperhead` (1.0 mm), `555 variable oscillator`, `5 V · 10 kHz–1 MHz · rev A` and `2026-11` (0.8 mm), centred at x 135–136, y 102.3–107.1.
- The block sits in the back-side-empty strip above U1/U2, clear of all THT pads, vias, holes and the edge.
- No front silkscreen, copper, track, via, zone or footprint change. The schematic is untouched.
- Open: outputs/ not re-exported (DEVPLAN task 9, together with the J2 spoke refill).
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: DRC clean (0 unconnected, only the 4 waived J1 findings, no silkscreen findings); ERC clean; drift clean

## 2026-11-11 — Change the F.SilkS board text 'probe shifts f' at (118.4, 110.6) to read 'probe shifts freq'. Keep it right-justified at the same anchor with the same 0.8 mm size and 0.15 mm stroke; the text grows to the left. Why: 'f' is cryptic to someone at the bench; the label warns that a probe on TP3 (TIMING) shifts the oscillator frequency (timing.node_loading, DEVPLAN TP3 row). Text change only: no footprint, pad, track, via, zone or net changes. Done when the new text stays inside the board outline, is at least 0.15 mm from every pad mask opening and every other silkscreen label (including D1, R1 and the 'TIMING' text), DRC keeps 0 unconnected with only the 4 waived J1 hole_clearance findings, ERC is unchanged, and docs (LAYOUT Silkscreen labels, BOM TP3 note, PINOUT TP3 row, DEVPLAN TP3 row) say 'probe shifts freq'.

- Change: silk-probe-shifts-freq
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/parts.intent.json, docs/BOM.md, docs/PINOUT.md, docs/DEVPLAN.md, docs/SUBSYSTEMS.md, docs/LAYOUT.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: ERC clean, DRC clean

## 2026-11-11 — TP3 silkscreen note 'probe shifts freq'

- Change: silk-probe-shifts-freq
- The F.SilkS board text at (118.4, 110.6) changes from `probe shifts f` to `probe shifts freq`. It keeps the same anchor, right justification, 0.8 mm size and 0.15 mm stroke, and grows about 2 mm to the left. Why: 'f' was cryptic at the bench; the note warns that a probe on TP3 (TIMING) shifts the frequency (`timing.node_loading`).
- No footprint, pad, track, via, zone or net change. The schematic is untouched.
- Docs now say 'probe shifts freq': LAYOUT Silkscreen labels, BOM TP3 note (through docs/parts.intent.json and draft_bom), PINOUT TP3 row, DEVPLAN TP3 row, SUBSYSTEMS TP3 row. Earlier CHANGELOG and DECISIONS entries keep the old text as history.
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/parts.intent.json, docs/BOM.md, docs/LAYOUT.md, docs/PINOUT.md, docs/DEVPLAN.md, docs/SUBSYSTEMS.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: DRC clean (0 unconnected, only the 4 waived J1 hole_clearance findings, no silkscreen findings); ERC clean; drift clean. The 0.15 mm clearance is a geometric estimate (text band y ≈ 110.2–111.0, nearest pad, refdes or label at y ≥ 111.4); no glyph-outline measurement was run here.

## 2026-11-11 — Widen the thermal relief spokes on J2's GND pads from 0.3 mm to 0.5 mm. J2 is the Amphenol B6252HB BNC (footprint Connector_Coaxial:BNC_Amphenol_B6252HB-NPP3G-50_Horizontal); its GND pads are all pads numbered 2 (the two 3.5 x 7.0 mm mounting lugs with 2.01 mm drills and the 1.6 x 2.5 mm ground pin with 0.89 mm drill). Set a pad-level thermal spoke (bridge) width override of 0.5 mm on those three board-instance pads only; keep thermal relief (not solid), keep the zone thermal gap 0.3 mm, and leave the zones' own thermal_bridge_width at 0.3 mm and the library footprint unchanged. Pad 1 (OUT) is not touched. Why: the BNC is the connector that is plugged and unplugged most, and wider spokes give its ground lugs a more robust connection to GND_F_pour and GND_B_plane while still relieving heat for hand soldering (BRIEF: the BNC may be hand-soldered; SPEC §5 ground return). Refill both GND zones after the change and save them filled. Verify: kicad-cli pcb drc --refill-zones shows 0 unconnected, no starved_thermal, and nothing beyond the 4 waived J1 hole_clearance findings; ERC unchanged. Record the override in docs/LAYOUT.md where J2/J3 GND spokes are described.

- Change: j2-gnd-spoke-width-0p5
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean, DRC clean

## 2026-11-11 — J2 GND thermal spokes 0.5 mm

- Change: j2-gnd-spoke-width-0p5
- Added a board-instance pad override `(thermal_bridge_width 0.5)` to J2's three GND pads (pad "2": both 3.5 × 7.0 mm lugs and the 1.6 × 2.5 mm ground pin), at the person's request: the BNC is plugged most, and wider spokes make its ground connection to `GND_F_pour` and `GND_B_plane` more robust while keeping relief for hand soldering.
- Unchanged: thermal relief (no `zone_connect`), the 0.3 mm thermal gap, both zones' `thermal_bridge_width 0.3`, J2 pad 1 (OUT), the library footprint, all other copper and the schematic.
- Open: the zones were **not** refilled or saved by a refill, because no tool here can do it. The saved fill and outputs/ gerbers still show 0.3 mm spokes at J2. Refill and save, run `kicad-cli pcb drc --refill-zones`, and re-export outputs/ (DEVPLAN task 9).
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: DRC (no refill) clean, only the 4 waived J1 hole_clearance findings; ERC clean, unchanged; `--refill-zones` NOT run

## 2026-11-11 — Fix crowded silkscreen reference labels on F.Silkscreen. Move only footprint Reference text fields and two board texts; no footprint, pad, track, via, zone or net changes, and keep text size 1.0 mm / 0.15 mm stroke. Why: a glyph-outline analysis found labels within 0.15 mm of pad mask openings or running into each other, which a fab may clip and which makes refdes ambiguous during hand assembly and bring-up (BRIEF: hand-soldered parts; LAYOUT 'Silkscreen labels'). Problems on the current board: SW1 label runs into the C3 label (0.09 mm); J1 label sits between R1 and R2 (0.17 mm from R2 pad 1); C6 and C4 labels sit between their pads and R4/R3 pads (0.08-0.12 mm); R4 and R3 labels read as 'R4R3'; D1 label touches the 'TIMING' text (0.21 mm); J2 label sits nearer R5's pads than J2's. New reference positions (x, y in mm, angle, justify): J1 (104.0, 124.0) 0 deg centre, below the connector; SW1 (130.0, 109.6) 0 deg centre, right of the switch body; TP3 (118.4, 113.4) 0 deg right-justified, left of its pad; C6 (122.2, 113.85) 90 deg centre and C4 (124.0, 113.85) 90 deg centre, above their parts; C3 (128.2, 113.7) 90 deg centre, right of C3; R4 (122.0, 123.9) 90 deg centre and R3 (124.0, 123.9) 90 deg centre, below their parts; J2 (153.0, 118.31) 0 deg centre, inside the J2 body outline between its mounting pads. Board texts (right-justified, otherwise unchanged): 'probe shifts f' to (118.4, 110.6) and 'TIMING' to (118.4, 111.8). Verified on a scratch copy of the current board: every reference label is at least 0.15 mm from every pad mask opening and other labels, and kicad-cli pcb drc --severity-all --refill-zones keeps 0 unconnected and only the 4 waived J1 hole_clearance findings. Update the Silkscreen labels section of docs/LAYOUT.md with the moved reference labels and why.

- Change: silk-refdes-declutter
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean, DRC clean

## 2026-11-11 — silkscreen reference labels de-cluttered

- Change: silk-refdes-declutter
- Moved the Reference fields of J1, SW1, TP3, C6, C4, C3, R4, R3 and J2 to the positions given by the person (docs/LAYOUT.md 'Reference labels moved'). TP3 is now right-justified.
- Moved the board texts `probe shifts f` to (118.4, 110.6) and `TIMING` to (118.4, 111.8); both stay right-justified, 0.8 mm.
- Why: a glyph-outline analysis found labels within 0.15 mm of pad mask openings or running together (SW1/C3, J1/R2, C6/C4 against R4/R3 pads, 'R4R3', D1/'TIMING', J2 nearer R5).
- No footprint, pad, track, via, zone or net change. Text sizes are unchanged. No '50 Ω' text added.
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: DRC clean (0 unconnected, only the 4 waived J1 findings; no refill here, the person's scratch-copy check with `--refill-zones` agrees); ERC clean; drift clean

## 2026-11-11 — Record the GND zone refill and re-export outputs from the refilled board (DEVPLAN pre-order tasks 6 and 8). Commit c6fb79e refilled and saved both GND zones (GND_F_pour, GND_B_plane) with kicad-cli pcb drc --refill-zones --save-board, at the person's request, after change timing-tie-45deg-under-u1. That commit moved no footprint, pad, track, via or zone outline (pcbnew object lists identical before and after). With the saved fill, DRC shows 0 unconnected, only the 4 waived J1 hole_clearance findings, no starved_thermal, and no via_dangling, including the 5 stitching vias at (137.2, 121), (140.3, 120.5), (143.9, 116.8), (143.9, 120.4) and (122.8, 124.3). (1) Docs only: mark DEVPLAN pre-order task 6 done with that result and commit; close risk 9 (J1 starved_thermal re-check) and the task 7 via_dangling check; update the zone-fill notes in docs/LAYOUT.md and DECISIONS so the saved fill is current; add a CHANGELOG line. (2) Re-export the outputs/ files that exist now from the current board: gerbers and drill, outputs/BOM.csv, board.step, board.svg, the outline DXF and the render. Do not change the board, schematic or zones; do not refill zones again. Leave tasks 2 and 3 (LCSC numbers, jlcpcb-bom.csv, CPL) as they are, and mark task 8 done only for what was re-exported. Verify: ERC clean, DRC 0 unconnected with only the 4 waived J1 findings, drift clean.

- Change: record-gnd-refill-reexport
- Files: outputs/, docs/DEVPLAN.md, docs/LAYOUT.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean, DRC clean

## 2026-11-11 — record GND zone refill; re-export outputs

- Change: record-gnd-refill-reexport
- Recorded the refill in commit c6fb79e. Both `GND_F_pour` and `GND_B_plane` were refilled and saved with `kicad-cli pcb drc --refill-zones --save-board`, and no object moved. The result: 0 unconnected, only the 4 waived J1 `hole_clearance` findings, no `starved_thermal`, and no `via_dangling`, including the 5 stitching vias.
- DEVPLAN:
  - task 6 is done;
  - the task 7 via_dangling check is closed;
  - risk 9 is closed;
  - task 8 is done only for the re-exported files, and `jlcpcb-bom.csv` and the CPL file (tasks 2 and 3) stay open.
- LAYOUT: the zone-fill notes now say the saved fill is current. The hand-patch caveats are marked superseded.
- Re-exported from the current board: gerbers, drill, outline DXF, board.step, board.svg and renders. outputs/BOM.csv was checked against docs/BOM.md and is unchanged.
- No board, schematic or zone change. No refill in this run.
- Files: docs/DEVPLAN.md, docs/LAYOUT.md, docs/DECISIONS.md, docs/CHANGELOG.md, outputs/*
- Verification: ERC clean; DRC 0 unconnected, only the 4 waived J1 findings; drift clean

## 2026-11-11 — Reroute the U1 pin 6 (THRES) to pin 2 (TRIG) link on net TIMING, F.Cu, so it follows the board's 45-degree routing convention (docs/LAYOUT.md, F.Cu routing uses 45-degree chamfers, commit e000c79). Today it is one 0.25 mm segment (126.525, 117.365)-(131.475, 118.635) at 14.4 degrees under the U1 body. Replace that one segment with three 0.25 mm F.Cu segments on net TIMING: (126.525, 117.365)-(128.365, 117.365), (128.365, 117.365)-(129.635, 118.635), (129.635, 118.635)-(131.475, 118.635): straight, a 45-degree step centred under U1, straight, the symmetric pattern other open 555 SOIC boards use (person's request after comparing renders, 2026-11-11). Copper-only: no placement, net, width, via, zone or schematic change; keep the TIMING_F_pour_keepout as it is. Refill both GND zones and save them filled. Verify: kicad-cli pcb drc --refill-zones gives 0 unconnected and nothing beyond the existing 4 J1 hole_clearance and 1 lib_footprint_issues findings; ERC unchanged. Record the change in docs/LAYOUT.md.

- Change: timing-tie-45deg-under-u1
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean, DRC clean

## 2026-11-11 — TIMING tie under U1: 45° step

- Change: timing-tie-45deg-under-u1
- The U1.6 → U1.2 TIMING tie was one 14.4° segment, (126.525, 117.365)–(131.475, 118.635). It is now three 0.25 mm F.Cu segments: (126.525, 117.365)–(128.365, 117.365), then a 45° step to (129.635, 118.635) centred under U1, then to (131.475, 118.635). Person's request after comparing renders, following the LAYOUT bend rule.
- Length ≈ 5.12 → ≈ 5.48 mm. The whole path stays inside `TIMING_F_pour_keepout`, which is unchanged.
- No placement, net, width, via, zone outline or schematic change. The saved fill did not overlap the new copper, so it was not patched.
- Open: the zone refill and `--refill-zones` DRC were requested but cannot be run here (DEVPLAN task 6). The `lib_footprint_issues` finding the request mentions did not appear in this run's DRC.
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: DRC clean (0 unconnected, only the 4 waived J1 findings), no refill; ERC clean

## 2026-11-11 — Add local GND stitching vias between GND_F_pour (F.Cu) and GND_B_plane (B.Cu), net GND, 0.6 mm pad / 0.3 mm drill like the existing vias. Purpose: a short layer-to-layer ground return for the output edges and no ungrounded F.Cu pour strips (SPEC §5 continuous ground; person's request after asking whether the board needs ground stitching, 2026-11-10). (1) Place 2 to 4 vias around J2's GND pin and near U2 (SN74LVC1G17 output buffer) and its output path to J2/J3, inside existing filled F.Cu pour, clear of all non-GND copper by the board rules. (2) Inspect the filled GND_F_pour: wherever a strip or island of it has no GND via, or joins the rest of the pour at one end only (a finger between tracks), add one via in it if it fits under the rules. Do not place vias in the TIMING_F_pour_keepout area or near the TIMING net (timing.node_loading). No perimeter via fence. No placement, track, net or schematic change. Each new via must sit in copper on both GND layers in the saved fill so DRC shows no via_dangling; if zones cannot be refilled here, say so and leave the refill as the existing DEVPLAN task 6. Verify: DRC 0 unconnected, no via_dangling, nothing beyond the 4 waived J1 hole_clearance findings; ERC unchanged. Update docs/LAYOUT.md (list the new vias with positions and why; close the open 'perimeter stitching vias every 5–8 mm' item as replaced by local stitching) and DECISIONS.

- Change: local-gnd-stitching-vias
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/CHANGELOG.md, docs/DECISIONS.md, outputs/
- Verification: ERC clean, DRC clean

## 2026-11-10 — local GND stitching vias

- Change: local-gnd-stitching-vias
- Added 5 GND vias (0.6 / 0.3 mm), at the person's request, for SPEC §5 continuous ground:
  - V1 (137.2, 121): F.Cu finger by U2 pin 4;
  - V2 (140.3, 120.5): finger by R5/R7/J3;
  - V3 (143.9, 116.8): above OUT, by J2's GND pin;
  - V4 (143.9, 120.4): below OUT, between J3 and J2;
  - V5 (122.8, 124.3): RV1/R4 pocket.
- V1, V2 and V5 fill F.Cu pour areas that previously had no via and joined at one end only.
- No via near TIMING or in its keepout, and no perimeter fence. The 'perimeter stitching vias' to-do is closed as replaced.
- No placement, track, net, zone or schematic change. The saved fill needed no patch, because each via is inside the fill on both layers.
- Open: the zone refill and `--refill-zones` DRC are still not runnable here (DEVPLAN task 6).
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/DECISIONS.md, docs/CHANGELOG.md, outputs/*
- Verification: DRC clean (0 unconnected, no via_dangling, only the 4 waived J1 findings); ERC clean

## 2026-11-10 — Chamfer the right-angle track bends and remove the acute +5V tee on F.Cu (research/layout/right-angle-bends/right-angle-bends.pdf).
Copper-only change on F.Cu: no placement, net, track-width, via, zone or schematic change.

1. Replace each of these 90-degree corners with a 45-degree chamfer of leg length c (mm), corner (x, y) in mm:
   #4  +5V      (132.800, 115.300)  c=0.3  -> (133.100, 115.300)-(132.800, 115.600)
   #5  +5V      (132.800, 116.095)  c=0.3  -> (132.500, 116.095)-(132.800, 115.795)
   #6  +5V      (136.000, 126.000)  c=1  -> (135.000, 126.000)-(136.000, 125.000)
   #7  /CAP_LO  (124.000, 112.000)  c=0.8  -> (124.000, 112.800)-(124.800, 112.000)
   #8  /CAP_LO  (125.600, 112.000)  c=0.8  -> (124.800, 112.000)-(125.600, 111.200)
   #9  /CC2     (108.500, 118.600)  c=0.3  -> (108.500, 118.900)-(108.800, 118.600)
   #10 /CC2     (108.500, 119.250)  c=0.3  -> (108.200, 119.250)-(108.500, 118.950)
   #11 /DIS     (124.000, 118.635)  c=0.6  -> (124.600, 118.635)-(124.000, 119.235)
   #13 CAP_HI   (120.600, 112.000)  c=0.8  -> (121.400, 112.000)-(120.600, 111.200)
   #14 CAP_HI   (122.200, 112.000)  c=0.8  -> (122.200, 112.800)-(121.400, 112.000)
   #16 RB_TRIM  (122.000, 122.445)  c=0.4  -> (122.000, 122.045)-(121.600, 122.445)
2. +5V tee near R2: delete the segment (112.4, 119.9)-(113.05, 119.25); extend the y=119.9 lane to (113.05, 119.9);
   split the x=113.05 trunk at (113.05, 119.9) and merge the now-collinear segments at (113.05, 119.25).
3. Leave the corners inside pads D1.1, C2.1, R3.2 and RV1.1 as they are.
4. Refill both GND zones and save them filled. Verify: kicad-cli pcb drc --refill-zones gives 0 unconnected
   and no new errors or warnings; ERC unchanged. Record in docs/LAYOUT.md that F.Cu routing uses
   45-degree chamfers, with no acute angles, and that pad-centre turns are allowed.

- Change: fcu-chamfer-bends-5v-tee
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/CHANGELOG.md, docs/DECISIONS.md, outputs/
- Verification: ERC clean, DRC clean

## 2026-11-10 — F.Cu 45° bend chamfers and +5V tee removal

- Change: fcu-chamfer-bends-5v-tee
- Chamfered 11 right-angle F.Cu corners per research/layout/right-angle-bends/right-angle-bends.pdf:
  - +5V #4, #5 and #6;
  - /CAP_LO #7/#8 and CAP_HI #13/#14 (each collinear pair merged into one diagonal);
  - /CC2 #9 and #10;
  - /DIS #11;
  - RB_TRIM #16.
- Removed the acute +5V tee near R2: the y = 119.9 lane now meets the x = 113.05 trunk at (113.05, 119.9).
- Pad-centre turns (D1.1, C2.1, R3.2, RV1.1) are left as they are. docs/LAYOUT.md records the rule: 45° chamfers, no acute angles, pad-centre turns allowed.
- No placement, net, width, via, zone outline or schematic change. TIMING is untouched.
- The saved `GND_F_pour` fill was cut back by hand at three new diagonals that it overlapped. The cuts are conservative.
- Open: the zones were **not** refilled or saved by a refill, because no tool here can do it. Refill and save, then run `kicad-cli pcb drc --refill-zones` before fab (DEVPLAN task 6).
- outputs/ re-exported.
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DEVPLAN.md, docs/DECISIONS.md, docs/CHANGELOG.md, outputs/*
- Verification: ERC clean; DRC on the saved fill clean apart from the 4 waived J1 findings; `--refill-zones` NOT run

## 2026-11-10 — Replace the range switch SW1 (C&K JS102011SAQN, right-angle, footprint Button_Switch_SMD:SW_SPDT_CK_JS102011SAQN) with the top-actuated C&K JS102011SCQN, as chosen in research/parts/range-switch.md and required by the brief's Parts line (slider moved from above; person's decision 2026-11-10). Use the committed project footprint lib/ck_switches.pretty/SW_SPDT_CK_JS102011SCQN.kicad_mod (pads from C&K datasheet sheet I-53: pads 1 and 3 at (-2.5, +2.5) and (+2.5, +2.5), pad 2 at (0, -2.5), each 1.0 x 3.0 mm), adding a project footprint library 'ck_switches' at ${KIPRJMOD}/lib/ck_switches.pretty to the footprint library table. Keep the schematic symbol Switch:SW_SPDT and the nets unchanged: pad 2 (common) = GND, pad 1 = /CAP_LO (C4), pad 3 = CAP_HI (C6), so the switch stays in the capacitors' ground return and off the TIMING trace (timing.range_switch, SPEC §3). Set MPN JS102011SCQN and LCSC C221661 in the BOM. Place SW1 near C4 and C6 on the top side, with at least 3 mm of clear board around the slider body so it can be pushed with a finger and no tall part (RV1, J2) beside it; the old position (123.1, 107) is fine if it fits. Route the three pads and keep GND connected to the planes. Align the 3D model ${KIPRJMOD}/lib/ck_switches.3dshapes/SW-SMD_JS102011SCQN.step (EasyEDA, origin may differ) so the body and leads sit on the pads, seating plane at z 0, and check numerically. The slider connects the common to the terminal on its own side (sheet I-53), so the slider at the pad-1 end selects LO: move the 'LO 10–100 kHz' and 'HI 100 kHz–1 MHz' silkscreen labels to the pad-1 and pad-3 ends respectively. Update research-derived text in docs (BOM, LAYOUT, DECISIONS, CHANGELOG, SPEC part mention). ERC must stay clean and DRC must show no new findings beyond the four waived J1 hole_clearance. Re-export outputs.

- Change: sw1-top-actuated-js102011scqn
- Files: fp-lib-table, 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/parts.intent.json, docs/BOM.md, 5-v-variable-frequency-555-oscillator.kicad_sch, outputs/, outputs/BOM.csv, docs/SPEC.md, docs/SUBSYSTEMS.md, docs/DEVPLAN.md, docs/LAYOUT.md, research/parts/range-switch.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean, DRC clean

## 2026-11-10 — SW1 → top-actuated C&K JS102011SCQN

- Change: sw1-top-actuated-js102011scqn
- SW1 is now the C&K JS102011SCQN (LCSC C221661, top slide), replacing the right-angle JS102011SAQN (brief Parts; research/parts/range-switch.md). Symbol `Switch:SW_SPDT` and nets are unchanged: pad 2 = GND, pad 1 = /CAP_LO, pad 3 = CAP_HI (`timing.range_switch`).
- Added `fp-lib-table` with the project library `ck_switches` (`${KIPRJMOD}/lib/ck_switches.pretty`). The footprint is `ck_switches:SW_SPDT_CK_JS102011SCQN` (sheet I-53 pads) and the SAQN NPTH pegs are removed.
- Placement is unchanged at (123.1, 107), 180°. The slider has ≥ 3 mm of clear board, and no tall part is beside it.
- The CAP_LO and CAP_HI traces are extended to the new pads at y 104.5. The GND stub and via at pad 2 are unchanged.
- 3D model: SW-SMD_JS102011SCQN.step, offset (0, +1.475, +0.625), checked numerically (docs/LAYOUT.md).
- Silkscreen: 'LO 10–100 kHz' (pad-1 end, right) and 'HI 100 kHz–1 MHz' (pad-3 end, left) moved to y 104.5.
- The schematic was re-drafted from the manifest (Value and Footprint fields only). docs/parts.intent.json was updated and BOM.md re-rendered. outputs/BOM.csv was updated and outputs/ re-exported.
- Open:
  - the `GND_F_pour` fill was hand-patched around SW1, so refill and save both zones before fab (DEVPLAN task 6);
  - confirm the SW1 direction with a meter;
  - inspect the 3D view once.
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, 5-v-variable-frequency-555-oscillator.kicad_sch, fp-lib-table, docs/parts.intent.json, docs/BOM.md, docs/LAYOUT.md, docs/SPEC.md, docs/SUBSYSTEMS.md, docs/DEVPLAN.md, docs/DECISIONS.md, docs/CHANGELOG.md, research/parts/range-switch.md, .copperhead/constraints.json, outputs/*
- Verification: ERC clean; DRC clean apart from the 4 waived J1 hole_clearance findings; legibility 0 errors; drift clean

## 2026-11-10 — Remove the B.Cu GND track network: all 24 B.Cu segments (net GND): the spine at x=102.5, the buses at y=103 and y=129.8, the riser at x=152.08, and their B.Cu branches to the GND vias and through-hole GND pads. The person asked for this after review. The network was added only because zones could not be filled at routing time (DECISIONS 2026-11-10, 'GND is connected by explicit tracks'). The GND zones GND_B_plane and GND_F_pour are now filled (commit 23aaf9f), so the tracks lie inside the plane and are redundant. Keep all 13 GND vias, the F.Cu GND stubs, all F.Cu tracks and both zones unchanged. No placement, net or schematic change. Refill both zones after the removal and save them filled. Verify with kicad-cli pcb drc --refill-zones: 0 unconnected items, and no new errors or warnings compared with before (including no via_dangling and no new starved_thermal). ERC unchanged. Update docs/LAYOUT.md and DECISIONS so GND connectivity is recorded as the filled zones plus the pad vias, superseding the explicit-track decision.

- Change: remove-bcu-gnd-track-network
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/CHANGELOG.md, docs/DEVPLAN.md, docs/DECISIONS.md
- Verification: ERC clean, DRC clean

## 2026-11-10 — remove B.Cu GND track network

- Change: remove-bcu-gnd-track-network
- Removed all 24 B.Cu GND segments, at the person's request after review:
  - the spine at x = 102.5;
  - the buses at y = 103 and y = 129.8;
  - the riser at x = 152.08;
  - their branches to the vias and the J2/J3 THT GND pads.
- Kept unchanged: the 13 GND vias, the F.Cu stubs, all F.Cu tracks, both zones, placement and nets. The schematic is untouched.
- GND connectivity is now the filled zones plus the pad vias. This supersedes the 'GND is connected by explicit tracks' decision.
- Open: the zones were not refilled or re-saved, because no tool here can refill. Before fab, refill and save, then run `kicad-cli pcb drc --refill-zones`.
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DECISIONS.md, docs/DEVPLAN.md, docs/CHANGELOG.md
- Verification: ERC clean; DRC on the saved fill clean (0 unconnected, only the 4 waived J1 findings, no via_dangling); the `--refill-zones` check is NOT run

## 2026-11-10 — Fix the missing 3D model on SW1 (C&K JS102011SAQN range switch, research/parts/range-switch.md). Its footprint Button_Switch_SMD:SW_SPDT_CK_JS102011SAQN points at ${KICAD10_3DMODEL_DIR}/Button_Switch_SMD.3dshapes/SW_SPDT_CK_JS102011SAQN.step, which KiCad 10 does not ship, so SW1 renders unpopulated in the 3D view and in outputs/board.step. Change only SW1's model path on the board to ${KIPRJMOD}/lib/ck_switches.3dshapes/SW-SMD_JS102011SAQN.step (committed, downloaded from EasyEDA for LCSC C221660). EasyEDA models use the EasyEDA footprint origin, so set the model offset and rotation so the switch body and its gull-wing terminals sit on SW1's KiCad pads, with the actuator facing the board edge as the footprint courtyard shows; check by exporting the board STEP or a 3D render. No copper, placement, net or schematic change. Re-export outputs/board.step and the renders. ERC and DRC must stay as they are.

- Change: sw1-3d-model-easyeda
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, outputs/, docs/DECISIONS.md, docs/LAYOUT.md, docs/CHANGELOG.md
- Verification: ERC clean, DRC clean

## 2026-11-10 — SW1 3D model (EasyEDA, LCSC C221660)

- Change: sw1-3d-model-easyeda
- SW1's model path changed from `${KICAD10_3DMODEL_DIR}/Button_Switch_SMD.3dshapes/SW_SPDT_CK_JS102011SAQN.step` to `${KIPRJMOD}/lib/ck_switches.3dshapes/SW-SMD_JS102011SAQN.step`. KiCad 10 does not ship the old file.
- Offset is (0, −0.475, +0.475) mm and rotation is (0, 0, 0). With that transform:
  - the pegs sit on the NPTH holes;
  - the seating plane is on the board;
  - the terminals sit on pads 1/2/3;
  - the actuator is on the courtyard-bulge side, toward the top board edge.
- The derivation is in docs/LAYOUT.md.
- No footprint, copper, placement, net or schematic change.
- Re-exported outputs/: gerbers, drill, outline.dxf, board.step (now contains SW-SMD_JS102011SAQN) and board.svg. The PCB SVG render is in .copperhead/renders/.
- Open: confirm visually in the KiCad 3D viewer. No 3D render could be inspected here.
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, outputs/*, docs/LAYOUT.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean; DRC unchanged (only the 4 waived J1 hole_clearance findings); drift clean

## 2026-11-10 — resolve design-state inconsistencies found by copperhead sync

- Change: sync-firmware-programmable-devices-doc
- Files: docs/SPEC.md, docs/SUBSYSTEMS.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean

## 2026-11-10 — sync: firmware.programmable_devices in docs

- Change: sync-firmware-programmable-devices-doc
- The sync verifier found that registry key `firmware.programmable_devices` (max 0) was not mentioned in any doc. It is now stated in:
  - docs/SPEC.md §1, as a new 'Programmable devices: none' bullet;
  - docs/SUBSYSTEMS.md 'Not present', on the MCU line.
- Documentation only. No value, budget or KiCad file changed.
- Files: docs/SPEC.md, docs/SUBSYSTEMS.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC and drift run

## 2026-11-10 — Write docs/DEVPLAN.md, the create pipeline's stage 8 deliverable (the pipeline stopped at stage 7 on a copperhead firmware-gate limitation: 74xGxx is missing from NON_PROGRAMMABLE_LIB, although firmware/README.md correctly says 'No firmware'). Contents: bring-up steps in order (current-limited 5 V first, then the timer, then the buffer and outputs, then each range end), the test points TP1–TP5 and what to meter first, the risk list, and the prototype order plan for about 5 boards assembled at JLCPCB. Include among the risks and pre-order tasks: all BOM lines are UNVERIFIED so outputs/jlcpcb-bom.csv is empty and there are no LCSC part numbers; there is no pick-and-place (CPL) file in outputs/; the J2 BNC is the substituted B6252HB-NPP3G-50; the J1 hole_clearance waiver; SW1's LO/HI direction must be confirmed with a meter on the first board; the four worst-case range endpoints in SPEC §3 must be measured, with the TLC555 delays pulling the HI top end down; and the ngspice check of the range ends that SPEC §8 lists as open. Do not touch the .kicad_pcb, .kicad_sch or .kicad_pro.

- Change: devplan-bringup-order
- Files: docs/DEVPLAN.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean, DRC clean

## 2026-11-10 — create pipeline stage 8: DEVPLAN

- Change: devplan-bringup-order
- Added docs/DEVPLAN.md. It is the stage 8 deliverable, written by hand because the pipeline stopped at stage 7 on a copperhead firmware-gate limitation: `74xGxx` is missing from NON_PROGRAMMABLE_LIB, although firmware/README.md correctly says "No firmware".
- Contents:
  - bring-up in order: unpowered checks including SW1 direction, then current-limited 5 V (30 mA limit), then the timer, then the buffer and outputs, then the four range ends;
  - TP1–TP5 and what to meter first;
  - a risk list;
  - the JLCPCB prototype order plan for about 5 boards.
- Risks and pre-order tasks recorded:
  - every BOM line is UNVERIFIED, so `outputs/jlcpcb-bom.csv` holds only its header row and there are no LCSC numbers;
  - outputs/ has no CPL file;
  - J2 is the substituted B6252HB-NPP3G-50;
  - the J1 hole_clearance waiver;
  - SW1 LO/HI direction is to be confirmed with a meter;
  - the SPEC §3 worst-case endpoints are to be measured, and TLC555 delays pull the HI top down;
  - the ngspice check (SPEC §8) is open.
- Documentation only. No .kicad_sch, .kicad_pcb or .kicad_pro was touched.
- Files: docs/DEVPLAN.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC, DRC and drift run on the unchanged sources

## 2026-11-10 — create pipeline stage: firmware

- Change: firmware-none-555-oscillator
- Files: docs/CHANGELOG.md, docs/DECISIONS.md, firmware/README.md
- Verification: ERC clean

## 2026-11-10 — create pipeline stage: firmware

- Change: firmware-none-555-oscillator
- Replaced the workspace template in firmware/README.md with a README headed "# No firmware". The template's pins.h and PINOUT.md rule is kept under "If this changes".
  - The board has no MCU or other programmable device (SPEC §1/§2, SUBSYSTEMS "Not present").
  - No HAL, pins.h or driver stubs were generated.
- Two schematic libraries are outside the stage allowlist, and the README flags both:
  - `74xGxx` (U2 SN74LVC1G17, fixed-function logic);
  - `copperhead_power` (engine-synthesized power symbols).
  - Neither is programmable.
- No .kicad_sch, .kicad_pcb or .kicad_pro was touched. No toolchain was needed, so no DEVPLAN.md entry.
- Files: firmware/README.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC and drift run this stage

## 2026-11-10 — create pipeline stage: outputs

- Change: outputs-package
- Files: outputs/, outputs/BOM.csv, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean, DRC clean

## 2026-11-10 — create pipeline stage: outputs

- Change: outputs-package
- Gates before export:
  - ERC clean.
  - DRC clean apart from the 4 waived J1 `hole_clearance` findings (docs/LAYOUT.md Waiver). Zones are filled (commit 23aaf9f).
- outputs/ contents (checked by file signature after export):
  - `gerbers/`: 20 Gerber X2 files (KiCad 10.0.6, Protel extensions), including F/B Cu, Mask, Paste, Silkscreen and Edge_Cuts. Courtyard, Fab, Adhesive, Margin and User layers are also exported; JLCPCB ignores them.
  - `gerbers/5-v-variable-frequency-555-oscillator.drl`: one Excellon (M48) drill file, MixedPlating (PTH and NPTH together), which JLCPCB accepts.
  - `outline.dxf/5-v-variable-frequency-555-oscillator-Edge_Cuts.dxf`: `outline.dxf` is a directory, not a single file.
  - `board.step`.
  - `board.svg` (PCB render).
  - `renders/5-v-variable-frequency-555-oscillator.svg` (schematic render).
  - `export_outputs` reported a `schematic.svg`, but no file by that name exists. The schematic render is the `renders/` file above.
  - No SVG was found under .copperhead/renders/ by search. That search may skip dot-directories, so it is unconfirmed either way.
  - Not produced (not requested): JLCPCB CPL / pick-and-place file and LCSC part numbers. Both are needed for a JLCPCB PCBA order.
- outputs/BOM.csv: an ordering BOM (refdes, MPN, qty) made from docs/BOM.md.
  - Grouped by MPN: 19 lines, 23 placed parts.
  - TP1–TP5 and H1–H2 are left out on purpose: they are bare pads and holes, so there is nothing to buy.
  - Every MPN is still UNVERIFIED against distributor stock (SPEC §8).
  - No "50 Ω" anywhere (`output.load`).
- Open before ordering:
  - The ngspice check of the four range ends (SPEC §8) has not been run.
  - Perimeter stitching vias are not added yet. They are optional and do not block fab.
  - Confirm the SW1 LO/HI direction on the first board.
  - JLCPCB DFM may flag the J1 holes; answer with the waiver.
- No .kicad_sch, .kicad_pcb or .kicad_pro was touched.
- Files: outputs/*, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean; DRC clean (only the 4 waived J1 findings); every export succeeded; drift clean

## 2026-11-10 — Documentation only: in docs/LAYOUT.md replace the 'Library-footprint findings (not fixable here)' paragraph with a recorded waiver for the 4 hole_clearance findings inside J1 (GCT USB4105-GF-A): pads A1, A12, B1, B12 [GND] sit 0.1944 mm from the footprint's own NPTH locating holes against the 0.25 mm board rule. Accepted because: it is GCT's recommended land pattern in the stock KiCad footprint; the copper is J1's own GND pads, so a drill nick cannot short anything; JLCPCB's capabilities page (https://jlcpcb.com/capabilities/Capabilities, read 2026-11-10) lists 0.2 mm NPTH-to-track minimum, so this is 6 µm under. Also record in docs/LAYOUT.md that the GND zones are now filled (commit 23aaf9f, kicad-cli --refill-zones, 0 unconnected) and remove the 'run Fill All Zones before fab' to-do. Record the waiver in DECISIONS. Do not touch the .kicad_pcb, .kicad_sch or .kicad_pro.

- Change: j1-hole-clearance-waiver-zones-filled
- Files: docs/LAYOUT.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean, DRC clean

## 2026-11-10 — J1 hole_clearance waiver; zones filled

- Change: j1-hole-clearance-waiver-zones-filled
- docs/LAYOUT.md: the 'Library-footprint findings' note is replaced by a recorded waiver for the 4 J1 `hole_clearance` findings.
  - The finding: pads A1, A12, B1 and B12 (GND) sit 0.1944 mm from the footprint's NPTH holes, against the 0.25 mm rule.
  - The basis: it is GCT's recommended land pattern; the copper is only J1's own GND; JLCPCB's minimum is 0.2 mm NPTH-to-track, so this is ≈ 6 µm under.
- docs/LAYOUT.md: the GND zones are recorded as filled (commit 23aaf9f, `--refill-zones`, 0 unconnected). The 'Fill All Zones before fab' to-do is removed. Perimeter stitching vias stay open.
- Documentation only. No .kicad_pcb, .kicad_sch or .kicad_pro was touched.
- Files: docs/LAYOUT.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: DRC clean (only the 4 waived J1 hole_clearance findings); ERC and drift run

## 2026-11-10 — Add the F.SilkS labels required by docs/SPEC.md §5 'Silkscreen' and the timing.range_switch constraint. Answers to the previous run's questions: (a) SW1 direction: research/parts/range-switch.md records from the C&K datasheet (sheet I-52) that the JS102011SAQN actuator connects the common pin 2 to the terminal on its own side; on this board pad 1 (/CAP_LO) is at x≈125.6 mm and pad 3 (CAP_HI) at x≈120.6 mm, so the slider at the right selects LO and the slider at the left selects HI. Put 'LO 10–100 kHz' on the right-hand side of SW1 and 'HI 100 kHz–1 MHz' on the left-hand side. (b) Label TP5 'OUT', not BUF: it is on net OUT after R5, matching SPEC §4. Also: at RV1 'CW = f ↑' (TIMING on pad 3, wiper tied to pad 1; clockwise moves the wiper toward pin 3 per the Bourns 3296 datasheet, so it lowers R_B and raises f); 'OUT (Hi-Z)' at J2; 'SIG' and 'GND' at the J3 pins; test-point names 5V, GND, TIMING, RAW, OUT at TP1–TP5; 'probe shifts f' near TP3. Never write '50 Ω' anywhere (SPEC §7). Use text at least 0.8 mm high with a 0.15 mm stroke, keep every label off pads and inside the board outline, and do not move any footprint or change any copper. Done when ERC and DRC stay clean with no silkscreen-over-pad or silkscreen-clipped findings, and docs/LAYOUT.md lists each label.

- Change: silkscreen-labels
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/SUBSYSTEMS.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean, DRC clean

## 2026-11-10 — silkscreen labels

- Change: silkscreen-labels
- Added 12 F.SilkS text labels (≥ 0.8 mm high, 0.15 mm stroke):
  - `LO 10–100 kHz` right of SW1 and `HI 100 kHz–1 MHz` left of SW1, per research/parts/range-switch.md (`timing.range_switch`);
  - `CW = f ↑` at RV1;
  - `OUT (Hi-Z)` at J2;
  - `SIG` and `GND` at the J3 pins;
  - `5V`, `GND`, `TIMING`, `RAW` and `OUT` at TP1–TP5;
  - `probe shifts f` at TP3.
- No "50 Ω" anywhere (`output.load`). No footprint moved and no copper changed.
- docs/SUBSYSTEMS.md silkscreen list updated to match (J3 is labelled SIG/GND rather than "OUT (Hi-Z)").
- Open: confirm the SW1 direction with a meter on the first assembled board.
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/SUBSYSTEMS.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: ERC clean; DRC clean (only the 4 known J1 hole_clearance library findings; no silkscreen findings)

## 2026-11-10 — Set the zone connection of J1 (USB4105-GF-A) GND pads A1, A12, B1 and B12 to solid (full) connection to the GND pours, instead of thermal relief. Reason: with the zones filled, 'kicad-cli pcb drc --refill-zones' reports 4 starved_thermal errors on exactly these pads against zone GND_F_pour on F.Cu (the fine pin pitch leaves too few spokes). Solid connection is the usual treatment for USB-C GND pins and serves the SPEC §5 ground-plane requirement. Do not move any footprint or change any route. Note: run_drc here does not refill zones, so it cannot show this finding; done when ERC and DRC stay clean and the four pads' zone connection is solid. Update docs/LAYOUT.md.

- Change: j1-gnd-solid-zone-connect
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: ERC clean, DRC clean

## 2026-11-10 — J1 GND pads solid zone connection

- Change: j1-gnd-solid-zone-connect
- J1 pads A1, A12, B1, B12 (GND) get a board-level `(zone_connect 2)` (solid) override instead of thermal relief.
  - Reason: `kicad-cli pcb drc --refill-zones` reported 4 `starved_thermal` errors on these pads against `GND_F_pour` (F.Cu).
  - Solid is the usual treatment for USB-C GND pins and serves the SPEC §5 ground plane.
- No footprint, track, via or zone moved. The library footprint is unchanged.
- Open: `run_drc` here does not refill zones. Confirm that no `starved_thermal` remains with `--refill-zones` (or Fill All Zones + DRC in KiCad) before fab.
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: ERC clean; DRC clean (only the 4 known J1 hole_clearance library findings); drift clean

## 2026-11-10 — Route the board so it has no unrouted connections: complete all 46 connections left as ratsnest in docs/LAYOUT.md, and add a continuous GND pour on B.Cu under the oscillator and output path (SPEC §5 ground-plane requirement, brief Design constraints), plus a GND pour on F.Cu with stitching vias. Do not move any footprint: the person reviewed and approved the placement on 2026-11-10. Keep the TIMING net (U1 pins 2/6, RV1, C4, C6) as short as possible and away from BUF_OUT/OUT (timing.node_loading, brief Design constraints). Use JLCPCB two-layer rules. Done when DRC reports zero unrouted connections and no new errors, ERC stays clean, and docs/LAYOUT.md is updated. The 4 J1 hole_clearance findings inside the USB4105 library footprint are out of scope.

- Change: route-board-gnd-pours
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean, DRC clean

## 2026-11-10 — route board and GND pours

- Change: route-board-gnd-pours
- Routed every remaining connection (46 → 0) with JLCPCB two-layer rules, and moved no footprint.
  - The TIMING tie U1.6 → U1.2 is one straight segment of about 5.1 mm.
  - RAW, BUF_OUT and OUT run on the far side of U1.
  - +5V is 0.4 mm on F.Cu only.
- GND: an SMD stub and a via at every SMD GND pad, onto a B.Cu track network.
- Zones: a full-board B.Cu GND zone, a full-board F.Cu GND zone, and an F.Cu pour keepout over TIMING. Inter-layer stitching comes from the 13 GND pad vias.
- 16 perimeter stitching vias were added and then removed: with the F.Cu pour unfilled they were dangling on F.Cu and failed DRC.
- Open:
  - the zones are saved unfilled, so fill all zones in KiCad before fab export;
  - add perimeter stitching vias after the fill.
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: DRC clean, 0 unrouted (only the 4 known J1 hole_clearance library findings); ERC clean

## 2026-11-10 — create pipeline stage: layout-draft

- Change: layout-draft-555-oscillator
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: ERC clean, DRC clean

## 2026-11-10 — create pipeline stage: layout-draft

- Change: layout-draft-555-oscillator
- Outline resized to 60 × 35 mm.
- Placement: J1 on the left edge, J2 BNC on the right edge, H1 and H2 at opposite corners, the U1 timing cluster in the centre, and U2 and the outputs toward J2.
- Routed on F.Cu: TIMING (≈ 8 mm, with the TP3 stub), DIS, CAP_LO, CAP_HI, and +5V for U1.8/C2/R3.
- Moved reference labels to clear silkscreen overlaps.
- Unrouted: 46 connections (from 56).
- Open: GND pour, rest of +5V, silkscreen range/output labels. DRC lists 4 J1 hole_clearance findings inside the library footprint (see docs/LAYOUT.md Draft quality).
- Files: 5-v-variable-frequency-555-oscillator.kicad_pcb, docs/LAYOUT.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: DRC clean (apart from library-footprint findings); ERC and drift run this stage

## 2026-11-10 — create pipeline stage: schematic

- Change: schematic-555-oscillator
- Files: schematic.intent.json, 5-v-variable-frequency-555-oscillator.kicad_sch, docs/PINOUT.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean

## 2026-11-10 — create pipeline stage: schematic

- Change: schematic-555-oscillator
- Wrote schematic.intent.json (30 parts, 15 nets) and drafted the sheet on A3 with draft_schematic. There are 7 groups, one per SUBSYSTEMS heading.
- Nets: +5V, GND, CC1, CC2, DIS, RB_TRIM, TIMING, CAP_LO, CAP_HI, CONT, RAW, BUF_OUT, OUT, LED_PWR, LED_ACT.
- TIMING carries only RV1.3, C4, C6, U1 pins 2 and 6, and TP3. SW1's common (pin 2) is on GND, and its throws go to CAP_LO and CAP_HI.
- No-connects: J1 D+, D−, SBU1 and SBU2; U2 pin 1.
- Added docs/PINOUT.md.
- Open: verify_symbols reports the power symbols that draft_schematic synthesizes (+5V, GND, PWR_FLAG) as being in library copperhead_power and not power. The engine owns these, and the drafted sheet cannot be edited by hand. ERC is clean.
- Open: ngspice check of the four range ends (SPEC §8) not run yet.
- Files: schematic.intent.json, 5-v-variable-frequency-555-oscillator.kicad_sch, docs/PINOUT.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC clean; legibility 0 errors and 1 advisory (a long cross-group wire); drift clean

## 2026-11-10 — create pipeline stage: part-selection

- Change: part-selection-555-oscillator
- Files: docs/parts.intent.json, docs/BOM.md, docs/SUBSYSTEMS.md, docs/SPEC.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC not required

## 2026-11-10 — create pipeline stage: part-selection

- Change: part-selection-555-oscillator
- Wrote docs/parts.intent.json (30 parts) and rendered docs/BOM.md with draft_bom.
- SW1 is the C&K JS102011SAQN.
- J2 is the B6252HB-NPP3G-50, substituted for 31-5536-RFX, which has no installed footprint. The installed 031-6575 footprint has pads 3 and 4 with no symbol pin.
- D1 is drawn as Device:D_TVS on SOD-523.
- Current: no change to the ≈ 14.7 mA upper bound. The quiescent and leakage currents of the chosen parts sit inside the existing allowances.
- Files: docs/parts.intent.json, docs/BOM.md, docs/SUBSYSTEMS.md, docs/SPEC.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: draft_bom clean; check_drift run; ERC not required (no schematic)

## 2026-11-10 — The brief (docs/BRIEF.md, commit b6ced00) changed from one frequency range to two: a top-side slide switch selects between two C0G timing capacitors, about 3.3 nF (low range) and 330 pF (high range), with the same 3296W-1-104LF 100 kΩ trimmer. The ranges must overlap so that together they cover 10 kHz to 1 MHz worst case. Reason: the 3296 datasheet (REV. 02/26) gives absolute minimum resistance '1 % or 2 ohms max., whichever is greater', so one range spans just under 100:1 at worst (research/parts/frequency-trimmer.md). Update docs/SPEC.md (remove 'one range, no range switch' from the must-nots and design, add the range switch and both capacitors, keep the Budgets section), the constraint registry (replace timing.cap_nF with the two capacitor values; make timing.trimmer_end_resistance_ohm reflect the datasheet's 1 % worst case; add the range switch), the openspec capability specs and docs/SUBSYSTEMS.md to match. Choose exact capacitor and resistor values so each range's worst-case endpoints, including trimmer end resistance and ±10 % trimmer tolerance, overlap and cover 10 kHz to 1 MHz with margin. Add range-switch position labels to the silkscreen requirements. Do not change anything else in the brief's requirements.

- Change: two-range-timing-switch
- Files: .copperhead/constraints.json, docs/SPEC.md, docs/SUBSYSTEMS.md, openspec/specs/oscillator/spec.md, openspec/specs/physical/spec.md, openspec/specs/power/spec.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC not required

## 2026-11-10 — two-range timing (brief b6ced00)

- Change: two-range-timing-switch
- One range became two:
  - SW1, a top-side SPDT slide switch with its common to GND, selects C4 3.3 nF C0G (LO) or C6 330 pF C0G (HI);
  - R3 1.00 kΩ, R4 120 Ω and RV1 3296W 100 kΩ are unchanged.
- Worst case, with R ±1 %, C ±5 %, trimmer ±10 % and 1 % end resistance (≤ 1.1 kΩ):
  - LO 2.54–120.6 kHz;
  - HI 25.4 kHz–1.206 MHz;
  - overlap 4.7:1.
- SPEC: §1, §2 and §3 rewritten for two ranges; §5 gains SW1 on the top side and silkscreen range labels "LO 10–100 kHz" and "HI 100 kHz–1 MHz". The §7 'no range switch' must-not is removed. The Budgets section is kept.
- Current upper bound is 9.6 → ≈ 14.7 mA, against 30 mA.
- Registry:
  - timing.cap_nF replaced by timing.cap_low_nF and timing.cap_high_pF;
  - timing.trimmer_end_resistance_ohm set to ≤ 1100 Ω, the datasheet 1 %;
  - timing.range_switch added;
  - signal.frequency_range_Hz, timing.node_loading and timing.cap_dielectric updated.
- Files: docs/SPEC.md, docs/SUBSYSTEMS.md, .copperhead/constraints.json, openspec/specs/{oscillator,physical,power}/spec.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: ERC not required (no schematic); check_drift run

## 2026-11-10 — create pipeline stage: architecture

- Change: architecture-555-oscillator
- Files: docs/SUBSYSTEMS.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC not required

## 2026-11-10 — create pipeline stage: architecture

- Change: architecture-555-oscillator
- Added docs/SUBSYSTEMS.md with these sections: power entry, timer core, output buffer, output connectors, indicators, test points, mechanical, and current budget. It also lists what is intentionally not present: MCU, connectivity, regulator and range switch.
- Provisional timing values: R_A = 1.00 kΩ, R_B = 120 Ω + 100 kΩ trimmer, C = 1 nF C0G. The ideal frequency range is 7.2 kHz to 1.16 MHz.
- Open risk: trimmer end resistance and TLC555 delays may hold the top end below 1.1 MHz. Registered as `timing.trimmer_end_resistance_ohm`, to be verified at the schematic stage.
- The activity LED is driven from BUF_OUT.
- Worst-case supply current is ≈ 9.6 mA against the 30 mA budget.
- Files: docs/SUBSYSTEMS.md, docs/CHANGELOG.md, docs/DECISIONS.md, .copperhead/constraints.json
- Verification: ERC not required (no schematic); check_drift run

## 2026-11-10 — create pipeline stage: spec-seed

- Change: verify-spec-seed-555-oscillator
- Files: (none)
- Verification: ERC not required

## 2026-11-10 — create pipeline stage: spec-seed

- Change: seed-spec-555-oscillator
- Files: openspec/specs/power/spec.md, openspec/specs/oscillator/spec.md, openspec/specs/output/spec.md, openspec/specs/physical/spec.md, docs/SPEC.md, docs/DECISIONS.md, docs/CHANGELOG.md
- Verification: ERC not required

## 2026-11-10 — create pipeline stage: spec-seed (recovery)

- Change: seed-spec-555-oscillator
- Patched docs/SPEC.md:
  - added the keys timing.cap_nF, timing.trimmer, board.mounting_holes and build.quantity;
  - added an R_A row to §3;
  - added the 25-turn trimmer and build quantity of about 5.
- Recorded those four constraints in .copperhead/constraints.json.
- Seeded openspec/specs/power, oscillator, output and physical with Given/When/Then scenarios.
- Files: docs/SPEC.md, docs/CHANGELOG.md, docs/DECISIONS.md, .copperhead/constraints.json, openspec/specs/*/spec.md
- Verification: ERC not required (no schematic); check_drift run at end

## 2026-11-10 — create pipeline stage: spec-seed

- Change: seed-spec-555-oscillator
- Files: docs/SPEC.md, docs/CHANGELOG.md, docs/DECISIONS.md
- Verification: ERC not required

## 2026-11-10 — create pipeline stage: spec-seed (completion)

- Change: seed-spec-555-oscillator
- Read docs/SPEC.md back: it covers identity, power, signal, interfaces, physical, environment, must-not and open items. The ESD clamp (≤10 V at 1 A) is stated as above the SN74LVC1G17's 6.5 V abs-max.
- Added the `timing.ra_min_ohm` key (R_A ≥ 1 kΩ, ASSUMED) to SPEC §2 and the constraint registry, the only budget that had no registry entry.
- openspec/specs/ not seeded: only this run's change folder exists.
- Files: docs/SPEC.md, .copperhead/constraints.json, docs/CHANGELOG.md
- Verification: ERC not required (no schematic); check_drift clean (vacuous)

## 2026-11-10 — create pipeline stage: spec-seed

- Change: seed-spec-555-oscillator
- Files: docs/SPEC.md, docs/DECISIONS.md
- Verification: ERC not required
