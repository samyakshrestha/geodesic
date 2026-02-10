# Geodesic
Real-time Kerr black hole visualization.

Renders a spinning black hole with WebGL using Three.js and GLSL.

## Features
- GPU ray tracing with geodesic integration in the fragment shader
- Volumetric accretion disk with turbulent structure
- Doppler beaming, gravitational redshift, and photon ring
- Procedural star field with optional Milky Way sky map
- Interactive GUI controls
- Adaptive quality scaling for stable frame rates

## Technical Details
- Single-page app: all code and shaders in `index.html`
- Fullscreen quad with Three.js ShaderMaterial
- Geodesic integration runs per-pixel in the fragment shader
- Multi-pass rendering: main scene, bloom extraction, final composite
- GUI provided by lil-gui

## Runtime Controls
Top-right GUI panel:

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

Press `Space` to pause/resume animation.

## Sky Map
When enabled, the shader blends procedural stars with a Milky Way panorama from Wikipedia. If the network request fails, a fallback texture is generated. The HUD displays `SKYMAP REAL`, `SKYMAP FALLBACK`, or `SKYMAP OFF`.

## Run Locally
Open the file directly:

```bash
open index.html
```

Or use a local server:

```bash
python3 -m http.server 8080
```

Then navigate to `http://localhost:8080/`

## Troubleshooting
**Black screen:** WebGL is disabled or unsupported.

**Sky map not working:** Check the HUD. `SKYMAP FALLBACK` means the network request failed and a procedural texture is being used instead.

**Low FPS:** Reduce `Scattered Light`, `Detector Noise`, or `Image Sharpening`. The quality system will adapt automatically after a few seconds.


