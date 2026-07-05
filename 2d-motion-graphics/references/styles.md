# Motion Graphics Styles

A reference for implementing advanced aesthetic patterns natively in HTML/CSS.

### 1. Glowing Flowcharts & Maps (Motion Paths)
- **Vibe:** System architecture, global logistics.
- **Technique:** Use SVG `stroke-dashoffset` for glowing lines and CSS `offset-path` (with `offset-rotate: auto`) for elements traveling along complex vector curves. Apply `rotateX` for 2.5D map tilts.

### 2. Glassmorphism & Light Refraction
- **Vibe:** Ethereal, premium, Apple/fintech.
- **Technique:** `backdrop-filter: blur(20px) saturate(150%)` on floating foreground cards. Animate colorful glowing orbs in the background behind them.

### 3. The "Virtual Camera" Pan
- **Vibe:** Vox journalistic explainer, massive scale.
- **Technique:** Wrap everything in a `.world` container. Apply perfectly timed `scale()` and `translate()` transforms with very slow `cubic-bezier` easing to simulate camera mass.

### 4. Code-to-UI Compilation (Terminal Cascade)
- **Vibe:** Hacker, developer tool.
- **Technique:** Use `steps()` or `step-end` for typing text effects on monospace blocks. Detach code lines and visually morph them (`clip-path`, `border-radius`) into rendered UI components.

### 5. Kinetic Typography
- **Vibe:** High-energy, marketing bumpers.
- **Technique:** Split text into `<span>` tags. Use perfectly staggered `animation-delay` offsets combined with `clip-path` masks to slide words out of invisible floors.

### 6. Skeuomorphic Mechanics (Odometer)
- **Vibe:** Physical, tactile milestones.
- **Technique:** Vertical strip of numbers in an `overflow: hidden` container. Spin with an aggressive, springy `transform: translateY()` easing.

### 7. Cyberpunk HUD & Retro Arcade
- **Vibe:** Sci-fi scanning lines or chunky 8-bit.
- **Technique:** `mix-blend-mode: screen` and layered SVGs with different rotation speeds. For retro: use blocky `steps()` animations, scanlines, and CRT curvature.

### 8. Brutalist Scrapbook & Memphis Pop-Art
- **Vibe:** Gritty physical collage or loud 80s MTV.
- **Technique:** Sudden `scale(1)` pops (no smooth fades), slight messy angles (`transform: rotate(-3deg)`), and hard offset drop shadows (`4px 4px 0 #000`).

### 9. Editorial Data & Vintage Collage
- **Vibe:** NYT infographics, Da Vinci sketchbooks.
- **Technique:** For editorial: `mix-blend-mode: multiply` on yellow divs for highlighter effects. For vintage: SVG noise (`feTurbulence`), antique line-art drawing itself via `stroke-dasharray`, and abrupt "cutout" slide-ins.

### 10. Morphing UI & Bento Box
- **Vibe:** Seamless transitions, asymmetric grids.
- **Technique:** Orchestrate `width`, `height`, and `border-radius` transitions on a container. Simultaneously use `clip-path: inset(...)` and precise `animation-delay` to reveal inner content seamlessly.
