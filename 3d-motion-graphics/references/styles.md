# 3D Motion Graphics Styles

A reference for 3D aesthetics and technical implementations using Three.js.

### 1. Isometric Dioramas & Exploded Views
- **Vibe:** Product explainers, scene setting.
- **Technique:** `OrthographicCamera` with soft shadows for dioramas. For exploded views, use object grouping and `GSAP` tweening for assembly/disassembly animations.

### 2. Abstract Particle Morphing & Data Topography
- **Vibe:** Data journalism, abstract concepts (AI, networks).
- **Technique:** Use `InstancedMesh` or `Points` with GPU compute shaders to morph shapes. For topography, use `SVGLoader` extrusion or map GeoJSON to meshes with height-based gradients.

### 3. Kinetic Typography
- **Vibe:** High-impact titles, voiceover highlights.
- **Technique:** `TextGeometry` coupled with custom vertex shaders for wave/distortion effects and environment mapping for premium reflections.

### 4. Glassmorphism & Refractive Objects
- **Vibe:** Premium, modern UI/luxury aesthetics.
- **Technique:** `MeshPhysicalMaterial` (leveraging `transmission`, `thickness`, `roughness`) combined with HDRI Environment Maps.

### 5. Schematic Blueprints & Cel-Shading
- **Vibe:** Software architecture, anime/hand-drawn styling.
- **Technique:** For blueprints: `EdgesGeometry` + `LineBasicMaterial` with Bloom post-processing. For cel-shading: `MeshToonMaterial` + `OutlineEffect` and custom gradient maps.

### 6. Low-Poly Landscapes & Volumetrics
- **Vibe:** Moody atmospheres, sweeping B-roll.
- **Technique:** `PlaneGeometry` with displaced vertices and `CatmullRomCurve3` for camera tracking. Add `THREE.FogExp2` and GodRays post-processing for volumetric light.

### 7. Raymarching & Soft Body Physics
- **Vibe:** Mathematical blobs, jelly/cloth dynamics.
- **Technique:** For physics: Ammo.js or Cannon-es. For raymarching: skip traditional geometry entirely and use custom GLSL fragment shaders (SDFs).
