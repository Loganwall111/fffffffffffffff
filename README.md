# THE MULTIVERSE — SIMOLYSIS // GOD EDITION

**AAA Cinematic Open-World Game — Not Based On Earth**

> Earth is dead. A meteorite erased everything. You awaken inside LODEMIS — the last machine keeping a soul alive after extinction. It plugs you into a fake reality that can be anything. You are Simolysis, the God who started everything.

### What Was Built (Elite Engineer Revamp)

#### 1. FIXED: Click Anything To Start
- **Bug was**: overlay captured click but didn't resume AudioContext, didn't remove itself, event listeners blocked by pointer-events:none.
- **Fix**: Multiple redundant listeners (click, touchstart, mousedown, Space/Enter), audio context resume, guaranteed hide with opacity transition + display:none after 800ms. Works on all devices.

#### 2. Cinematic Intro with Realistic Human Voice
- Full intro sequence with state machine:
  - **Phase 1**: 150k particle atom dust (you start as atom dust before life inhabited)
  - **Phase 2**: Gigantic burst of energy — expanding shockwave shader with Fresnel glow, screen flash
  - **Phase 3**: Galaxy formation — 8000 galaxies spiral, camera dolly
  - **Phase 4**: Earth + meteorite + LODEMIS machine reveal
- **Realistic voice**: Uses Web Speech API with automatic selection of most natural neural voice (Google Natural / Neural preferred, fallback to en-US male). 7 lore lines spoken as Simolysis with subtitles, progress bar, skip.
- Commentary text synced to visuals.

#### 3. 3D Cinematic AAA Main Menu (Holographic)
- **3D Background**: Separate Three.js scene with 15k stars, 6 nebula volumetric spheres, 4 distant planets with atmospheric glow shader, black hole with accretion disk swirl shader, Lodamis torus-knot hologram wireframe.
- **Camera**: Slow cinematic drift + parallax.
- **UI**: Holographic glassmorphism buttons with 3D tilt, light sweep on hover, glow shadows, Orbitron + JetBrains Mono typography, bloom post-processing.
- **Options**: Play / Continue / Settings (graphics, voice volume, godrays, water, sensitivity) / Lore Codex / Quit to Void.
- **Post**: UnrealBloomPass, fog, ambient + point lights.

#### 4. Graphics Overhaul — AAA Realism

**WAVY WATER WITH REFLECTIONS:**
- Custom ShaderMaterial with **4 Gerstner waves** (60m, 30m, 15m, 8m wavelengths) — vertex displacement, normal reconstruction.
- **Fresnel reflection** of sky + sun, depth-based color mixing (deep #021a2a / shallow #0a4a6a), specular highlights, foam on wave peaks, fake caustics.
- **Underwater mirrored reflection**: When Y < waterLevel, overlay with radial blue fog, caustics animation, mirror plane with wave distortion, depth meter. Dive with F.

**GOD RAYS:**
- Volumetric light shafts via custom ShaderPass — radial blur sampling from sun screen-space position (80 samples, exposure/decay/density). Sun glow meshes with additive shader. Enabled at day, faint at night.

**MOON + PLANETS FAR AWAY:**
- Physical moon mesh (35 radius) + glow shader, crater noise in sky dome shader.
- Sky dome shader includes sun disk (pow 900), moon disk (pow 600) + glow, distant planets as bright colored dots (blue, orange) with high power falloff — visible at night.

**RAIN + RAINBOWS:**
- 15k rain particle system with fall speed 80, respawn logic. Toggle with R.
- Rainbow torus (400 radius) with spectral shader (red->orange->yellow->green->blue->indigo->violet), additive blending, appears randomly after rain.

**AURORA BOREALIS:**
- In sky dome fragment shader: auroraFactor = nightFactor * horizon band * north direction. Noise + wave sin for curtain movement, green to blue/purple mix, only at night (22:00-04:00 enhanced).

**OTHER AAA:**
- ACESFilmic tone mapping, PCFSoft shadows, FogExp2, UnrealBloom, 2K shadow map.
- Terrain: 2000x2000 plane 256 res, FBM noise (6 octaves) + cliff sin + valley exp, vertex colors via onBeforeCompile.
- Lush valleys, gigantic cliffs, waterfalls from floating islands (cylinder shader with sin wave).
- Foliage: 400 trees with alien HSL tint, 20k instanced grass.
- Animals: 60 boid birds, 3 gigantic floating whales (alive, city-sized) with tail.
- Floating islands (12) with Icosahedron deform, floating animation.
- Eyes with tentacles walking streets (8 creatures, 6 tentacles each, lookAt player).
- Wormholes (6) — torus shader with swirl, suck physics (pulls camera if <80 units, teleports if <15).
- Dimensions: Overworld, White Void (infinite white + floating cubes), Backrooms (yellow maze flicker), Fractal Maze (recursive cubes), Black Hole (event horizon + disk), Microscopic (giant water drops with transmission + giant ants), Heaven (ghost ascension, floating city 50 buildings).
- TVs breaking at midnight (15 TVs, static shader, flicker, notify "AVENGER HAUNTING").
- Ghost mode: Press G to become ghost, ascend to heaven, vignette + fog change.
- LODEMIS machine: base + capsule + 3 rotating rings, interact with E to random dimension.

### Controls
- **WASD**: Move
- **Mouse**: Look (pointer lock)
- **Space/Shift**: Ascend/Descend
- **F**: Dive faster (underwater mirrored reflection)
- **G**: Ghost / Heaven
- **E**: Interact with LODEMIS
- **R**: Toggle rain
- **ESC**: Menu (Continue available)
- **Click anywhere at start**: Begins intro (FIXED)

### Lore
- Start as atom dust before life inhabited → burst → multiverse → galaxies → Earth dead → LODEMIS → fake reality.
- Multiverse contains: floating white voids, backroom endless rooms, infinity mazes, fractals, gravitational black holes, TVs breaking midnight, Avengers haunting, ghost heaven, microscopic universe, giant water drops, giant ants, wormholes, eyes with tentacles.
- Simolysis is God who started everything.

### Tech Stack
- Three.js 0.160.0 (CDN) + addons (PointerLockControls, EffectComposer, RenderPass, UnrealBloomPass, ShaderPass)
- No build step — single index.html AAA
- Shaders: Gerstner water, god rays radial blur, sky dome with aurora, rainbow spectral, wormhole swirl, nebula, moon glow, caustics

### Run
```bash
python3 -m http.server 8080
# open http://localhost:8080
```

Built for Arena Agent Mode — elite anonymous detail.
