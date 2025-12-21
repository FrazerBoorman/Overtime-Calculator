# AVD Tools — Codex Front Door

## Shared invariants (apply to all AVD tools)

- **Version pill:** `v0.10+` and **increment on every index.html change**.
- **Details panels:** all `<details>` panels are **closed by default on refresh**.
- When a `<details>` opens, it **highlights** (accent border + subtle fill) while keeping the **dashed border + padded container** styling.
- All `<details>` (including nested) use the **same caret marker** that rotates on open.

This repo contains single-file HTML tools used by Audio Visual Direct UK (AVD).

## Core conventions (do not break)

- **Single-file**: each tool is a standalone `index.html`.
- **Version pill**: semantic version `v0.xx` in header; clicking copies full `index.html` to clipboard and also populates the “Replacement index.html output” panel.
- **Hidden-by-default panels**: Debug, API key, AI Debugger, Replacement output, Calendar settings, Tool info.
- **OpenAI key storage**: shared localStorage key: `avd_job_report_openai_key`.
- **UI details consistency**:
  - All `<details>` components are **closed on every page refresh**.
  - When open, the `<summary>` row **highlights** (same visual language across tools).
  - `<details>` containers use **dashed border + padded container** styling.
  - Nested `<details>` automatically inherit the same caret + open highlight styling.

## Tool-specific manuals

- `context/OT-CALC.md` — AVD Overtime Calculator (TOOL_CODE: `OT-CALC`)
