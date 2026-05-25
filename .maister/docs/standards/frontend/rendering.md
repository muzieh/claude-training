# Frontend: Rendering

### Single top-level `render()` orchestrator
There is one `render()` function that calls every region renderer (`renderStaticLabels`, `renderProgress`, `renderNav`, `renderLesson`). After any state change, call `render()` (or the specific `renderX()` functions you affected) rather than mutating the DOM directly. New event handlers follow this pattern: update state, then re-render.

### Plain re-render on state change, no virtual DOM
Rendering is plain functions that assign a template-literal HTML string to `innerHTML`. There is no virtual DOM, no diffing, no reactivity library. The page is small enough that wholesale re-renders are cheap and keep the code linear and obvious.

### Always escape interpolations with `escapeHtml()`
Every `${…}` inside an `innerHTML` template literal that contains lesson, exercise, or any non-constant data must be wrapped in `escapeHtml()`. No exceptions in the existing file, none in new code. This is the only XSS defense the app has.

```js
nav.innerHTML = LESSONS.map(lesson =>
  `<button data-lesson="${escapeHtml(lesson.id)}">${escapeHtml(t(lesson.title))}</button>`
).join("");
```

**Why this matters**: The render pattern keeps the file readable as it grows; the escape discipline is the security boundary. Both must hold for every new dynamic region.
