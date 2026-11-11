# Subsystems

Source: `docs/SPEC.md` and `.copperhead/constraints.json` (2026-11-10). This is the architecture stage. Values here are **provisional** and get confirmed at schematic capture. Refdes are planned, not final.

## Block diagram (prose)

USB-C (J1) supplies VBUS, which passes the ESD diode (D1) and the 10 µF bulk capacitor (C1) to form net **+5V**. The CC1 and CC2 pins each get their own 5.1 kΩ pull-down, so a source offers default USB power. +5V feeds the timer core and the output buffer directly; there is no regulator.

The timer core is a TLC555 (U1) in the conventional astable configuration. R_A runs from +5V to DIS. R_B runs from DIS to the timing node and is made of a fixed resistor in series with the 100 kΩ trimmer. Two C0G timing capacitors, 3.3 nF (LO range) and 330 pF (HI range), each have one end on that node. A top-side slide switch (SW1) connects the other end of the selected capacitor to ground. The raw output **RAW** (U1 OUT) feeds the SN74LVC1G17 Schmitt buffer (U2). U2's output **BUF_OUT** passes a 33 Ω series resistor to net **OUT**, which goes to the BNC (J2) and to pin 1 of the 2-pin header (J3).

The activity LED hangs off BUF_OUT, never off the timing node. The power LED hangs off +5V. Test points: 5V, GND, TIMING, RAW and OUT.

Signal flow is one-directional: power entry → timer core → output buffer → output connectors. The indicators and test points are leaves.

## Not present (intentional)

- **MCU: none** (`firmware.programmable_devices` = 0; firmware/README.md is "# No firmware"). The oscillator is purely analog plus logic. Frequency is set by hand at the trimmer, with no firmware, no programming header and no clock to manage.
- **Connectivity: none.** USB-C carries power only. D+ and D− are left unconnected (SPEC §2), so the receptacle's data pins carry no-connect flags in the schematic.
- **Regulator: none, and battery: none.** Both are forbidden (`power.regulator`). Every IC runs from VBUS at 4.75–5.25 V, which is inside the recommended operating range of both the TLC555 and the SN74LVC1G17.

## Power entry

| Item | Value | Rationale |
| ---- | ----- | --------- |
| J1 | GCT USB4105-GF-A | Brief part; VBUS and GND only |
| R1, R2 | 5.1 kΩ 1 %, CC1 and CC2 to GND, one each | `usb.cc_pulldown_ohm`. Must be separate resistors: a shared one breaks e-marked or flip detection |
| D1 | TPD1E10B06DYAR, VBUS to GND, at J1 | `power.vbus_esd_vrwm_V`. Its leakage is ≤ 1 µA, which is negligible against 30 mA. No dedicated library symbol exists, so it is drawn as Device:D_TVS on Diode_SMD:D_SOD-523 (a bidirectional single diode, so pin order does not matter) |
| C1 | 10 µF X5R/X7R, ≥ 10 V, at J1 | Bulk capacitance; also soaks up the ESD residue that passes D1's ≤ 10 V clamp (SPEC §8). X5R is fine here: this is not the timing capacitor |
| Net | +5V (= VBUS after D1/C1) | One supply net; no regulator |

Risk carried from SPEC §8: D1's clamp is above U2's 6.5 V absolute maximum. The mitigation is layout: put C1 at J1 and C5 at U2 pin 5. This is accepted for a bench board.

## Timer core

| Item | Value | Rationale |
| ---- | ----- | --------- |
| U1 | TLC555IDR (SOIC-8) | Brief part; CMOS, so quiescent current is ≈ 0.2 mA |
| C4 (timing, LO) | 3.3 nF C0G/NP0 ±5 %, 0603, ≥ 50 V; TIMING to SW1 LO throw | `timing.cap_low_nF`, `timing.cap_dielectric` |
| C6 (timing, HI) | 330 pF C0G/NP0 ±5 %, 0603, ≥ 50 V; TIMING to SW1 HI throw | `timing.cap_high_pF`, `timing.cap_dielectric`. It is C6 because C5 is U2's bypass |
| SW1 (range) | C&K JS102011SCQN (LCSC C221661) SPDT SMD slide switch, top (vertical) slide moved from above, −40 to +85 °C; common to GND. Project footprint `ck_switches:SW_SPDT_CK_JS102011SCQN` (C&K sheet I-53) | `timing.range_switch`. It sits in the capacitor ground return, so no switch contact is on the TIMING trace. Break-before-make leaves TIMING uncapped for a moment, which only makes U1 run fast briefly |
| R3 (R_A) | 1.00 kΩ 1 % | `timing.ra_min_ohm` floor; R_A is chosen at its minimum to maximise the top frequency |
| R4 (R_B fixed) | 120 Ω 1 % | Keeps a defined low phase when the trimmer is at its end stop |
| RV1 (R_B variable) | Bourns 3296W-1-104LF, 100 kΩ ±10 %, wired as a rheostat (wiper tied to one end) | `timing.trimmer`; shared by both ranges |
| C2 | 100 nF at U1 pin 8 | Local decoupling |
| C3 | 10 nF, CONT (pin 5) to GND | SPEC §2 (ASSUMED) |
| U1 RESET (pin 4) | Tied to +5V | Always running |
| U1 THR and TRIG (pins 6 and 2) | Tied together at the timing node, net **TIMING** | Conventional astable |

