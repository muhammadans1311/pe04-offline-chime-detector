# PE-04 | Offline Chime Detector

ESP32-S3 | KiCad | LTspice | Sound analysis

Ahmed Yehia Mohamed and I are designing a USB-powered chime detector for Practical Electronics at Rhine-Waal University of Applied Sciences. The board captures sound with an electret microphone, conditions it for an ESP32-S3 and is intended to give visual notifications through three LEDs.

![PCB layout](images/pcb/latest-layout-screenshot-2026-11-18.jpg)

*KiCad PCB layout, 18 November 2026.*

## What I worked on

- Analyzed microwave, doorbell and smoke-detector test recordings to compare tone frequencies and beep patterns.
- Tested a Python/Goertzel microwave-beep detector. Adding tone-purity and timing checks helped reject hand claps that triggered the first frequency-only version.
- Simulated microphone biasing, amplification and filtering in LTspice. I examined AC and transient responses and investigated op-amp model convergence problems.
- Worked with Ahmed on the ESP32-S3 schematic and PCB, including the microphone signal chain, power and I/O connections.

## PCB design

| Section | Design |
| --- | --- |
| Microcontroller | ESP32-S3-WROOM-1 |
| Power | USB-C, TLV62569DBV buck converter, 3.3 V supply |
| Microphone | AOM-5024P-HD-MB-R |
| Analog circuit | AD8656 preamplifier, TLV9062 fourth-order low-pass filter |
| I/O | GPIO4 ADC input, three LED channels |

The schematic uses a 1.65 V analog reference, a nominal 11× preamp and two Sallen-Key filter sections. The intended low-pass corner is around 7 kHz.

[Hardware notes](docs/hardware-architecture.md) | [KiCad files](hardware/archive/earlier-kicad-sources/) | [Design-value BOM](hardware/archive/earlier-kicad-sources/pe04-design-bom.csv)

## LTspice experiments

![LTspice AC sweep](images/ltspice/initial-ac-frequency-response.png)

The early amplifier and RC-filter simulation shows approximately +20.08 dB combined gain at 2.054 kHz. I also explored transient signals, supply ripple and problems with an imported op-amp model.

[LTspice notes and plots](docs/ltspice-experiments.md)

## Sound detection experiments

![Doorbell and smoke-detector spectrogram](images/audio/doorbell-and-smoke-detector-spectrogram.png)

The offline detector was developed for microwave beeps around 2,050 Hz. A simple frequency trigger reacted to claps; adding tone purity and three-beep timing checks improved the behavior. The four development recordings produced the expected alert counts: 1, 1, 1 and 0.

Doorbell and smoke-detector recordings were analyzed, but they need their own recognition rules.

[Sound-analysis notes](docs/sound-analysis.md)

## Status

This is an ongoing university team project. The repository has an earlier editable KiCad revision, the November PCB screenshot, LTspice plots and acoustic analysis. Next are the matching latest KiCad files, original `.asc` files, the Python notebook and recordings, ERC/DRC, firmware and bench testing.

Sound-to-LED assignments are not yet defined. This demonstrator cannot replace a certified smoke alarm.

Team: Muhammad Ans and Ahmed Yehia Mohamed.
