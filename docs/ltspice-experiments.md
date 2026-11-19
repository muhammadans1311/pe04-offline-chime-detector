# LTspice microphone front-end experiments

## Purpose

I used LTspice to explore how a low-level microphone signal could be biased around a mid-supply voltage, amplified and low-pass filtered before an ADC input. This work came before the integrated KiCad design.

## Early amplifier and RC-filter run

![Saved LTspice circuit screenshot](../images/ltspice/initial-frequency-sweep-schematic.png)

The circuit screenshot shows a simplified microphone source, a nominal 3.3 V supply, a 1.65 V reference, an amplifier with a resistive feedback network and a **3.3 kΩ / 10 nF output RC filter**. The ideal single-pole RC corner is approximately **4.8 kHz**.

![Saved AC sweep](../images/ltspice/initial-ac-frequency-response.png)

The plotted ratio is `V(adc_out)/V(mic_raw)`: **amplifier-plus-filter gain**, not the attenuation of a filter by itself. At **2.0536624 kHz**, the [saved cursor](../images/ltspice/initial-ac-gain-cursor.png) displays approximately **+20.0777 dB**. This figure belongs to this early test circuit.

An additional Sallen–Key plus RC filtering arrangement was explored during development. However, the original executable `.asc` file and matching plot for that later arrangement are not included here, so I have not presented its separate filter-only readings as reproduced results.

## Transient and model work

![Microphone bias transient plot](../images/ltspice/real-mic-bias-transient.png)

I also explored microphone current-source modeling, transient behavior around a 1.65 V reference, noise injected onto an idealized 3.3 V supply, and RC decoupling of the microphone bias.

The imported MCP6021-family PSpice model raised convergence problems in some multi-stage tests. Generic LTspice op-amp models were used for further conceptual exploration. Those runs should not be confused with device-level validation.

## How this relates to KiCad

The uploaded KiCad schematic has an **AD8656 preamp** and a **TLV9062 fourth-order low-pass network**. Neither is the same complete circuit as the screenshot above. There is no claim here that the shown LTspice curves are the frequency response or noise performance of the final board.

To reproduce the simulation work, the original `.asc` files and permitted model files need to be added. A future simulation should use the actual KiCad stage values, supply rails and appropriate op-amp models.
