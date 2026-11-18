# KiCad component source audit — archived native revision

> **Source-of-truth scope:** This audit compares the **actual two native design files currently archived in this repository**, not the later November 18 layout screenshot. The screenshot's matching editable PCB is not yet available. These are design-file values, **not a validated assembled BOM**.

## Sources used

- [Archived KiCad schematic](../hardware/archive/earlier-kicad-sources/PraticalElectronics_AY2.kicad_pro(1).kicad_sch) (`.kicad_sch`, KiCad 10)
- [Archived KiCad PCB](../hardware/archive/earlier-kicad-sources/PE04_Chime_Detector_Schematics.kicad_pcb) (`.kicad_pcb`, KiCad 10)
- [Eight-block circuit guide](../reports/eight-block-circuit-guide.pdf) (secondary explanatory reference)

## Result

- **57 physical PCB footprints** identified.
- **57 unique non-power physical schematic references** identified (multi-unit op-amps U4/U5 counted once).
- **0 reference/value mismatches** between physical PCB and archived schematic.
- **0 schematic physical references missing from PCB**.
- This compares **reference designators and Value fields only**. It does **not** verify electrical connectivity, pin nets, footprints-to-symbol pin maps, actual purchased parts, ERC, DRC, or the newer screenshot.

## Important design values

| Function | Native reference(s) | Value or part |
| --- | --- | --- |
| USB-C receptacle | J2 | 629722000214 |
| USB-C CC pull-downs | R3, R4 | 5K1 each |
| USB data protection | U3 | USBLC6-2SC6 |
| 3.3 V buck regulator | U1 | TLV62569DBV |
| Feedback network | R1, R2 | 450K, 100K |
| Buck inductor | L1 | 2.2uH |
| Controller | U2 | ESP32-S3-WROOM-1 |
| Microphone | MK1 | AOM-5024P-HD-MB-R |
| Microphone bias / decoupling | R14, R23, C13, C11 | 2K2, 100R, 10uF, 100nF |
| Midrail reference | R12, R13 | 10K each (nominal 1.65 V from 3.3 V) |
| Analog preamp | U4 | AD8656, with R9=47K and R10=4K7 (nominal 11×) |
| Active filter | U5 | TLV9062, two Sallen–Key sections, nominal target near 7 kHz **per design documentation** |
| First filter stage | R15, R16, C12, C14 | 2K49, 2K49, 8.2nF, 10nF |
| Second filter stage | R17, R18, C15, C16 | 2K67, 2K67, 22nF, 3.3nF |
| ADC input | R19, C18 | 220R, 1nF |
| LED channels | D1, D2, D3; R20, R21, R22 | Green, blue, red; 330R each |
| Debugging | SW1, SW2, TP1, TP2, TP3 | RESET, BOOT, three test points |

**Clarification:** Earlier LTspice experiments used generic op amps and an MCP6021-family model. **Neither MCP6021 nor UniversalOpamp2 appears as a final amplifier value in these archived KiCad design files.** Their simulations are **earlier alternatives**, not simulations of this AD8656/TLV9062 PCB. Another earlier microphone candidate AOM-5024L-HD-R is **not** the MK1 part currently saved in this design.

## All 57 physical components, checked by reference and value

| Reference | PCB Value | Schematic Value | Comparison |
| --- | --- | --- | --- |
| C1 | 10uF | 10uF | Matches |
| C2 | 100nF | 100nF | Matches |
| C3 | 22uF | 22uF | Matches |
| C4 | 100nF | 100nF | Matches |
| C5 | 10uF | 10uF | Matches |
| C6 | 100nF | 100nF | Matches |
| C7 | 1uF | 1uF | Matches |
| C8 | 100nF | 100nF | Matches |
| C9 | 10uF | 10uF | Matches |
| C10 | 100nF | 100nF | Matches |
| C11 | 100nF | 100nF | Matches |
| C12 | 8.2nF | 8.2nF | Matches |
| C13 | 10uF | 10uF | Matches |
| C14 | 10nF | 10nF | Matches |
| C15 | 22nF | 22nF | Matches |
| C16 | 3.3nF | 3.3nF | Matches |
| C17 | 100nF | 100nF | Matches |
| C18 | 1nF | 1nF | Matches |
| D1 | Green LED | Green LED | Matches |
| D2 | Blue LED | Blue LED | Matches |
| D3 | Red LED | Red LED | Matches |
| J2 | 629722000214 | 629722000214 | Matches |
| L1 | 2.2uH | 2.2uH | Matches |
| MK1 | AOM-5024P-HD-MB-R | AOM-5024P-HD-MB-R | Matches |
| R1 | 450K | 450K | Matches |
| R2 | 100K | 100K | Matches |
| R3 | 5K1 | 5K1 | Matches |
| R4 | 5K1 | 5K1 | Matches |
| R5 | 10K | 10K | Matches |
| R6 | 10K | 10K | Matches |
| R7 | 22R | 22R | Matches |
| R8 | 22R | 22R | Matches |
| R9 | 47K | 47K | Matches |
| R10 | 4K7 | 4K7 | Matches |
| R11 | 22K | 22K | Matches |
| R12 | 10K | 10K | Matches |
| R13 | 10K | 10K | Matches |
| R14 | 2K2 | 2K2 | Matches |
| R15 | 2K49 | 2K49 | Matches |
| R16 | 2K49 | 2K49 | Matches |
| R17 | 2K67 | 2K67 | Matches |
| R18 | 2K67 | 2K67 | Matches |
| R19 | 220R | 220R | Matches |
| R20 | 330R | 330R | Matches |
| R21 | 330R | 330R | Matches |
| R22 | 330R | 330R | Matches |
| R23 | 100R | 100R | Matches |
| SW1 | RESET | RESET | Matches |
| SW2 | BOOT | BOOT | Matches |
| TP1 | TestPoint | TestPoint | Matches |
| TP2 | TestPoint | TestPoint | Matches |
| TP3 | TestPoint | TestPoint | Matches |
| U1 | TLV62569DBV | TLV62569DBV | Matches |
| U2 | ESP32-S3-WROOM-1 | ESP32-S3-WROOM-1 | Matches |
| U3 | USBLC6-2SC6 | USBLC6-2SC6 | Matches |
| U4 | AD8656 | AD8656 | Matches |
| U5 | TLV9062 | TLV9062 | Matches |

## Validation still required

1. Obtain the **matching native files for the latest screenshot** and rerun this audit on that exact version.
2. Run native KiCad ERC and DRC and review warnings and unconnected pad declarations.
3. Check actual nets, USB-C, converter feedback, analog reference/filter topology, footprint mapping and supply-current requirements with datasheets.
4. Only then export a production BOM and manufacturing files.
