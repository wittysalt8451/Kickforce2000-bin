# Kickforce 2000

909-style kick drum synthesizer for the Noise Engineering Versio platform, with a distortion stage and a stereo input built in.

The kick itself is built from two independent parts — a **transient** (the click) and a **body** (the tone and pitch drop) — so you can dial in anything from a tight, minimal-techno thump to a resonant drone or a full-on bass tone. That's the core of it, but most of the module's range actually comes from its two switches: they decide what the Color knob does, and what your stereo input does — right up to a mode that turns the whole thing into a standalone filter/VCA/distortion effect with no kick involved at all.

---

## Flashing the firmware

### Via Daisy Web Programmer (recommended)

1. Download `kickforce2000_vX.X.X.bin`
2. Open [https://electro-smith.github.io/Programmer/](https://electro-smith.github.io/Programmer/) in Chrome or Edge (other browsers not supported)
3. Put the Versio in DFU mode: hold **BOOT**, press **RESET**, release both
4. Click **Connect** and select the Daisy
5. Click **Choose File** and select the `.bin`
6. Click **Program** — done in a few seconds

> The module restarts automatically after flashing.

### Via dfu-util (command line)

```bash
dfu-util -a 0 -s 0x08000000:leave -D kickforce2000_vX.X.X.bin
```

---

## Controls (kick mode — Input switch on THRU or SC)

| Knob | Function |
|------|----------|
| 1 | **Pitch** — base frequency, roughly 40–120 Hz, 1V/oct CV input |
| 2 | **Pitch env amount** — how far the pitch sweeps on each hit |
| 3 | **Amp decay** — how long the kick sustains; all the way up it latches at a non-zero floor, so you get a drone instead of a hit |
| 4 | **Pitch env time** — how fast the pitch sweep moves; the upper range adds a quick pitch attack before it falls |
| 5 | **Color** — what this knob does depends on the Color switch (see below) |
| 6 | **Drive** — a warm, soft-edged saturation that thickens the kick without ever turning harsh or digital; same knob. Push past halfway and the top end blooms into a wide stereo image — with the Color switch on TUBE, that's also where a slow, resonant low-mid tail opens up underneath |
| 7 | **Transient** — starts as a clean, sharp sine click; turn it up and a thick, noisy burst piles on top of it, growing from a light snap to a dense, gritty attack |

---

## Switches

### Color switch — TUBE / FOLD / FM

Sets what the Color knob (5) does to your sound before it hits the Drive. 

| Position | Name | What you get |
|----------|------|---------------|
| L | TUBE | Feeds low-passed noise into the diode — a grainy, textured edge rather than a tonal change. Good for adding grit without touching the pitch |
| C | FOLD | A wavefolder ahead of the diode — turn it up for increasingly dense, buzzing harmonics |
| R | FM | Color becomes the FM ratio on the kick body — for metallic, clangy, bell-like kicks |

> In GT mode (Input switch on R) this switch does a different job — see [GT mode](#gt-mode) below.

### Input switch — THRU / SC / GT

Decides what happens to your stereo input.

| Position | Name | What it's for |
|----------|------|----------------|
| L | THRU | Passes your input through untouched — for when you just want a clean stereo signal running alongside the kick |
| C | SC | Ducks the input on every hit and eases it back in following the kick's own decay, no hard snap-back. Reach for this when you're tight on space and don't want to dedicate a whole module to sidechaining |
| R | GT | Switches the kick off and turns the whole module into a standalone triggered filter + VCA + distortion unit on your input — see [GT mode](#gt-mode) below |

> When there's no signal at the input, the sidechain path bypasses automatically, so the output is kick-only with no residual noise. That applies in THRU and SC; in GT mode there's no kick to fall back on, so silence in means silence out.

---

## GT mode

Flip the Input switch to R and the kick synth switches off completely. In its place you get a triggered lowpass filter and VCA envelope, feeding the same two-stage fold + diode distortion the kick uses — three effects stacked behind one trigger. Feed it a drone and turn it into a wide, plucky, rhythmic voice; feed it a bassline and shape it into filtered, distorted hits. It needs a **trigger** (gate or tap, same input as the kick) to open — it won't react to the incoming audio on its own, unless Decay (knob 3) is turned all the way up, in which case the gate stays open permanently and audio passes through even with no trigger at all.

The knobs are the same physical controls as in kick mode, just repurposed:

| Knob | Kick mode | Function in GT mode |
|------|-----------|----------------------|
| 1 | Pitch | **Filter bottom** — where the lowpass settles at the end of the sweep, roughly 75 Hz up to fully open. Fully clockwise bypasses the filter entirely |
| 2 | Pitch env amount | **Filter top** — how far above the bottom the filter opens on each trigger. Set below the bottom position and there's no sweep at all |
| 3 | Amp decay | **Decay** — the VCA envelope length. All the way up holds the gate open permanently for continuous pass-through, with no trigger needed at all, instead of gated hits |
| 4 | Pitch env time | **Filter decay** — how fast the filter closes after a trigger; also sets how long the attack boost on knob 7 lasts |
| 5 | Color | **Color** — always the wavefolder ahead of the diode here, regardless of the Color switch position |
| 6 | Drive | **Drive** — the same diode as in kick mode; past halfway it opens the same stereo widener |
| 7 | Transient | **Transient** — an attack boost shaped like the filter-open envelope, no click or noise layer here |

In GT mode the Color switch takes on a different job: it tilts the tone going into the distortion.

| Position | Effect |
|----------|--------|
| L | Pushes the bass into the distortion — flattens the low end for a thin, tight result |
| C | Flat, no tilt |
| R | Pushes the highs into the distortion — the low end stays clean, the bite sits on top |

The tilt only makes an audible difference once Color (the fold) is open; with Color closed and only Drive active, the three positions sound close to identical.

---

## Changelog

| Version | Notes |
|---------|-------|
| v1.0.0 | Initial release |
| v1.1.0 | Some minor fixes |
| v2.0.0 | Uniform diode distortion across all Color switch positions (Drive no longer changes character with the switch). Gate mode replaced by a standalone GT effects channel: triggered lowpass filter + VCA envelope with its own two-stage fold+diode distortion and pre-emphasis tone tilt. Smoother sidechain-duck release — the input eases back in with the kick's decay instead of snapping back. |

---

© 2026 — free to use for personal use. Redistribution or commercial use not permitted.
