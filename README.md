# Neural Swarm

Interactive 3D boid simulation built with Three.js. The project visualizes a school of 1,024 autonomous agents that move using classic flocking behavior, react to mouse input, and can shift between multiple formation modes.

## Overview

Neural Swarm simulates collective movement using three core boid rules:

- **Separation**: agents avoid crowding nearby agents.
- **Alignment**: agents try to match the direction of nearby agents.
- **Cohesion**: agents move toward the average position of nearby agents.

The result is an organic swarm that can behave like a free-moving school, a structured sphere, a double helix, or a chaotic field.

## Features

- **1,024 active boids** rendered with Three.js `InstancedMesh`.
- **Real-time flocking controls** for separation, alignment, cohesion, and speed.
- **Multiple formation modes**:
  - Free School
  - Sphere Grid
  - Double Helix
  - Chaos Field
- **Mouse interaction**:
  - left mouse button attracts the swarm
  - right mouse button repels the swarm
  - scroll zooms the camera
- **Color modes**:
  - Neon Rainbow
  - Deep Ocean
  - Thermal Vision
  - Matrix Green
- **Post-processing bloom** for a neon visual style.
- **Orbit camera controls** for rotating, zooming, and inspecting the simulation.
- **FPS counter and status panel** for runtime feedback.
- **Responsive full-screen canvas**.

## Tech Stack

- HTML
- CSS
- JavaScript
- Tailwind CSS via CDN
- Three.js r128 via CDN
- Three.js `EffectComposer`
- Three.js `UnrealBloomPass`
- Three.js `OrbitControls`

## How It Works

Each boid stores:

- position
- velocity
- acceleration
- color offset

On every animation frame, each boid calculates steering forces from nearby boids:

```js
sep.multiplyScalar(CONFIG.separation);
ali.multiplyScalar(CONFIG.alignment);
coh.multiplyScalar(CONFIG.cohesion);
```

Those forces are added to acceleration, then applied to velocity and position. Velocity is clamped by `CONFIG.maxSpeed`, while steering force is limited by `CONFIG.maxForce`.

The simulation wraps boids around a cubic boundary, so agents leaving one side of the world reappear on the opposite side.

## Formation Modes

### Free School

The swarm behaves like a natural flock using only separation, alignment, and cohesion.

### Sphere Grid

Each boid receives a target point on a spherical distribution, creating a structured globe-like swarm.

### Double Helix

Boids are assigned alternating points along two rotating spiral strands.

### Chaos Field

Each boid follows animated sine and cosine targets, creating a turbulent moving formation.

## Controls

### Interface Controls

| Control | Description |
| --- | --- |
| Separation | Controls how strongly boids avoid each other. |
| Alignment | Controls how strongly boids match nearby movement direction. |
| Cohesion | Controls how strongly boids group together. |
| Speed Limit | Sets the maximum boid velocity. |
| Formation Logic | Switches between school, sphere, helix, and chaos modes. |
| Color Mode | Changes the color palette used by the boids. |
| Settings | Shows or hides the control panel. |

### Mouse Controls

| Input | Action |
| --- | --- |
| Left mouse button | Attract boids toward the cursor. |
| Right mouse button | Repel boids away from the cursor. |
| Scroll wheel | Zoom camera in or out. |
| Drag / orbit | Rotate the camera view with OrbitControls. |

## Running Locally

This is a static browser project. No package installation or build step is required.

1. Clone the repository.
2. Open the main HTML file in a modern browser.

Example:

```bash
git clone https://github.com/your-username/neural-swarm.git
cd neural-swarm
```

Open:

```text
index.html
```

Or run a local server:

```bash
python -m http.server 8000
```

Then visit:

```text
http://localhost:8000
```

## Suggested Project Structure

For the current single-file version:

```text
neural-swarm/
├── index.html
└── README.md
```

For a cleaner expanded version:

```text
neural-swarm/
├── index.html
├── src/
│   ├── boid.js
│   ├── simulation.js
│   ├── formations.js
│   └── ui.js
├── styles/
│   └── main.css
└── README.md
```

## Main Configuration

The main behavior is controlled through the `CONFIG` object:

```js
const CONFIG = {
  count: 1024,
  separation: 1.5,
  alignment: 1.0,
  cohesion: 1.0,
  maxSpeed: 4.0,
  maxForce: 0.1,
  perception: 50,
  colorMode: 'rainbow',
  formation: 'school'
};
```

Adjusting these values changes the swarm density, movement style, speed, and visual behavior.

## Browser Requirements

Use a modern browser with WebGL support:

- Google Chrome
- Microsoft Edge
- Firefox
- Safari

Performance depends on GPU capability, device pixel ratio, and screen resolution.

## Notes

- The project loads Tailwind CSS and Three.js from CDNs, so an internet connection is required unless the dependencies are downloaded locally.
- `InstancedMesh` is used to render many boids efficiently.
- The current neighbor search loops through all boids for each boid, which is simple but can become expensive as the boid count increases. A spatial partitioning structure such as a grid or octree would improve performance for larger simulations.
- The renderer currently uses `window.devicePixelRatio` directly. Limiting it with `Math.min(window.devicePixelRatio, 2)` can improve performance on high-DPI displays.
