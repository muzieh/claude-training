# Project Vision

## Pitch
**claude-training** is a bilingual (English/Polish) self-paced training companion that helps non-technical local-government communications staff become confident Claude Desktop users by walking them through hands-on exercises grounded in their actual day-to-day work.

## Problem Statement
Public-sector communications professionals — people who write Facebook posts, answer resident enquiries, prepare presentations, and compile briefings — can save hours per week with Claude Desktop, but generic tutorials assume technical fluency or use examples that feel irrelevant to municipal comms work. There is no gentle, task-grounded on-ramp that meets them where they are.

## Target Users
**Primary**: Communications and media staff at Gmina Kosakowo (initial user: project author's wife). Comfortable with web browsers and Office tools; no programming background; works daily in both Polish and English contexts.

**Secondary**: Other local-council comms staff in Poland who could benefit from the same curriculum once the format is proven.

Their needs:
- Concepts explained in plain language, with no CLI / developer jargon
- Bilingual content (PL primary for the learner, EN preserved so the material can be shared / reviewed)
- Exercises that map directly onto real tasks (FB posts about Gmina Kosakowo, resident FAQs, multi-source briefings, proofreading, presentation outlines)
- A way to track progress without installing anything

## Key Features
- Single static HTML page — open in any browser, no install
- Lesson tracks: **Basic chatting → Projects → Skills → MCP (intro)**
- Each lesson pairs a short conceptual explainer with one or more practice exercises that the learner runs in Claude Desktop in another window
- EN/PL language toggle persisted in `localStorage`
- Per-exercise "mark as done" checkboxes with progress saved in `localStorage`
- Exercise content rooted in Gmina Kosakowo communications scenarios

## Success Criteria
- The primary learner completes the curriculum end-to-end and reports feeling comfortable using Claude Desktop for at least three real work tasks unprompted.
- Lessons can be followed without any external help (no need to ask the author what something means).
- The page works offline after first load (single file, CDN-cached assets).
- Content quality in Polish is on par with English — not a machine translation feel.

## Non-Goals
- **Not** a Claude Code CLI tutorial. This is exclusively for Claude Desktop users.
- **Not** an MCP server / Claude Desktop integration. Progress tracking is browser-local; there is no automatic completion detection from Claude Desktop activity.
- **Not** a comprehensive reference manual — opinionated curriculum, not exhaustive docs.
- **Not** aimed at developers; technical depth is intentionally limited.

## Differentiators
- **Audience-specific scenarios** — every exercise is a real comms task, not a toy example.
- **Bilingual from day one** — most Claude tutorials are EN-only; this one teaches in PL alongside.
- **Zero-friction delivery** — one HTML file, no accounts, no setup, no install.
- **Companion-app model** — explicitly designed to sit next to Claude Desktop, not replace it or proxy through it.
