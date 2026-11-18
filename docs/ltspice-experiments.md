# LTspice analog-front-end exploration

## Scope and models
These experiments studied an **earlier standalone analog candidate** and do not verify the later team PCB. The analog source was an idealized 3.3 V rail with a simplified electret current-source model, rather than a physical microphone, buck regulator or ESP32 ADC.

Initial bias: 2.2 kΩ microphone feed; AC-coupling 10 nF; 1.65 V reference using two 10 kΩ resistors and a 10 µF capacitor. Non-inverting amplifier feedback: 100 kΩ and 10 kΩ, nominal gain `1+100k/10k=11` (~20.83 dB). The later generic two-stage candidate used a unity-gain Sallen–Key section (6.8 kΩ + 6.8 kΩ, 10 nF + 4.7 nF) and final 3.3 kΩ / 10 nF RC section.

## AC-sweep findings
With generic two-op-amp models and the **earlier third-order candidate**, the isolated filter transfer function `V(adc_out)/V(amp_out)` showed:

| Sweep cursor frequency | Simulated gain |
| --- | ---: |
| 501.53 Hz | −0.0376 dB |
| 2057.17 Hz | −1.0930 dB |
| 3007.03 Hz | −3.2132 dB |
| 5037.21 Hz | −10.5920 dB |
| 8115.82 Hz | −20.9243 dB |
| 13998.01 Hz | −34.2438 dB |
| 16041.68 Hz | −37.6847 dB |

A separate nominal tolerance run recorded about −1.103 dB near 2.07 kHz and −34.263 dB near 14 kHz.

## Debugging and validation exercises
- An early single-op-amp generic-model AC run showed approximately 20.08 dB at 2053.66 Hz.
- Investigated MCP6021-family manufacturer PSpice macromodel import (including syntax/pin mapping). A single-stage model operated, but two manufacturer instances failed numerical convergence, including reported internal node `u1:21`. Generic `UniversalOpamp2` was therefore used for the later two-stage simulations.
- Updated a microphone simulation from sine voltage to current sink: `SINE(0.5m 5u 2050)` with AC amplitude 1 µA.
- Checked low- and high-input amplitude cases for simulated signal swing and clipping risk.
- Injected ±20 mV, 5 kHz ripple on the 3.3 V supply; explored a 220 Ω + 10 µF microphone-supply decoupling branch and observed improved simulated signals.
- Tested reference settling during a 500 ms startup run. The 400 ms proposed no-detection window remains an unverified firmware recommendation.
- Compared nominal, all-low and all-high passive tolerance corners. This was an exploratory sensitivity check, **not** Monte Carlo or hardware acceptance.

## Reproducibility
The original LTspice `.asc` files and model text are not yet uploaded to this repository. Existing screenshots and the detailed PDF report document the investigation, but a schematic screenshot does not substitute for an executable netlist. Obtain and add original schematics, manufacturer-model licensing information, `.plt` settings if available, and repeatable simulation commands.

## Relationship to current PCB
**Do not describe these numbers as the frequency response or noise behavior of the later AD8656/TLV9062 two-stage fourth-order PCB.** Verify the later topology separately with actual device models and bench tests.
