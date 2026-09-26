# Creative Motion Studio

[![Next.js](https://img.shields.io/badge/Next.js-14.2-black?logo=next.js)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue?logo=typescript)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-38B2AC?logo=tailwind-css)](https://tailwindcss.com/)
[![Vitest](https://img.shields.io/badge/Vitest-Tested-green?logo=vitest)](https://vitest.dev/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> A high-performance, web-based creative motion and visual composition studio engineered for motion graphics, social media visuals, typography animations, logo sequences, and video production planning.

**Creator:** Fahad Iqbal  
**Identity:** Full-Stack Developer • Cybersecurity • AI Engineering • Creative Technology  
**Repository:** [https://github.com/fahadiqbal/creative-motion-studio](https://github.com/fahadiqbal/creative-motion-studio)

---

## 1. Executive Summary

**Creative Motion Studio** is a browser-based creative software suite bridging the gap between static graphic design tools and heavyweight digital compositing applications. Designed specifically for creative professionals, video planners, and content creators, the application allows users to compose visual scenes, layer typography, animate vector shapes, import imagery, scrub a deterministic keyframe timeline, and export production-ready PNG snapshots and WebM video sequences.

Every button, slider, and timeline track in this repository connects to functional code—no fake buttons, placeholder dashboards, or simulated mockups.

---

## 2. Core Features

### A. Creative Canvas & Vector Engine
- **Scalable Viewport:** Pan, zoom (20% to 250%), fit-to-screen, and customizable grid guides.
- **Dynamic Elements:**
  - **Typography:** Multi-line text with custom font families (*Space Grotesk*, *Inter*, *Playfair Display*, *JetBrains Mono*, *Syne*), weight, letter spacing, line height, text transforms, and double-click inline text editing.
  - **Vector Shapes:** Rectangles, rounded cards with corner radius, circles, and divider lines with custom fill, stroke, and opacity.
  - **Image Ingestion:** Safe client-side image uploading (PNG, JPG, SVG, WebP) with auto-rescaling and aspect ratio preservation.
- **Interactive Transform Controls:** Direct manipulation on canvas featuring an 8-point bounding box (corners and edges) and a top rotational handle with 45° shift-snapping.

### B. Layer Hierarchy & Management
- **Visual Layer Stack:** Reorder layers forward/backward (`zIndex` adjustment).
- **Controls:** Lock protection to prevent accidental edits, visibility toggle, layer duplication (`Ctrl+D`), deletion, and inline double-click layer renaming.

### C. Deterministic Motion & Timeline System
- **Precision Timecode:** Real-time scrubbing ruler with sub-second frame ticks and interactive playhead.
- **Track Timing Bars:** Visual layer bars with draggable start times and right-edge trimming handles.
- **Motion Presets with Mathematical Easing:**
  - **Entrance:** Fade In, Slide Up, Slide Down, Slide Left, Slide Right, Scale In, Pop In (`ease-out-back` overshoot).
  - **Exit:** Fade Out, Slide Up, Slide Down, Slide Left, Slide Right, Scale Out.
  - **Attention / Ambient:** Subtle sinusoidal pulse, floating oscillation, small rotational shake.
- **Real-Time Playback:** High-precision `requestAnimationFrame` loop maintaining continuous synchronization between the timeline playhead and canvas interpolation.

### D. Built-in Editorial Templates
One-click generation of six distinct production compositions:
1. **Cinematic Intro:** Letterboxed widescreen composition with delayed typography entrance.
2. **Minimal Title:** High-contrast serif editorial layout with subtle scale breathing.
3. **Social Announcement:** Square 1:1 release graphic with pill badges and call-to-action blocks.
4. **Music Release:** Synth-wave vinyl record visual with pulsing concentric rings.
5. **YouTube Intro:** High-energy widescreen banner with bold typographic branding.
6. **Quote Visual:** Elegant quotation layout with balanced hierarchy and accent dividers.

### E. AI Creative Director Layer
- **Pluggable Architecture:** Replaceable provider layer (`IAIProvider`) that works seamlessly with external LLM endpoints (e.g. OpenAI) or falls back to an internal **Creative Heuristic Engine**.
- **Contextual Direction:** Analyzes prompts (e.g., *"Create a cinematic intro for my song Words Left Unsaid"*) and returns structured aesthetic concepts, curated color palettes, typographic recommendations, and motion timing strategies.
- **One-Click Application:** Instantly re-themes canvas background, headlines, and animation parameters.

### F. Genuine Multi-Format Export
- **PNG / JPEG Snapshot:** Rasterizes canvas at the current playhead timestamp with 1x or 2x high-resolution retina scaling.
- **WebM Video Export:** Sequential frame-by-frame rendering at 30 FPS using HTML5 Canvas and `MediaRecorder` (`video/webm;codecs=vp9`), with a live visual progress bar and frame counter.
- **Project JSON:** Complete serialization and deserialization of the project schema with validation.

---

## 3. Architecture & Tech Stack

```text
┌────────────────────────────────────────────────────────────────────────┐
│                        User Interface Layer                            │
│  [TopBar]   [ToolBar]   [LayerPanel]   [Canvas]   [Properties]   [Timeline]
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│                     Studio State & History Core                        │
│   • Active Project State (React hooks)                                 │
│   • HistoryManager (Undo / Redo stack with immutability guarantees)    │
│   • RAF Playback Engine (High-precision continuous timecode loop)     │
└─────────────┬─────────────────────┬────────────────────┬───────────────┘
              │                     │                    │
              ▼                     ▼                    ▼
   ┌────────────────────┐ ┌───────────────────┐ ┌────────────────────────┐
   │  Animation Engine  │ │  Security Layer   │ │   AI Creative Core     │
   │  • Easing Curves   │ │  • Schema check   │ │  • Replaceable Provider│
   │  • State Evaluator │ │  • SVG sanitizer  │ │  • Prompt Builder      │
   │  • Phase Calculator│ │  • File validator │ │  • Heuristic Engine    │
   └──────────┬─────────┘ └───────────────────┘ └────────────────────────┘
              │
              ▼
   ┌──────────────────────────────────────────┐
   │          Rendering & Export Engine       │
   │   • DOM / CSS3 Hardware Acceleration     │
   │   • Canvas 2D Raster Engine              │
   │   • MediaRecorder WebM Video Pipeline    │
   │   • Portable JSON Schema Exporter        │
   └──────────────────────────────────────────┘
```

- **Frontend Framework:** Next.js 14 (App Router)
- **Language:** TypeScript 5.0 (Strict mode enabled)
- **Styling:** Tailwind CSS with custom editorial dark palette
- **Icons:** Lucide React
- **Testing:** Vitest with 21 unit and integration tests
- **Storage:** LocalStorage persistence with JSON schema migration fallback

---

## 4. Getting Started

### Prerequisites
- Node.js >= 18.17 (Node 20+ recommended)
- npm >= 9

### Installation
```bash
# 1. Clone the repository
git clone https://github.com/fahadiqbal/creative-motion-studio.git
cd creative-motion-studio

# 2. Install dependencies
npm install

# 3. Configure environment variables (optional)
cp .env.example .env.local

# 4. Start local development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 5. Keyboard Shortcuts

| Shortcut | Description |
| -------- | ----------- |
| `Space` | Play / Pause timeline playback |
| `Delete` / `Backspace` | Delete active selected layer |
| `Ctrl + Z` / `Cmd + Z` | Undo last editing action |
| `Ctrl + Shift + Z` / `Cmd + Shift + Z` / `Ctrl + Y` | Redo previously undone action |
| `Ctrl + S` / `Cmd + S` | Save current project to local storage |
| `Ctrl + D` / `Cmd + D` | Duplicate selected element |
| `Arrow Keys` | Nudge position by 1px |
| `Shift + Arrow Keys` | Nudge position by 10px |
| `Escape` | Deselect active element |

---

## 6. Testing & Quality Assurance

The repository includes comprehensive unit and integration tests across mathematical interpolation, history management, security validation, template integrity, and AI direction services:

```bash
# Run test suite
npm run test

# Run build verification
npm run build
```

**Test Coverage Summary:**
- `tests/animation.test.ts`: Easing curves, boundary checks, entrance/exit/attention interpolation.
- `tests/history.test.ts`: Stack depth capping, undo/redo tree bifurcation, state cloning.
- `tests/validation.test.ts`: Schema bounds, canvas dimensions, coordinate safety, string sanitization.
- `tests/templates.test.ts`: Validation of all 6 starter compositions.
- `tests/ai.test.ts`: Creative heuristic fallback and schema normalization.

---

## 7. Portfolio Presentation — Engineering Deep Dive

### What I Built
I designed and engineered **Creative Motion Studio**, a full-stack, browser-based motion composition tool built with Next.js, TypeScript, and HTML5 Canvas. The software allows users to layout typography and vector elements, sequence entrance/attention/exit animations on an interactive timeline, and render both static high-DPI assets and dynamic `.webm` video clips completely client-side.

### Why I Built It
Standard web applications frequently default to generic administrative tables and analytics dashboards. I built Creative Motion Studio to demonstrate that full-stack developers can build complex, state-heavy creative software with strict performance, spatial coordinate math, and elegant UI/UX design. Creative software demands a different level of engineering rigor: sub-frame animation timing, low-latency drag-and-drop mechanics, deterministic rendering, and memory management.

### Technical Challenges
1. **Interactive Coordinate Transformations Under Scale:** When users drag or resize an element on a canvas zoomed to 40% or 120%, naive mouse offsets drift wildly. I engineered a coordinate mapping pipeline where all client offsets are normalized through the active viewport zoom factor:
   $$\Delta X_{\text{canvas}} = \frac{X_{\text{client}} - X_{\text{start}}}{\text{zoom}}$$
2. **Unified Rendering Parity:** Ensuring that what the user previews interactively via CSS3 transforms in the DOM matches pixel-for-pixel with the offscreen Canvas 2D raster engine used during PNG and WebM export. This was solved by creating a single-source evaluation function (`computeElementState`) shared between both environments.
3. **In-Browser Video Encoding:** Implementing client-side video export without massive server-side FFmpeg infrastructure. By driving an offscreen canvas across discrete time steps and piping its `captureStream()` through the browser's `MediaRecorder` API, users can generate real `.webm` video files directly on their device.

### Engineering Decisions
- **Declarative Animation Model:** Instead of imperatively animating elements with DOM mutations, element states are treated as pure functions of timestamp $t$:
  $$\text{State}(t) = \operatorname{evaluate}(\text{Element}, t)$$
  This guarantees that scrubbing forward, backward, or jumping to arbitrary timecodes is instantaneous and deterministic.
- **Fail-Safe AI Architecture:** External AI APIs frequently encounter rate limits, network latency, or invalid API keys. I structured the AI system with a pluggable provider pattern that falls back smoothly to an intelligent internal heuristic engine. Users are never blocked by missing API credentials.
- **Defensive Input Handling:** Creative tools frequently handle user-supplied SVGs and text. I implemented multi-stage sanitization to strip malicious script tags, inline event handlers, and out-of-bounds dimensional allocations.

### What I Learned
- Balancing React state updates with high-frequency mouse and timeline events requires careful batching. Continuous operations like dragging or playhead updates must avoid pushing to the undo/redo stack until the user interaction concludes.
- Canvas 2D text layout requires precise font metrics measurement and custom word-wrapping logic when rendering offscreen assets.

### Future Improvements
- Multi-element group selection and bulk alignment tools (align center, distribute horizontal).
- Keyframe curve graph editor for custom cubic Bézier control points.
- WebCodecs / MP4 container export via browser-native hardware acceleration.

---

## 8. Author

**Fahad Iqbal**  
*Full-Stack Developer • Cybersecurity • AI Engineering • Creative Technology*  
- Portfolio: [https://github.com/fahadiqbal](https://github.com/fahadiqbal)
- Specialization: Mission-critical web applications, creative technology suites, defensive cybersecurity architecture, and generative AI systems.

---

## 9. License

This project is open-source software licensed under the [MIT License](LICENSE).
