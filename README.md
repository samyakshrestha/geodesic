# Geodesic
Real-time Kerr black hole visualization in a single `index.html` file.

This project renders a spinning black hole scene in WebGL using Three.js and GLSL.  
It is built for direct sharing as a public link, including GitHub Pages.

## What It Does
- Simulates light bending near a spinning black hole with iterative geodesic stepping in a fragment shader.
- Renders a volumetric accretion disk with procedural structure.
- Adds Doppler-like beaming, gravitational redshift tinting, and photon-ring-like highlights.
- Renders a background star field, with an optional Milky Way sky map.
- Exposes runtime controls through a GUI panel.
- Uses adaptive quality scaling to keep frame rate stable.

## Technical Summary
- Architecture: single-page app, all logic and shaders in `index.html`.
- Renderer: full-screen quad with Three.js `ShaderMaterial`.
- Core simulation: geodesic stepping in the fragment shader.
- Post-processing: bloom pass plus final composite pass.
- UI: `lil-gui`.

## Runtime Controls
The top-right panel includes:

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
- `Preset: Baseline`
- `Pause/Resume Animation`

Keyboard shortcut:
- `Space` toggles pause/resume.

## Current Default Values
Defaults are loaded from `index.html`:

- `Mass`: `3.79`
- `Spin`: `0.138`
- `Observer Distance`: `25.5`
- `Observer Inclination`: `4.8`
- `Time Dilation`: `1.19`
- `Disk Angular Speed`: `0.25`
- `Disk Sharpness`: `0.72`
- `Background Drift Speed`: `-0.5`
- `Coronal Emission`: `0.78`
- `Ring Sharpness`: `0.3`
- `Image Sharpening`: `0.43`
- `Optical Aberration`: `0.93`
- `Detector Noise`: `0.39`
- `Scattered Light`: `0.65`
- `Sky Map Background`: `true`
- `Sky Map Strength`: `0.72`
- `Debug Grid`: `false`

## Sky Map Behavior
- If `Sky Map Background` is enabled, the shader blends stars with a panoramic sky texture.
- Primary URL: `https://upload.wikimedia.org/wikipedia/commons/6/60/ESO_-_Milky_Way.jpg`
- If network loading fails, the app uses a generated fallback sky texture.
- HUD reports sky map state as `SKYMAP REAL`, `SKYMAP FALLBACK`, or `SKYMAP OFF`.

## Performance Notes
- Most cost comes from per-pixel geodesic stepping in the fragment shader.
- Additional cost comes from bloom and final composite passes.
- Adaptive scaling changes internal render resolution and step budget when FPS drops.
- 60 FPS cannot be guaranteed on all devices at identical visual quality.
- Hosting on GitHub Pages does not materially change GPU workload after page load.

## Run Locally
Open directly:

```bash
open index.html
```

Or run a local server:

```bash
python3 -m http.server 8080
```

Then open:
- `http://localhost:8080/`

## Deploy to GitHub Pages
1. Push this repository to GitHub.
2. Open GitHub repo settings, then open `Pages`.
3. Set `Source` to `Deploy from a branch`.
4. Set branch to `main` and folder to `/(root)`.
5. Save and wait for deployment.
6. Share `https://<username>.github.io/<repo>/`.

Optional hardening for static hosting:

```bash
touch .nojekyll
git add .nojekyll
git commit -m "Add .nojekyll for GitHub Pages"
git push
```

## Troubleshooting
- Black screen: WebGL is disabled or unsupported in the browser.
- Sky map toggle has no visible effect: check HUD `SKYMAP` state.
- `SKYMAP FALLBACK` means remote image did not load; fallback texture is active.
- Low FPS: lower `Scattered Light`, `Detector Noise`, or `Image Sharpening`, and wait for adaptive scaling.


