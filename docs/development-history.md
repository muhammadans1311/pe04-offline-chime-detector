# Engineering development history

This is a condensed chronology; the detailed 36-page lab report should be added under `reports/`.

## October 2026 — Requirements and acoustic feasibility
Defined an offline USB-C-powered ESP32-S3 visual alert system for audible household notifications. Early frequency-only microwave-beep detection incorrectly responded to hand claps (events noted at 5.504 s and 9.088 s). This prompted combining tonal purity with beep length and temporal-pattern criteria.

## October 19–21 — Offline signal-processing proof of concept
The saved Python/Google Colab prototype used a Hann-windowed Goertzel frequency measurement at 2050 Hz and a three-beep timing pattern. Four development recordings yielded expected detections of **1 / 1 / 1 / 0** for microwave 1, microwave 2, microwave plus claps, and claps-only respectively. The tiny development set is not a field-accuracy benchmark. The original notebook and WAV files are not yet committed.

## October 20–21 — LTspice analog exploration
Constructed a 3.3 V electret-microphone equivalent, 1.65 V reference, non-inverting preamp, a unity-gain second-order Sallen–Key filter, and a final first-order RC low-pass network. Explored MCP6021-family manufacturer-model compatibility, solver convergence, nominal and stress inputs, noisy 3.3 V supply, RC microphone-bias decoupling, startup and passive tolerance corners. Successful **two-stage** analysis used generic UniversalOpamp2 models; it is not equivalent to verifying the later actual op-amp ICs.

## Late October–November — Team KiCad architecture and PCB development
The later team design adopted an ESP32-S3-WROOM-1, USB-C, buck supply, electret mic, AD8656 preamp and TLV9062 cascaded fourth-order low-pass stages. A screenshot supplied November 18 shows active PCB layout work. The corresponding latest native source, ERC/DRC, manufacturing data, assembled board and measurements have not been verified in this repository.

## Next
Obtain source files matching the latest screenshot; run ERC/DRC; archive reproducible LTspice schematics, test audio, Colab notebook and later ESP32 firmware; record dated fabrication and board bring-up evidence.
