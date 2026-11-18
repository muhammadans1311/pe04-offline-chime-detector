# KiCad hardware files

The latest supplied layout is currently only a screenshot from 18 November 2026. **The matching editable PCB file is still pending** and should not be confused with the older native project files.

The historical KiCad source should be placed under `hardware/archive/earlier-kicad-sources/` when transferred to GitHub. That historical set contains a substantial board `PE04_Chime_Detector_Schematics.kicad_pcb`, a related `.kicad_pro`, and `PraticalElectronics_AY2.kicad_pro(1).kicad_sch` (as supplied). Original filenames are preserved intentionally: do not casually rename sources until project consistency has been checked in KiCad.

When the latest files arrive, add all three matching native files under a clearly named current-design folder. Run KiCad ERC/DRC and record exact results before using phrases like "manufacturing ready".
