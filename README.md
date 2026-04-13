# Todo Item Card

A single-file, zero-dependency task card UI built with semantic HTML, CSS, and vanilla JavaScript.

## Live URL

> `https://<your-netlify-or-pages-url>`

---

## How to Run Locally

No install step needed. Just open the file:

```bash
# Option 1 — open directly in browser
open index.html

# Option 2 — serve with any static server
npx serve .
# → http://localhost:3000
```

---

## What It Does

- Displays a task card with title, description, priority badge, status indicator, due date, time remaining, checkbox, and tags
- Due date and time remaining update automatically every 30 seconds
- Time remaining is human-readable: `Due in 3 days`, `Overdue by 2 hours`, `Due in 45m`
- Checking the checkbox marks the card as complete and freezes the time display to `Completed`
- All interactive elements (edit, delete, checkbox) are keyboard accessible

---

## All `data-testid` Attributes

| Element           | `data-testid`                    |
|-------------------|----------------------------------|
| Card container    | `test-todo-card`                 |
| Title             | `test-todo-title`                |
| Description       | `test-todo-description`          |
| Priority badge    | `test-todo-priority`             |
| Due date          | `test-todo-due-date`             |
| Time remaining    | `test-todo-time-remaining`       |
| Status indicator  | `test-todo-status`               |
| Checkbox          | `test-todo-complete-toggle`      |
| Tags list         | `test-todo-tags`                 |
| Tag (each)        | `test-todo-tag-{name}`           |
| Edit button       | `test-todo-edit-button`          |
| Delete button     | `test-todo-delete-button`        |

---

## Decisions Made

**Single file** — the brief is a UI component, not an app. One `index.html` is the simplest possible deliverable that satisfies every requirement.

**Semantic HTML** — card is an `<article>`, title is `<h2>`, dates use `<time datetime="...">`, tags are a `<ul role="list">`, buttons are real `<button>` elements, checkbox is a real `<input type="checkbox">` with an associated `<label>`.

**Zero dependencies** — no React, no build step, no `npm install`. Opens directly in a browser. Deploys to GitHub Pages, Netlify, or Vercel with no configuration.

**30-second interval** — the spec says update every 30–60 seconds. 30 seconds chosen so overdue states become visible quickly during demos.

**`datetime` attribute** — both `<time>` elements carry a machine-readable ISO 8601 `datetime` attribute alongside the human-readable label, satisfying accessibility tooling and the HTML spec.

---

## Trade-offs

- **Static data** — the task content and due date are hardcoded. In a real app they'd come from props or an API. The due date is easy to change: edit the `DUE` constant at the top of the `<script>` block.
- **No persistence** — checkbox state resets on page refresh. Adding `localStorage` would be one extra line but was out of scope.
- **No edit/delete logic** — the buttons exist with correct `data-testid` and `aria-label` attributes for the test suite, but clicking them does nothing. Wiring them up requires an app layer that wasn't part of the brief.
"# todo-card" 
