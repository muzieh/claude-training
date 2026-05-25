# System Architecture

## Overview
**claude-training** is a single-file static web application. There is no server, no build step, no framework runtime — just one `index.html` opened in a browser. All behaviour runs client-side; all state lives in `localStorage`. The user uses this page **alongside Claude Desktop in a separate window** — the two do not communicate directly.

## Architecture Pattern
**Pattern**: Single-page, single-file static app with client-side state.

```
┌─────────────────────────────┐        ┌────────────────────────┐
│  Browser window             │        │  Claude Desktop window │
│  index.html (this app)      │        │  (separate process)    │
│  ─────────────────          │        │  ─────────────────     │
│  • Lesson navigation        │        │  • Where the learner   │
│  • Concept text (EN/PL)     │        │    actually does the   │
│  • Exercise instructions    │ ◀────▶ │    exercises            │
│  • "Mark done" checkboxes   │  user  │                        │
│  • Progress bar             │        │                        │
│  • localStorage state       │        │                        │
└─────────────────────────────┘        └────────────────────────┘
```
There is **no integration** between the two windows. The learner reads instructions on the left, executes them in Claude Desktop on the right, and ticks the box when done. This is deliberate — see [[vision]] non-goals.

## System Structure

### `index.html` — single artifact
- **Location**: repository root.
- **Purpose**: contains everything: markup, styles (via Tailwind CDN), data, behaviour.
- **Internal sections** (top to bottom inside the file):
  1. `<head>` — meta, Tailwind CDN `<script>`, page title.
  2. `<body>` — semantic landmarks: `<header>` with language toggle + progress bar, `<nav>` with lesson list, `<main>` with the active lesson, `<footer>`.
  3. Inline `<script type="module">` — lesson data, state module, render functions, event wiring.

### Lesson data
A single JS constant inside the script:
```js
const LESSONS = [
  {
    id: "basics",
    title: { en: "What is Claude", pl: "Czym jest Claude" },
    body:  { en: "...", pl: "..." },
    exercises: [
      { id: "basics-1", title: { en: "...", pl: "..." }, prompt: { en: "...", pl: "..." } },
      ...
    ]
  },
  ...
]
```
Lesson and exercise `id` values are stable strings — never reuse or rename them once shipped, because they're keys in the user's saved progress.

### State module (inside the script)
Three thin helpers wrap `localStorage`:
- `getLang() / setLang(lang)` — `"en" | "pl"`, defaults to `"pl"` (primary audience).
- `getProgress() / markDone(exerciseId) / clearProgress()` — JSON map of `{exerciseId: true}`.
- `t(field)` — given a `{ en, pl }` field, return the right string for the current language.

### Render functions
Plain functions that take state and produce DOM:
- `renderNav()` — lesson list with completion indicators.
- `renderLesson(id)` — concept body + exercise list with checkboxes.
- `renderProgress()` — top-of-page progress bar (`done / total` exercises).

A single top-level `render()` calls all three; every state change calls `render()` again. No virtual DOM — the page is small enough that re-rendering innerHTML is fine and keeps the code linear.

## Data Flow
1. Page loads → script reads `lang` and `progress` from `localStorage`.
2. `render()` paints the UI from `LESSONS` + state.
3. User clicks an exercise checkbox → `markDone(exerciseId)` → `render()`.
4. User toggles EN ⇄ PL → `setLang(...)` → `render()`.
5. No network calls. No server. No telemetry.

## External Integrations
**None.**
- No API calls.
- No analytics in Phase 1 (privacy-respecting view counter is a Phase 3 *consideration*, see [[roadmap]]).
- No Claude Desktop integration. The learner is the bridge between the two windows.

## Database Schema
Not applicable. `localStorage` keys, fully specified:

| Key                          | Type   | Example                              |
|------------------------------|--------|--------------------------------------|
| `claude-training:lang`       | string | `"pl"` or `"en"`                     |
| `claude-training:progress`   | JSON   | `{"basics-1": true, "projects-2": true}` |

The progress object is **append-only in practice** — exercises are added, never silently renamed. If an exercise is retired, its old key is left in place (harmless) rather than removed.

## Configuration
None. The only configurable runtime value is the default language, which is hard-coded to `"pl"` in the source.

## Deployment Architecture
**Phase 1**: open `index.html` directly in a browser (`file://...`) or serve via any static host.
**Phase 3 (planned)**: GitHub Pages from `main` branch root. No build step, so the deployed artifact is the same file that's in the repo.

## Accessibility & Bilingual Considerations
- All interactive controls reachable by keyboard; visible focus rings (Tailwind's default ring utilities, not removed).
- `<html lang="...">` attribute updated when the language toggle changes — important for screen readers and for browser spell-check in Polish content.
- Exercise instructions written in plain language at roughly B1 reading level in both languages; jargon (project / skill / MCP) introduced explicitly when first used and added to a future glossary (see [[roadmap]] Phase 3).

---
*Based on project context provided at init time — no codebase existed at the moment of analysis.*
