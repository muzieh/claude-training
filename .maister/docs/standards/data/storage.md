# Data: Storage Conventions

### Namespaced `localStorage` keys with `claude-training:` prefix
All persisted keys use the `claude-training:` prefix and are declared as module-level SCREAMING_SNAKE constants (not inlined string literals). Current keys:

- `claude-training:lang` — `"en"` or `"pl"`
- `claude-training:progress` — JSON map `{ exerciseId: true }`

Any new persisted key follows the same prefix-and-constant pattern. Do not introduce other persistence mechanisms (IndexedDB, cookies, sessionStorage) without a written reason.

### Stable lesson and exercise IDs
Lesson `id` and exercise `id` values are stable strings — never reuse or rename them once shipped. Exercise IDs follow the form `<lesson-id>-<n>` (e.g. `basics-1`, `mcp-3`). They are the keys in the user's saved progress, so renaming silently breaks resumed progress for existing users.

The progress object is append-only in practice: add new exercises with the next number; if an exercise is retired, leave the old key in place (harmless) rather than removing it.

**Why this matters**: These IDs and keys are the only contract with the user's browser. Breaking them resets every learner's progress with no recovery path.
