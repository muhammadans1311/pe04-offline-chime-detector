# LTspice experiments | Microphone analog front-end

*Simulation work documented by Muhammad Ans*

## What I wanted to test

An electret microphone produces a small AC signal. I investigated how to power its bias network, AC-couple the signal, amplify it around a mid-supply reference and filter unwanted high-frequency content before ADC sampling.

I used LTspice for AC sweeps, transient tests, startup behavior and model troubleshooting. This was a development circuit explored before the full ESP32-S3 board.

## Early amplifier and RC-filter circuit

![Early LTspice schematic](../images/ltspice/initial-frequency-sweep-schematic.png)

This circuit uses a nominal 3.3 V supply, a 1.65 V bias reference, a non-inverting amplifier and an output RC filter with R = 3.3 kΩ and C = 10 nF. The RC-only corner is about `1/(2πRC) = 4.8 kHz`.

![AC frequency response](../images/ltspice/initial-ac-frequency-response.png)

The graph is for `V(adc_out)/V(mic_raw)`. It includes amplifier gain and the RC network, so it is not a stand-alone filter attenuation plot. At 2.0536624 kHz the [saved cursor screenshot](../images/ltspice/initial-ac-gain-cursor.png) reads +20.0777 dB.

The historical microphone-front-end work also explored a Sallen-Key plus RC topology, but its original executable `.asc` source and matching plot have not been recovered. I have not treated its reported values as independently reproducible from the present repository.

## Transient behavior and bias

![Transient simulation](../images/ltspice/real-mic-bias-transient.png)

I explored a simplified microphone-current model, the input signal swing around 1.65 V and settling after startup. I also injected supply ripple into an idealized 3.3 V source and evaluated the effect of an RC branch (220 Ω and 10 µF) on microphone bias noise.

## Op-amp model troubleshooting

I imported an MCP6021-family PSpice model to explore real-device behavior. Simulations involving multiple instances encountered convergence problems. Generic LTspice amplifier models were used for further conceptual testing rather than presenting the failed manufacturer model as a valid simulation.

## How I used the results

These experiments helped me understand microphone biasing, gain, AC coupling, supply decoupling and the limits of idealized op-amp simulations. The team KiCad design later uses an AD8656 preamp and TLV9062 fourth-order active filter. They require their own matching simulation and, ultimately, hardware measurements.

The original LTspice schematic files are still needed to let someone rerun these experiments.
