# KiCad hardware — version control and source provenance

The repository now contains the **original earlier KiCad files** in [`hardware/archive/earlier-kicad-sources/`](archive/earlier-kicad-sources/):

- `PE04_Chime_Detector_Schematics.kicad_pcb`
- `PE04_Chime_Detector_Schematics.kicad_pro`
- `PraticalElectronics_AY2.kicad_pro(1).kicad_sch`

These are editable project sources, but their file names were supplied in this mixed form and should not be taken as a KiCad project that has already been reopened and validated without adjustment. Do not silently rename or rewrite original evidence.

The PCB screenshot dated **18 November 2026** in `images/pcb/latest-layout-screenshot-2026-11-18.jpg` is a later layout image. **Its matching native PCB revision is not yet in this repository.**

The archived `.kicad_sch` and `.kicad_pcb` were audited by component reference and value: **57/57 physical components match**, zero reference/value discrepancies. This audit does **not** validate net connectivity, pin mapping, fabrication requirements, ERC/DRC or the later screenshot. [Read the component audit](../docs/kicad-source-component-audit.md).

**Next steps:** obtain matching latest `.kicad_sch`, `.kicad_pcb` and `.kicad_pro` files, run KiCad ERC and DRC, verify board/fab parameters and save the reports. Do not label a design 'manufacturing ready' without evidence.
