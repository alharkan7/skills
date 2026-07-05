---
name: 2d-motion-graphics
description: Use when the user wants to create a new motion graphics animation HTML sequence for the Mograph Player application. Covers best practices for CSS animation timing, responsiveness, design aesthetics, specific motion patterns, and the Mograph export contract.
---

# Mograph Sequence Authoring

The Mograph Player (`/mograph/sequences/`) renders HTML sequences frame-by-frame for video export. Strict rules regarding layout, CSS animations, and design must be followed.

## 1. Core Architecture Contract

*   **CSS/WAAPI Only:** Rely exclusively on CSS `@keyframes` or native Web Animations API (`element.animate`).
*   **No External Libraries:** 🚫 No GSAP or JS animation libraries unless explicitly requested.
*   **No Infinite Loops:** 🚫 No `infinite` animations. They break duration calculations. Use fixed repeats or forwards fills.
*   **No JS Timing:** 🚫 No `requestAnimationFrame` or `setInterval`.
*   **No Dynamic Runtime Layout:** 🚫 Do not use `getBoundingClientRect()`. Use deterministic CSS relative units (`vw`, `vh`, `%`).
*   **No Heavy Assets:** 🚫 No videos or unpredictably loading assets.

## 2. Animation & Timing Fundamentals

*   **End State First:** Position elements in their final visible state statically. Animate *from* a hidden/offset state *to* the normal state.
*   **Fill Modes & Chaining:**
    *   **Entry Animations:** Use `animation-fill-mode: both`. The `0%` keyframe MUST fully define the absolute invisible state (e.g. `transform: scale(0)` or `clip-path`).
    *   **Exit Animations:** Use `animation-fill-mode: forwards`. **Never use `both` for exits**, as its `0%` state will leak backward and override earlier states in chained animations.
    *   **Property Conflicts:** If sequential animations target the same property (e.g. `transform`), use `forwards` on the later animation, or use independent CSS properties (`translate` vs `scale`).
*   **Orchestration & Speed:**
    *   Chain scenes with `animation-delay`. (Note: To override delay on multiple chained animations, supply comma-separated values: `animation-delay: 0s, 1.5s;`).
    *   Offset first animation by `0.1s - 0.3s` to avoid a jump cut at `t=0`.
    *   **Entrances:** Longer (0.4s-0.8s), use `ease-out` (starts fast, decelerates). e.g., `cubic-bezier(0.16, 1, 0.3, 1)`.
    *   **Exits:** Shorter (0.2s-0.3s), use `ease-in` (starts slow, accelerates). e.g., `cubic-bezier(0.76, 0, 0.24, 1)`.
    *   **Keyframe-Specific Easing:** For chained motions needing the same curve on each segment, set global timing to `linear` and inject `animation-timing-function: cubic-bezier(...)` directly into keyframes.
*   **Scene Transitions (The Stage Pattern):**
    *   Overlap transitions: Next scene's entry should begin *while* previous scene's exit is in motion.
    *   Wrap entire scenes in `.stage` containers. Animate the `.stage` itself on/off screen.
    *   **Final Scene:** Always animate the exit of the final sequence back to a blank canvas for seamless looping.

## 3. Layout, Composition & Scale

*   **Scale Everything Up:**
    *   Use `100vw`/`100vh` for root `.scene` containers. 🚫 No fixed pixel max-heights/widths.
    *   Use `clamp()` for fonts and padding. e.g., Headlines: `clamp(4rem, 10vw, 8rem)`.
*   **Bulletproof Centering (The Flexbox Squish Bug):**
    *   🚫 Flexbox centering + fixed large canvas = scaling clipping issues.
    *   ✅ **Fix:** Use absolute centering (`left: 50%; top: 50%; transform: translate(-50%, -50%)`). If dynamic scaling is needed, calculate with JS (`Math.min(window.innerWidth / 1920)`) and apply via `transform: scale()`.
*   **Marquee Translation:** When sliding containers off-screen, calculate the *entire trailing width* (e.g. `-350vw`), not just `-100vw`.
*   **Frame Density:** 8-10 elements per scene (Background texture, Midground message, Foreground accents). Avoid floating single items. Anchor to edges.

## 4. Design Aesthetics & Visual Patterns

*   **Theme & Color:**
    *   **Theme Lock:** Hardcode hex colors and enforce `color-scheme`. 🚫 No dynamic OS theme adjustments.
    *   **Palette:** Favor dark modes (`#0a0a0f`). High contrast.
    *   **Gradients:** 🚫 No full-screen linear gradients on dark backgrounds (video banding). Use radial glows.
*   **Motion Elements:**
    *   **Cinematic Reveals:** Use `clip-path: inset(...)` wipes or circular masks rather than generic opacity/scale bounces.
    *   **Virtual Camera:** Use a massive `.canvas` wrapper and pan/zoom a `.camera` wrapper using deterministic `translate`/`scale`. Keep hero elements centered.
    *   **Isometric 3D:** 🚫 Do NOT mix tilt (`rotateX/Z`) and scroll (`translateY`) on the same element. Nest an outer `.tilt-wrapper` and an inner `.scroll-camera`.
    *   **Typography:** Modern Google Fonts. Use Marker Sweeps, Burst Lines, or Cascades for emphasis. 🚫 No emojis (use inline SVGs).
*   **SVG Flowcharts:**
    *   **Orthogonal Connections:** Beziers should have strictly vertical/horizontal tangents. Set `fill="none"`.
    *   **Path Tracing:** 🚫 Don't use `pathLength="100"` (fails in headless). Use exact pixel length. 🚫 Don't use bouncy easing for drawing paths.
    *   **Routing (`offset-path`):** Use `offset-anchor: auto` to center shapes. `offset-rotate: auto` aligns axis to tangent (great for velocity squash/stretch via `scaleX/Y`).

## 5. Chroma Key (Green Screen) Safe Design

*   **No Opacity Fades:** 🚫 Fading elements blend into green screens, causing muddy ghosting. Use `transform: scale()` or slide them on/off. Use `visibility` instead of `opacity`.
*   **No Soft Shadows:** 🚫 Semi-transparent drop shadows cannot be cleanly keyed out. Use solid, hard borders or hard-offset drop shadows instead.
*   **Safe Colors:** 🚫 Avoid greens close to `#00FF00` or `#00B140`. Ensure high contrast at edges.

## 6. Workflow Checklist

1. Create the HTML sequence in `/mograph/sequences/<name>.html`.
2. Apply the design and animation rules.
3. Update `/mograph/sequences/manifest.json`: `{ "file": "<name>.html", "name": "..." }`
4. Inform the user they can test in the Mograph player and export as video.

## 7. Supporting Files

*   **Template:** When starting a new sequence, you can base your structure on `assets/template.html`.
*   **Design Explorations:** For inspiration on advanced visual patterns (Glassmorphism, HUDs, Isometric paths, etc.), refer to `references/styles.md`.
