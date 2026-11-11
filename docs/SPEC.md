# Specification

Source: `docs/BRIEF.md` (2026-11-10). Values marked **ASSUMED** are defaults this
spec proposes where the brief is silent; change them here first, then in the design.
Every numeric budget below is also recorded in `.copperhead/constraints.json` under
the key shown in brackets.

## 1. What the device is

A compact bench square-wave oscillator, adjustable from about 10 kHz to 1 MHz, powered
from 5 V USB-C. It feeds an oscilloscope or a 5 V CMOS logic input.

- Core: TLC555IDR CMOS timer in the conventional astable configuration. It is a 555 astable, **not** a Hartley/LC oscillator.
- Output conditioning: an SN74LVC1G17DBVR Schmitt-trigger buffer drives the outputs. The raw timer output only reaches a test point.
- Frequency control: one Bourns 3296W-1-104LF 100 kΩ 25-turn top-adjust trimmer, set with a screwdriver, in **two** overlapping ranges. A top-side SPDT slide switch (SW1) selects the timing capacitor: 3.3 nF C0G for the LO range or 330 pF C0G for the HI range. Together the ranges cover 10 kHz to 1 MHz worst case (§3). Two ranges are needed because the 3296's end resistance (up to 1 % of track, datasheet REV. 02/26) limits one range to just under 100:1 (`research/parts/frequency-trimmer.md`).
- Programmable devices: **none** (`firmware.programmable_devices` = 0). There is no MCU, no programming header and no firmware; `firmware/README.md` is "# No firmware". U2 (SN74LVC1G17) is fixed-function logic, and the +5V/GND/PWR_FLAG power symbols are not devices.
- Outputs: a right-angle BNC (Amphenol RF B6252HB-NPP3G-50, substituted at part selection for the brief's 31-5536-RFX, which has no installed footprint) and a parallel 2-pin 2.54 mm header (Samtec TSW-102-07-G-S, signal + GND).

## Budgets

The budgets are the tables in sections 2 to 6 below, each with its key in `.copperhead/constraints.json`.

## 2. Power

| Item | Requirement | Key |
| ---- | ----------- | --- |
| Input | 5 V DC from USB-C receptacle GCT USB4105-GF-A, VBUS only | — |
| Input voltage range | 4.75 V to 5.25 V (USB 2.0 VBUS). **ASSUMED**: the brief says only "5 V" | `power.vbus_V` |
| Supply current | **< 30 mA total**, all operating points, both LEDs lit | `power.supply_current_mA` |
| CC1 / CC2 | 5.1 kΩ pull-down to GND on each, separately (sink advertisement; draws default USB current, ≤ 500 mA available) | `usb.cc_pulldown_ohm` |
| D+ / D− | Unconnected (USB is power only) | — |
| Regulation | **None.** No onboard regulator and no battery; every IC runs directly from VBUS | `power.regulator` |
| ESD | TPD1E10B06DYAR (SOD-523) on VBUS. Working voltage ≥ 5.25 V, leakage ≤ 1 µA. Its clamp is ≤ 10 V at 1 A (SLLSEB1G), **above** the SN74LVC1G17's 6.5 V abs-max, so the 10 µF bulk and 100 nF local capacitors must absorb the residual ESD energy. That is acceptable for a bench board fed from a USB port; see §8. See `research/parts/vbus-esd.md` | `power.vbus_esd_vrwm_V` |
| Bulk decoupling | 10 µF at the input | — |
| Local decoupling | 100 nF at each IC supply pin (TLC555, SN74LVC1G17), placed close to the pin | — |
| Timer CONT pin | 10 nF to GND. **ASSUMED**: standard 555 practice for noise immunity; not in the brief | — |

### Current estimate (ASSUMED values; to be confirmed at schematic stage)

| Consumer | Estimate | Basis |
| -------- | -------- | ----- |
| Power LED | ≈ 1–2 mA | **ASSUMED**: high-efficiency LED, series R sized for about 1.5 mA |
| Activity LED | ≈ 1–2 mA average | **ASSUMED**: driven from the buffered output (or its own buffer), never from the timing node |
| TLC555 quiescent | ≈ 0.2 mA (datasheet typ at 5 V) | TI TLC555 datasheet |
| TLC555 dynamic at its top frequency | ≈ 1 mA | **ASSUMED**; verify against the datasheet supply-current curve at the schematic stage |
| Timing network | ≤ 5.3 mA through R_A while DIS is on, plus ≤ 2.2 mA capacitor charging (C·ΔV·f, ΔV ≈ 1.75 V) | R_A ≥ 1 kΩ (**ASSUMED**; `timing.ra_min_ohm`). Both ranges have the same C·f product at the ideal end stop (3.3 nF × ≈ 0.35 MHz = 330 pF × ≈ 3.5 MHz), so the range switch does not change this |
| Buffer driving cable + scope (≈ 115 pF) | ≤ 2.2 mA at the ideal HI end stop (≈ 3.6 MHz, C·V·f); ≈ 0.6 mA at 1 MHz | 1 m RG-58 ≈ 100 pF + 15 pF scope input. The TLC555 stops below the ideal end-stop frequency, so this is an upper bound |
| **Total** | **≈ 15 mA upper bound** (≈ 14.7 mA, docs/SUBSYSTEMS.md), against the 30 mA budget | — |

## 3. Signal

| Item | Requirement | Key |
| ---- | ----------- | --- |
| Frequency range | 10 kHz to 1 MHz, continuously adjustable in two overlapping ranges selected by SW1: LO (C4, 3.3 nF) and HI (C6, 330 pF) | `signal.frequency_range_Hz`, `timing.range_switch` |
| Endpoint margin | Worst case: fixed R ±1 %, C ±5 %, trimmer track 90–110 kΩ, and trimmer end resistance up to 1 % of track (≤ 1.1 kΩ, Bourns 3296 REV. 02/26). Under that case, LO reaches ≤ 9 kHz at its bottom, HI reaches ≥ 1.1 MHz at its top, and the LO top is ≥ 2× the HI bottom. **ASSUMED** margins (about 10 % at each end, 2:1 overlap). Calculated: LO 2.54–120.6 kHz, HI 25.4 kHz–1.206 MHz, overlap 25.4–120.6 kHz (4.7:1), before TLC555 delays (docs/SUBSYSTEMS.md) | `signal.frequency_range_Hz`, `timing.trimmer_end_resistance_ohm` |
| Tuning law | f ∝ 1/R, so within each range most of the trimmer's travel tunes the low end and the top of each range is coarse. Accepted in the brief (2026-11-10) | — |
| Duty cycle | Not guaranteed 50 %; it varies with frequency (conventional astable) | — |
| Timing capacitors | **C4 3.3 nF (LO)** and **C6 330 pF (HI)**, both C0G/NP0, ±5 % or better. **ASSUMED** tolerance. X7R/X5R/Y5V forbidden | `timing.cap_low_nF`, `timing.cap_high_pF`, `timing.cap_dielectric` |
| Range switch | SW1, an SPDT slide switch on the top side. Its common goes to GND and its throws to the ground ends of C4 and C6. The switch therefore sits in the capacitor's ground return and not on the TIMING trace. The part is chosen at part selection | `timing.range_switch` |
| Timing resistors | 1 % tolerance (fixed resistors) | `timing.resistor_tolerance_pct` |
| Timing trimmer | **100 kΩ, 25-turn**, top adjust, ±10 %, ±100 ppm/°C cermet (Bourns 3296W-1-104LF) | `timing.trimmer` |
| R_A minimum | ≥ 1 kΩ. **ASSUMED**, to bound timing current at 1 MHz | `timing.ra_min_ohm` |
| Output level | 0 V to about 5 V (VBUS) square wave, from SN74LVC1G17 | — |
| Series resistor | 33 Ω at the buffer output, before BNC and header | `output.series_R_ohm` |
| Output load | **High impedance only** (≥ 1 kΩ ‖ ≤ 150 pF, typically 1 MΩ ‖ 15 pF scope or a CMOS input). **ASSUMED** load numbers. 50 Ω drive is **not** claimed and must not be written on silkscreen or in docs | `output.load` |
| Timing-node isolation | Only these connect to the timing capacitor node: the timing R/C network (R4/RV1, C4, C6, and SW1 in their ground return), the TLC555 THR/TRIG pins and a test point. The activity LED must not load it | `timing.node_loading` |

## 4. Interfaces and test points

- J1 USB-C (power), BNC output, 2-pin output header (pin 1 signal, pin 2 GND; **ASSUMED** pinout).
- Test points, all on the top side: **5V**, **GND**, **TIMING** (TLC555 timing-capacitor node), **RAW** (TLC555 OUT), **OUT** (buffered output, after the 33 Ω).
- The TIMING test point is a bare pad. A probe adds about 10–15 pF and shifts the frequency; the silkscreen notes this. **ASSUMED**

## 5. Physical

| Item | Requirement | Key |
| ---- | ----------- | --- |
| Layers | 2-layer PCB | `board.layers` |
| Outline | about 60 × 35 mm (±5 mm acceptable. **ASSUMED** tolerance) | `board.size_mm` |
| Mounting | **Two M3** holes (3.2 mm plated or NPTH, **ASSUMED** diameter) | `board.mounting_holes` |
| Top side | Trimmer, range switch SW1, USB-C, BNC, both LEDs, all test points | — |
| BNC | At a board edge | — |
| Ground | Continuous ground plane under the oscillator and the output path | — |
| Layout | Timing-node trace short and routed away from the buffered output | — |
| Silkscreen | The board carries these labels:<br>- frequency direction at the trimmer (which way raises f);<br>- range-switch positions at SW1, "LO 10–100 kHz" and "HI 100 kHz–1 MHz", each inside that position's worst-case range;<br>- output labels at the BNC and header;<br>- test-point names. | `timing.range_switch` |
| Assembly | Fab PCBA (e.g. JLCPCB). BNC, header and trimmer may be hand-soldered | — |
| Build quantity | about **5** boards | `build.quantity` |
| Enclosure | None | — |

## 6. Environment

| Item | Requirement | Key |
| ---- | ----------- | --- |
| Operating temperature | 0 °C to 70 °C (commercial), indoor bench | `env.temperature_C` |
| Part temperature grade | Every part rated across 0–70 °C at minimum | `env.temperature_C` |

## 7. Must not

- No claim of 50 Ω output drive, in silkscreen, docs or BOM.
- No battery and no onboard regulator.
- The activity LED must not load the timing node.

## 8. Open items (not blocking)

- Lifecycle and stock of the TI devices, the USB4105 and the BNC are not yet checked against a distributor. The trimmer and the ESD diode were checked on 2026-11-10.
- VBUS ESD clamp (≤ 10 V at 1 A) exceeds the SN74LVC1G17's 6.5 V absolute maximum. The schematic stage should place the buffer's 100 nF close to the pin and keep the 10 µF bulk capacitor at the connector. If more margin is wanted, revisit the diode choice (`research/parts/vbus-esd.md`).
- Timing values are set in docs/SUBSYSTEMS.md: R_A = 1.00 kΩ, R_B = 120 Ω + 100 kΩ trimmer, C4 = 3.3 nF, C6 = 330 pF. Three effects are not yet verified:
  - TLC555 propagation and discharge delays at the HI top;
  - stray capacitance on TIMING (THR/TRIG, trace, TP3, and the unselected capacitor through SW1's off-capacitance);
  - the very short low phase at the trimmer end stop (≈ 0.693 × 120 Ω × 330 pF ≈ 27 ns).
  The worst-case HI top keeps ≈ 20 % margin above 1 MHz to absorb them. Simulate in ngspice at the schematic stage.
- The range switch SW1 is chosen: C&K JS102011SCQN (LCSC C221661), a top-slide (vertical) SPDT SMD gull-wing slide switch rated −40 to +85 °C, operated from above (research/parts/range-switch.md). It replaced the right-angle JS102011SAQN on 2026-11-10. All MPNs in docs/BOM.md are still UNVERIFIED against distributor stock.
- The BNC is the Amphenol RF B6252HB-NPP3G-50, not the brief's 31-5536-RFX (footprint availability; docs/parts.intent.json substitutions). The brief should be updated by the person to match.
