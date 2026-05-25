# Documentation Index

**IMPORTANT**: Read this file at the beginning of any development task to understand available documentation and standards.

## Quick Reference

### Project Documentation
Project-level documentation covering vision, goals, architecture, and technology choices for **claude-training** — a bilingual EN/PL beginner Claude Desktop training companion web app for local council media/comms staff (initial user: Gmina Kosakowo). Built as a single static HTML page with vanilla JS + Tailwind via CDN; progress persisted in browser localStorage.

### Technical Standards
Coding standards, conventions, and best practices organized by domain. This project uses the **architecture**, **content**, **data**, **global**, and **frontend** standard categories. Backend and testing standards were skipped (no backend; testing strategy can be added later if needed).

---

## Project Documentation

Located in `.maister/docs/project/`

### Vision (`project/vision.md`)
Bilingual (EN/PL) self-paced Claude Desktop training companion for non-technical local-government comms staff (initial user: Gmina Kosakowo); single static HTML, lesson tracks Basics → Projects → Skills → MCP, browser-local progress, plain-language PL-primary content with municipal-comms scenarios.

### Roadmap (`project/roadmap.md`)
Three-phase plan: Phase 1 MVP (single-file skeleton, lesson data model, EN/PL toggle, progress tracking, lessons 1–4); Phase 2 real-world exercises (FB content, resident FAQs, research, briefings, proofreading, presentations); Phase 3 quality & reach (PL review, glossary, print stylesheet, GitHub Pages hosting, light analytics); plus future enhancements.

### Tech Stack (`project/tech-stack.md`)
Single static `index.html` with HTML5, Tailwind via CDN, and vanilla ES2020+ JavaScript; no backend, no framework, no build step, no package manager; persistence via `localStorage` (`claude-training:lang`, `claude-training:progress`); no testing or CI/CD in Phase 1, GitHub Pages hosting planned for Phase 3; PL content authored by hand.

### Architecture (`project/architecture.md`)
Single-page, single-file static app with client-side state, used alongside (not integrated with) Claude Desktop in a separate window; inline `<script type="module">` holds the `LESSONS` data, thin `localStorage` state helpers (`getLang`/`setLang`, `getProgress`/`markDone`, `t()`), and plain render functions (`renderNav`, `renderLesson`, `renderProgress`) driven by a single top-level `render()`; no network calls, no telemetry, stable exercise IDs for forward-compatible progress; deployment is opening the file or serving it statically.

---

## Technical Standards

### Architecture Standards

Located in `.maister/docs/standards/architecture/`

#### Single-File App (`standards/architecture/single-file.md`)
The entire application lives in one `index.html` at the repo root — markup, styles, lesson data, state helpers, and render functions all inline; no `src/` directory, no cross-file module imports, no splitting.

#### No Build Tooling (`standards/architecture/no-tooling.md`)
No `package.json`, `node_modules/`, bundler, or transpiler; no frontend framework (React/Vue/Svelte/Alpine/htmx) — only Tailwind via CDN; no enforced linter, formatter, or type-checker; JSDoc optional.

#### System Boundaries (`standards/architecture/boundaries.md`)
No backend, no network calls, no telemetry — all state is client-side `localStorage`; the app is a companion window to Claude Desktop, never an integration or automation layer; must work offline after first load.

### Content Standards

Located in `.maister/docs/standards/content/`

#### Bilingual EN/PL (`standards/content/bilingual.md`)
Polish is primary (default lang `"pl"`), English preserved for sharing; PL content is hand-authored, not machine-translated; the language toggle must also update `<html lang>` for screen readers and spell-check.

#### Audience & Scenarios (`standards/content/audience.md`)
Write at ~B1 reading level for non-technical local-government comms staff; avoid CLI/developer jargon; introduce domain terms (project, skill, MCP) on first use; exercises must be real Gmina Kosakowo / municipal comms scenarios — no toy or programming examples.

### Data Standards

Located in `.maister/docs/standards/data/`

#### Storage Conventions (`standards/data/storage.md`)
All `localStorage` keys use the `claude-training:` prefix and live as module-level SCREAMING_SNAKE constants (`claude-training:lang`, `claude-training:progress`); no other persistence mechanisms; lesson and exercise IDs (`<lesson-id>-<n>`) are stable forever — never rename or reuse; progress map is append-only in practice.

#### i18n Shape & Helpers (`standards/data/i18n.md`)
All user-facing strings use the bilingual `{ en, pl }` shape (no extra locales, no separate locale files, no i18n library); read bilingual fields exclusively through `t(field)` — never inline language checks at call sites; all `localStorage` access funnels through five thin helpers (`getLang`, `setLang`, `getProgress`, `markDone`, `t`).

