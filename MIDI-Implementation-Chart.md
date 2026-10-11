# Aether Sand — MIDI Implementation Chart

**Manufacturer:** TribalVoice  
**Model:** Aether Sand  
**Version:** 2026-10  
**Date:** 2026-10-11  
**Type:** Software (browser-based granular synthesizer)

MIDI is input-only. Web MIDI API is used (requires a secure context: HTTPS or localhost). Enable MIDI from the UI button.

---

## Basic Channel

| Function              | Transmit | Recognize | Remarks                          |
|-----------------------|----------|-----------|----------------------------------|
| Default channel       | —        | All       | Any channel accepted             |
| Changed channel       | —        | All       | No channel filtering             |
| Note number range     | —        | 0–127    | Sets grain position              |
| Velocity              | —        | Ignored   | Note On only (velocity > 0)      |
| Aftertouch            | —        | No        |                                  |
| Pitch Bend            | —        | No        |                                  |
| Control Change        | —        | Yes       | See table below                  |
| Program Change        | —        | No        |                                  |
| System Exclusive      | —        | No        |                                  |
| System Common         | —        | No        |                                  |
| System Real Time      | —        | No        |                                  |

---

## Note Messages

| Message   | Recognize | Behaviour                                      |
|-----------|-----------|------------------------------------------------|
| Note On   | Yes       | Sets grain position marker: `note / 127` (0–1) |
| Note Off  | No        | Ignored                                        |

---

## Control Change Messages

All values are scaled linearly from the 0–127 MIDI range unless noted.

| CC  | Name / Function          | Range mapped to              | Remarks                     |
|-----|--------------------------|------------------------------|-----------------------------|
| 1   | Modulation Wheel         | Smear 0.00 – 1.00           | Freeze textural control    |
| 7   | Channel Volume           | Master Volume 0.00 – 1.00   |                             |
| 10  | Pan                      | Spread 0.00 – 0.40          | Grain position scatter     |
| 11  | Expression               | Reverb Mix 0.00 – 1.00      | Dry/wet                     |
| 71  | Resonance                | Note Filter Q 0.5 – 12.0    |                             |
| 72  | Sound Controller 3       | Density 2 – 40 grains/s     |                             |
| 73  | Sound Controller 4       | Grain Size 10 – 200 ms      |                             |
| 74  | Sound Controller 5       | Note Filter Freq 40 – 2000 Hz |                         |
| 75  | Sound Controller 6       | Note Filter Cut 0 – –30 dB   | Negative = cut             |
| 76  | Sound Controller 7       | Pitch 0.25 – 2.00           | Playback rate              |
| 77  | Sound Controller 8       | Reverb Decay 2 – 40 s       |                             |
| 78  | Sound Controller 9       | Reverb Tone 400 – 10000 Hz  | Low-pass darkening         |

All other Control Change numbers are ignored.

---

## Notes

- MIDI must be enabled via the “Enable MIDI In” button in the interface.
- Notes immediately update the grain position marker and redraw the waveform.
- Continuous controllers update the corresponding on-screen controls and audio parameters in real time.
- No MIDI output is implemented.
- No clock, start/stop, or song-position support.

**Support:** ko-fi.com/tribalvoice  
MIT License. Copyright 2026 TribalVoice.
