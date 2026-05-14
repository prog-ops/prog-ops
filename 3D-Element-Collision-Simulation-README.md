# ✔️ 3D Element Collision Simulation (Wind -> Water -> Fire -> Metal -> Earth -> Wind)

https://github.com/user-attachments/assets/abcd411e-fe26-4f99-9f2c-53b7d6799bf0

_Note: FPS and resolution is reduced to limit recording file size_

A highly interactive, physics-based 3D simulation running in the browser, built from scratch using Vanilla JavaScript and **Three.js**. It visually simulates an "elemental battle" where different natural elements collide, bounce, and conquer each other until only one reigns supreme.

## 🚀 Features

- **3D Physics Simulation:** Implements pure elastic collision mathematics mapped seamlessly into a 3D WebGL environment.
- **Elemental Hierarchy:** A classic battle mechanic:
  - Wind beats Water
  - Water beats Fire
  - Fire beats Metal
  - Metal beats Rock
  - Rock beats Wind
  - ... The cycle continues.
- **Dynamic Speed Scaling:** Elements accelerate as they win collisions, increasing the simulation's chaos and intensity.
- **Auto-Detect Endgames:** The system automatically detects single winners, draws, or "stuck" states where remaining elements cannot defeat each other.

## 🛠️ Tech Stack

- **Frontend:** HTML5, CSS3, Vanilla JavaScript
- **3D Rendering Engine:** [Three.js](https://threejs.org/) (WebGL)
- **Bundler / Tools:** Webpack, Bun

## 🎨 Three.js Implementation Highlights

This project heavily emphasizes the use of **Three.js** to elevate a simple 2D concept into a polished 3D experience. Key implementations include:

- **Orthographic Camera:** Instead of a standard perspective camera, it uses an `OrthographicCamera` to create a perfect "top-down" strategic view. This ensures accurate visual scaling and boundary mapping regardless of the browser window size.
- **PBR Materials (Physically Based Rendering):** Implements `MeshStandardMaterial` to give distinct physical properties to different elements. For example, the "Metal" element is highly reflective (`metalness: 1.0`), while "Earth/Rock" is rough and matte.
- **Environment Mapping:** Uses `CubeTextureLoader` to provide realistic environmental reflections on metallic objects without needing heavy, external HDRI files.
- **Dynamic Lighting & Shadows:** Utilizes `DirectionalLight` with `PCFSoftShadowMap` to cast soft, dynamic shadows across the 3D plane. This provides vital depth perception, making the spheres look like they are floating just above the surface.
- **Explicit Memory Management:** In a simulation where hundreds of objects are created and destroyed rapidly, garbage collection is critical. The code explicitly calls `dispose()` on geometries and materials when elements are destroyed to free up GPU memory and prevent memory leaks.

## 🧠 The Engineering Philosophy (A Senior's Perspective)

Behind the visual appeal lies a highly structured architectural approach:

1. **Separation of Concerns (MVC Pattern):** The core physics logic (calculating vectors, velocities, overlaps, and boundaries) is entirely decoupled from the visual rendering. The internal state (`_simulationX`, `_simulationZ`) calculates the pure math, and Three.js simply reads this state to update the `mesh.position`.
2. **Algorithmic Vector Math:** The collision system relies on foundational linear algebra (dot products, vector normalization, and tangential vector calculations) rather than relying on a heavy third-party physics engine like Cannon.js or Ammo.js.
3. **Scalable Architecture:** The project's core, `simulation3d.js`, demonstrates a highly scalable architecture. It seamlessly translates underlying 2D logical physics directly into a full WebGL 3D implementation without breaking or complicating the fundamental business logic.
4. **Emergent Behavior:** It models how simple, deterministic micro-rules (Element A beats Element B) combined with entropy (random spawn points, bouncing angles) create a highly unpredictable, organic macro-system.

## 💻 How to Run Locally

1. Clone this repository to your local machine.
2. Open the directory and install dependencies (if using the Webpack pipeline):
   ```bash
   bun install
   ```
3. Run the development server or open the project using a local live server:
   ```bash
   bun run dev
   ```
   _Note: Because Three.js loads external textures (for environment mapping), simply opening `index.html` via `file://` might cause CORS errors. Running it through a local server is highly recommended._
