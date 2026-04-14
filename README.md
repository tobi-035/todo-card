# Todo Item Card — Stage 1

An interactive, stateful todo card built with semantic HTML, CSS, and vanilla JavaScript. No frameworks. No dependencies for the card itself.

## Live URL

> `https://tobi-035.github.io/todo-card`

---

## How to Run Locally

```bash
# Open directly — no server needed
open index.html

# Or serve with a static server
npx serve .
# → http://localhost:3000
```

---

## How to Run the Tests

```bash
npm install           # installs Cypress (one time only)
npm test              # run all tests headlessly
npm run test:open     # open the Cypress visual runner
```

Tests run against the live GitHub Pages URL by default. To run locally, edit `cypress.config.js` and change `baseUrl` to `http://localhost:3000`.

---

## What Changed from Stage 0

| Feature | Stage 0 | Stage 1 |
|---|---|---|
| Edit mode | Button existed, no logic | Full edit form with save/cancel |
| Status | Display only | Segmented control — Pending / In Progress / Done |
| Priority | Badge only | Badge + glowing dot indicator + left border accent |
| Description | Always fully shown | Collapsible if > 100 chars |
| Overdue | Time remaining coloured red | Explicit flashing Overdue badge |
| Checkbox ↔ status | Checkbox toggled done | Full two-way sync with status control |
| Time format | Hours only | Granular — minutes, hours, days |
| Focus management | None | Focus trapped in edit form, returned to Edit on close |

---

## All `data-testid` Attributes

### Stage 0 (still present)
| Element | `data-testid` |
|---|---|
| Card | `test-todo-card` |
| Title | `test-todo-title` |
| Description | `test-todo-description` |
| Priority badge | `test-todo-priority` |
| Due date | `test-todo-due-date` |
| Time remaining | `test-todo-time-remaining` |
| Status display | `test-todo-status` |
| Checkbox | `test-todo-complete-toggle` |
| Tags list | `test-todo-tags` |
| Tags | `test-todo-tag-{design,mobile,ux,sprint}` |
| Edit button | `test-todo-edit-button` |
| Delete button | `test-todo-delete-button` |

### Stage 1 (new)
| Element | `data-testid` |
|---|---|
| Edit form | `test-todo-edit-form` |
| Title input | `test-todo-edit-title-input` |
| Description textarea | `test-todo-edit-description-input` |
| Priority select | `test-todo-edit-priority-select` |
| Due date input | `test-todo-edit-due-date-input` |
| Save button | `test-todo-save-button` |
| Cancel button | `test-todo-cancel-button` |
| Status control | `test-todo-status-control` |
| Priority indicator | `test-todo-priority-indicator` |
| Expand toggle | `test-todo-expand-toggle` |
| Collapsible section | `test-todo-collapsible-section` |
| Overdue indicator | `test-todo-overdue-indicator` |

---

## Design Decisions

**State object** — all card data lives in a single `state` object. Every render function reads from it. This makes save/cancel trivial: snapshot on open, restore on cancel.

**Two-way status sync** — checkbox and the segmented status control stay in sync at all times. Checking the checkbox sets status to Done. Setting status to Done checks the checkbox. Unchecking reverts to Pending.

**Collapse threshold** — descriptions longer than 100 characters are truncated with a Show more toggle. The threshold is a named constant at the top of the script so it's easy to adjust.

**Focus trap** — Tab cycles through the edit form's focusable elements without escaping. Escape cancels. Focus returns to the Edit button when the form closes.

**Overdue indicator** — separate from the time remaining badge. The `test-todo-overdue-indicator` element always exists in the DOM (for the test suite) but is only visually shown when the task is past due and not done.

---

## Known Limitations

- Delete button has no logic — it exists for the test suite but does not remove the card
- Tags are not editable in Stage 1
- No persistence — state resets on page refresh
- Due date defaults to a hardcoded value; change the `state.due` line in the script to adjust it

---

## Accessibility Notes

- Edit form traps focus (Tab / Shift+Tab cycle within the form)
- Escape closes the edit form from any focused element inside it
- All interactive elements have `aria-label` or an associated `<label>`
- Status control has `role="group"` and each button has `aria-pressed`
- Expand toggle has `aria-expanded` and `aria-controls`
- Time remaining and overdue indicator have `aria-live` for screen reader announcements
- Checkbox has both a visually hidden `<label>` and an `aria-label`
