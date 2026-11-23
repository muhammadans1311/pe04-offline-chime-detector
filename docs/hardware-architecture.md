# PE-04 Hardware Design

## PCB overview

This is the V2 hardware design dated 22 November 2026. I worked on the signal-chain integration and reviewed how the microphone circuit, supply, ADC and outputs fit together in the KiCad project.

| PCB detail | V2 source |
| --- | --- |
| Copper stack | 2 layers: F.Cu and B.Cu |
| Board outline | 74.3 × 57.5 mm |
| Board thickness | 1.6 mm in the KiCad file |
| Electronic placements | 57 |
| Mechanical holes | H1–H4, 2.2 mm M2 |
| Routing in the saved PCB | 383 segment entries and 57 via entries |
| Ground plane | GND copper zone on B.Cu |

The current project contains [the schematic](../hardware/current/PE04_Chime_Detector.kicad_sch), [PCB](../hardware/current/PE04_Chime_Detector.kicad_pcb), [project configuration](../hardware/current/PE04_Chime_Detector.kicad_pro), [design rules](../hardware/current/PE04_Chime_Detector.kicad_dru) and [custom KiCad libraries](../hardware/current/libraries/).

## 1. USB-C and 3.3 V supply

The board accepts nominal 5 V through a 629722000214 USB-C connector (J2). R3 and R4 are separate 5.1 kΩ CC pull-downs. U3 (USBLC6-2SC6) protects the USB data interface. U1 (TLV62569DBV) is the buck regulator, paired with a 2.2 µH inductor (L1). R1 = 450 kΩ and R2 = 100 kΩ form its feedback network for the intended 3.3 V output.

The supply has to power the ESP32-S3 and the microphone/analog stages. I would start first power-up by checking 3.3 V without connecting any external signal source.

## 2. Electret microphone and bias

MK1 is the AOM-5024P-HD-MB-R electret microphone.

- R14 = 2.2 kΩ biases the microphone.
- R23 = 100 Ω and C13 = 10 µF filter its supply.
- C11 = 100 nF AC-couples the microphone signal.
- R11 = 22 kΩ provides the input's reference path. The simple C11/R11 high-pass estimate is about 72 Hz.

This lets the small AC microphone signal be handled by an amplifier running from one positive supply rail.

## 3. Mid-supply reference and preamplifier

R12 and R13 are both 10 kΩ, making a nominal 1.65 V midpoint from 3.3 V. C9 = 10 µF and C10 = 100 nF filter this node. U4B buffers the midpoint, and U4A is the microphone preamplifier. Both op-amps are in the dual AD8656ARZ package.

The preamp feedback has R9 = 47 kΩ and R10 = 4.7 kΩ:

```text
Nominal gain = 1 + R9 / R10
             = 1 + 47 kΩ / 4.7 kΩ
             = 11 V/V, about 20.8 dB
```

That is the resistor-ratio design gain. I still need to compare it with measured waveforms after assembly.

## 4. Active filter and ADC

U5 is a TLV9062. The design uses two second-order Sallen-Key filter stages:

| Stage | R values | C values |
| --- | --- | --- |
| First | R15/R16 = 2.49 kΩ each | C12 = 8.2 nF; C14 = 10 nF |
| Second | R17/R18 = 2.67 kΩ each | C15 = 22 nF; C16 = 3.3 nF |

The intended overall filter is fourth-order with a corner around 7 kHz. R19 = 220 Ω and C18 = 1 nF sit at the ESP32 ADC input (GPIO4 / ADC1_CH3).

For the firmware stage I still have to choose the ESP32 ADC sample rate. The 16 kHz rate from the offline Python recordings is not automatically the hardware rate, and the filter's rejection near Nyquist must be checked.

## 5. ESP32, programming and LED outputs

U2 is an ESP32-S3-WROOM-1. The design includes RESET and BOOT switches and three test points. The three indicators use separate ESP32 outputs and 330 Ω series resistors:

| Channel | LED | Selected part |
| --- | --- | --- |
| D1 / R20 | Green / 330 Ω | Kingbright APT3216LZGCK |
| D2 / R21 | Blue / 330 Ω | Kingbright APT3216LVBC/D |
| D3 / R22 | Red / 330 Ω | Kingbright APT3216SURCK |

The supplier selections are in [the parts supplements](../procurement/). We still need to check actual LED brightness and assign each sound category to an output in firmware.

## 6. Layout and mechanical work

The saved PCB has two copper layers, a B.Cu ground zone, four mounting holes and a defined ESP32 antenna area. The PCB outline is 74.3 × 57.5 mm. The editable V2 source is the main layout reference; the image currently on the README is a screenshot from an earlier routing stage.

The next checks are the native ERC/DRC reports, final visual inspection around the connector and antenna, then assembly. [I have a separate bench log](assembly-and-testing.md) for the measurements once the board is soldered.

## KiCad files and BOM

- [V2 schematic](../hardware/current/PE04_Chime_Detector.kicad_sch)
- [V2 routed PCB](../hardware/current/PE04_Chime_Detector.kicad_pcb)
- [V2 project](../hardware/current/PE04_Chime_Detector.kicad_pro)
- [V2 design rules](../hardware/current/PE04_Chime_Detector.kicad_dru)
- [Full assembly BOM](../procurement/PE04_V2_Assembly_BOM.csv)
- [Selected supplier parts](../procurement/PE04_Supplementary_Selected_Parts.csv)
