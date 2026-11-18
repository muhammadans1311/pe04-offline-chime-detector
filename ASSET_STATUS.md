# Repository asset status — verified 18 November 2026

The following assets were confirmed **present on the main branch**, based on an actual GitHub repository tree check. No original assets were modified during the documentation audit.

## Uploaded original source and evidence

| Location | Evidence | Availability |
| --- | --- | --- |
| `images/pcb/latest-layout-screenshot-2026-11-18.jpg` | Latest team layout screenshot, no native matching file | **Uploaded** |
| `images/pcb/earlier-layout-screenshot.png` | Earlier routing screenshot | **Uploaded** |
| `images/ltspice/initial-frequency-sweep-schematic.png` | Circuit schematic screenshot | **Uploaded** |
| `images/ltspice/initial-ac-frequency-response.png` | AC frequency sweep plot | **Uploaded** |
| `images/ltspice/initial-ac-gain-cursor.png` | AC cursor values | **Uploaded** |
| `images/ltspice/real-mic-bias-transient.png` | Simulated waveform screenshot | **Uploaded** |
| `images/audio/doorbell-and-smoke-detector-spectrogram.png` | Audio waveform/spectrogram | **Uploaded** |
| `reports/development-and-verification-report.pdf` | 36-page development history | **Uploaded** |
| `reports/eight-block-circuit-guide.pdf` | 8-page schematic study guide | **Uploaded** |
| `hardware/archive/earlier-kicad-sources/PE04_Chime_Detector_Schematics.kicad_pcb` | Earlier editable PCB | **Uploaded** |
| `hardware/archive/earlier-kicad-sources/PE04_Chime_Detector_Schematics.kicad_pro` | Earlier KiCad project settings | **Uploaded** |
| `hardware/archive/earlier-kicad-sources/PraticalElectronics_AY2.kicad_pro(1).kicad_sch` | Earlier editable schematic | **Uploaded** |

## Source consistency

The two archived native KiCad design files were compared for physical component reference designators and Value fields: **57/57 match**, with **zero reference/value discrepancies**. This is not a full netlist, symbol-to-footprint pin-map, component availability or ERC/DRC check.

See [component audit](docs/kicad-source-component-audit.md) and [hardware notes](hardware/README.md).

## Still pending / not claimed

- Native `.kicad_sch`, `.kicad_pcb` and `.kicad_pro` files that exactly match the **18 November 2026** screenshot.
- Original LTspice `.asc` files and associated permitted model dependencies.
- Original Google Colab notebook `.ipynb` and four WAV test recordings.
- Verified ERC/DRC reports, Gerbers, fabricated/assembled board photos and electrical measurements.
- ESP32-S3 on-device classifier/LED firmware and measured deployment accuracy.

**Revision policy:** the latest screenshot and the archived native schematic/PCB must not be presented as if they were one proven identical PCB version.
