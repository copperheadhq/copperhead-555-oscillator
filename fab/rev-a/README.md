# Fabrication outputs, rev A

**Released 2026-11-11 from the design at `6d0c6c8` (release commit `c822784`). This board has never been fabricated or powered. Until bring-up passes, it is unverified. If you send these files to a fab, that decision is yours.**

**Rev A is a bare-PCB release.** There is no fab BOM: all 23 parts in [`../../docs/BOM.md`](../../docs/BOM.md) are still marked UNVERIFIED, so `copperhead export bom` left every one of them out. Assemble by hand, or wait for a revision with a checked BOM.

The copperhead logo and the `555 variable oscillator` / `5 V · 10 kHz–1 MHz · rev A` lines are on the front silkscreen in these files. The back silkscreen is blank.

## What is here

| File | What |
| --- | --- |
| `555-oscillator-gerbers.zip` | 10 files: copper, mask, paste and silkscreen for both sides, the outline, and the drill file |
| `gerbers/` | the same files unzipped, plus the `.gbrjob` job file |
| `555-oscillator-cpl-jlcpcb.csv` | component placement, 23 parts, in KiCad's CSV format. Useful for hand assembly; a fab cannot place from it without a BOM |
| `drc.json` | DRC report on this board (zones refilled, schematic parity, all severities) |

## Where they came from

Every gerber, the drill file, the job file and the placement file are byte-for-byte copies of the frozen rev A release (`releases/rev-a/` in the design workspace). Only the placement file was renamed. Their SHA-256 sums match the ones recorded at release:

```text
4d5a1b09d9b6579c5dd9557d56fa8c7b2729b1a3692a6b97473988aa9ad46e22  555-oscillator-cpl-jlcpcb.csv
b3447e2c8904476dfb0b65b27e3af22a70495026cfc5decadad8eace5d2e749e  gerbers/5-v-variable-frequency-555-oscillator.drl
94fb5230e18b5078dc523b0f39851003fff64897d3006f23712eb01bbbf9a341  gerbers/5-v-variable-frequency-555-oscillator-F_Cu.gtl
6d9a7f8fca9b51d63f5d2d23bd5ea791a95564d5fae1efcef5619ea41ff90287  gerbers/5-v-variable-frequency-555-oscillator-B_Cu.gbl
4869b6d40ea8b79f5b21ddc9409beaecbe956805d1f21a912c35269ebf2585cd  gerbers/5-v-variable-frequency-555-oscillator-F_Silkscreen.gto
571f10dfc51ea1adf6c94343d85f181275d391085f5188b82ce7ec543c7d4afe  gerbers/5-v-variable-frequency-555-oscillator-job.gbrjob
```

The drill file has 35 holes: 18 vias and 17 drilled pads (including 4 plated slots and 4 non-plated holes).

## Checks on this board

- KiCad DRC (`--refill-zones --schematic-parity --severity-all`): 0 unconnected items; 4 violations, all hole_clearance inside the GCT USB4105 (J1) library footprint, waived; 7 parity issues (below).
- Refilling the zones changes nothing: the copper gerbers are byte-identical before and after.
- KiCad ERC: 0 violations.
- copperhead check: ERC 0, DRC 0 beyond the waived J1 findings, 0 unrouted, no drift between the board and its design documents; 1 schematic legibility advisory (a long TIMING wire, drawing only).

## On the order form

- Two layers, 1.6 mm. No special copper weight, finish or hole size is required by the design.
- J2 (BNC), J3 (header) and RV1 (trimmer) are through-hole; J2's barrel overhangs the right board edge.
- If you order assembly anyway, there is no BOM to match against: every part would come up unmatched.

## What has not been checked

- **Nothing in rev A has been built or measured.**
- **The frequency range.** An ngspice study with TI's TLC555 model finds that, as built (C4 3.3 nF, C6 330 pF), the worst-case top of the HI range is about **744 kHz**, short of the 1 MHz the brief asks for. Fitting C4 = 2.2 nF and C6 = 150 pF reached 1.19 MHz at every corner in the same model. The footprints are 0603 either way, so this can be decided at assembly.
- **Every part** against its datasheet and its stock: the BOM is UNVERIFIED.
- **The BNC.** The brief names Amphenol 31-5536-RFX; the board carries the KiCad footprint for Amphenol RF B6252HB-NPP3G-50. Fit the B6252HB.
- The gerbers in a viewer, and the fab's DFM report. Do that before you pay for anything.
- Signal integrity, EMC, and temperature behaviour.

## Known issues

- **No BOM** (see above).
- **HI range may stop short of 1 MHz** with the fitted C4 and C6 (see above).
- **Schematic parity:** TP1 to TP5, H1 and H2 are marked "exclude from BOM" on their footprints but not on their schematic symbols. No copper is affected, and the placement file already leaves them out.
- **J1 hole clearance:** four DRC findings inside the USB4105 library footprint's own pads, waived.
