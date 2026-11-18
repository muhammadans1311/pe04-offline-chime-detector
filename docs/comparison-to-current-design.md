# Comparison of two analog-design iterations

| | Earlier October LTspice exploration | Later group KiCad architecture |
|---|---|---|
| Purpose | Independently explore an analog signal chain and filtering | Integrated USB-powered ESP32-S3 board |
| Amplifier | Generic UniversalOpamp2 in successful final two-stage simulation; MCP6021-family model tried separately | AD8656 preamplifier |
| Filter | Second-order Sallen–Key followed by single RC, third order overall | Two cascaded second-order Sallen–Key stages, fourth order overall |
| Operating supply | Ideal 3.3 V source | USB-C → buck 3.3 V planned |
| Results | AC, transient, startup, noise and tolerance evidence recorded | Native source revision / ERC / DRC / real bench results pending |
| ADC | Output labeled ADC_OUT, with no real ADC model | ESP32-S3 ADC input interface |

### Why both are useful
The October work shows a real engineering thought process: simulation, topology choices, error investigation, supply-noise experiments and refinement. The later KiCad iteration documents integration into an ESP32-S3 board. Both belong in the portfolio, but **the October numerical plots are not later PCB validation**.

### Required next comparison
Obtain final KiCad native source, verify actual net connectivity and component values, build matching simulation(s), and measure assembled analog output once a board exists.
