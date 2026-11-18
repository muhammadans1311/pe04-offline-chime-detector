# Sound recordings and offline Goertzel feasibility

## Why sound patterns?
An early single-frequency threshold around 2048–2055 Hz responded to both the microwave chime and unrelated claps. The clap-only test produced erroneous detections at approximately 5.504 s and 9.088 s. This motivated adding spectral purity and repeated timing constraints.

## October Colab prototype — microwave event
The documented Python notebook used:
- Sample rate 16,000 samples/s, mono recordings.
- Hann window with 1,024 samples (64 ms) and 160-sample hop (10 ms).
- Goertzel target 2,050 Hz; tone threshold −55 dBFS; tonal purity at least 0.60.
- Accepted beep duration 0.22–0.85 s, onset gaps 0.50–0.95 s, inter-beep silence at least 0.04 s, cooldown 2.2 s.
- Offline third-order Butterworth digital bandpass 500–5,000 Hz.

Four development recording outcomes reproduced in the source report:

| Test file | Expected alerts | Detected | Outcome |
| --- | ---: | ---: | --- |
| microwave_1.wav | 1 | 1 | PASS |
| microwave_2.wav | 1 | 1 | PASS |
| microwave_clap.wav | 1 | 1 | PASS |
| claps_only.wav | 0 | 0 | PASS |

**Important:** Four known development samples do not establish a general accuracy percentage. The offline zero-phase filtering implementation cannot be copied directly into real-time microcontroller firmware.

## Additional sound characterization
Recorded doorbell activations showed an approximate 608–455–385–455–608 Hz characteristic sequence. A smoke-alarm test signal exhibited three bursts around 2,813 Hz, with about 1.38 s between onset times. These are **recording characteristics**, not evidence that doorbell/smoke detection has been implemented on the ESP32.

## Repository assets
The spectrogram graphic and the original Colab notebook, recordings, and code should be stored under `images/audio/` and `software/` once available. The 36-page development report includes the earlier notebook code listing and fuller test details.

**Safety note:** The device is a student demonstrator. It must not be used in place of a certified smoke alarm or safety notification system.
