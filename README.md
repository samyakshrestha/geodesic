# Geodesic
Real-time black hole visualizations in WebGL (Three.js + GLSL), focused on geodesic lensing and relativistic disk appearance.

## Demos
- `index.html`: single spinning black hole (Kerr-inspired visual model)
- `merger.html`: binary black hole inspiral -> merger -> ringdown (Post-Newtonian driven)

## Scientific Scope
This project uses physically motivated approximations suitable for real-time rendering on consumer hardware.

- Null-ray geodesic integration in an effective relativistic potential
- Spin-coupled deflection terms to emulate frame-dragging behavior
- Photon-ring and shadow phenomenology
- Accretion disk radiative model with turbulence and orbital advection
- Relativistic Doppler beaming and gravitational redshift-style color shifts
- Binary inspiral from post-Newtonian-style orbital evolution (`x = M/r`, `dx/dt`, `dphi/dt`)

Not included:
- Full Kerr geodesics in Boyer-Lindquist coordinates
- Full numerical relativity / GRMHD
- Waveform-calibrated surrogate data files

## Rendering Architecture
- Single-file apps: all HTML, JS, and GLSL in one file per demo
- Fullscreen quad + `ShaderMaterial`
- Per-pixel geodesic integration in the fragment shader
- Multi-pass pipeline: main render, bloom extraction, composite pass
- Adaptive quality system for stable frame rate
- GUI with `lil-gui`

## Single-Black-Hole (`index.html`)
Core controls:
- `Mass`
- `Spin`
- `Observer Distance`
- `Observer Inclination`
- `Time Dilation`
- `Disk Angular Speed`
- `Disk Sharpness`
- `Background Drift Speed`
- `Coronal Emission`
- `Ring Sharpness`
- `Image Sharpening`
- `Optical Aberration`
- `Detector Noise`
- `Scattered Light`
- `Sky Map Background`
- `Sky Map Strength`
- `Debug Grid`

## Binary-Merger (`merger.html`)
Core controls:
- `Total Mass`
- `Mass Ratio q`
- `Spin a1`, `Spin a2`
- `Initial Separation`
- `Inspiral Rate`
- `Observer Distance`, `Observer Inclination`
- `Disk Angular Speed`
- `Disk Sharpness`
- `Merger Disk Wobble`
- `Disk Bridge Strength`
- `Background Drift Speed`
- `GW Ripple`, `GW Ripple Strength`
- `Auto Frame`
- `Far-Field RK2`
- `Playback Speed`

Playback actions:
- `Play/Pause`
- `Toggle Rewind`
- `Reset to Inspiral`
- `Skip to Post-Merger`

## Sky Map
When enabled, the shader blends procedural stars with a Milky Way sky map. If network texture loading fails, a procedural fallback sky is used. HUD state:
- `SKYMAP REAL`
- `SKYMAP FALLBACK`
- `SKYMAP OFF`

## Run Locally
Open directly:

```bash
open index.html
open merger.html
```

Or run a local server:

```bash
python3 -m http.server 8080
```

Then open:
- `http://localhost:8080/index.html`
- `http://localhost:8080/merger.html`

## GitHub Pages
- Single BH: `https://samyakshrestha.github.io/geodesic/`
- Binary merger: `https://samyakshrestha.github.io/geodesic/merger.html`

## Performance Notes
- Single BH typically runs faster than binary merger.
- Binary mode is heavier because two potentials and merger transitions are evaluated per pixel.
- Adaptive quality lowers internal resolution/step budget when FPS drops.

## Troubleshooting
**Black screen**
- WebGL disabled or unsupported browser/GPU path.

**Sky map not visible**
- Check HUD. `SKYMAP FALLBACK` means network sky texture failed and fallback is active.

**Low FPS**
- Reduce `Scattered Light`, `Detector Noise`, or `Image Sharpening`.
- In merger mode, also reduce `GW Ripple Strength` and keep `Background Drift Speed` near `0`.
