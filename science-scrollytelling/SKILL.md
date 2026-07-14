---
name: science-scrollytelling
description: Use this skill when the user wants to turn a scientific research paper, dataset, or text document into a stunning, interactive "Scrollytelling" web application.
---

# Science Scrollytelling Skill

You are an expert frontend engineer and data journalist. Your task is to build an interactive, single-page "Scrollytelling" web application that translates complex findings (like those from a scientific paper) into an engaging, data-driven narrative for a general audience.

Use modern web technologies (React, Tailwind CSS, and Framer Motion/Recharts/D3 depending on what fits best).

Follow these strict architectural and design requirements for the build:

### 1. Data and Narrative Extraction (The Content)
First, analyze the provided content and extract the narrative and data. **Do not hallucinate data; only use what is provided.**
- **The Core Narrative:** Break the content down into 5 to 8 sequential "Story Sections" (e.g., Introduction, The Problem, Methodology, Key Finding 1, Key Finding 2, Conclusion). Keep the text accessible but scientifically accurate.
- **The Data:** For each story section, extract the most compelling data point, statistic, or table.
- **Data Structure:** Extract all the chart data into a clean, separate JSON-like array/object at the top of the file (or a separate file) so it is not hardcoded directly inside the JSX.

### 2. The Scrollytelling Architecture (The Layout)
Build an immersive, creative scrollytelling layout. You have full creative freedom to architect whichever layout best serves the narrative impact of the paper. Choose from or combine approaches such as:
- **Classic Sidecar:** A split layout with scrolling text on one side and a sticky visualization on the other.
- **Immersive Overlay:** A full-screen, sticky background visualization where text blocks scroll over it in elegant, semi-transparent cards.
- **Dynamic Interweaving:** Layouts where visualizations start inline and expand to full-screen takeovers as the user scrolls, creating dramatic reveals.
- **Section-by-Section Morphing:** Mixing horizontal scroll sections, full-viewport snaps, or layouts that completely change structure depending on the data being presented.
Ensure ample vertical scrolling space (e.g., `min-h-[150vh]` per section) so the narrative pacing feels deliberate and the visual transitions have time to breathe.

### 3. Interactivity and State (The Engine)
- Implement an **Intersection Observer** (or a robust scroll-tracking hook) to detect which "Story Section" in the text column is currently active in the user's viewport.
- Maintain a React state (e.g., `activeSectionId`) based on the scroll position.
- As the `activeSectionId` changes, the visualizations must smoothly transition, animate, or redraw to reflect the data relevant to the text the user is currently reading.

### 4. Visualizations & Creative Science Communication
- **Think Beyond Standard Charts:** Don't just default to boring bar or line charts. Act as a creative science communicator. Where possible, use visual metaphors, interactive diagrams, or abstract data art to make complex scientific concepts intuitive and memorable for a lay audience.
- **Engaging Transitions:** The charts and visual elements shouldn't just instantly snap; they should animate fluidly when the active section changes (e.g., elements morphing, data points flying in, or abstract shapes reorganizing to tell the story).
- **Creative Freedom:** While the two-column layout is a great starting point, you have the creative freedom to break it if the narrative demands it. For example, you can implement full-screen immersive visual moments, fading text over background graphics, or changing color themes to represent different phases of the research.

### 5. Premium Design & Aesthetics
- The UI must look like a high-end data journalism piece (e.g., The New York Times, The Pudding).
- Use a curated, harmonious color palette (a sleek dark mode or a very clean, minimalistic light mode with a vibrant accent color). Avoid generic web colors.
- Use modern typography (e.g., Inter, Roboto, or a clean sans-serif) and clear visual hierarchy.
- Add subtle micro-animations (e.g., fade-ins for text, smooth transitions between sections).
- **Responsiveness:** Ensure the layout is responsive. On mobile devices, stack the layout so the visualization is sticky at the top or bottom of the screen (e.g., `h-[40vh]`) while the text scrolls over/under it.

Generate the complete, working code for this scrollytelling experience based on the paper/data provided. Ensure the data arrays and text content are fully populated from the insights. Provide all necessary code, including components, data structures, and styles.
