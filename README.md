# Vinyl Simulator

A browser-based vinyl record simulator built with the Web Audio API. Drop any audio file onto the player and apply real-time analogue processing to give it the character of a vinyl record.

---

## Effects Reference

### Implemented

| Effect | Slider | Description |
|--------|--------|-------------|
| **Warmth** | 0–100% | Boosts ~220 Hz with a peaking filter, rolls off the high shelf, and adds harmonic saturation via a soft-clip waveshaper. Models the tonal colour of the RIAA playback chain. |
| **Surface Noise** | 0–100% | Looping pink noise (Paul Kellett's algorithm) shaped through a 4 kHz lowpass. Simulates the continuous hiss of a dusty groove. |
| **Wow & Flutter** | 0–100% | Two LFOs modulate a shared delay node: 0.5 Hz (wow — slow pitch drift from platter speed variation) and 7 Hz (flutter — fast mechanical wobble). |
| **Crackle** | 0–100% | Sparse exponential-decay impulses baked into a looping buffer, filtered through a 2.2 kHz bandpass. Simulates dust and micro-scratches on the groove wall. |
| **Vinyl Age** | 0–100% | Progressive high-frequency softening — rolls the lowpass cutoff down from 14.5 kHz to 8 kHz as the record ages. Models years of accumulated wear on the groove walls. |
| **Stylus Resonance** | 0–100% | Peaking filter at 10 kHz (Q = 2.5, up to +6 dB). The cartridge's natural resonant peak adds brightness, air, and presence — more pronounced on moving-magnet cartridges. |
| **Worn Stylus** | 0–100% | High-shelf cut above 8 kHz (up to −8 dB). A worn diamond tip rounds off the groove edges, dulling transients and reducing high-frequency detail. |
| **Turntable Rumble** | 0–100% | Pink noise through a narrow 30 Hz bandpass filter. Represents low-frequency vibration from the motor and platter bearings — felt more than heard on a real system. |
| **Ghost Echo** | 0–100% | Delayed copy of the signal at one full vinyl revolution (60 / 33.33 ≈ 1.8 s) mixed in at −32 dB max. Simulates adjacent-groove bleed — loud passages faintly imprint into neighbouring grooves. |
| **RIAA Mismatch** | 0–100% | Shifts the effective playback EQ. Below 50%: warm/lush (low-shelf boost, high-shelf cut). Above 50%: bright/punchy (low-shelf cut, high-shelf boost). Center = neutral. |

---

### Planned

| Effect | Description |
|--------|-------------|
| **Vinyl Drift** | Smooth once-per-revolution pitch drift caused by an off-centre spindle hole. A 0.556 Hz LFO (33.33 RPM) modulates delay time independently of Wow & Flutter. |
| **Inner Groove Distortion** | Intermodulation distortion and high-frequency loss from the reduced groove velocity near the record label. Distortion increases as a function of playback position. |
| **Stylus Pinch** | Frequency-doubling distortion triggered by heavy bass content pushing the stylus against the groove wall. Approximated via a bass-sensitive waveshaper. |
| **Vinyl Compression** | Mechanical groove compression — bass energy modulates the treble, creating subtle pumping and HF ducking. Requires a sidechain-style dynamics stage. |
| **Stereo Field** | Mid-Side width control from tight mono to wide spacious stereo. Implemented via a ChannelSplitter/Merger M-S matrix. |
| **Mastering House** | Four distinct mastering chain presets (different lathe, tape, and EQ characters) selectable via a toggle. Each has its own saturation curve and shelving fingerprint. |
