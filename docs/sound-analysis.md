# Microwave Chime Detection and Sound Analysis

## The problem

I started by recording different household alerts. I wanted to see whether frequency alone could tell a microwave completion beep from other noises. It couldn't. In a clap-only test, the first simple frequency trigger produced false events around 5.504 s and 9.088 s.

![Doorbell and smoke-alarm test recordings](../images/audio/doorbell-and-smoke-detector-spectrogram.png)

The recordings also showed why one detection rule would not work for every sound:

| Sound | What I observed |
| --- | --- |
| Microwave | A repeated tone near 2,050 Hz |
| Doorbell | A changing sequence of tones, roughly 608 / 455 / 385 / 455 / 608 Hz |
| Smoke-alarm test signal | Repeated bursts near 2.8 kHz, with longer onset spacing |

The working offline detector test focuses on the microwave. I have not built separate working detectors for the other two sound patterns yet.

## Goertzel experiment

I used a Goertzel-based narrowband measurement and added checks for tone purity and the timing of three beeps. The development settings were:

| Setting | Value |
| --- | --- |
| Audio sampling rate | 16,000 Hz, mono |
| Frame/window | 1,024 samples, Hann window |
| Hop | 160 samples (10 ms) |
| Target frequency | 2,050 Hz |
| Tone threshold | −55 dBFS |
| Minimum tonal purity | 0.60 |
| Beep length | 0.22–0.85 s |
| Three-beep onset gaps | 0.50–0.95 s |

The recorded-audio preprocessing included an offline Butterworth bandpass. Real-time filtering on the ESP32 will be a separate implementation.

## Development recordings

| Recording | Expected alerts | Reported alerts |
| --- | ---: | ---: |
| `microwave_1.wav` | 1 | 1 |
| `microwave_2.wav` | 1 | 1 |
| `microwave_clap.wav` | 1 | 1 |
| `claps_only.wav` | 0 | 0 |

The four-file test was useful for catching a false-trigger problem, but it is not a measured accuracy rate. The original `.ipynb` notebook and `.wav` recordings are not yet in the repository, so another person cannot rerun these results from GitHub alone.

## Next experiments

When we move to the ESP32, I need to select an actual ADC rate, use causal frame processing, decide which LED represents each sound and test recordings at different distances and background-noise levels. The doorbell and smoke-test signals will need separate frequency and timing logic.

### Original files to upload later

```text
software/goertzel/microwave_detector.ipynb
software/goertzel/recordings/microwave_1.wav
software/goertzel/recordings/microwave_2.wav
software/goertzel/recordings/microwave_clap.wav
software/goertzel/recordings/claps_only.wav
```

These are suggested GitHub filenames. Use the real original filenames if yours differ; do not rename or reconstruct tests just to make the repository look complete.
