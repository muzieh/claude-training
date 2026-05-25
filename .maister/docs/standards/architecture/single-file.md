# Architecture: Single-File App

### Single static HTML file at repo root
The entire application is one file: `index.html`. All markup, inline styles, lesson data, state helpers, and render functions live there. Do not split into multiple HTML/JS/CSS files, do not add a `src/` directory, do not introduce module imports from other files.

**Why this matters**: The project ships by opening the file or serving it statically. Splitting it would force a bundler, which is explicitly out of scope (see `architecture/no-tooling.md`).
