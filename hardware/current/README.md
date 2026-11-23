# PE-04 V2 KiCad source

This folder contains the project files supplied for the current team design revision, dated **22 November 2026** (V2). The files have not been altered during GitHub packaging.

Open **`PE04_Chime_Detector.kicad_pro`** in KiCad 10. Keep the `libraries/` folder, `fp-lib-table` and `sym-lib-table` alongside the project. The footprint and symbol tables use paths relative to `${KIPRJMOD}`. Custom `.kicad_mod`, `.kicad_sym` and STEP 3D files are included.

The `.kicad_prl` (local preferences/session state), macOS metadata and `.DS_Store` were intentionally omitted.

- `PE04_Chime_Detector.kicad_sch`: V2 schematic
- `PE04_Chime_Detector.kicad_pcb`: V2 two-layer PCB
- `PE04_Chime_Detector.kicad_pro`: matching project settings
- `PE04_Chime_Detector.kicad_dru`: supplied AISLER-based design rules
- `fp-lib-table` and `sym-lib-table`: project libraries
- `libraries/`: custom footprints, symbols and 3D models

There are 57 electronic components and four mounting holes in the PCB file. Design rules are supplied, but no passing KiCad ERC or DRC report was provided. The next steps are review, assembly and bench tests.

Earlier native files are preserved in [hardware/archive/earlier-kicad-sources](../archive/earlier-kicad-sources/) for development history.
