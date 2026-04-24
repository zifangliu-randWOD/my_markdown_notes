# docs/

Project-level documentation that isn't training content.

## Structure

- **`specs/`** — design documents. One file per design decision. Each spec captures the *what* and *why* of a structural change before any implementation. Format: `YYYY-MM-DD-<topic>-design.md`.
- **`plans/`** — implementation plans. One file per spec, generated after the spec is approved. Each plan breaks the spec down into concrete file-level changes with a checklist. Format: `YYYY-MM-DD-<topic>-plan.md`.

## Workflow

1. Athlete or coach proposes a structural change (e.g., "split CLAUDE.md into memory files").
2. Brainstorm session produces a **spec** in `specs/`. Athlete reviews + approves.
3. Spec drives an **implementation plan** in `plans/`. Athlete reviews + approves.
4. Plan is executed; the spec and plan stay in this folder as the historical record of why the vault is shaped the way it is.

## What does NOT belong here

- Training programming (lives in `Training Program/`)
- Athlete profile / current state (lives in `.memory/`)
- Coaching review notes (live in daily notes inside `Training Program/Week N/`)
