# Status, open engineering questions and next steps

## Evidence currently available
- November 18, 2026 team board **screenshot** (not the corresponding native KiCad PCB source).
- Earlier separate KiCad schematic/PCB source files, which must not be presented as the current screenshot revision.
- LTspice screenshots and a historical 36-page development and verification report.
- Eight-block circuit guide and combined acoustic spectrogram.
- Offline Goertzel feasibility on four development recordings (original `.ipynb` pending).

## Verification checklist
1. Obtain the matched current `.kicad_sch`, `.kicad_pcb`, and `.kicad_pro`.
2. Reconcile microphone exact part number, package, polarity, bias and footprint. Earlier materials mention AOM-5024L-HD-R; later KiCad documentation uses AOM-5024P-HD-MB-R.
3. Run KiCad ERC and DRC, then save actual result reports.
4. Verify USB-C wiring, buck regulator, 3.3 V supply margin, ADC drive/loading and antenna keep-out.
5. Recreate analog AC/transient results on final AD8656/TLV9062 topology, not merely on the older generic model.
6. Add original LTspice schematic/model files and the notebook with reproducible inputs/outputs.
7. After fabrication: photographs, power-rail measurements, ADC captures, firmware and independent acoustic tests.
8. Confirm teammate attribution and university/publication rights before changing the repository from private.

No measured detection accuracy, complete PCB fabrication, real-time on-device classification, or certified smoke-alarm functionality is claimed.
