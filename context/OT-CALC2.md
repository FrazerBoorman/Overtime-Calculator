# OT-CALC

## Shared invariants
- All `<details>` panels are closed by default on refresh.
- Open `<details>` highlights (accent border + subtle fill) while keeping dashed + padded container styling.
- All `<details>` (including nested) use the same caret marker that rotates on open.
- Version pill increments on every index change.
 — AVD Overtime Calculator (Service Manual)

## Purpose

A stable daily overtime calculator with optional Google Calendar event picker.

- Calendar picker is convenience only; manual entry must always work.
- Provides a log table and printable PDF export for sign-off.

## Non‑negotiables / invariants

### 1) Calendar flow

- After OAuth success (“Signed in”), auto-fetch events for the default range.
- Events are sorted **newest-first** in the dropdown.
- Auto-select the most recent event and auto-fill Job/Location + Date.
- Applying or resetting the advanced date range **re-fetches immediately** (no extra “Load” button).

### 2) Advanced date range UX (must match other AVD tools)

- Implemented as a native `<details>/<summary>` disclosure row.
- **Closed by default on every refresh**.
- All `<details>` (including nested) share:
  - a consistent caret/triangle indicator
  - “open” highlight on the `<summary>`
  - dashed border + padded container styling

### 3) Overtime logic integrity

- Overtime is time **before 09:00** and **after 17:00**.
- Apply the 15-minute deduction(s):
  - Field day: deduct 15 minutes from pre-09 and 15 minutes from post-17 (when present).
  - Office-finish day: deduct 15 minutes from pre-09 only; no post-17 overtime.
  - Full office/admin day: no overtime.
- **OT Due** is based on payable overtime minutes (after deductions).
- “Total overtime” in the table/report must reflect payable minutes so finance can verify OT Due directly.

### 4) Persistence

- Keep `STORAGE_KEY` stable unless explicitly migrating saved state.
- Persist:
  - log table rows
  - base rate
  - calendar ID
  - employee name (default “Frazer” if unavailable)

### 5) Safe edits discipline

- Do not refactor unrelated sections.
- No silent changes to time rules, deduction logic, checkbox semantics, or export format.

## Regression checklist (run after any change)

### Visual / UX

- [ ] All `<details>` are closed after refresh (tool info, debug, API, AI debugger, replacement output, calendar settings, advanced date range).
- [ ] Any open `<details>` summary row highlights correctly.
- [ ] Caret indicator appears on all summaries, including nested `<details>`.
- [ ] `<details>` containers have dashed border + padded container.
- [ ] Advanced date range summary looks like a disclosure row (not a button).

### Calendar

- [ ] Sign in → events auto-load for default range.
- [ ] Dropdown lists newest-first.
- [ ] Latest event auto-fills Job/Location + Date.
- [ ] Apply date range → immediate re-fetch with custom range (future allowed).
- [ ] Reset → returns to default range and re-fetches.

### Overtime maths

- [ ] Field day: deductions apply as expected.
- [ ] Office-finish: no post-17 OT, pre-09 deduction applies.
- [ ] Full office/admin: OT always 0.
- [ ] Table “Total overtime” equals payable minutes used for OT Due.
- [ ] PDF totals match table totals.

## Key implementation notes (for Codex)

- Advanced range state is controlled by `USE_CUSTOM_RANGE`.
- Default range = last 14 days inclusive.
- Sorting newest-first is applied after fetching.
- “All details closed on refresh” should be done centrally (e.g., `document.querySelectorAll("details").forEach(d=>d.open=false);`)
  so nested disclosures inherit behavior with no per-panel special cases.