### Timing arithmetic (ideal astable, f ≈ 1.443 / ((R_A + 2·R_B)·C))

Worst-case inputs:

- R3 = 1.00 kΩ ±1 % and R4 = 120 Ω ±1 %.
- RV1 track 90–110 kΩ (±10 %).
- RV1 end resistance at the minimum end ≤ 1 % of track, which is ≤ 1.1 kΩ. Bourns 3296 REV. 02/26 states "1 % or 2 ohms max., whichever is greater".
- C4 and C6 ±5 %.

The bottom of each range takes the smallest R and C; the top takes the largest.

| Point | R_A + 2·R_B | C | f |
| ----- | ----------- | - | - |
| LO bottom, worst case (highest) | 0.99 kΩ + 2·(118.8 Ω + 90 kΩ) = 181.2 kΩ | 3.135 nF | **2.54 kHz** |
| LO top, worst case (lowest) | 1.01 kΩ + 2·(121.2 Ω + 1.1 kΩ) = 3.45 kΩ | 3.465 nF | **120.6 kHz** |
| HI bottom, worst case (highest) | 181.2 kΩ | 313.5 pF | **25.4 kHz** |
| HI top, worst case (lowest) | 3.45 kΩ | 346.5 pF | **1.206 MHz** |
| LO nominal, bottom … top | 201.2 kΩ … 3.24 to 1.24 kΩ | 3.3 nF | 2.17 kHz … 135 to 353 kHz |
| HI nominal, bottom … top | 201.2 kΩ … 3.24 to 1.24 kΩ | 330 pF | 21.7 kHz … 1.35 to 3.53 MHz |

The nominal top depends on the end resistance. It is 3.24 kΩ with 1 kΩ (1 % of 100 kΩ) left at the end stop, and 1.24 kΩ at the 2 Ω floor.

**Result.**

- In the worst case LO covers 2.54–120.6 kHz and HI covers 25.4 kHz–1.206 MHz.
- Together that is 2.54 kHz–1.206 MHz, with a 25.4–120.6 kHz overlap (4.7:1).
- This beats the SPEC §3 margins of ≤ 9 kHz at the bottom, ≥ 1.1 MHz at the top and ≥ 2:1 overlap.
- Silkscreen positions are "LO 10–100 kHz" and "HI 100 kHz–1 MHz"; each lies inside its range's worst case.

**Why these values.**

- The worst-case R span per range is 181.2 / 3.45 = 52.5:1, and the C tolerance cuts that to 47.5:1 in frequency.
- C4/C6 = 10:1 exactly gives both ranges the same R span and leaves about 5:1 of overlap.
- A larger C4 would only push the LO bottom further down.
- A smaller C6 would raise the HI top but shrink the overlap, and stray capacitance would matter more.
- R3 stays at the `timing.ra_min_ohm` floor. R4 keeps a defined low phase at the end stop.

**Remaining risks for the schematic stage (UNVERIFIED).** The datasheet's 1 % trimmer end resistance is already in the worst case above, and `timing.trimmer_end_resistance_ohm` records it as ≤ 1.1 kΩ. Three risks remain:

1. **TLC555 propagation and discharge delays** at the HI top. The worst-case 1.206 MHz is ≈ 20 % above 1 MHz, so delays plus stray capacitance must take less than that.
2. **Stray capacitance on TIMING.**
   - Sources: the THR/TRIG inputs, the trace, TP3, and the unselected capacitor.
   - The unselected capacitor's top stays on TIMING while its bottom floats at SW1's open throw. It therefore adds only about SW1's off-capacitance in series, a few pF.
   - 10 pF in total on 330 pF lowers HI by ≈ 3 %.
3. **Short low phase at the trimmer end stop.**
   - With end resistance near the 2 Ω floor, t_low ≈ 0.693 × 120 Ω × 330 pF ≈ 27 ns in HI. R4 keeps it defined, but the TLC555's own delays dominate.
   - The ideal nominal HI top (up to ≈ 3.5 MHz) is beyond the TLC555. In HI, the last turns near the end stop therefore do little.

The schematic stage simulates the astable in ngspice with the TLC555 model at all four range ends, before freezing R3, R4, RV1, C4 and C6.

### Current

- **R_A current.** While DIS is on, the current from +5V through R_A is about 5 mA. It stays within bound because R_A ≥ 1 kΩ.
- **Capacitor charging.** It adds C·ΔV·f, with ΔV ≈ V_CC/3 ≈ 1.75 V. The ideal end-stop C·f product is the same in both ranges (3.465 nF × 353 kHz ≈ 346.5 pF × 3.53 MHz), so charging adds ≤ 2.2 mA in either range.
- **SW1** adds no current.

## Output buffer

