# AVD Tools — Codex Front Door

This repository contains AVD single‑file tools (static `index.html`) with a shared UI/behaviour template.

## Non‑negotiables (apply to all tools)

- **Be Strict:** never invent facts, never silently change core business logic or calculations.
- **Minimise edits:** avoid refactors unless explicitly requested; keep unrelated sections untouched.
- **Versioning:** version pill uses semantic `v0.xx` and must be updated when behaviour/UI changes.
- **Hidden-by-default panels:** Debug, API key, AI Debugger, Replacement index output, Calendar settings.
- **Shared OpenAI key:** `localStorage['avd_job_report_openai_key']` (same key across tools).

## OT-CALC (AVD Overtime Calculator)

- **Tool code:** `OT-CALC`
- **Core purpose:** daily overtime calculation + optional Google Calendar event picker convenience.
- **Calendar behaviour:** after OAuth success, auto-fetch events (default last 14 days), newest-first, auto-fill from latest event.
- **Advanced date range:** must be a `<details>/<summary>` disclosure row (not a button), closed by default, with a consistent caret marker.
- **Overtime integrity:** “Total overtime” in log/PDF must match payable overtime (after 15m deductions) and therefore align with OT Due.

## Where the full details live

- `context/OT-CALC.md` — invariants, regression checks, and implementation notes.
