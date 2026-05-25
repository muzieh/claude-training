# Architecture: No Build Tooling

### No build step, bundler, or package manager
The project must not introduce `package.json`, `node_modules/`, a bundler (Vite, webpack, esbuild, etc.), or any transpilation step. The file is hand-written and runs as-is in the browser.

### Vanilla JavaScript only — no frontend framework
No React, Vue, Svelte, Alpine, htmx, or similar. The only runtime dependency is Tailwind, loaded via CDN. State, rendering, and event handling are all hand-written vanilla ES2020+.

### No mandated linter, formatter, or type-checker
Prettier defaults in the editor are fine if used; nothing is enforced. Type checking is not used. JSDoc comments are welcome where they clarify lesson data shape, but are not required. Keep the file readable by hand.

**Why this matters**: Zero tooling is a load-bearing constraint — it keeps the project trivially openable for non-technical contributors and means there is nothing to maintain, upgrade, or break.
