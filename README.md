[README.md](https://github.com/user-attachments/files/35287730/README.md)
# ESP32-S3 Offline Chime Detector

**Practical Electronics | Mechatronic Systems Engineering | Rhine-Waal University of Applied Sciences**

`ESP32-S3` `KiCad 10` `Two-layer PCB` `Analog electronics` `LTspice` `Goertzel`

I'm working on a small USB-C-powered board that listens for familiar household sounds and turns them into visual alerts. I wanted to build something that works locally, without sending sound to a cloud service. The hardware brings together a microphone, analog signal conditioning, an ESP32-S3 and three indicator LEDs.

My work on PE-04 has focused on recording and analysing the sounds, testing a Goertzel-based microwave-beep detector, exploring the microphone front-end in LTspice and working on the KiCad circuit/PCB with my teammate.

## Project at a glance

| | |
| --- | --- |
| **Latest design** | KiCad V2, 22 November 2026 |
| **Microcontroller** | ESP32-S3-WROOM-1 |
| **Power** | USB-C 5 V input, TLV62569 buck converter to 3.3 V |
| **Audio input** | AOM-5024P-HD-MB-R electret microphone |
| **Analog front-end** | AD8656ARZ preamplifier + TLV9062 active filtering |
| **PCB** | 2 copper layers, 1.6 mm board, 74.3 × 57.5 mm outline |
| **Layout** | 57 electronic footprints, four M2 mounting holes, bottom GND copper zone |
| **Output** | Three individual LED channels |
| **Current stage** | V2 schematic and routing available; assembly and measurements next |

![PCB routing view from an earlier design stage](images/pcb/latest-layout-screenshot-2026-11-18.jpg)

*KiCad routing screenshot taken 18 November. The current editable V2 PCB is linked below. A new V2 layout export and 3D render will replace this preview once exported from KiCad.*

## Project files

- [KiCad V2 schematic](hardware/current/PE04_Chime_Detector.kicad_sch)
- [KiCad V2 PCB](hardware/current/PE04_Chime_Detector.kicad_pcb)
- [KiCad project and libraries](hardware/current/)
- [Design rules](hardware/current/PE04_Chime_Detector.kicad_dru)
- [PCB assembly BOM](procurement/PE04_V2_Assembly_BOM.csv) and [selected supplier parts](procurement/PE04_Supplementary_Selected_Parts.csv)
- [Hardware design notes](docs/hardware-architecture.md)
- [LTspice experiments](docs/ltspice-experiments.md)
- [Sound-analysis tests](docs/sound-analysis.md)
- [Assembly and bench-testing log](docs/assembly-and-testing.md)

## My work

### 1. Recording and identifying sound patterns

I started with sound recordings because a single frequency is not enough to identify an event. I checked the microwave completion beeps, the doorbell melody and a smoke-alarm *test* signal. The microwave signal has a strong tone near 2,050 Hz. The doorbell moves between several tones, while the smoke-alarm test signal has repeated bursts around 2.8 kHz.

![Doorbell and smoke-alarm test recordings](images/audio/doorbell-and-smoke-detector-spectrogram.png)

The first microwave detector was too simple: it also reacted to hand claps. I then tested a Goertzel-based approach that considers tone purity, duration and the timing of a full three-beep pattern.

| Development recording | Expected alerts | Reported alerts |
| --- | ---: | ---: |
| Microwave 1 | 1 | 1 |
| Microwave 2 | 1 | 1 |
| Microwave with claps | 1 | 1 |
| Claps only | 0 | 0 |

These four results are from offline Python tests on a small set of recordings. The doorbell and smoke-alarm patterns have been analysed, but separate detectors for them are still to be built.

[How I analysed the recordings](docs/sound-analysis.md)

### 2. Testing the microphone front-end in LTspice

I used LTspice to understand what happens to the small microphone signal before it reaches an ADC. I worked with a 3.3 V supply, a 1.65 V reference, non-inverting amplification and low-pass filtering. Along the way I tested transient response, microphone-bias noise and an op-amp model that gave convergence problems.

![Early LTspice circuit](images/ltspice/initial-frequency-sweep-schematic.png)

![Early LTspice AC response](images/ltspice/initial-ac-frequency-response.png)

For the circuit pictured here, the saved AC cursor shows **+20.08 dB at 2.054 kHz** for `V(adc_out)/V(mic_raw)`. That is the gain of the amplifier *and* output RC network in this early simulation. It is not the measured response of our later AD8656ARZ/TLV9062 PCB.

[LTspice plots and notes](docs/ltspice-experiments.md)

### 3. KiCad schematic and PCB development

The V2 hardware combines eight practical blocks: USB-C input, 3.3 V conversion, microphone bias, preamplifier and reference, active low-pass filter, ADC interface, ESP32-S3, and LED outputs.

**Signal path:** microphone → AC coupling → AD8656ARZ gain stage → TLV9062 filter → ESP32-S3 GPIO4 ADC → LED channels.

| Circuit section | Main components | What it does |
| --- | --- | --- |
| USB-C / protection | J2, R3/R4, U3 | Power/data connector, CC resistors and USB protection |
| Power supply | U1, L1 | Buck conversion from 5 V to 3.3 V |
| Microphone input | MK1, R14, R23/C13, C11 | Microphone bias, supply filtering and AC coupling |
| Reference and preamp | U4A/U4B, R9/R10, R12/R13 | Buffered 1.65 V reference and nominal 11× gain |
| Low-pass filter | U5, R15–R18, C12/C14/C15/C16 | Two second-order Sallen-Key stages, targeting about 7 kHz |
| Microcontroller / indicators | U2, D1–D3 | Sound-sampling controller and three LED channels |

The V2 PCB has 61 footprints in total, including four mounting holes. The full editable project, local symbol/footprint libraries, two 3D model files and assembly BOM are in the repository.

[PCB circuit details and component references](docs/hardware-architecture.md)

## What I learned

- A frequency match alone can mistake a clap for a chime; the timing of the sound matters.
- An electret microphone needs the right DC bias and enough analog gain to produce a usable ADC signal.
- A simulated gain plot only describes the particular model and circuit used in that run.
- The analog filter cutoff and microcontroller sampling frequency have to be considered together.

## Current build status

| Stage | Status |
| --- | --- |
| V2 schematic, PCB and custom KiCad libraries | Available |
| V2 BOM and selected supplier parts | Available |
| Offline microwave-beep analysis | Development tests recorded |
| LTspice microphone-front-end studies | Screenshots and notes available |
| KiCad ERC / DRC results | Not yet published |
| Soldering, first power-up, measurements | Next stage |
| ESP32 firmware and three-sound recognition | Not yet implemented |

The original `.asc` simulation files, the Goertzel notebook and WAV recordings are also still to be added for reproducibility. The intended LED-to-sound mapping has not been implemented. This is a university demonstrator, not a replacement for a certified smoke alarm.

## Opening the KiCad design

Install KiCad 10 and open [`hardware/current/PE04_Chime_Detector.kicad_pro`](hardware/current/PE04_Chime_Detector.kicad_pro). Keep the `libraries/` folder and the local `fp-lib-table` and `sym-lib-table` in the same project directory.


