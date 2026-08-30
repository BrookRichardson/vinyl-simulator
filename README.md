# Vinyl Simulator

A browser-based vinyl record simulator built with the Web Audio API. Drop any audio file onto the player and apply real-time analogue processing to give it the character of a vinyl record.

**[Try it live](https://brookrichardson.github.io/vinyl-simulator/)** — runs entirely in your browser, nothing to install.

---

## Getting Started

1. Open the [live page](https://brookrichardson.github.io/vinyl-simulator/), or clone the repo and open `index.html` in a modern browser (Chrome or Edge recommended)
2. Drop an audio file onto the player, or click the upload zone to browse
3. Press play — all effects are applied in real time
4. Adjust sliders while audio is playing to hear changes immediately

**Best heard on:** headphones or speakers with decent bass response. Laptop speakers will struggle to reproduce Turntable Rumble and Ghost Echo.

---

## Effects Reference

### Warmth

**What it does:** Boosts the low-mids (~220 Hz) with a peaking filter, rolls off the high shelf above 6 kHz, and adds harmonic saturation through a soft-clip waveshaper. Collectively this mimics the tonal colouration introduced by the RIAA playback chain and analogue circuitry.

**How to hear it:** Play a track with vocals and acoustic instruments. Raise Warmth from 0% to 100% — the sound becomes progressively more rounded and "analogue", with a fuller midrange and slightly softened top end. At high values you'll also hear gentle harmonic grit on peaks.

**Default:** 50%

---

### Surface Noise

**What it does:** A looping pink noise buffer (generated using Paul Kellett's approximation) passed through a 4 kHz lowpass filter. This produces the continuous low-level hiss that sits under the music on a dusty or worn record.

**How to hear it:** Easiest to hear in quiet passages or at the start/end of a track. Raise the slider slowly from 0% — you'll hear a soft hiss emerge beneath the music. At high values it becomes an obvious tape-like noise floor.

**Default:** 40%

---

### Wow & Flutter

**What it does:** Two LFOs modulate a shared delay node to create pitch instability. A 0.5 Hz oscillator produces *wow* — the slow, seasick pitch drift caused by platter speed variation. A 7 Hz oscillator produces *flutter* — a faster, more mechanical wobble from belt or bearing irregularities.

**How to hear it:** Best heard on sustained notes — a held piano chord, a long vocal note, or a synth pad. Raise the slider from 0% and listen for the pitch gently wavering. At high values it becomes an obvious seasick warble. On percussive music the effect is much harder to notice.

**Default:** 35%

---

### Crackle

**What it does:** Sparse exponential-decay impulses are baked into a looping buffer, then filtered through a 2.2 kHz bandpass. Each impulse mimics a dust particle or micro-scratch passing under the stylus.

**How to hear it:** Most audible in quiet passages. Raise the slider from 0% — you'll hear irregular pops and ticks appearing in the background. At high values it sounds like a well-used 45 played on a dusty deck. Crackle is randomised on each play, so it never repeats.

**Default:** 30%

---

### Vinyl Age

**What it does:** A second lowpass filter that progressively rolls off the high-frequency ceiling as the record "ages". At 0% the cutoff is 14.5 kHz (imperceptible). At 100% it drops to 8 kHz, removing most of the air and shimmer from the recording.

**How to hear it:** Play a track with prominent hi-hats, cymbals, or acoustic guitar string noise. With Vinyl Age at 0%, those details are clear. Drag the slider toward 100% and listen to the top end gradually disappear — the sound becomes duller and more muffled, like a record played hundreds of times.

**Default:** 0% (new record)

---

### Stylus Resonance

**What it does:** A peaking filter at 10 kHz (Q = 2.5, up to +6 dB). Moving-magnet cartridges have a natural resonant peak in the upper treble caused by the interaction between the stylus mass and the cantilever compliance. This adds brightness, air, and a slight edge to high-frequency content.

**How to hear it:** Play a track with clear high-frequency content — cymbals, sibilant vocals, or an acoustic guitar. Raise the slider from 0% and listen for a brightening and slight "zing" around the upper presence region. At 100% it becomes noticeably shimmery compared to the dry signal.

**Default:** 25%

---

### Worn Stylus

**What it does:** A high-shelf cut above 8 kHz (up to −8 dB). A diamond stylus that has accumulated hundreds of hours of play becomes rounded, losing the ability to trace fine groove detail. The result is a loss of high-frequency resolution and a dulling of transients.

**How to hear it:** Play a track with crisp, bright content. Set Worn Stylus at 0% and note how clear the top end is. Raise it toward 100% — the hi-hats become cloudy, vocals lose their air, and the overall sound becomes fatigued and dull, like music heard through a worn cartridge.

**Default:** 0% (new stylus)

---

### Turntable Rumble

**What it does:** Pink noise fed through a bandpass filter centred at 55 Hz. This replicates the low-frequency mechanical vibration transferred from the motor and platter bearings into the tonearm and stylus. On a real system it is felt as much as heard.

**How to hear it:** Requires headphones or speakers capable of reproducing bass below 80 Hz — laptop speakers will not reproduce this effect. Play a track and raise the slider slowly from 0%. You'll hear (and feel) a low, continuous thudding drone emerge beneath the music. At high values it sounds like the turntable itself is in the room.

**Default:** 20%

---

### Ghost Echo

**What it does:** A delayed copy of the processed signal mixed back in at a very low level with a delay time of approximately 1.8 seconds — exactly one revolution of a 33⅓ RPM record. This simulates adjacent-groove bleed, where the signal from a neighbouring groove (one revolution away) faintly bleeds into the current playback.

**How to hear it:** Best heard on tracks with loud transient peaks — a snare hit, a loud vocal entry, or a sharp guitar chord. Raise the slider from 0% while listening carefully in the 1–2 seconds before those peaks. You'll hear a faint ghost of the loud moment arriving slightly early. It is subtle by nature; at 100% it becomes clearly audible as a faint pre-echo.

**Default:** 15%

---

### RIAA Mismatch

**What it does:** Shifts the effective playback EQ curve to simulate a mismatch between the curve used when the record was cut and the curve applied by the phono preamp. Below 50%: bass shelf boost (+3 dB at 200 Hz) and treble shelf cut (−4 dB at 3 kHz) — a warm, lush character typical of older mastering. Above 50%: bass shelf cut and treble boost — a brighter, more forward, punchy sound.

**How to hear it:** Play a track with a wide mix — bass, vocals, and hi-hats all present. Drag the slider slowly from 0% (warm) to 100% (bright) and listen to the tonal balance shift. At 0% the low end feels prominent and the top is smooth. At 100% the midrange becomes more present and the bass recedes. The effect is a gradual tilt, not a switch — most audible at the extremes.

**Default:** 50% (neutral — no effect)

---

## Planned Effects

| Effect | Description |
|--------|-------------|
| **Vinyl Drift** | Smooth once-per-revolution pitch drift from an off-centre spindle hole. A 0.556 Hz LFO modulates delay time independently of Wow & Flutter. |
| **Inner Groove Distortion** | Intermodulation distortion and HF loss from reduced groove velocity near the label. Intensity increases with playback position. |
| **Stylus Pinch** | Frequency-doubling distortion triggered by heavy bass pushing the stylus against the groove wall. |
| **Vinyl Compression** | Mechanical groove compression — bass energy modulates the treble, creating subtle pumping and HF ducking. |
| **Stereo Field** | Mid-Side width control from tight mono to wide spacious stereo. |
| **Mastering House** | Four distinct mastering chain presets with different lathe, tape, and EQ characters. |
