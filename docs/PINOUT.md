# Pinout

Source: `schematic.intent.json` (drafted into `5-v-variable-frequency-555-oscillator.kicad_sch`, 2026-11-10). Pin numbers are the installed KiCad symbol pins.

## Connectors

### J1 — USB-C, GCT USB4105-GF-A (power only)

| Pin | Name | Net | Note |
| --- | ---- | --- | ---- |
| A4, A9, B4, B9 | VBUS | +5V | Through D1 / C1; no regulator (`power.regulator`) |
| A1, A12, B1, B12 | GND | GND | |
| SH | SHIELD | GND | Shell tied directly to GND |
| A5 | CC1 | CC1 | R1 5.1 kΩ to GND (`usb.cc_pulldown_ohm`) |
| B5 | CC2 | CC2 | R2 5.1 kΩ to GND, separate resistor |
| A6, B6 | D+ | — | No-connect: USB is power only |
| A7, B7 | D− | — | No-connect |
| A8, B8 | SBU1/SBU2 | — | No-connect |

### J2 — BNC, Amphenol RF B6252HB-NPP3G-50

| Pin | Name | Net | Note |
| --- | ---- | --- | ---- |
| 1 | In (center) | OUT | After R5 33 Ω; high-Z load only, no 50 Ω drive claim (`output.load`) |
| 2 | Ext (shell) | GND | |

### J3 — 2-pin header, Samtec TSW-102-07-G-S

| Pin | Net | Note |
| --- | --- | ---- |
| 1 | OUT | Signal (SPEC §4, ASSUMED pinout) |
| 2 | GND | |

## ICs

### U1 — TLC555IDR (SOIC-8)

| Pin | Name | Net | Note |
| --- | ---- | --- | ---- |
| 1 | GND | GND | |
| 2 | TRIG | TIMING | Tied to THRES (astable) |
| 3 | OUT | RAW | To U2 input and TP4 only |
| 4 | ~RST | +5V | Always running |
| 5 | CONT | CONT | C3 10 nF to GND |
| 6 | THRES | TIMING | |
| 7 | DISCH | DIS | R3 (R_A) from +5V, R4 (R_B fixed) to RB_TRIM |
| 8 | VCC | +5V | C2 100 nF local |

### U2 — SN74LVC1G17DBVR (SOT-23-5)

| Pin | Name | Net | Note |
| --- | ---- | --- | ---- |
| 1 | NC | — | No-connect (internally unconnected) |
| 2 | A | RAW | Schmitt input |
| 3 | GND | GND | |
| 4 | Y | BUF_OUT | To R5 (33 Ω) and R7/D3 activity LED |
| 5 | VCC | +5V | C5 100 nF local |

## Timing network and range switch

| Part | Pin | Net | Note |
| ---- | --- | --- | ---- |
| RV1 | 1 (end) | RB_TRIM | Rheostat: wiper tied to this end |
| RV1 | 2 (wiper) | RB_TRIM | |
| RV1 | 3 (end) | TIMING | |
| C4 3.3 nF C0G | 1 / 2 | TIMING / CAP_LO | LO range |
| C6 330 pF C0G | 1 / 2 | TIMING / CAP_HI | HI range |
| SW1 | 1 (A) | CAP_LO | LO throw |
| SW1 | 2 (B, common) | GND | Switch is in the capacitor ground return, not on TIMING (`timing.range_switch`) |
| SW1 | 3 (C) | CAP_HI | HI throw |

TIMING carries only RV1.3, C4.1, C6.1, U1.2, U1.6 and TP3 (`timing.node_loading`).

## Indicators

| Part | Pins | Nets |
| ---- | ---- | ---- |
| R6 2.0 kΩ / D2 power LED | R6: +5V → LED_PWR; D2 A(2)=LED_PWR, K(1)=GND | |
| R7 2.0 kΩ / D3 activity LED | R7: BUF_OUT → LED_ACT; D3 A(2)=LED_ACT, K(1)=GND | Never on TIMING |

## Test points

| TP | Net |
| -- | --- |
| TP1 | +5V |
| TP2 | GND |
| TP3 | TIMING (probe shifts freq) |
| TP4 | RAW |
| TP5 | OUT |

D1 (TPD1E10B06DYAR, bidirectional): pin 1 = +5V, pin 2 = GND. H1 and H2 have no pins.
