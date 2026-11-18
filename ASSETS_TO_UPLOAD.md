# Remaining binary evidence — upload guide

The GitHub connector has published the source documentation. The uploaded PNG/JPEG/PDF/KiCad files are not yet committed. GitHub file paths below match the README's intended media layout.

## How to upload the remaining files
1. Download the prepared [PE04_Chime_Detector_Repository_Release.zip] package from the ChatGPT conversation and extract it.
2. In this private repository select **Add file → Upload files**.
3. Drag the **`images`**, **`reports`**, and **`hardware/archive/earlier-kicad-sources`** contents from the extracted local package (preserving relative paths).
4. Commit with message `Add original PCB, simulation and report evidence`.
5. Verify README's image paths; then replace the temporary "pending upload" wording with real links.
6. When the latest matching native KiCad source is received, add it under `hardware/current/` and document ERC/DRC results.

## Files awaiting transfer
- `images/pcb/latest-layout-screenshot-2026-11-18.jpg` — latest screenshot only, not source.
- `images/pcb/earlier-layout-screenshot.png` — earlier revision.
- `images/ltspice/initial-frequency-sweep-schematic.png`
- `images/ltspice/initial-ac-frequency-response.png`
- `images/ltspice/initial-ac-gain-cursor.png`
- `images/ltspice/real-mic-bias-transient.png`
- `images/audio/doorbell-and-smoke-detector-spectrogram.png`
- `reports/development-and-verification-report.pdf`
- `reports/eight-block-circuit-guide.pdf`
- `hardware/archive/earlier-kicad-sources/PE04_Chime_Detector_Schematics.kicad_pcb`
- `hardware/archive/earlier-kicad-sources/PE04_Chime_Detector_Schematics.kicad_pro`
- `hardware/archive/earlier-kicad-sources/PraticalElectronics_AY2.kicad_pro(1).kicad_sch`

**Do not claim those files are on GitHub until an explicit repository verification finds them.**

The archived original KiCad filenames are intentionally unmodified. The current matching native board has not been received. Original LTspice `.asc` files and Colab `.ipynb` also remain unavailable.
