# PE-04 | Assembly and bring-up plan

**Stage:** KiCad V2 source files collected; assembly and electrical tests still to be recorded.

## 1. Before soldering

- [ ] Open the V2 KiCad schematic and PCB with project-local libraries.
- [ ] Run ERC; record warnings and resolved issues.
- [ ] Run DRC with `PE04_Chime_Detector.kicad_dru`; resolve routing, clearances, antenna keep-out and mechanical concerns.
- [ ] Confirm that the assembled board matches the V2 BOM and board revision.
- [ ] Check component polarity and orientation: microphone, LEDs, buck IC, op amps, ESP32 module and USB-C connector.
- [ ] Inspect the three selected Kingbright LED types and the existing 330 Ω series resistors for suitable current and brightness.

## 2. First power-up

- [ ] Inspect for solder bridges and check power-to-ground resistance before connecting USB.
- [ ] Apply a current-limited 5 V source; monitor supply current.
- [ ] Measure 3.3 V buck output and the nominal 1.65 V analog reference.
- [ ] Confirm ESP32 boot/reset and available test points.

## 3. Analog front-end measurements

- [ ] Verify microphone bias and C11 AC coupling.
- [ ] Inject a known safe signal; measure AD8656ARZ gain and any clipping.
- [ ] Sweep frequency and measure TLV9062 filter response with a defined measurement setup.
- [ ] Check ADC input DC level, noise and signal range before sampling.

## 4. Firmware and recognition

- [ ] Select a documented ADC sample rate and review filter anti-aliasing.
- [ ] Implement real-time audio frames, tone detection and a three-beep timing state machine.
- [ ] Define which LED corresponds to each sound class.
- [ ] Test the microwave pattern against clap-only and mixed recordings.
- [ ] Develop and separately verify doorbell and smoke-alarm *test-sound* patterns.
- [ ] Record false positives, missed triggers, sound levels, distances and backgrounds.

## Evidence to add after assembly

Photographs of the finished board, real ERC/DRC reports, test date and equipment, measured voltage/analog/ADC plots, firmware source and recorded detection results.

This is a student demonstrator, not a certified life-safety notification device.
