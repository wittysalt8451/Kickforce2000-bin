# Kickforce 2000

909-style kick drum synthesizer for the Noise Engineering Versio platform.

Two independent sections — **transient** and **body** — with a distortion stage and stereo sidechain input. Ranges from surgical minimal techno kick to resonant drone or bass sound.

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

## Controls

| Knob | Function |
|------|----------|
| 1 | **Pitch** — base frequency, approx. 40–120 Hz |
| 2 | **Pitch env amount** — how far the pitch sweeps on each hit |
| 3 | **Amp decay** — sustain length; top position latches a non-zero floor (drone) |
| 4 | **Pitch env time** — sweep speed; upper range adds a pitch attack before the fall |
| 5 | **Color** — works with Drive; distortion character in Tube mode, comb filter in Foldback mode, FM ratio in FM mode |
| 6 | **Distortion drive** — drive amount for the selected distortion mode |
| 7 | **Transient** — from pure sine click to bandpass noise |

---

## Switches

### SW 0 — Distortion

| Position | Mode | Character |
|----------|------|-----------|
| L | Tube | Warm, controlled saturation; Color sets distortion character |
| C | Foldback | Dense harmonics; Color controls a comb filter |
| R | FM | Frequency modulation algorithm; Color sets the FM ratio |

### SW 1 — Sidechain

Controls how the stereo input relates to the kick.

| Position | Mode | Behaviour |
|----------|------|-----------|
| L | Bypass | Stereo input passed through unaffected |
| C | Sidechain duck | Full silence during the kick; dry passthrough between hits |
| R | Gate | Input audible only during the kick itself |

> When the input is silent, the sidechain path bypasses automatically — output is kick-only with no residual.

---

## Changelog

| Version | Notes |
|---------|-------|
| v1.0.0 | Initial release |

---

© 2025 — free to use for personal use. Redistribution or commercial use not permitted.
