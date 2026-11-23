# Hardware design | PE-04 V2

*Technical notes: Muhammad Ans · KiCad revision V2, 22 November 2026*

The V2 design integrates a USB-C interface, 3.3 V converter, electret microphone, analog preamplifier and filter, ESP32-S3 and three LEDs. The source files below are the current set received for assembly, not the archived first revision.

## KiCad source

- [Project](../hardware/current/PE04_Chime_Detector.kicad_pro)
- [Schematic](../hardware/current/PE04_Chime_Detector.kicad_sch)
- [PCB](../hardware/current/PE04_Chime_Detector.kicad_pcb)
- [Design rules](../hardware/current/PE04_Chime_Detector.kicad_dru)
- [Custom symbols, footprints and 3D files](../hardware/current/libraries/)
- [Assembly BOM](../procurement/PE04_V2_Assembly_BOM.csv)

The project-local library tables use `${KIPRJMOD}` paths. Open `hardware/current/PE04_Chime_Detector.kicad_pro` in KiCad so the project files and libraries resolve together. The supplied files identify KiCad 10.

## Power and USB-C

| Item | V2 parts | Purpose |
| --- | --- | --- |
| USB-C | J2, 629722000214 | Input and USB connection |
| CC detection | R3/R4, 5.1 kΩ | USB-C sink pull-downs |
| ESD | U3, USBLC6-2SC6 | USB data protection |
| Buck | U1, TLV62569DBV | Nominal 5 V to 3.3 V |
| Inductor | L1, 2.2 µH | Buck conversion |
| Buck feedback | R1/R2, 450 kΩ / 100 kΩ | Sets the designed output voltage |

## Microphone and analog front-end

- MK1: AOM-5024P-HD-MB-R electret microphone.
- R14: 2.2 kΩ microphone bias.
- R23 / C13: 100 Ω / 10 µF microphone-supply RC filtering.
- C11 / R11: 100 nF audio coupling and 22 kΩ input reference path; simple RC estimate near 72 Hz.
- R12 / R13: two 10 kΩ resistors establishing nominal 1.65 V midpoint.
- C9 / C10: 10 µF / 100 nF reference filtering.
- U4B: second half of the AD8656ARZ, buffering the midpoint.
- U4A: AD8656ARZ preamplifier with R9 = 47 kΩ and R10 = 4.7 kΩ, nominal gain `1 + 47 / 4.7 = 11` (about 20.8 dB).

V2 specifically labels U4 as **AD8656ARZ**, instead of the generic AD8656 designation in the earlier archived design.

## Active filter and ADC

U5 is a TLV9062 with two second-order Sallen-Key sections:

| Stage | Resistors | Capacitors |
| --- | --- | --- |
| 1 | R15/R16: 2.49 kΩ each | C12: 8.2 nF; C14: 10 nF |
| 2 | R17/R18: 2.67 kΩ each | C15: 22 nF; C16: 3.3 nF |

The design targets a fourth-order low-pass near 7 kHz. R19 = 220 Ω and C18 = 1 nF provide ADC input conditioning before ESP32-S3 GPIO4. The final response has not been bench-measured.

The Python sound experiments used 16 kHz recorded audio, but that does not establish the MCU ADC rate. The final ADC sampling rate and anti-aliasing margin must be selected and checked together.

## Controller, LEDs and mechanical layout

- U2: ESP32-S3-WROOM-1.
- D1 green, D2 blue, D3 red; R20/R21/R22 are each 330 Ω.
- The supplementary purchasing lists select Kingbright 1206 parts: D1 APT3216LZGCK; D2 APT3216LVBC/D; D3 APT3216SURCK.
- SW1/2: RESET and BOOT switches; TP1–TP3 test points.
- V2 adds H1–H4 mounting holes, 2.2 mm M2.

The board has **61 footprints**, including four mounting holes; the other 57 references match the V2 schematic values. The LEDs and resistors still need actual brightness/current checks during bring-up.

## Before assembly

Open the native KiCad project, run ERC and DRC with the supplied rule file, review any warnings and export a final schematic PDF and manufacturing files if required. A supplied `.kicad_dru` contains rules, not proof that a DRC has passed. Check the PCB's tracks, ground return, USB-C connections, analog layout and ESP32 antenna keep-out.

[Assembly and bring-up checklist](assembly-and-testing.md)
