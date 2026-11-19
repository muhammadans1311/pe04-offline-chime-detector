# Offline sound analysis and detection experiments

## Recordings

The initial recordings focused on a microwave completion chime, including deliberate hand claps as interference. Doorbell and smoke-alarm test recordings were also inspected for their frequency and time patterns.

![Recorded doorbell and smoke detector test signatures](../images/audio/doorbell-and-smoke-detector-spectrogram.png)

The smoke-alarm test recording contained repeated tonal bursts near **2.8 kHz**. The doorbell recording showed a changing sequence of strong frequencies rather than one constant tone. These were recording observations, not demonstrations of the final PCB detecting either sound.

## From frequency trigger to complete beep pattern

An early frequency-only approach around **2,048–2,055 Hz** responded to claps, with false event timestamps reported at about 5.504 s and 9.088 s in one clap-only trial. This showed that energy near a target frequency is not sufficient to establish that a complete chime occurred.

The offline prototype then used:
- Audio resampled to **16 kHz mono**.
- Hann-windowed **1,024-sample frames** (64 ms), with a 160-sample hop (10 ms).
- Goertzel magnitude near **2,050 Hz** and a tonal-purity measure.
- A minimum tone duration and checks for the timing of three successive beeps.
- A non-causal offline Butterworth bandpass used for analysis before the Goertzel stage.

The saved development settings included a threshold of −55 dBFS, minimum tonal purity 0.60, beep durations 0.22–0.85 s, and onset intervals 0.50–0.95 s. These are exploratory settings, not calibrated production thresholds.

## Development recording results

| File | Expected alerts | Reported alerts |
| --- | ---: | ---: |
| microwave_1.wav | 1 | 1 |
| microwave_2.wav | 1 | 1 |
| microwave_clap.wav | 1 | 1 |
| claps_only.wav | 0 | 0 |

This is **four development examples**, not sufficient evidence for a reliability or accuracy claim.

## Next experiment

For an ESP32-S3 implementation, the offline filtering needs to be replaced or adapted to a causal streaming approach. Testing should include different loudness levels, rooms, background sounds, distances, microphone input levels and repeated negative examples. Hardware ADC sampling and LED behavior remain to be tested on an assembled board. The original notebook and recordings are not yet present as runnable source files.
