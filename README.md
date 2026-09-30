# Kickforce 2000

909-style kick drum synthesizer for the Noise Engineering Versio platform.

Two independent sections — **transient** and **body** — with a distortion stage and stereo sidechain input. Ranges from surgical minimal techno kick to resonant drone or bass sound.

---

## What's new in v2.0.0

Two big changes from v1.1:

**1. One distortion, not three.** The Distortion switch used to pick between three separate distortion algorithms (Tube, Foldback, FM), each with its own character. That's gone: there is now **one fixed distortion path** (a soft diode) on the Drive knob, the same in every switch position. What the switch now picks is what the **Color** knob does *before* the diode:

- **L** — Color adds noise into the diode (it's not a tone/saturation control — it's literally noise, shaped by the diode and ducked by the kick body)
- **C** — Color is a wavefolder placed in front of the diode
- **R** — Color is the FM ratio on the kick body

Drive itself — the diode amount, and what its upper half opens up (stereo widening, and in Noise mode a slow low-mid resonant tail) — no longer changes with the switch. It's one knob doing one thing everywhere.

**2. The Gate switch position is now a standalone effects channel, not a kick variant.** Kickforce is a sound *generator* first (which fits better on the Noise Engineering's Alia platform), so a "gate the input" mode always sat a bit awkwardly on it. In the spirit of what the Versio platform is generally used for, the old Gate position has been rebuilt into a self-contained **Decay / Low-pass filter / LPG-style / 2× distortion** unit: the kick synth switches off entirely and every knob is repurposed to run your stereo input through a triggered filter+VCA envelope and the same two-stage distortion the kick uses. See [SW_1 = R — VCA / FX mode](#sw_1--r--vca--fx-mode) below for the full knob map — it's a different instrument in that switch position, not "kick with less signal getting through."

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

## Controls (kick modes — SW_1 = L or C)

| Knob | Function |
|------|----------|
| 1 | **Pitch** — base frequency, approx. 40–120 Hz, 1V/oct CV input |
| 2 | **Pitch env amount** — how far the pitch sweeps on each hit |
| 3 | **Amp decay** — sustain length; top position latches a non-zero floor (drone) |
| 4 | **Pitch env time** — sweep speed; upper range adds a pitch attack before the fall |
| 5 | **Color** — what this does depends on the Color-mode switch (see below): noise into the diode, a wavefolder ahead of the diode, or the FM ratio |
| 6 | **Drive** — the diode distortion amount; the same knob and the same algorithm in every Color-mode position. Upper half also opens a subtle stereo widening on the kick's top end |
| 7 | **Transient** — from pure sine click to bandpass noise |

---

## Switches

### Color mode

Chooses what the Color knob (5) does. Drive (6) is unaffected — it's always the diode, at the same range, in every position.

| Position | Mode | Color knob does |
|----------|------|------------------|
| L | Tube | Adds low-passed noise into the diode clipper — texture, not tone |
| C | Fold | Wavefolder placed before the diode; dense harmonics as it opens |
| R | FM | Sets the FM ratio on the kick body |

> In GT mode (SW_1 = R) this switch does something else entirely — see below.

### Mode (was: Creative Sidechain)

Controls how the stereo input relates to the kick — or, in the third position, replaces the kick synth altogether.

| Position | Mode | Behaviour |
|----------|------|-----------|
| L | THRU | Stereo input passed through unaffected |
| C | SC | Silence at the hit, then eases back in following the kick's own decay — no hard snap-back |
| R | GT | Kick synth off; the module becomes a standalone triggered filter + distortion effect on the stereo input. Every knob is repurposed — see below |

> When the input is silent, the sidechain path bypasses automatically — output is kick-only with no residual. This applies in Bypass and Sidechain duck; in VCA/FX mode there is no kick to fall back to, so silence in is silence out.

---

## SW_1 = R — GT - VCA / FX mode

The kick synth is switched off. Instead, your stereo input is fed through a triggered lowpass filter and VCA, then through the same two-stage distortion (fold + diode) the kick uses. It needs a **trigger** (gate or tap, same input as the kick) to open — it does not open itself off the incoming audio.

| Knob | Function in this mode |
|------|------------------------|
| 1 | **Filter bottom** — where the lowpass settles at the end of the sweep, roughly 75 Hz up to fully open. Turned fully clockwise, the filter is bypassed entirely (unity pass-through) |
| 2 | **Filter top** — how far above the bottom the filter starts open on each trigger. Set below the bottom position, there's no sweep at all |
| 3 | **Decay** — the VCA's loudness envelope. Top position holds it open (continuous pass-through instead of gated hits) |
| 4 | **Filter decay** — how fast the filter closes from top to bottom after a trigger; also sets how long the attack-boost on knob 7 lasts |
| 5 | **Color** — always the wavefolder ahead of the diode here, regardless of the Color-mode switch |
| 6 | **Drive** — the diode, same knob as in kick mode; upper half again opens the widener |
| 7 | **Transient** — an attack boost (gain lift) shaped like the filter-open envelope; no click or noise layer here, unlike in kick mode |

The **Color-mode switch** takes on a different job here too: instead of picking what Color does, it tilts the tone going *into* the distortion —

| Position | Effect |
|----------|--------|
| L | Bass is pushed into the distortion — the low end gets flattened, result is thin and tight |
| C | Flat — no tilt |
| R | Highs are pushed into the distortion — the low end stays clean, the bite sits on top |

This tilt only has an audible effect once Color (the fold) is open; with Color closed and only Drive active, the difference between switch positions is minor.

---

## Changelog

| Version | Notes |
|---------|-------|
| v1.0.0 | Initial release |
| v1.1.0 | Some minor fixes |
| v2.0.0 | Uniform diode distortion across all Color-mode positions (Drive no longer changes character with the switch). Gate mode replaced by a standalone VCA/FX channel: triggered lowpass filter + VCA envelope with its own two-stage fold+diode distortion and pre-emphasis tone tilt. Smoother sidechain-duck release — the input eases back in with the kick's decay instead of snapping back. |

---

© 2026 — free to use for personal use. Redistribution or commercial use not permitted.
