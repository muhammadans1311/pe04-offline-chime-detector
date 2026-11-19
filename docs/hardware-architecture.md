# Hardware design and KiCad files

## System approach

The PE-04 board is designed around an ESP32-S3-WROOM-1. USB-C provides power and a USB data interface; a switching converter supplies the 3.3 V rail. An electret microphone is AC-coupled into a preamplifier referenced around mid-supply. Two active low-pass filter stages condition the signal for the ESP32 ADC. GPIO outputs drive three separate indicator LEDs.

**Signal path:** Electret mic → bias / AC coupling → AD8656 preamplifier → TLV9062 filtering → ADC input conditioning → ESP32-S3 → three LED channels.

## Major components in the uploaded native KiCad revision

| Design block | Reference | Component / values |
| --- | --- | --- |
| USB-C connector | J2 | 629722000214 |
| USB CC resistors | R3, R4 | 5.1 kΩ each |
| USB data protection | U3 | USBLC6-2SC6 |
| Switching supply | U1, L1 | TLV62569DBV; 2.2 µH |
| Buck feedback | R1, R2 | 450 kΩ, 100 kΩ |
| Microphone | MK1 | AOM-5024P-HD-MB-R |
| Mic bias / supply decoupling | R14, R23, C13, C11 | 2.2 kΩ, 100 Ω, 10 µF, 100 nF |
| Analog reference | R12, R13 | 10 kΩ each; nominal 1.65 V midpoint |
| Preamplifier | U4, R9, R10 | AD8656; 47 kΩ, 4.7 kΩ; nominal 11× gain |
| Active filter | U5 | TLV9062, two Sallen–Key stages |
| First filter stage | R15, R16, C12, C14 | 2.49 kΩ, 2.49 kΩ, 8.2 nF, 10 nF |
| Second filter stage | R17, R18, C15, C16 | 2.67 kΩ, 2.67 kΩ, 22 nF, 3.3 nF |
| ADC input | R19, C18 | 220 Ω, 1 nF |
| Control / indicators | U2, D1–D3, R20–R22 | ESP32-S3-WROOM-1; green, blue, red; 330 Ω each |

The intended fourth-order active filter is described as having an approximately 7 kHz cutoff target. Its response has **not** been measured or independently verified on the later integrated board.

## Native source files

The archive contains **an earlier revision** of these KiCad files:

- [PCB](../hardware/archive/earlier-kicad-sources/PE04_Chime_Detector_Schematics.kicad_pcb)
- [Schematic](../hardware/archive/earlier-kicad-sources/PE04_Chime_Detector_Schematics.kicad_sch)
- [Project settings](../hardware/archive/earlier-kicad-sources/PE04_Chime_Detector_Schematics.kicad_pro)

The schematic is stored under the common project basename for easier opening alongside the PCB and project file. Its original filename is retained in Git history. No component data or schematic wiring was changed as part of that rename.

The schematic and PCB were compared by reference and component Value field: **57 physical references, all agreeing**. That check does not evaluate electrical connectivity, symbol-to-footprint pin mapping or manufacturing rules.

![Current available PCB screenshot](../images/pcb/latest-layout-screenshot-2026-11-18.jpg)

*Later layout screenshot, 18 November 2026. The matching latest editable PCB has not yet been supplied.*

## Before fabrication

The next design revision should be saved as a matching set of KiCad project files. The team should complete ERC and DRC, inspect the USB-C and switching-supply implementation, verify analog headroom and filter response with appropriate op-amp models, check ADC sampling/anti-aliasing, and confirm ESP32 antenna clearance. These checks have not been recorded as passed.
