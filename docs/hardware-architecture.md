# Hardware architecture — later team KiCad design

The following design blocks are documented in the uploaded eight-block circuit study guide. The latest native PCB and complete design verification remain pending.

| Block | Main elements | Role |
| --- | --- | --- |
| 01 USB-C interface | J2, CC resistors, USB protection | Power/data input and protection |
| 02 3.3 V switching supply | Buck regulator, L1 and filtering | Convert nominal 5 V USB input to 3.3 V |
| 03 Electret microphone | MK1, R23/C13 decoupling, R14 bias, C11 coupling | Convert sound to biased AC signal |
| 04 Reference and preamp | AD8656; R12/R13, R9/R10, U4 | 1.65 V midrail and nominal 11× analog gain |
| 05 Four-pole analog filter | Two TLV9062 Sallen–Key stages | Attenuate high-frequency components (design target ~7 kHz) |
| 06 ADC conditioning | R19=220 Ω, C18=1 nF | Isolate and condition ESP32 ADC input |
| 07 ESP32 control | ESP32-S3-WROOM-1, reset/boot, UART test points | Sampling, software control and debug |
| 08 Visual outputs | Red, blue and green LEDs with separate resistors | Three independent visual notification channels |

## Signal path
Electret microphone → microphone-bias filtering → AC coupling → 1.65 V-biased preamp → two active low-pass stages → ADC RC input network → ESP32-S3 GPIO4 / ADC1_CH3 → planned classification → LEDs on GPIO5/6/7.

## Power path
USB-C VBUS nominal 5 V → switching regulator → 3.3 V for ESP32 and analog stages. USB D+/D− are data connections, not the power supply.

## Important boundaries
This is a **design description**, not an ERC/DRC result or measured board performance. The earlier October LTspice simulation uses a different amplifier/filter topology and must not be cited as a simulation of these exact AD8656/TLV9062 KiCad stages. The microphone part-number difference between historical selection and later KiCad documentation also requires checking.
