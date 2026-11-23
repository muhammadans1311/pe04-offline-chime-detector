# PE-04 V2 | Assembly and purchasing

The two spreadsheet supplements supplied by the team are dated **22 November 2026**. They contain **21 supplier lines** and quantities adding up to **27 individual electronic placements** on the V2 board. They are supplementary lists, not evidence that all project parts have been ordered, received or soldered.

## Files

- [Full V2 assembly BOM (61 PCB footprints)](PE04_V2_Assembly_BOM.csv)
- [Selected supplier lines mapped to PCB references](PE04_Supplementary_Selected_Parts.csv)
- [Original supplement 1 - Excel](Partslist_Group_PE04_Supplement_1.xlsx)
- [Original supplement 2 - Excel](Partslist_Group_PE04_Supplement_2.xlsx)

The V2 PCB has 57 electronic component positions plus four mounting holes. All 61 appear in the assembly BOM. The 27 positions covered by the supplements have manufacturer codes, vendor information and reference assignments; the others retain their design values/footprints with procurement fields blank rather than inferred.

## Selected part examples

| Board reference | Supplier selection |
| --- | --- |
| U4 | Analog Devices AD8656ARZ |
| D1 green | Kingbright APT3216LZGCK |
| D2 blue | Kingbright APT3216LVBC/D |
| D3 red | Kingbright APT3216SURCK |
| SW1, SW2 | C&K PTS645SL50-2 LFS |
| R20–R22 | YAGEO 330 Ω, 1%, 0805 |

Supplementary price estimates in the Excel sheets were entered on 22 November 2026 and are not live quotations. Line amounts total approximately **€8.03 before VAT**, or **€9.55 including 19% VAT**, for these *supplementary* items only.

## Assembly notes

The specific LED types are selected in the supplement, but the current design still uses 330 Ω series resistors. Verify expected current and visible brightness using those actual parts before soldering.

Check that the full set of components, footprints and pin orientations matches the PCB revision used for assembly. The native KiCad files are in [hardware/current](../hardware/current/).
