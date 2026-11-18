# Technical design review checklist

- [ ] Confirm all original and current KiCad files are matching revisions.
- [ ] Verify the exact microphone part, polarity and footprint.
- [ ] Inspect USB-C receptacle connections, separate CC resistors, GND shield and D+/D− lines.
- [ ] Recheck switching regulator design against the actual IC datasheet, inductor current and output network.
- [ ] Verify 3.3 V supply distribution and capacitor placement.
- [ ] Check 1.65 V analog reference and preamp DC/AC headroom.
- [ ] Verify the fourth-order TLV9062 topology and calculated vs simulated frequency response.
- [ ] Assess anti-aliasing and ESP32-S3 ADC loading at intended sample rate.
- [ ] Check GPIO boot/strap pins, reset wiring, and LED current.
- [ ] Check antenna clearance, board stackup, traces, ground return and manufacturing tolerances.
- [ ] Run ERC and DRC and archive real reports; resolve or explain findings.
- [ ] Export manufacturing files only from a reviewed matching PCB revision.
- [ ] Test USB power, bias, microphone, analog output, ADC waveform and visual alerts on assembled hardware.
- [ ] Separately evaluate false positives, varied sound distances and background conditions.

This is a test plan, **not evidence that any item has passed**.
