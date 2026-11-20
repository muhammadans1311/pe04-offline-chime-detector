# PE-04 | ESP32-S3 Offline Chime Detector

**Muhammad Ans | Mechatronic Systems Engineering | Practical Electronics, Hochschule Rhein-Waal**

KiCad · PCB design · LTspice · Analog electronics · Python signal processing

For my Practical Electronics project, I am working on a USB-powered sound detector that translates household chimes into visual alerts. It combines a microphone front-end, analog filtering, an ESP32-S3 and three LED channels. The aim is to recognize a sound by its frequency **and** timing pattern without relying on cloud processing.

My main work documented here covers audio analysis, Goertzel-based detection experiments, analog circuit simulation and participation in the ESP32-S3 schematic/PCB design.

![PE-04 PCB layout in KiCad](images/pcb/latest-layout-screenshot-2026-11-18.jpg)

*PCB layout under development, November 2026.*

## My engineering work

### 1. Sound analysis and detection logic

I started with real recordings to find the frequency and timing patterns of a microwave chime, doorbell and smoke-detector test signal. An early frequency-only trigger near 2,050 Hz produced false alerts when I added hand claps.

I tested a more selective offline approach using:

- 16 kHz mono audio, 1,024-sample Hann windows and a 160-sample hop.
- Goertzel analysis around the microwave's 2,050 Hz tone.
- Tone-purity, minimum beep-duration and three-beep timing checks.

The development recordings produced the expected alert counts:

| Recording | Expected | Detected |
| --- | ---: | ---: |
| Microwave recording 1 | 1 | 1 |
| Microwave recording 2 | 1 | 1 |
| Microwave with claps | 1 | 1 |
| Claps only | 0 | 0 |

![Doorbell and smoke-detector test recordings](images/audio/doorbell-and-smoke-detector-spectrogram.png)

The implemented *offline detection rules* currently target microwave beeps. The doorbell and smoke-detector recordings were characterized separately and require different recognition rules.

[Read my sound-analysis notes](docs/sound-analysis.md)

### 2. Analog signal conditioning and LTspice

I explored how to bring a small electret-microphone signal into an ADC-friendly range using a 3.3 V supply, mid-supply bias, non-inverting amplification and low-pass filtering.

![LTspice AC simulation](images/ltspice/initial-ac-frequency-response.png)

In the saved amplifier-plus-RC-filter experiment, the AC cursor reads approximately +20.08 dB at 2.054 kHz for `V(adc_out)/V(mic_raw)`. I also investigated startup and transient behavior, microphone-bias supply noise, and convergence problems when importing an op-amp manufacturer model.

The screenshot above is from an earlier LTspice concept, with different op-amps and filtering from the integrated KiCad design. I keep those experiments separate to make it clear what each plot demonstrates.

[Read my LTspice experiments](docs/ltspice-experiments.md) · [Circuit screenshot](images/ltspice/initial-frequency-sweep-schematic.png) · [Transient traces](images/ltspice/real-mic-bias-transient.png)

### 3. PCB and electronic system design

I have also worked on the team's KiCad schematic and two-layer PCB, focusing on the microphone signal path, circuit integration and power/I/O interfaces. The board brings together these stages:

| Function | Circuit implementation |
| --- | --- |
| Power and USB | USB-C input, TLV62569DBV 3.3 V buck converter, USB protection |
| Microphone | AOM-5024P-HD-MB-R electret microphone, bias and AC coupling |
| Reference and gain | AD8656 buffered 1.65 V reference and nominal 11× preamplifier |
| Analog filtering | TLV9062 with two second-order Sallen-Key low-pass sections |
| Microcontroller | ESP32-S3-WROOM-1; ADC connected on GPIO4 |
| Indicators | Three LED channels with individual series resistors |

The analog circuit aims for a fourth-order low-pass response around 7 kHz. The nominal preamplifier gain, filter and ADC input network are documented in the [hardware notes](docs/hardware-architecture.md). A [57-component design-value BOM](hardware/archive/earlier-kicad-sources/pe04-design-bom.csv) is also available.

The latest PCB layout screenshot is shown above. [Earlier editable KiCad files](hardware/archive/earlier-kicad-sources/) are included for design inspection; the matching native files for the newest layout will be added when available.

## Design lessons

- A frequency match alone can misclassify short sounds. Temporal patterns and tone purity matter.
- A microphone front-end needs correct DC biasing and sufficient signal swing for the ADC.
- Simulation values only describe the circuit and models used for that particular run.
- Sampling frequency and analog filter cutoff must be chosen together to avoid aliasing.

## Project files

| Folder | Contents |
| --- | --- |
| [`docs/hardware-architecture.md`](docs/hardware-architecture.md) | Circuit blocks, component values, design checks |
| [`docs/ltspice-experiments.md`](docs/ltspice-experiments.md) | Analog simulations and troubleshooting |
| [`docs/sound-analysis.md`](docs/sound-analysis.md) | Frequency analysis, Goertzel parameters and test cases |
| [`hardware/`](hardware/archive/earlier-kicad-sources/) | KiCad schematic, PCB, project file and BOM |
| [`images/`](images/) | PCB, oscilloscope-style simulation plots and spectrogram |

## Current status

The design is in progress. The repository contains an earlier native KiCad revision, an updated PCB screenshot and documented simulation/audio experiments. The original LTspice `.asc` files, offline Python notebook and test recordings are not yet included. Next steps are the matching latest KiCad files, ERC/DRC, real-time ESP32 firmware, board bring-up and measurements.

The sound-to-LED mapping has not yet been implemented. This student prototype is not a certified smoke-alarm or safety device.

*Team project: Muhammad Ans; schematic and PCB collaboration with Ahmed Yehia Mohamed.*
