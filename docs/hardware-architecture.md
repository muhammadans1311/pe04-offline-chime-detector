# Hardware architecture — archived native KiCad design

This technical summary is grounded in the actual `.kicad_sch` and `.kicad_pcb` archived in this repository, with the [eight-block guide](../reports/eight-block-circuit-guide.pdf) as explanatory support. **It does not assert that those native files correspond to the later November 18 screenshot.**

The [source component audit](kicad-source-component-audit.md) compared 57 physical PCB references and Value fields against the earlier native schematic. **All 57 match**; electrical connectivity, footprint pin mapping, ERC/DRC and the latest board revision remain unverified.

| Block | Actual reference numbers and values | Intended role |
| --- | --- | --- |
| 01 USB-C | J2 629722000214, R3/R4 5K1, U3 USBLC6-2SC6 | Nominal 5 V USB power/data and ESD interface |
| 02 Switching supply | U1 TLV62569DBV; L1 2.2uH; R1 450K, R2 100K; C1–C4 | USB 5 V to nominal 3.3 V |
| 03 Electret input | MK1 AOM-5024P-HD-MB-R, R23 100R, C13 10uF, R14 2K2, C11 100nF | Microphone bias and coupling |
| 04 Midrail/preamp | U4 AD8656; R12/R13 10K, R9 47K, R10 4K7, R11 22K, C8–C10 | Buffered nominal 1.65 V reference and 11× gain |
| 05 Active low-pass | U5 TLV9062; R15/R16 2K49; R17/R18 2K67; C12 8.2nF, C14 10nF, C15 22nF, C16 3.3nF, C17 100nF | Two Sallen–Key stages, fourth order; design target around 7 kHz, not measured |
| 06 ADC interface | R19 220R; C18 1nF | Input conditioning for ESP32 ADC |
| 07 Controller | U2 ESP32-S3-WROOM-1; SW1 RESET, SW2 BOOT; TP1–TP3 | MCU, USB/serial debug, ADC and digital outputs |
| 08 LEDs | D1 Green, D2 Blue, D3 Red; R20/R21/R22 330R | Three independent light indicators |

### Intended signal chain

MK1 electret mic → R14 bias/C11 AC coupling → U4 AD8656 preamplifier (biased around 1.65 V) → two TLV9062 Sallen–Key stages → R19/C18 ADC input → U2 ESP32-S3 GPIO4/ADC1_CH3 → *planned* classification → GPIO5/6/7 indicator control.

### Intended power chain

J2 USB-C nominal 5 V → U1 buck conversion → 3.3 V logic/analog supply. D+ and D− are USB data lines, not supply lines.

### Technical limits

- The approximate 7 kHz design target is sourced from the eight-block guide; the assembled fourth-order response has **not** been verified by matching-device simulation or bench measurements.
- The historical LTspice study used a **different amplifier and third-order filtering implementation**. MCP6021 and generic UniversalOpamp2 are not the U4/U5 components in this archived KiCad design.
- AOM-5024L-HD-R was an earlier considered microphone, not the current `MK1` Value field. The archived schematic and PCB both specify **AOM-5024P-HD-MB-R**.
- No full ERC/DRC, native layout/net connectivity, assembled-board or production testing is claimed.
