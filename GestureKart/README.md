# GestureKart

**Physical Gesture-Controlled Traffic Rule Training Simulator**

Interactive web-based 3D driving game controlled by body gestures via webcam (MediaPipe Pose) + keyboard fallback. Players navigate a simulated urban road, obey traffic signals, and receive a downloadable Civic Driving Score.

---

## Quick start (no build step)

1. Open `gesturekart.html` in a modern browser **over HTTPS** (or `localhost`).
2. Allow camera permission when prompted.
3. On the **Camera setup** screen:
   - Stand so your **shoulders and both hands** are visible.
   - Press **Calibrate neutral pose** while holding a neutral “steering wheel” position.
   - Press **Start driving**.
4. Drive with gestures (or keyboard).

> Webcam access requires a **secure context** (HTTPS or localhost). Deploy to Vercel / Netlify / Render for a live link.

### Local test server (recommended)

```bash
# From this folder
npx serve .
# or
python3 -m http.server 8080
```

Then open `http://localhost:8080/gesturekart.html`.

---

## Gesture controls

| Action        | Gesture                                      | Keyboard fallback |
|---------------|----------------------------------------------|-------------------|
| Steer left/right | Tilt hands left/right (like a steering wheel) | A / D or ← / →   |
| Accelerate    | Spread hands wider (after calibrate)         | W or ↑            |
| Brake / Stop  | Raise either hand above shoulder             | Space              |
| Pause         | —                                            | P or Esc          |

If tracking is lost, the car eases off and then brakes automatically.

---

## What’s included

```
GestureKart/
├── gesturekart.html          ← Main playable game (MediaPipe already wired)
├── README.md
├── src/lib/
│   ├── gestureEngine.ts      ← Calibration, smoothing, dead-zone, lost-tracking
│   ├── poseLoop.ts           ← MediaPipe PoseLandmarker loop (for Vite/React)
│   ├── scoring.ts            ← Score rules & ratings
│   ├── scoring.test.ts
│   └── pdf.ts                ← jsPDF score card helper
├── supabase/
│   └── schema.sql            ← Optional backend tables
└── models/
    ├── ferrari-optimized.glb
    └── CesiumMilkTruck.glb
```

The single-file `gesturekart.html` already embeds:

- Three.js 3D road, traffic, signals, pedestrians
- MediaPipe Pose (lite model from CDN)
- `GestureEngine` (same logic as `src/lib/gestureEngine.ts`)
- Keyboard fallback
- Score + result screen

---

## How the camera feature works

1. **Camera setup screen** requests `getUserMedia` and shows a mirrored preview.
2. **MediaPipe Pose Landmarker** (lite, GPU when available) runs every frame on the video.
3. Landmarks used:
   - 11 / 12 – shoulders  
   - 15 / 16 – wrists  
4. `GestureEngine`:
   - Calibrates neutral hand distance
   - Maps hand tilt → `steer` (-1…1)
   - Maps hand spread → `throttle` (0…1)
   - Hand above shoulder → `brake`
   - Lost tracking → ease off, then brake
5. Values are written into `window.GestureKart.input`, which the game loop already reads (with keyboard OR).

---

## Deploy (hackathon checklist)

1. **Live HTTPS URL** – e.g. drag the folder to [Vercel](https://vercel.com) or Netlify, or:
   ```bash
   npx vercel
   ```
2. **GitHub repo** – push this folder, keep the README.
3. **Demo video** – 2 min showing camera permission → calibrate → live gesture driving → score.
4. **LinkedIn post** – use the template from the brief.

---

## Optional: Vite + React + R3F upgrade

```bash
npm create vite@latest gesturekart-app -- --template react-ts
cd gesturekart-app
npm i @mediapipe/tasks-vision three @react-three/fiber jspdf @supabase/supabase-js
npm i -D vitest
```

Copy `src/lib/*` into the new project, put `pose_landmarker_lite.task` in `public/models/`, and wire `onCtl` from `poseLoop.ts` to the same input object your game reads. Keep keyboard fallback.

---

## Scoring (from `scoring.ts`)

- Start: 100  
- Red light: −15  
- Crossing violation: −12  
- Collision: −10  
- Speeding: −2  
- Proper stop: +3  
- Ratings: Exemplary (≥90) · Safe Driver (≥70) · Needs Practice (≥45) · Unsafe

---

## Team roles (reference)

| Role        | Focus                                      |
|-------------|--------------------------------------------|
| CV Lead     | MediaPipe pipeline, 60 FPS, zero lag       |
| Game Dev    | Three.js scene, road, signals, physics     |
| UI/UX       | HUD, audio, scorecard                      |
| DevOps      | Vercel, GitHub, demo video, Classroom post |

---

Built for the Web Design & Development hackathon — GestureKart.