### Global Standards

Located in `.maister/docs/standards/global/`

#### Coding Style (`standards/global/coding-style.md`)
Naming consistency, automatic formatting, descriptive names, focused single-purpose functions, uniform indentation, removing dead code, avoiding unnecessary backward compatibility, and DRY (extract repeated logic).

#### Commenting (`standards/global/commenting.md`)
Let code speak through structure and naming, comment sparingly only when intent isn't self-evident, and avoid changelog-style "what changed" comments.

#### Conventions (`standards/global/conventions.md`)
Predictable file/directory structure, up-to-date README, clean version control (clear commits, feature branches, PR descriptions), env-var configuration (no committed secrets), minimal dependencies, consistent code reviews, defined testing standards, feature flags over long-lived branches, changelog upkeep, and building only what's needed.

#### Error Handling (`standards/global/error-handling.md`)
Clear user messages without leaking internals, fail-fast input validation, typed exceptions over generic ones, centralized handling at boundaries, graceful degradation for non-critical failures, retry with exponential backoff for transient errors, and guaranteed resource cleanup.

#### Minimal Implementation (`standards/global/minimal-implementation.md`)
Build only what's actually called, every method must have a caller or aid readability, delete exploration artifacts, no future stubs or placeholder interfaces, no speculative abstractions (factories/strategies/adapters without immediate need), review for unused code before commit, and treat dead code as debt.

#### Validation (`standards/global/validation.md`)
Always validate server-side (client-side is feedback only), validate as early as possible, specific field-level error messages, allowlists over blocklists, systematic type/format/range checks, sanitize input against injection attacks (SQL/XSS/command), enforce business rules at the appropriate layer, and apply validation consistently across all entry points.

### Frontend Standards

Located in `.maister/docs/standards/frontend/`

#### Accessibility (`standards/frontend/accessibility.md`)
Semantic HTML elements, full keyboard navigation with visible focus indicators, 4.5:1 color contrast for normal text (don't rely on color alone), descriptive alt text and form labels, screen-reader verification, ARIA only when semantic HTML isn't enough, proper h1–h6 heading order, and focus management in dynamic content/modals.

#### Components (`standards/frontend/components.md`)
Single responsibility per component, reusability via configurable props, composability over monoliths, explicit documented prop interfaces with sensible defaults, encapsulation of implementation details, consistent naming, local state kept close to use, minimal props (split or compose if too many), and usage documentation.

#### CSS (`standards/frontend/css.md`)
Stick to one methodology (Tailwind, BEM, CSS modules) across the codebase, work with the framework rather than override it, document design tokens (colors/spacing/typography), minimize custom CSS in favor of framework utilities, and use purging/tree-shaking in production.

#### Rendering (`standards/frontend/rendering.md`)
Single top-level `render()` orchestrates region renderers (`renderStaticLabels`, `renderProgress`, `renderNav`, `renderLesson`) — state changes call `render()`, never mutate the DOM directly; plain `innerHTML` re-render with template literals, no virtual DOM or reactivity library; every `${…}` containing non-constant data must be wrapped in `escapeHtml()` as the sole XSS defense.

#### Responsive Design (`standards/frontend/responsive.md`)
Mobile-first progressive enhancement, consistent breakpoints (mobile/tablet/desktop), fluid percentage-based layouts, relative units (rem/em) over fixed pixels, multi-device testing, touch-friendly tap targets (min 44x44px), mobile performance optimization, readable typography at every breakpoint, and content prioritization on small screens.

### Backend Standards

*Not initialized for this project. The current architecture is a static, client-only HTML app with no backend. If a backend is added later, you can:*
- *Add standards manually using the docs-manager skill*
- *Run `/maister:standards-discover --scope=backend` to auto-discover from the codebase*

### Testing Standards

*Not initialized for this project. If you want to formalize a testing approach, you can:*
- *Add standards manually using the docs-manager skill*
- *Run `/maister:standards-discover --scope=testing` to auto-discover from the codebase*

---

## How to Use This Documentation

1. **Start Here**: Always read this INDEX.md first to understand what documentation exists
2. **Project Context**: Read relevant project documentation before starting work
3. **Standards**: Reference appropriate standards when writing code
4. **Keep Updated**: Update documentation when making significant changes
5. **Customize**: Adapt all documentation to your project's specific needs

## Updating Documentation

- Project documentation should be updated when goals, tech stack, or architecture changes
- Technical standards should be updated when team conventions evolve
- Always update INDEX.md when adding, removing, or significantly changing documentation
