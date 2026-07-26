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

## License

```text
Gilberto Jemal
```