| Item | Value | Rationale |
| ---- | ----- | --------- |
| U2 | SN74LVC1G17DBVR (SOT-23-5) | Brief part. The Schmitt input squares up RAW, and it is 5 V tolerant at VCC = 5 V |
| U2 input | Net RAW (U1 OUT) | The timing node stays unloaded; the buffer sees only U1's push-pull output |
| C5 | 100 nF at U2 pin 5 | Local decoupling, close to the pin (SPEC §8) |
| R5 | 33 Ω 1 %, from BUF_OUT to OUT | `output.series_R_ohm`. Damps cable ringing into a high-Z load. **It is not a 50 Ω match, and no 50 Ω drive is claimed** (`output.load`) |

## Output connectors

| Item | Value | Rationale |
| ---- | ----- | --------- |
| J2 | Amphenol RF B6252HB-NPP3G-50, right-angle THT BNC, at a board edge | Center pin to OUT, shell to GND. Substituted for the brief's 31-5536-RFX at part selection: no 31-5536 footprint is installed, and the installed 031-6575 footprint has two pads with no symbol pin. Right-angle, board-edge and through-hole are kept (docs/parts.intent.json substitutions) |
| J3 | Samtec TSW-102-07-G-S | Pin 1 = OUT, pin 2 = GND (ASSUMED pinout, SPEC §4) |
| Load | High-Z only: ≥ 1 kΩ ‖ ≤ 150 pF, typically a 1 MΩ scope | `output.load`. Silkscreen will say "Hi-Z"; it will never say "50 Ω" |

## Indicators

| Item | Value | Rationale |
| ---- | ----- | --------- |
| D2 power LED + R6 | Würth 150060GS75000 green 0603; 2.0 kΩ from +5V | (5 V − ≈2 V) / 2 kΩ ≈ 1.5 mA. A high-efficiency 0603 LED is visible at this current |
| D3 activity LED + R7 | 2.0 kΩ from **BUF_OUT** (U2 output, before R5) | `timing.node_loading`: the LED is two stages away from TIMING. Average current ≤ 1.5 mA. U2 sources this easily. It lights whenever the oscillator runs, and it does not blink visibly at ≥ 10 kHz |

Why BUF_OUT and not RAW: an LED load on RAW would shift U1's output edges and couple supply current into the timer. On BUF_OUT it only draws ≈ 1.5 mA from a 24 mA-capable driver.

## Test points

The test points are bare pads on the top side:

| Test point | Net | Note |
| ---------- | --- | ---- |
| TP1 | 5V (+5V) | |
| TP2 | GND | |
| TP3 | TIMING | Silkscreen note: "probe shifts freq" (a probe adds about 10–15 pF: ≈ 0.3–0.5 % in LO, ≈ 3–4.5 % in HI) |
| TP4 | RAW | |
| TP5 | OUT | Sits after R5 |

TP3 is the only extra load allowed on TIMING (`timing.node_loading`).

## Mechanical and layout

- 2 layers (`board.layers`), about 60 × 35 mm (`board.size_mm`), two M3 holes H1 and H2 at 3.2 mm (`board.mounting_holes`).
- Top side: J1, J2 (at an edge), J3, RV1, SW1, D2, D3 and TP1–TP5.
- Placement follows the signal flow: J1 at one short edge, then power entry, then U1 with C4, C6, SW1, R3, R4 and RV1 clustered at pins 2, 6 and 7 (C4 and C6 tops at the TIMING node, SW1 beside them on their ground side), then U2 and R5, then J2 at the opposite edge.
- The TIMING trace is as short as possible and routed away from BUF_OUT and OUT.
- Bottom layer is a continuous GND pour under the oscillator and the output path.
- Silkscreen:
  - a frequency-direction label at RV1 ("CW = f ↑");
  - range-switch positions "LO 10–100 kHz" (right of SW1, the pad-1/CAP_LO side) and "HI 100 kHz–1 MHz" (left of SW1, the pad-3/CAP_HI side);
  - "OUT (Hi-Z)" at J2, and "SIG" and "GND" at the J3 pins;
  - the test-point names.

## Current budget (`power.supply_current_mA` ≤ 30 mA)

| Consumer | Worst case |
| -------- | ---------- |
| D2 power LED | 1.6 mA (at 5.25 V) |
| D3 activity LED | 1.6 mA |
| U1 TLC555 quiescent | ≈ 0.4 mA (allowing above typ 0.2 mA) |
| U1 TLC555 dynamic at its top frequency | ≈ 1 mA (ASSUMED; verify against the datasheet supply-current curve) |
| Timing network (R_A while DIS is on) | ≤ 5.3 mA |
| Timing capacitor charging, either range at the end stop | ≤ 2.2 mA |
| U2 static | ≈ 0.01 mA |
| U2 dynamic, 115 pF load, up to the ≈ 3.6 MHz ideal HI end stop | ≤ 2.2 mA (≈ 0.6 mA at 1 MHz) |
| U2 internal C_pd ≈ 20 pF (ASSUMED), same frequency | ≤ 0.4 mA |
| D1 leakage | ≤ 0.001 mA |
| **Total** | **≈ 14.7 mA** upper bound, about 49 % of the budget. The 3.6 MHz figure is the ideal end stop with 2 Ω end resistance. The TLC555 stops lower, so the real current is less |
