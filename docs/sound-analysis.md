# Microwave chime analysis

## Goal of the experiment

I wanted to distinguish a repeated microwave completion chime from short unrelated sounds such as hand claps. The prototype evaluated one pattern: a tone close to 2,050 Hz, repeated in a three-beep sequence.

Doorbell and smoke-alarm test recordings were also analyzed, but the microwave detector rules are not detectors for those other sounds.

## Sound recordings

![Doorbell and smoke-detector waveform and spectrogram](../images/audio/doorbell-and-smoke-detector-spectrogram.png)

The doorbell recording contains changing tones, while the smoke-detector test recording shows repeated bursts around 2.8 kHz, with onset spacing around 1.35 s. The microwave rules centered at 2.05 kHz with shorter onset spacing would not recognize those signals as intended.

## Prototype method

The offline Python development used:

- 16,000 Hz mono audio.
- 1,024-sample Hann-windowed frames (64 ms), spaced every 160 samples (10 ms).
- A Goertzel target of 2,050 Hz, plus a tonal-purity check.
- Beep-duration and three-beep timing rules, intended to reject isolated percussive sounds.
- An offline Butterworth bandpass as part of the recorded-audio analysis, not a real-time ESP32 implementation.

Exploratory parameters included a −55 dBFS tone threshold, tonal purity ≥0.60, beep length 0.22–0.85 s and onset spacing 0.50–0.95 s.

## Development tests

The four development recordings gave the following alert counts:

| Recording | Expected events | Reported detections |
| --- | ---: | ---: |
| `microwave_1.wav` | 1 | 1 |
| `microwave_2.wav` | 1 | 1 |
| `microwave_clap.wav` | 1 | 1 |
| `claps_only.wav` | 0 | 0 |

I still need to add the original notebook and WAV files.

## What comes next

The doorbell and smoke-detector patterns need their own spectral and timing rules and new tests. For a hardware implementation, the offline filtering must be adapted to causal processing, the ESP32-S3 ADC rate and input range must be chosen and checked, and LED mappings must be defined. The current results are from offline sound analysis, not a functioning ESP32 firmware detector.
