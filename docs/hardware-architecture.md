# Hardware — ESP32-S3 Chime Detector

The PE-04 schematic integrates USB-C power/data, a 3.3 V buck converter, an electret microphone, an analog preamplifier, two active low-pass filter stages, ESP32-S3 ADC input and three LED outputs.

## Main signal path

Electret microphone → bias network → C11 AC coupling → AD8656 preamplifier at 1.65 V reference → TLV9062 fourth-order active low-pass → R19/C18 ADC input → ESP32-S3 GPIO4.

The microcontroller is intended to classify sound patterns and drive individual LEDs. Firmware and sound-to-LED assignments are still to be developed.

## Components in the uploaded KiCad revision

| Function | References | Saved values |
| --- | --- | --- |
| USB connector and CC | J2, R3, R4 | 629722000214, 5.1 kΩ, 5.1 kΩ |
| USB ESD device | U3 | USBLC6-2SC6 |
| Buck supply | U1, L1, R1, R2 | TLV62569DBV, 2.2 µH, 450 kΩ, 100 kΩ |
| Microphone | MK1 | AOM-5024P-HD-MB-R |
| Microphone bias | R14 | 2.2 kΩ |
| Microphone-supply RC filtering | R23, C13 | 100 Ω, 10 µF |
| Audio AC coupling | C11 | 100 nF; passes AC to the preamp |
| Preamp input reference path | R11 | 22 kΩ to 1.65 V reference |
| Mid-supply divider | R12, R13 | 10 kΩ each |
| Preamplifier feedback | U4, R9, R10 | AD8656, 47 kΩ, 4.7 kΩ; nominal 11× |
| Filter stage 1 | U5, R15, R16, C12, C14 | TLV9062, 2.49 kΩ each, 8.2 nF, 10 nF |
| Filter stage 2 | U5, R17, R18, C15, C16 | TLV9062, 2.67 kΩ each, 22 nF, 3.3 nF |
| ADC isolation | R19, C18 | 220 Ω, 1 nF |
| Indicators | D1–D3, R20–R22 | Green, blue, red; 330 Ω each |

C11 with R11 has a nominal single-RC high-pass corner near **72 Hz** (`1 / (2π · 22 kΩ · 100 nF)`). This is a simplified estimate, not a measured response of the complete amplifier.

The two Sallen–Key sections are designed to produce a fourth-order low-pass with an approximate 7 kHz target. The actual integrated circuit response should be checked by matching-part simulation and then on hardware.

## KiCad project files

These source files are an **earlier revision**, not necessarily the PCB version shown in the November 18 screenshot:

- [Schematic (.kicad_sch)](../hardware/archive/earlier-kicad-sources/PE04_Chime_Detector_Schematics.kicad_sch)
- [PCB (.kicad_pcb)](../hardware/archive/earlier-kicad-sources/PE04_Chime_Detector_Schematics.kicad_pcb)
- [Project (.kicad_pro)](../hardware/archive/earlier-kicad-sources/PE04_Chime_Detector_Schematics.kicad_pro)

![Latest supplied PCB view](../images/pcb/latest-layout-screenshot-2026-11-18.jpg)

## Checks for the next revision

The three LED footprints currently have 330 Ω series resistors, but LED part numbers and brightness requirements have not been specified. Calculate current and choose resistors after the actual LEDs and forward-voltage range are selected.

The offline sound experiments used 16 kHz audio. That is **not an established ESP32 ADC sampling rate**. Before implementing the detector, choose a hardware sample rate and verify analog anti-aliasing; a 7 kHz cutoff would provide limited rejection near an 8 kHz Nyquist frequency if sampling at 16 kHz.

For the later PCB revision, run ERC and DRC, verify connections, inspect the ESP32 antenna keep-out and remaining possible open track ends, and record the actual findings before fabrication.
