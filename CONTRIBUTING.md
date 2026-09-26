# Contributing to Creative Motion Studio

Thank you for your interest in contributing to **Creative Motion Studio**, developed by **Fahad Iqbal**.

We welcome contributions from engineers, UI/UX designers, and creative technologists who value clean code, maintainable architecture, and robust creative software.

---

## 1. Development Principles

1. **Honest Engineering:** Avoid superficial mockups, fake UI buttons, or pretend features. If a feature is present, it must function end-to-end.
2. **Type Safety:** Maintain strict TypeScript typing. Do not introduce unchecked `any` types.
3. **Performance First:** Motion editing requires high rendering responsiveness. Minimize unnecessary React re-renders, avoid canvas memory leaks, and profile timeline scrubbing.
4. **Clean Design Aesthetic:** Adhere to the established editorial dark theme (`#090A0F`, crisp `#272A34` borders, high-contrast typography, zero flashy neon clutter).

---

## 2. Getting Started

### Prerequisites
- Node.js >= 18.17 (Node 20+ recommended)
- npm >= 9

### Setup Steps
```bash
# 1. Clone repository
git clone https://github.com/fahadiqbal/creative-motion-studio.git
cd creative-motion-studio

# 2. Install dependencies
npm install

# 3. Create environment file (optional for external AI)
cp .env.example .env.local

# 4. Start development server
npm run dev
```

Visit `http://localhost:3000` in your browser.

---

## 3. Scripts

- `npm run dev`: Launch development server with fast refresh.
- `npm run build`: Compile Next.js production build and type-check.
- `npm run start`: Launch production server.
- `npm run test`: Run the Vitest unit and integration test suite.
- `npm run lint`: Run ESLint analysis.

---

## 4. Branching & Commit Guidelines

- Branch names should follow semantic conventions:
  - `feat/add-polygon-shape-element`
  - `fix/timeline-scrub-offset`
  - `perf/raster-cache-optimization`
  - `docs/clarify-export-pipeline`
- Commits should follow Conventional Commits specification:
  - `feat: add ease-in-out-sine curve to animation presets`
  - `fix: resolve layer drag bounds on custom aspect ratio canvas`
  - `test: add boundary tests for image upload sanitizer`

---

## 5. Pull Request Process

1. Ensure all Vitest tests pass (`npm run test`).
2. Verify production build compiles with zero errors (`npm run build`).
3. Include test coverage for any newly introduced mathematical or storage logic.
4. Open PR with a clear summary of changes, motivation, and visual preview.
