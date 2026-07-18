---
name: 3d-motion-graphics
description: Use when the user wants to create a new 3D motion graphics animation using Three.js. Covers best practices for Three.js scene setup, animation loops, lighting, and composite video export rules.
---

# Three.js Motion Graphics Authoring

Three.js animations can be built for web playback and composite WebM video export. Strict architectural rules are recommended to ensure canvas pixels export correctly.

## 1. Core Architecture & Export Contract

*   **Export-Safe Canvas:** 
    *   ✅ **CRITICAL:** You MUST set `{ alpha: true, antialias: true, preserveDrawingBuffer: true }` on the `WebGLRenderer`. Without `preserveDrawingBuffer`, video exports will be blank/black.
*   **Transparent Backgrounds:** 
    *   ✅ Manage backgrounds via CSS composite logic when transparency is needed. 
    *   🚫 Avoid using `scene.background = new THREE.Color(...)` in your Three.js code if exporting with transparency.
*   **Vite Compatibility:**
    *   ✅ Import dependencies using bare module specifiers: `import * as THREE from 'three';` and `import { OrbitControls } from 'three/addons/controls/OrbitControls.js'`.
    *   🚫 Do NOT use CDNs (`https://unpkg.com...`), and do NOT inject `<script type="importmap">`.

## 2. Animation, Timing & Controls

*   **The Render Loop:**
    *   ✅ All animation logic (rotations, tweening) should happen inside the `requestAnimationFrame(animate)` loop. 
    *   🚫 Avoid `setInterval` or `setTimeout` as they can desync from external playback controls.
*   **Duration Communication:** 
    *   ✅ External recording tools often use the DOM Web Animations API (`document.getAnimations()`) to calculate the end time. Consider applying dummy Web Animations to an invisible DOM element (e.g., `<div id="timing-dummy"></div>`) if your scene uses pure Three.js math looping, so external recorders know when to stop.
*   **Native Math Tweening:** 
    *   ✅ Prefer native math-based easing (e.g., `(time % loopDuration)`) inside the render loop over external libraries like GSAP for perfect video export loops.
*   **Cinematic Camera:** 
    *   ✅ For sweeping camera moves during export, use `OrbitControls` with `controls.autoRotate = true` and configure `controls.autoRotateSpeed`.

## 3. Materials, Lighting & Styling

*   **Premium Lighting:**
    *   ✅ Use `MeshStandardMaterial` or `MeshPhysicalMaterial`. Enable shadows (`renderer.shadowMap.enabled = true`, use `THREE.PCFSoftShadowMap`).
    *   ✅ Use an `AmbientLight` for soft fill and `DirectionalLight` for sharp, dramatic shadows.
*   **CAD / Blueprint Overlays:**
    *   ✅ For glowing wireframes, pair `THREE.EdgesGeometry` with `THREE.LineSegments`. This looks far superior to basic `material.wireframe = true`.
*   **Legibility & Contrast:**
    *   ✅ For `CanvasTexture` text, use high-contrast text colors and consider adding a subtle halo (`shadowColor = 'rgba(255,255,255,0.9)'`) to guarantee legibility against variable backgrounds.
    *   ✅ **Dual Materials for TextGeometry:** Reflective front faces can be unreadable. Use an array `[frontMat, sideMat]`: flat/emissive material for the front, highly reflective material for the extruded sides.
*   **Flat Shading (Low-Poly):**
    *   ✅ To get crisp, faceted low-poly lighting (e.g., on `PlaneGeometry`), you MUST convert the geometry using `geometry.toNonIndexed()` before displacing vertices, then set `flatShading: true` on the material.

## 4. Advanced Geometry & Shaders

*   **Model Orientation (OrbitControls):** 
    *   ✅ `OrbitControls` locks the Y-axis. To pan horizontally along a long object, do not fight the camera. Group the object and rotate the group (`group.rotation.z = -Math.PI / 2`), letting the default Y-axis auto-rotation circle the object perfectly.
*   **Local Fonts:**
    *   ✅ Always host `TextGeometry` JSON fonts locally in `/public/fonts/` (download via `curl`). 🚫 Do NOT rely on CDNs (CORS/Vite pathing issues).
*   **Kinetic Shaders (`onBeforeCompile`):**
    *   ✅ When injecting GLSL vertex modifications (like sine waves), always program a "readable state" (e.g., dial uniform strength to 0 for a few seconds) so users can read the text. Never stop motion entirely; keep a subtle 10% base wave active.
*   **GPU Particle Systems:**
    *   ✅ **Morphing:** Use `MeshSurfaceSampler` to extract vertices, load into custom `BufferAttribute` arrays, and `mix()` within a `ShaderMaterial` vertex shader.
    *   ✅ **Sizing:** Multiply `gl_PointSize` by a massive base multiplier (e.g., `300.0 * pixelRatio`) to prevent perspective attenuation from collapsing particles into 1px dust.
    *   ✅ **Blending & Glows:** 🚫 Do NOT use `THREE.AdditiveBlending` if exporting on white (it renders invisible). Use `THREE.NormalBlending`. Instead of PNG textures, use a math-based alpha fade in the fragment shader for perfect glowing orbs.

## 5. Workflow Checklist

1. Create a new directory for your animation.
2. Add an `index.html` containing the Three.js scene (use ES modules).
3. Ensure `preserveDrawingBuffer: true` and `alpha: true` are set on the `WebGLRenderer` if video export is intended.
4. Test the sequence in a browser to ensure smooth playback and correct timing.

## 6. Design Explorations

*   **Inspiration:** Draw inspiration from advanced visual patterns like Particles, Data Topography, and Isometric Dioramas.
