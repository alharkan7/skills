---
name: svg-diagram
description: Generates highly aesthetic, modern, soft-styled SVG diagrams without relying on Mermaid, focusing on precise coordinate layouts, drop shadows, and bezier curves.
---

# Premium SVG Diagram Generation Skill

This skill provides instructions for generating highly polished, modern, and aesthetically pleasing SVG diagrams natively, bypassing the visual limitations of tools like Mermaid. This approach is ideal for executive presentations, UI wireframes, and enterprise architecture documents.

## 1. Core Aesthetic Principles
When a user requests a "beautiful", "modern", or "soft" diagram, adhere to these styling rules:
*   **Color Palette (Soft/Pastels):** Avoid harsh primary colors (e.g., pure red `#FF0000`). Use curated, soft background fills with slightly darker, saturated borders and text.
    *   *Blue:* Fill `#f5f9ff`, Stroke `#d4e4f7`, Text `#00477a`
    *   *Red/Pink:* Fill `#fff9f9`, Stroke `#f6dce0`, Text `#8f000b`
    *   *Yellow/Warm:* Fill `#fefcf5`, Stroke `#f3e4c4`, Text `#7a5900`
    *   *Green:* Fill `#f4fcf7`, Stroke `#b2e3c6`, Text `#0e5927`
*   **Curved Angles & Radii:** 
    *   Use `rx="12"` (or higher) on `<rect>` elements to create soft cards or pill shapes.
    *   Avoid sharp right-angle connectors. Use quadratic (`Q`) or cubic (`C`) Bézier curves for connecting lines (e.g., `path d="M 100 200 Q 150 200 150 250"`).
*   **Depth & Shadows:** Always define a subtle drop shadow filter in the `<defs>` section and apply it to interactive or elevated cards using `filter="url(#shadow)"`.
    ```xml
    <filter id="shadow" x="-5%" y="-5%" width="110%" height="110%">
      <feDropShadow dx="0" dy="4" stdDeviation="5" flood-color="#a0b0c0" flood-opacity="0.15" />
    </filter>
    ```

## 2. Layout & Coordinate Management
*   **Canvas Sizing:** Always start with a generous `viewBox` (e.g., `viewBox="0 0 1000 800"`). Ensure the canvas width and height match the viewBox.
*   **Breathing Room:** Never let text or boxes overlap with section titles. Always leave at least `30px` to `50px` of vertical padding below a header before starting a box.
*   **Mathematical Alignment:** Calculate centers explicitly. If a canvas is `1000px` wide and you need 3 columns, space the centers at approximately `166`, `500`, and `833`. Calculate the `x` attribute of a `<rect>` as `Center - (Width / 2)`.

## 3. Typography & Text Handling
*   **Global Fonts:** Apply `font-family="Inter, Helvetica Neue, Arial, sans-serif"` at the top-level `<g>` tag to ensure cross-platform modern typography.
*   **Text Wrapping:** SVG does not support native text wrapping inside `<rect>` elements. You must manually break text into multiple `<text>` lines.
    *   Use a `13px` or `14px` font size for body text.
    *   Calculate ~30-40 characters per line depending on box width.
    *   Increment the `y` coordinate by `20px` to `25px` for each new line.
*   **Visual Hierarchy:** Use `font-weight="bold"` and distinct font sizes (e.g., 20px for titles, 16px for subtitles, 12px for body) to guide the eye.

## 4. Advanced SVG Techniques (The "Wow" Factor)
*   **Background Textures/Graphs:** Instead of boring blank cards, add massive, abstract representations of data in the background of a card with very low opacity (`opacity="0.08"`). 
    *   *Example:* A giant swooping line graph or thick bar chart behind a KPI metric adds incredible texture and professional polish.
*   **Grouping & Layering:** Order matters in SVG.
    1. Draw background canvas.
    2. Draw connecting lines/arrows (so they hide behind cards).
    3. Draw the cards/boxes.
    4. Draw the text.
*   **Emojis as Icons:** If SVGs paths for icons are too complex to generate, use emojis inside `<text>` tags (e.g., ⚙️, 🛡️, 💰) centered perfectly over a small circular background pad.

## 6. Supporting Files

*   **Template:** When starting a new diagram, base your structure on `assets/template.svg`.
*   **Design Styles:** For inspiration on colors, shadows, bounding boxes, and routing aesthetics, refer to `references/styles.md`.
