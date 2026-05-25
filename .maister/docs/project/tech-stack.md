# Technology Stack

## Overview
This document describes the technology choices and rationale for **claude-training**. The stack is intentionally tiny: the deliverable is a single static HTML file that runs in any modern browser with no build step and no backend.

## Languages

### HTML5
- **Usage**: Page structure, semantic landmarks for accessibility.
- **Rationale**: Universal, zero-toolchain, prints reasonably well.

### CSS — via Tailwind (CDN)
- **Usage**: All styling.
- **Rationale**: Utility-first classes keep the single file readable without a separate stylesheet; CDN means no build step.

### JavaScript (ES2020+, vanilla)
- **Usage**: Lesson rendering, EN/PL language toggle, progress state, `localStorage` I/O.
- **Rationale**: A single-file app with a few hundred lines of state doesn't need a framework. Vanilla keeps the file readable, learnable, and dependency-free.

## Frameworks

### Frontend
- **None** (by design). Tailwind via CDN is the only runtime dependency; everything else is hand-written vanilla JS.

### Backend
- **None.** There is no server. All state lives in the browser via `localStorage`.

### Testing
- **None (Phase 1).** Manual smoke-testing against the primary learner is the test plan for the MVP. A lightweight test pass may be added later if the file grows.

## Database
**Not applicable.** Persistence is browser `localStorage`:
- `claude-training:lang` — `"en"` or `"pl"`
- `claude-training:progress` — JSON map of `{exerciseId: true}`

## Build Tools & Package Management
**None.** The project ships as a single `index.html` file. No `package.json`, no bundler, no transpilation.

## Infrastructure

### Containerization
Not applicable.

### CI/CD
Not applicable for Phase 1. May add a trivial GitHub Actions job in Phase 3 to deploy to GitHub Pages on push to `main`.

### Hosting
**Phase 1**: open `index.html` locally in a browser.
**Phase 3 (planned)**: GitHub Pages (or any static host) — see [[roadmap]].

## Development Tools

### Linting & Formatting
None mandated. Prettier defaults (in the editor) are fine if used. Keep the file readable by hand.

### Type Checking
Not used. JSDoc comments are welcome where they clarify the lesson data shape but are not required.

## Key Dependencies
- **Tailwind CSS** — loaded via `<script src="https://cdn.tailwindcss.com"></script>`. CDN play mode is acceptable because this is a learning aid, not a production product where unused CSS would matter.

## Version Management
**No package versions to manage.** Tailwind via CDN tracks the latest 3.x; if a breaking change ever lands, pin to a specific CDN version then.

## Internationalization Approach
Content is stored as `{ en: "…", pl: "…" }` pairs inside a single JS lesson data object. There is no i18n library — a small `t(field)` helper reads the current language from `localStorage` and returns the right string. Polish content is authored by hand (not machine-translated) since the primary audience is Polish-speaking.

---
*Auto-detected*: nothing — repo was empty at init time.
*User-provided*: all of the above.
