# BOM

<!-- rendered from parts.intent.json by copperhead draft_bom; edit the manifest, not this table -->

| Refdes | Value | Footprint | MPN | Rationale | Symbol |
| --- | --- | --- | --- | --- | --- |
| J1 | USB4105-GF-A | Connector_USB:USB_C_Receptacle_GCT_USB4105-xx-A_16P_TopMnt_Horizontal | USB4105-GF-A (UNVERIFIED) | Brief part. GCT USB4105 16-pin USB 2.0 Type-C receptacle, top-mount horizontal; only VBUS, GND, CC1 and CC2 are used. Datasheet operating range is -30 to +85 C, which covers env.temperature_C. | Connector:USB_C_Receptacle_USB2.0_16P |
| R1 | 5.1k | Resistor_SMD:R_0603_1608Metric | RC0603FR-075K1L (UNVERIFIED) | CC1 pull-down per usb.cc_pulldown_ohm. Yageo RC0603 thick film: 1 %, 1/10 W, -55 to +155 C. | Device:R |
| R2 | 5.1k | Resistor_SMD:R_0603_1608Metric | RC0603FR-075K1L (UNVERIFIED) | CC2 pull-down, separate from R1 per usb.cc_pulldown_ohm. Yageo RC0603: 1 %, -55 to +155 C. | Device:R |
| D1 | TPD1E10B06DYAR | Diode_SMD:D_SOD-523 | TPD1E10B06DYAR (UNVERIFIED) | VBUS ESD per power.vbus_esd_vrwm_V and research/parts/vbus-esd.md. TI SLLSEB: VRWM 5.5 V >= 5.25 V; leakage <= 1 uA at 5 V, negligible against 30 mA; -40 to +125 C. Single bidirectional diode, so it is drawn with the stock 2-pin diode symbol (no dedicated library symbol). | Device:D_TVS |
| C1 | 10uF | Capacitor_SMD:C_0805_2012Metric | CL21A106KAYNNNE (UNVERIFIED) | Bulk input capacitor. Samsung 10 uF 25 V X5R 0805 +/-10 %, -55 to +85 C. 25 V rating keeps DC-bias derating at 5 V modest. X5R is allowed because this is not a timing capacitor. | Device:C |
| U1 | TLC555IDR | Package_SO:SOIC-8_3.9x4.9mm_P1.27mm | TLC555IDR (UNVERIFIED) | Brief part. TI TLC555 LinCMOS timer, SOIC-8, I grade -40 to +85 C. Supply current about 170 uA typ at 5 V, within the 0.4 mA allowance in the SUBSYSTEMS current budget. Astable operation to about 2 MHz per datasheet. | Timer:TLC555xD |
| C2 | 100nF | Capacitor_SMD:C_0603_1608Metric | CL10B104KB8NNNC (UNVERIFIED) | U1 pin 8 local decoupling. Samsung 100 nF 50 V X7R 0603, -55 to +125 C. | Device:C |
| C3 | 10nF | Capacitor_SMD:C_0603_1608Metric | CL10B103KB8NNNC (UNVERIFIED) | U1 CONT to GND, SPEC 2 (ASSUMED). Samsung 10 nF 50 V X7R 0603. Not a timing capacitor, so X7R is acceptable. | Device:C |
| C4 | 3.3nF C0G | Capacitor_SMD:C_0603_1608Metric | GRM1885C1H332JA01D (UNVERIFIED) | LO-range timing capacitor per timing.cap_low_nF and timing.cap_dielectric. Murata GRM18 series: 5C = C0G (0 +/-30 ppm/C), 1H = 50 V, 332 = 3300 pF, J = +/-5 %; -55 to +125 C. | Device:C |
| C6 | 330pF C0G | Capacitor_SMD:C_0603_1608Metric | GRM1885C1H331JA01D (UNVERIFIED) | HI-range timing capacitor per timing.cap_high_pF and timing.cap_dielectric. Murata GRM18: C0G, 50 V, 330 pF, +/-5 %, -55 to +125 C. | Device:C |
| R3 | 1.00k | Resistor_SMD:R_0603_1608Metric | RC0603FR-071KL (UNVERIFIED) | R_A at the timing.ra_min_ohm floor; 1 % per timing.resistor_tolerance_pct. Yageo RC0603, 100 ppm/C. Dissipation is 25 mW at 5 V, which is under the 100 mW rating. | Device:R |
| R4 | 120 | Resistor_SMD:R_0603_1608Metric | RC0603FR-07120RL (UNVERIFIED) | Fixed R_B in series with RV1; 1 % per timing.resistor_tolerance_pct. Yageo RC0603. | Device:R |
| RV1 | 100k | Potentiometer_THT:Potentiometer_Bourns_3296W_Vertical | 3296W-1-104LF (UNVERIFIED) | Brief part, per timing.trimmer: Bourns 3296W 25-turn top-adjust cermet. 100 kOhm +/-10 %, +/-100 ppm/C, -55 to +125 C. End resistance is 1 % or 2 ohms max (REV. 02/26), which sets timing.trimmer_end_resistance_ohm. Wired as a rheostat. | Device:R_Potentiometer_Trim |
| SW1 | JS102011SCQN | ck_switches:SW_SPDT_CK_JS102011SCQN | JS102011SCQN (UNVERIFIED) | Range switch per timing.range_switch and research/parts/range-switch.md: C&K JS102011SCQN, top-slide (vertical) SPDT SMD, gull wing, LCSC C221661; replaces the right-angle JS102011SAQN so the slider is moved from above (brief Parts, person's decision 2026-11-10). Project footprint ck_switches (C&K sheet I-53 land pattern: 1.0 x 3.0 mm pads, 2.5 mm pitch). Slider at the pad-1 end selects LO; common to GND, throws to the C4 and C6 ground ends. Signal-level contacts (300 mA at 6 VDC), -40 to +85 C. It carries only capacitor return current. | Switch:SW_SPDT |
| U2 | SN74LVC1G17DBVR | Package_TO_SOT_SMD:SOT-23-5 | SN74LVC1G17DBVR (UNVERIFIED) | Brief part. TI single Schmitt buffer, SOT-23-5 (DBV). VCC 1.65 to 5.5 V; ICC <= 10 uA static; +/-24 mA output at 4.5 V; -40 to +125 C. | 74xGxx:74LVC1G17 |
| C5 | 100nF | Capacitor_SMD:C_0603_1608Metric | CL10B104KB8NNNC (UNVERIFIED) | U2 pin 5 local decoupling, placed close to the pin (SPEC 8 ESD residue). Samsung 100 nF 50 V X7R 0603. | Device:C |
| R5 | 33 | Resistor_SMD:R_0603_1608Metric | RC0603FR-0733RL (UNVERIFIED) | Output series resistor per output.series_R_ohm. Yageo RC0603, 1 %. This is not a 50 ohm match (output.load). | Device:R |
| J2 | B6252HB-NPP3G-50 | Connector_Coaxial:BNC_Amphenol_B6252HB-NPP3G-50_Horizontal | B6252HB-NPP3G-50 (UNVERIFIED) | Right-angle through-hole PCB BNC receptacle (Amphenol RF), at the board edge. It replaces the brief's 31-5536-RFX, which has no installed footprint (see substitutions). Center pin to OUT, shell to GND. The connector's 50 ohm rating is the connector family's impedance, not a drive claim (output.load). | Connector:Conn_Coaxial |
| J3 | TSW-102-07-G-S | Connector_PinHeader_2.54mm:PinHeader_1x02_P2.54mm_Vertical | TSW-102-07-G-S (UNVERIFIED) | Brief part. Samtec TSW 1x2 2.54 mm through-hole header, gold, single row; -55 to +105 C. Pin 1 is OUT and pin 2 is GND (SPEC 4). | Connector_Generic:Conn_01x02 |
| D2 | Green | LED_SMD:LED_0603_1608Metric | 150060GS75000 (UNVERIFIED) | Power LED. Wurth WL-SMCW 0603 green: VF about 2.0 to 3.2 V, -40 to +85 C. It runs at about 1.5 mA through R6, within the SUBSYSTEMS budget of 1.6 mA. | Device:LED |
| R6 | 2.0k | Resistor_SMD:R_0603_1608Metric | RC0603FR-072KL (UNVERIFIED) | D2 series resistor: (5.25 - 2) V / 2 k = 1.6 mA. Yageo RC0603, 1 %. | Device:R |
| D3 | Green | LED_SMD:LED_0603_1608Metric | 150060GS75000 (UNVERIFIED) | Activity LED, driven from BUF_OUT and never from TIMING (timing.node_loading). Same Wurth 0603 green as D2. | Device:LED |
| R7 | 2.0k | Resistor_SMD:R_0603_1608Metric | RC0603FR-072KL (UNVERIFIED) | D3 series resistor from BUF_OUT; average current <= 1.5 mA. Yageo RC0603, 1 %. | Device:R |
| TP1 | 5V | TestPoint:TestPoint_Pad_D1.5mm | (no part) | Bare top-side pad on +5V. | Connector:TestPoint |
| TP2 | GND | TestPoint:TestPoint_Pad_D1.5mm | (no part) | Bare top-side pad on GND. | Connector:TestPoint |
| TP3 | TIMING | TestPoint:TestPoint_Pad_D1.5mm | (no part) | Bare pad on TIMING, the only extra load allowed there (timing.node_loading). The silkscreen note reads 'probe shifts freq'. | Connector:TestPoint |
| TP4 | RAW | TestPoint:TestPoint_Pad_D1.5mm | (no part) | Bare pad on RAW (U1 OUT). | Connector:TestPoint |
| TP5 | OUT | TestPoint:TestPoint_Pad_D1.5mm | (no part) | Bare pad on OUT, after R5. | Connector:TestPoint |
| H1 | M3 | MountingHole:MountingHole_3.2mm_M3 | (no part) | M3 mounting hole, 3.2 mm, per board.mounting_holes. | Mechanical:MountingHole |
| H2 | M3 | MountingHole:MountingHole_3.2mm_M3 | (no part) | Second M3 mounting hole per board.mounting_holes. | Mechanical:MountingHole |

## Substitutions

| Part | Wanted | Chosen | Reason |
| --- | --- | --- | --- |
| J2 | 31-5536-RFX | B6252HB-NPP3G-50 | No footprint for the Amphenol 31-5536 right-angle BNC is installed on this machine (check_footprints: Connector_Coaxial has B6252HB-NPP3G-50_Horizontal, 031-5539_Vertical, B6252HB_Horizontal). The 031-6575_Horizontal footprint was tried first and rejected: its pads 3 and 4 match no pin of any installed coax symbol (Conn_Coaxial has In/Ext only), so they would float. The B6252HB-NPP3G-50 is the remaining installed Amphenol RF right-angle through-hole PCB BNC, and its electrical pads map 1:1 onto Conn_Coaxial, which keeps the brief's right-angle, board-edge, through-hole intent. |
