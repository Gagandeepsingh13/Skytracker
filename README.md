# ✈ SKYTRACK — 3D Live Flight Tracker

A production-quality 3D flight tracking app built with React + Vite + Three.js (react-three-fiber + drei). Visualizes live OpenSky aircraft data on a rotatable 3D Earth with real-time plane motion, altitude-accurate positioning, and cinematic post-processing.

## 🚀 Quick Start

```bash
# 1. Install dependencies
npm install

# 2. Start dev server
npm run dev

# 3. Open http://localhost:5173
```

## 🌍 Features

- **Live Aircraft Data** — fetches from OpenSky Network every 12 seconds
- **Smooth Interpolation** — aircraft glide between position updates in real-time
- **Altitude-Accurate Positioning** — planes orbit at correct height above the surface
- **Custom Earth Shaders** — day/night texture blend, specular ocean reflections, atmospheric rim lighting
- **Post-Processing** — Bloom, Chromatic Aberration, and Vignette via @react-three/postprocessing
- **Flight Detail Panel** — click any plane to see callsign, altitude, speed, heading compass, vertical speed indicator
- **Color-coded Altitude** — amber (ground), green (<10k ft), cyan (cruise), pink (high altitude)
- **Trail Lines** — recent flight paths rendered as 3D lines
- **Simulation Fallback** — if OpenSky is unreachable (CORS), 400 simulated aircraft are generated
- **Controls Panel** — toggle trails, labels, ground aircraft filter

## 🎮 Controls

| Action | Input |
|--------|-------|
| Rotate globe | Click + drag |
| Zoom | Scroll wheel |
| Select aircraft | Click |
| Deselect | Click empty space |

## 🎨 Architecture

```
src/
├── components/
│   ├── Scene.jsx          # Three.js canvas + post-processing
│   ├── Globe.jsx          # Earth sphere with custom shaders
│   ├── AircraftLayer.jsx  # All aircraft meshes + interpolation
│   ├── FlightPanel.jsx    # Selected aircraft info sidebar
│   ├── HUD.jsx            # Stats + controls overlay
│   ├── Starfield.jsx      # Background stars
│   └── LoadingScreen.jsx  # Suspense fallback
├── hooks/
│   └── useOpenSky.js      # Data fetching + simulation fallback
├── shaders/
│   └── earth.js           # GLSL vertex + fragment shaders
├── utils/
│   └── coordinates.js     # Lat/lon ↔ 3D math utilities
├── store.js               # Zustand global state
└── styles/
    └── globals.css        # CSS variables + animations
```

## 🌐 OpenSky API

The app uses the free [OpenSky Network API](https://opensky-network.org/api/states/all) (no key required, rate-limited). The Vite dev server proxies requests through `/opensky` to avoid CORS issues. In production, set up your own proxy or use authenticated API requests.

## 📦 Build for Production

```bash
npm run build
npm run preview
```

Note: In production, configure a backend proxy for OpenSky API calls.
