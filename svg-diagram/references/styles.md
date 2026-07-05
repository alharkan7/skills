# SVG Diagram Styles

A reference for creating premium, highly aesthetic SVG diagrams. These guidelines are designed to inspire—feel free to creatively combine or adapt them to suit the specific diagram you are building!

## 1. Soft Pastel Color Systems
Avoid harsh primary colors. Use deeply curated pastel palettes where the background, stroke, and text share a harmonious hue.
*   **Blue Theme:** Background `#d1e9ff`, Stroke `#d4e4f7`, Text/Icon `#00477a`
*   **Yellow Theme:** Background `#fbeea3`, Stroke `#f3e4c4`, Text/Icon `#7a5900`
*   **Red/Pink Theme:** Background `#ffd4d6`, Stroke `#f6dce0`, Text/Icon `#8f000b`
*   **Green Theme:** Background `#cbf1d8`, Stroke `#d7f0e1`, Text/Icon `#0e5927`

## 2. Layer & Bounding Boxes
When grouping concepts (like an "Architecture Layer" or "Phase"), use large bounding rectangles sent to the back.
*   Use very light backgrounds (e.g., `#fefcf5`, `#f5f9ff`, `#fff9f9`).
*   Apply dashed strokes (`stroke-dasharray="8,5"`) to denote logical grouping without adding visual weight.
*   Position a bold, dark label in the top-left corner of the box.

## 3. Shadows & Depth
To make cards pop off the canvas, always use a custom Drop Shadow filter.
*   *Critical:* Always define `x="-5%" y="-5%" width="110%" height="110%"` on the `<filter>` tag so the shadow doesn't clip at the element boundaries.
*   Use a subtle, cool-toned gray for the shadow: `flood-color="#a0b0c0" flood-opacity="0.15"`.

## 4. Connectors & Arrows
*   Use clean, curved bezier paths (`Q` or `C`) for organic data flows.
*   Define a `<marker id="arrow">` in the `<defs>` section and apply it using `marker-end="url(#arrow)"`.
*   Match the arrow color and connector stroke color (usually a soft steel blue `#8ca4bc` or green `#88c99f`).

## 5. Timelines & Layouts
*   **Timelines:** Draw a thick central axis line. Use dashed drop-lines to connect time nodes (circles) to detail cards below them.
*   **Pills:** For high-level strategic points, use heavily rounded rectangles (`rx="45"` on a height of 90).
*   **Vertical Text:** Rotate text for side-labels on lanes using `transform="rotate(-90, x, y)"`. Add a slightly opaque white `<rect>` behind it so it remains legible over grid lines.
