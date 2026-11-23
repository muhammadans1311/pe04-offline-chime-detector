# PCB Assembly and Bring-Up Log

**Board:** PE-04 Chime Detector, KiCad V2 (22 November 2026)  
**State:** Assembly and measurements to be recorded after soldering.

## Build history

| Date | Work | Evidence |
| --- | --- | --- |
| 22 Nov 2026 | V2 schematic and PCB files saved | Native KiCad source under `hardware/current/` |
| — | ERC and DRC | Add report/results after checking in KiCad |
| — | Component assembly and soldering | Add actual date and PCB photographs |
| — | First power-up | Add supply voltage/current measurements |
| — | Analog signal-chain check | Add oscilloscope traces |
| — | ESP32 firmware and sound tests | Add code and test recordings/results |

## Before powering the board

- Check solder joints and polarity of the electret microphone, LEDs, power IC and op-amps.
- Check for unintended continuity between 5 V, 3.3 V and GND.
- Verify USB-C connections, BOOT/RESET and the ESP32 antenna area.
- Review the supplied design rules, then record actual KiCad ERC/DRC results.

## DC measurements

Enter the actual values after assembly; nothing in this table is a measured result yet.

| Test | Expected / target | Measured | Date |
| --- | --- | --- | --- |
| USB-C input | Nominal 5 V | — | — |
| Regulator output | Nominal 3.3 V | — | — |
| Buffered reference, U4B | Nominal 1.65 V | — | — |
| Microphone bias | Check against schematic | — | — |
| ESP32 boot/reset | Boot and reset available | — | — |
| Supply current | Measure with current limit | — | — |

## Analog and output tests

| Test | What to record | Result |
| --- | --- | --- |
| Preamp gain | Known input, measured Vpp at U4A output, test frequency | — |
| Filter response | Sweep and measured transfer curve | — |
| ADC input | DC offset, signal range, unwanted noise | — |
| LED 1 / 2 / 3 | Voltage/current and visible brightness | — |
| USB / firmware | Whether the ESP32 is detected and program runs | — |
| Sound recognition | True/false triggers with room, distance and level | — |

## If something fails

Record the symptom first. Then check power, reference voltage, continuity, input/output signals and solder joints in that order. Do not write a root cause until the fault is actually isolated.

## Photos and captures to add after soldering

```text
images/bench/assembled-pcb-top.jpg
images/bench/assembled-pcb-bottom.jpg
images/bench/power-measurement.jpg
images/bench/preamp-waveform.png
images/bench/filter-sweep.png
```

Only add photos and measurements taken from the real board. This is a student sound-alert demonstrator, not a certified smoke-alarm product.
