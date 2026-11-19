# PE-04 — Offline Chime Detector

ESP32-S3 · KiCad · LTspice · Python signal analysis

For our Practical Electronics module at Rhine-Waal University of Applied Sciences, Ahmed Yehia Mohamed and I are designing a small USB-powered board that converts recognizable household chimes into visual notifications. The concept uses an electret microphone, an analog front-end, an ESP32-S3 and three indicator LEDs.

![PCB layout in KiCad](images/pcb/latest-layout-screenshot-2026-11-18.jpg)

*PCB layout in progress, 18 November 2026.*

## What I worked on

- **Sound analysis:** I analyzed recordings of microwave, doorbell and smoke-detector test sounds. I worked with a Python/Goertzel prototype focused on a 2,050 Hz microwave beep pattern and tested how adding duration and timing checks affected false triggers from claps.
- **Analog simulation:** I explored microphone biasing, amplification and filtering in LTspice, using frequency sweeps and transient plots. I also investigated difficulties with an imported op-amp model.
- **Board development:** I worked with Ahmed on the ESP32-S3 schematic and PCB design, including the microphone signal path, power and I/O interfaces. The PCB design is team work.

## Hardware

| Section | Components in the uploaded KiCad design |
| --- | --- |
| Microcontroller | ESP32-S3-WROOM-1 |
| USB and power | USB-C, TLV62569DBV buck regulator, 3.3 V rail |
| Microphone | AOM-5024P-HD-MB-R electret microphone |
| Analog front-end | AD8656 preamplifier, TLV9062 active low-pass filter |
| ADC connection | GPIO4 / ADC1_CH3, with input RC conditioning |
| Visual output | Three independently controlled red, blue and green LEDs |

The team schematic uses a 1.65 V mid-supply reference, a nominal 11× preamplifier stage, and two second-order active filter sections. The target is a fourth-order low-pass response around 7 kHz.

[Hardware description and KiCad files](docs/hardware-architecture.md)

## LTspice investigation

![LTspice AC frequency sweep](images/ltspice/initial-ac-frequency-response.png)

This screenshot is from an **early amplifier and RC-filter simulation**, not the later AD8656/TLV9062 PCB. The saved [cursor screenshot](images/ltspice/initial-ac-gain-cursor.png) shows approximately **+20.08 dB at 2.054 kHz** for `V(adc_out)/V(mic_raw)`, the combined gain plotted in that run. I also tested transient signal behavior and investigated op-amp model convergence.

[LTspice notes and screenshots](docs/ltspice-experiments.md)

## Chime recordings and detection

![Doorbell and smoke-detector recording spectrograms](images/audio/doorbell-and-smoke-detector-spectrogram.png)

The offline detector work so far targets **microwave beeps around 2,050 Hz**. A basic frequency trigger also responded to claps, so the prototype added checks for tone purity, beep duration and the spacing of a three-beep pattern. Earlier development tests reported the expected alert counts on four microwave/clap recordings.

Doorbell and smoke-detector signals have been **analyzed as recordings**, but not implemented as working detectors. Their sound patterns need separate recognition rules.

[Sound-analysis method and tests](docs/sound-analysis.md)

## Project status

| Available now | Next steps |
| --- | --- |
| KiCad schematic and PCB source from an earlier revision | Add the native files matching the November layout screenshot |
| PCB layout screenshots | Run ERC/DRC and inspect routing and antenna clearance |
| LTspice screenshots | Add original `.asc` files; simulate the actual board's analog circuit |
| Audio spectrogram and documented microwave/clap tests | Add original notebook and recordings; build ESP32 firmware and test hardware |
| Three LED channels in the schematic | Select LED parts, check brightness/current and assign sound-to-color mapping |

The board has not yet been documented as fabricated or tested. The Python tests used 16 kHz audio; the ESP32 ADC sample rate has not been set or verified. This is a student demonstrator, not a substitute for a certified smoke alarm.

## Files

- [Earlier KiCad design files](hardware/archive/earlier-kicad-sources/)
- [LTspice screenshots](images/ltspice/)
- [Sound spectrogram](images/audio/doorbell-and-smoke-detector-spectrogram.png)
- [Technical notes](docs/)

**Team:** Muhammad Ans and Ahmed Yehia Mohamed. Individual task boundaries and publication permissions for shared project material should be confirmed with the team.
