# Development Roadmap

This roadmap outlines the planned features and development phases for **claude-training**.

## Phase 1: MVP (Minimum Viable Product)
**Goal**: One working HTML file with the full lesson skeleton, EN/PL toggle, and progress tracking — usable end-to-end by the primary learner.

- [ ] **Single-file app skeleton** — `index.html` with Tailwind CDN, JS module inline, semantic structure (header, lesson nav, lesson view, footer). `[S]`
- [ ] **Lesson data model** — JS object holding lessons/exercises with `id`, `title.en`, `title.pl`, `body.en`, `body.pl`, `exercises[]`. `[S]`
- [ ] **EN/PL language toggle** — persisted in `localStorage`; switches all visible content live. `[S]`
- [ ] **Progress tracking** — checkbox per exercise + per-lesson completion state in `localStorage`; visible progress bar. `[S]`
- [ ] **Lesson 1: What is Claude + basic chatting** — concept + 2–3 exercises (e.g., "draft a friendly reply to a resident question about waste collection"). `[M]`
- [ ] **Lesson 2: Projects in Claude Desktop** — concept + exercises (e.g., "create a project for Gmina Kosakowo comms with the council's tone-of-voice in project knowledge"). `[M]`
- [ ] **Lesson 3: Skills** — concept + exercises (e.g., "use a skill to draft a Facebook post about an upcoming local event"). `[M]`
- [ ] **Lesson 4: MCP (intro level)** — conceptual only, no install hand-holding; examples of useful servers. `[S]`

## Phase 2: Polish & Real-World Exercises
**Goal**: Make exercises genuinely useful for the learner's actual workload.

- [ ] **Facebook content exercises** — multiple drafts, tone variations, image-prompt practice. `[M]`
- [ ] **Resident-FAQ exercises** — common questions for Gmina Kosakowo (office hours, waste, permits, events) with model answers. `[M]`
- [ ] **Research exercises** — gathering info on a local topic from multiple sources, citing them. `[M]`
- [ ] **Briefing-compilation exercise** — turn 3 source documents into a one-page brief. `[M]`
- [ ] **Proofreading exercise** — Polish-language proofreading workflow, including what Claude is/isn't good at. `[S]`
- [ ] **Presentation-outline exercise** — outline → speaker notes for a council presentation. `[S]`

## Phase 3: Quality & Reach
**Goal**: Make it good enough to share beyond the initial user.

- [ ] **PL content review** — get Polish content read by a native speaker (the primary learner) and iterate. `[M]`
- [ ] **Glossary** — short EN/PL glossary of key terms (project, skill, MCP, prompt, context window). `[S]`
- [ ] **Print stylesheet** — let learners print a lesson as a worksheet. `[S]`
- [ ] **Hosting** — publish to GitHub Pages (or similar) so the page has a permanent URL. `[S]`
- [ ] **Light analytics** — privacy-respecting page-view counter to see if/when lessons get used. `[S]`

## Future Enhancements
- [ ] **Self-check questions** — short multiple-choice "did you get it?" at the end of each lesson, scored locally.
- [ ] **Export progress** — download a small JSON of completed exercises (for the learner's own records).
- [ ] **Additional lessons** — Artifacts, file uploads, image inputs, working with long documents.
- [ ] **Onboarding for new comms hires** — package as an induction resource for the council.

---
**Effort Scale**: `S`: 2–3 days | `M`: 1 week | `L`: 2+ weeks
