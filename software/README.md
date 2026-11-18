# Sound-processing software — documented prototype

The project's earlier Colab prototype investigated a Hann-windowed Goertzel recurrence plus tone-purity and triple-beep timing checks. Source code is preserved in the 36-page report, but the original `Chime_Detector_Goertzel_Colab_Prototype.ipynb` and four development WAV recordings have **not** yet been uploaded here.

When source files are recovered:
1. Add the unmodified notebook and test recordings if sharing rights permit.
2. Document Python dependencies and execution instructions.
3. Capture reproducible outputs before asserting 4/4 results.
4. Implement and separately verify a real-time ESP32 variant. The Colab notebook's non-causal offline digital filtering is not directly appropriate for real-time microcontroller use.

No running ESP32 firmware or field accuracy is claimed at this stage.
