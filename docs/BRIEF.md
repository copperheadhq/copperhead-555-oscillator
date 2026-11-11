# 5 V variable-frequency 555 oscillator

## Purpose
A compact bench oscillator that generates an adjustable square wave from approximately 10 kHz to 1 MHz for an oscilloscope or 5 V logic input. This is a 555 astable oscillator, not a Hartley LC oscillator.

## Parts
- TLC555IDR CMOS timer (Texas Instruments)
- SN74LVC1G17DBVR single Schmitt-trigger buffer (Texas Instruments)
- USB4105-GF-A USB-C receptacle (GCT)
- 3296W-1-104LF 100 kΩ 25-turn top-adjust trimmer potentiometer for frequency (Bourns); see `research/parts/frequency-trimmer.md`. This replaces the 3310Y-001-104L in the first draft: that part is a single-turn panel pot (DigiKey and Farnell listings, read 2026-11-10), and the brief asks for multi-turn.
- 31-5536-RFX right-angle through-hole BNC receptacle (Amphenol RF)
- TSW-102-07-G-S 2-pin 2.54 mm output header (Samtec)
- TPD1E10B06DYAR ESD protection diode on VBUS, SOD-523 (Texas Instruments); see `research/parts/vbus-esd.md`
- Two C0G timing capacitors, about 3.3 nF and 330 pF, one per frequency range (exact values set by the build), 1% timing resistors, 100 nF local bypass capacitors, and a 10 µF input capacitor
- Power LED and output-activity LED, with the activity LED isolated from the timing node
- A top-side slide switch, with its slider moved from above, that selects the frequency range by switching the timing capacitor: C&K JS102011SCQN; see `research/parts/range-switch.md`. This replaces the right-angle JS102011SAQN of the first build, whose slider points sideways (person's decision, 2026-11-10)

## Power
5 V DC through USB-C, with 5.1 kΩ pull-down resistors on CC1 and CC2. Target consumption is below 30 mA. Include input ESD protection and local decoupling. No battery or onboard regulator.

## Interfaces
- Buffered square-wave output on BNC and a parallel 2-pin signal/ground header
- 33 Ω series resistor at the buffer output
- Frequency control by the top-access 25-turn trimmer, set with a screwdriver, in two ranges selected by the slide switch: a low range and a high range that overlap so that together they cover 10 kHz to 1 MHz
- Test points for 5 V, ground, the TLC555 timing capacitor, raw timer output, and buffered output

## Physical
- Two-layer PCB, approximately 60 by 35 mm, no enclosure
- Put the potentiometer, USB-C connector, BNC connector, LEDs, and test points on the top side
- Place the BNC at a board edge and provide two M3 mounting holes
- Assembled by a fab (PCBA, for example JLCPCB). The through-hole BNC, header and trimmer may be hand-soldered if the fab does not place them
- A few boards (about 5), used indoors on a bench. Commercial temperature range (0 to 70 °C) is enough

## Design constraints
- Nominal adjustment range: 10 kHz to 1 MHz into a high-impedance oscilloscope or CMOS logic input
- Use C0G/NP0 timing capacitors and 1% resistors for stability
- Keep the timing-node trace short and away from the buffered output
- Provide a continuous ground plane beneath the oscillator and output path
- Add clearly marked frequency endpoint, range-switch position, and output labels to the silkscreen
- Put a copperhead identity block on the top (front) silkscreen, in the free area along the bottom edge below RV1, U1 and TP4 and left of D3 and J3, clear of every pad: the copperhead mark (the fiducial, a ring with four ticks) beside the lowercase wordmark `copperhead`, then the board name `555 variable oscillator` and a line `5 V · 10 kHz–1 MHz · rev A`, all left-aligned to the mark's left edge. No date. The mark comes from `research/references/copperhead-branding/icon-transparent.svg`. Nothing of the block stays on the bottom silkscreen, and the existing front labels stay as they are (person's decision, 2026-11-11; it was first placed on the bottom the same day, then the date was dropped and the lines left-aligned)

## Must not
- Do not claim 50 Ω output drive. The BNC is intended for a high-impedance scope input, not a 50 Ω terminated load
- No battery and no onboard regulator
- The activity LED must not load the timing node

## Sources
- [TLC555 datasheet](https://www.ti.com/lit/ds/symlink/tlc555.pdf), for 5 V operation, astable configuration, and operation up to the requested frequency
- [SN74LVC1G17 datasheet](https://www.ti.com/lit/ds/symlink/sn74lvc1g17.pdf), for 5 V buffer operation and Schmitt-trigger input behavior
- [USB4105 product page](https://gct.co/connector/usb4105), for the USB-C receptacle
- [DigiKey 3310Y-001-104L](https://www.digikey.com/en/products/detail/bourns-inc/3310Y-001-104L/3310Y-001-104L-ND/1088216) and [Farnell 3310Y-001-104L](https://uk.farnell.com/bourns/3310y-001-104l/potentiometer-100k/dp/9353984), read 2026-11-10: single-turn, about 300°, ±1000 ppm/°C, panel mount. This is why it was replaced

Lifecycle and stock of the TI devices, connectors and the trimmer have not been checked against a distributor yet.

## Assumptions
- The requested circuit is a 555 astable oscillator. A Hartley oscillator is not included.
- A buffered 0 V to approximately 5 V square wave is preferred over the raw timer output.
- The BNC will normally feed a 1 MΩ oscilloscope input. The pin header may feed a high-impedance 5 V logic input.
- Frequency is set with a multi-turn control in two ranges. The first draft and the first refinement had one range; the person chose two ranges on 2026-11-10, after the trimmer's datasheet showed one range cannot be guaranteed. The 3296's absolute minimum resistance is "1 % or 2 ohms max., whichever is greater" (up to 1 kΩ for 100 kΩ), so one range spans just under 100:1 at worst, and 10 kHz to 1 MHz needs exactly 100:1 (see `research/parts/frequency-trimmer.md`). Exact endpoints will depend on component tolerances, stray capacitance and TLC555 propagation effects near 1 MHz. Within each range, most of the trimmer's travel tunes the low end, because frequency goes as 1/R.
- Duty cycle is allowed to vary with frequency in the conventional astable topology and is not guaranteed to be 50%.
- USB-C is used only for 5 V power. Its D+ and D− pins are unconnected.

## Open questions
- None.
