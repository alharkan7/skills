---
name: svg-diagram
description: Generates highly aesthetic, modern, soft-styled SVG diagrams without relying on Mermaid, focusing on precise coordinate layouts, drop shadows, and bezier curves.
---

# Premium SVG Diagram Generation Skill

This skill provides instructions for generating highly polished, modern, and aesthetically pleasing SVG diagrams natively, bypassing the visual limitations of tools like Mermaid. This approach is ideal for executive presentations, UI wireframes, and enterprise architecture documents.

## 1. Core Aesthetic Principles
When a user requests a "beautiful", "modern", or "soft" diagram, adhere to these styling rules:
*   **Color Palette (Soft/Pastels):** Avoid pure harsh primary colors (e.g., pure red `#FF0000`). Use curated, soft background fills with slightly darker, saturated borders and text.
    *   *Blue:* Fill `#f5f9ff` / `#d1e9ff`, Stroke `#d4e4f7`, Text `#00477a`
    *   *Red/Pink:* Fill `#fff9f9` / `#ffd4d6`, Stroke `#f6dce0`, Text `#8f000b`
    *   *Yellow/Warm:* Fill `#fefcf5` / `#fbeea3`, Stroke `#f3e4c4`, Text `#7a5900`
    *   *Green:* Fill `#f4fcf7` / `#cbf1d8`, Stroke `#b2e3c6` / `#d7f0e1`, Text `#0e5927`
    *   *Purple/Neutral:* Fill `#f8f5ff` / `#f1f5f9`, Stroke `#e2e0f0` / `#e2e8f0`, Text `#3b2f6b` / `#0f172a`
*   **Curved Angles & Radii:** 
    *   Use `rx="12"` (or higher) on `<rect>` elements to create soft cards or pill shapes.
    *   Avoid sharp right-angle connectors. Use quadratic (`Q`) or cubic (`C`) Bézier curves for connecting lines (e.g., `path d="M 100 200 Q 150 200 150 250"`).
*   **Depth & Shadows:** Always define a subtle drop shadow filter in the `<defs>` section and apply it to interactive or elevated cards using `filter="url(#shadow)"`.
    ```xml
    <filter id="shadow" x="-5%" y="-5%" width="110%" height="110%">
      <feDropShadow dx="0" dy="4" stdDeviation="5" flood-color="#a0b0c0" flood-opacity="0.15" />
    </filter>
    ```

## 2. Layout & Adaptive Detail Management
*   **Adaptive Canvas Sizing:** Pick a `viewBox` that fits the content density. Set `width="100%"` `height="100%"` on the root svg.
    *   *Simple:* (2-6 nodes) ~`900x600` to `1100x720`.
    *   *Standard:* (normal process) ~`1100x780` to `1300x900`.
    *   *Rich:* (dense architecture) ~`1280x900` to `1600x1100`. Do not force a tiny canvas when content needs room.
*   **Breathing Room:** Never let text or boxes overlap with section titles. Always leave at least `30px` to `50px` of vertical padding below a header before starting a box.
*   **Mathematical Alignment:** Calculate centers explicitly. Calculate the `x` attribute of a `<rect>` as `Center - (Width / 2)`. Ensure that every single line exactly meets the border of the box it connects to (no overlapping).

## 3. Typography & Text Handling
*   **Global Fonts:** Apply `font-family="Inter, Helvetica Neue, Arial, sans-serif"` at the top-level `<g>` tag.
*   **Text Wrapping:** SVG does not support native text wrapping inside `<rect>` elements. You must manually break text into multiple `<text>` lines.
    *   Use `13-14px` for body text, `18-22px` for titles, `11-12px` for captions.
    *   Increment the `y` coordinate by `18px` to `24px` for each new line.
*   **Text Legibility over Connectors:** Any text label placed over lines/connectors MUST have a white background so it is readable. Achieve this by either placing a small `<rect fill="#ffffff" rx="4">` exactly behind the text, or by applying a white outline halo directly to the `<text>` element using:
    `paint-order="stroke fill" stroke="#ffffff" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"`

## 4. Advanced SVG Techniques & Safety
*   **Strict Layering (Z-Index):** SVG uses the painter's algorithm. Maintain this exact order:
    1. Backgrounds (swimlanes, section wrappers)
    2. Lines/connectors/arrows (so they cross over backgrounds)
    3. Foreground shapes/cards/nodes (so they hide line endpoints cleanly)
    4. Text/labels (absolute top, never obscured)
*   **Background Textures:** Add abstract representations of data in the background of a card with very low opacity (`opacity="0.08"`) for texture.
*   **No Emojis:** NEVER use emojis anywhere in the diagram (no emojis in text, titles, or labels). Use pure SVG paths/shapes if an icon is needed.

## 5. Supporting Files

*   **Template:** When starting a new diagram, base your structure on `assets/template.svg`.
*   **Design Styles:** For inspiration on colors, shadows, bounding boxes, and routing aesthetics, refer to `references/styles.md`.
