# Design Spec — CLAUDE.md / `.memory/` Split

**Date:** 2026-04-24
**Status:** Awaiting athlete review
**Author:** Claude (drafted) + athlete (decisions)

---

## Problem

`CLAUDE.md` (138 lines) currently mixes four content categories:

1. **Workflow guidelines** — how to work in this project (Post-Workout Review Process, Daily Note Template Requirements, Conventions). *Belongs in CLAUDE.md.*
2. **Stable project structure** — vault layout, phase definitions, program timeline. *Belongs in CLAUDE.md.*
3. **Athlete profile (stable)** — demographics, training history, current PRs, target PRs, priority stack. *Does NOT belong in a "how to work" doc.*
4. **Current operating state (fluid)** — limiter discoveries, active protocols, calendar shifts, pending decisions, recent bodyweight readings. *Does NOT belong in a "how to work" doc.*

Categories 3 and 4 cause CLAUDE.md to bloat after every coaching review (e.g., the 2026-04-24 Wk 4 review added 8 protocols + a new limiter + calendar shifts + pending decisions). A workflow document should be stable; a state document should be fluid. Mixing them produces a file that is too detailed to serve as a quick reference and too unstable to be canonical workflow guidance.

## Goal

Three-way separation of concerns:

- **`CLAUDE.md`** — pure workflow + stable project structure
- **`.memory/profile.md`** — stable athlete identity (changes only at test weeks or by explicit decision)
- **`.memory/state.md`** — current operating state (changes after every Coach's Review when state changes)

## Non-Goals

- This spec does NOT change training programming, daily note format, weekly summary format, or the phase-file structure
- This spec does NOT add a new memory subsystem or external tool — `.memory/` is plain markdown files in the vault
- This spec does NOT propose archiving or removing past Coach's Reviews — they remain the historical record in daily notes
- This spec does NOT change Obsidian configuration; `.memory/` is hidden by filesystem convention but reachable via Obsidian's "Show hidden files" if the athlete wants to browse it directly

## Design

### File 1 — `CLAUDE.md` (slimmed)

**Sections retained (verbatim or lightly edited):**

- `# Training Program Vault` — title + project description
- `## Program Design` — phases, deload weeks, test weeks (stable program philosophy; no current calendar)
- `## Vault Structure` — file layout reference
- `## Memory Files` (NEW, ~5 lines) — explains where athlete state lives; tells any agent reading CLAUDE.md to consult `.memory/profile.md` + `.memory/state.md` at session start
- `## How to Help the Athlete` — process guidance only; references to limiters / priority stack / current PRs become "see `.memory/state.md`" or "see `.memory/profile.md`"
- `## Conventions` — RPE scale, knee scale, daily note frontmatter rules
  - `### Daily Note Template Requirements` — structural rules for daily notes
  - `### Post-Workout Review Process` — adds one new step: "if Coach's Review surfaces a new finding / closes a limiter / changes a protocol / shifts the calendar, update `.memory/state.md`"

**Sections removed (migrated):**

| Removed from CLAUDE.md | Migrated to |
| --- | --- |
| `## Athlete Quick Reference` (demographics, training history, schedule) | `profile.md` |
| `### Current PRs` | `profile.md` |
| `### Target PRs` | `profile.md` |
| `### Priority Stack` | `profile.md` |
| `### Known Physical Limiters` | `state.md` |
| `### Active Permanent Protocols` | `state.md` |
| `### Pending Structural Decisions` | `state.md` |
| `### Calendar (current — adjusted for Wk 5 trip)` | `state.md` |

**Net result:** CLAUDE.md drops from ~138 lines to ~70–80 lines, all of it process / conventions / structure. Zero athlete-specific content.

### File 2 — `.memory/profile.md`

**Purpose:** stable athlete identity. Updated only at test weeks (Wk 8, 16, 24) when PRs are retested, OR when priority stack / training schedule changes through explicit discussion.

**Sections:**

1. **Athlete Identity** — height, weight (baseline), age, sex, dominance
2. **Training Background** — years bodybuilding, years CrossFit, self-coached
3. **Schedule** — weekly training pattern (e.g., Mon–Fri ~1 hr + 15–20 min accessory, rest weekends)
4. **Current PRs** — with `Last updated:` date stamp; only refreshed at test weeks
5. **Target PRs / Unlock Goals** — back squat, snatch, C&J targets + skill unlocks (ring MU, HS walk)
6. **Priority Stack** — 1–5 ranked priorities
7. **Program Timeline** — start date, end date, total weeks
8. **Update cadence note** (footer) — explicit rule about when this file is touched

**Update trigger:** test week PR retest OR explicit priority/schedule change discussion.

### File 3 — `.memory/state.md`

**Purpose:** current operating state. Updated after every Coach's Review when state changes (new finding, limiter status change, protocol added/removed, calendar shift, decision made/changed).

**Sections:**

1. **`Last updated:` date stamp** at top — every edit refreshes this; also note which session triggered the update
2. **`## Active Limiters`** — each limiter as its own subsection with: status (`active` / `managing` / `closing` / `closed`), evidence trail (key data points with dates), current management protocol, red-flag boundaries
3. **`## Active Permanent Protocols`** — numbered list of currently-active rules (belt thresholds, pre-session fueling, daily warm-up additions, heavy clean stand-up breathing, bar drop, pre-bed mobility, wider jerk stance, bodyweight tracking)
4. **`## Calendar`** — current dates per week, with shifts noted and reasons documented (e.g., "Wk 6 shifted +1 wk from May 4 → May 11 due to Wk 5 trip")
5. **`## Pending Decisions`** — open structural decisions awaiting athlete input (currently: squat clean at the box decision, options a/b/c with coach's recommendation)
6. **`## Recent State Notes`** — light-touch tracking of items that aren't full limiters but worth flagging (e.g., bodyweight 91.8 kg Wk 4 Thu, monitoring trend; sleep deficit pattern; etc.)
7. **Update cadence note** (footer) — explicit rule about update triggers

**Update trigger:** any Coach's Review that surfaces a state change. Trigger types: new finding, limiter status change, protocol added/removed/modified, calendar shift, pending decision created/resolved.

### File 4 — Workflow integration in CLAUDE.md

Two specific edits to make CLAUDE.md aware of the memory files without re-introducing state:

**Edit A — Add at top of `## How to Help the Athlete`:**

> **Before any work, read `.memory/state.md` for current athlete state (limiters, protocols, calendar, decisions) and `.memory/profile.md` for stable context (PRs, demographics, priority stack). Daily notes and phase files reference these — do not duplicate their contents.**

**Edit B — Modify `### Post-Workout Review Process` to add step 5:**

> 5. **Update `.memory/state.md` if state changed** — if the review surfaced a new finding, closed a limiter, modified a protocol, shifted the calendar, or made/created a pending decision, edit the relevant section of `state.md` and refresh its `Last updated:` stamp. Coach's reviews stay in the daily note (history); state.md holds current state only.

These two edits are the only behavior-level changes — everything else is pure content migration.

## Architecture

```
Vault root
├── CLAUDE.md                   ← workflow + project structure (stable)
├── .memory/
│   ├── profile.md              ← stable athlete identity
│   └── state.md                ← current operating state (fluid)
├── docs/
│   ├── README.md
│   ├── specs/                  ← design documents (this file)
│   └── plans/                  ← implementation plans
└── Training Program/
    ├── 00 - Program Overview.md
    ├── Phase 1 - Weeks 1-4.md
    ├── Phase 1 - Weeks 5-8.md
    ├── Protocols & Reference.md
    └── Week N/
        └── ...daily notes
```

**Boundary rules (the cleavage logic):**

- If it's true for months at a time and only changes at test weeks → `profile.md`
- If it changes after a single training day → `state.md`
- If it's about *how to do the work* and applies to any athlete using this vault structure → `CLAUDE.md`
- If it's a specific session's prescription or result → `Training Program/`

## Data Flow

**Reading flow (any agent / future Claude session):**

1. Session opens. Agent reads CLAUDE.md to learn workflow + that memory files exist.
2. Agent reads `.memory/state.md` to load current limiters, protocols, calendar, decisions.
3. Agent reads `.memory/profile.md` for stable context (PRs, priority stack).
4. Agent proceeds with the task using daily notes / phase files for programming details.

**Writing flow (during a Coach's Review):**

1. Coach's Review is added to the daily note (existing behavior, unchanged).
2. If the review surfaces a state change (per the trigger types above), `state.md` is edited.
3. `state.md` `Last updated:` stamp is refreshed; the coach's review remains the canonical history.
4. `profile.md` is NOT touched unless the change is at a test week or an explicit discussion-driven update.

## Migration Plan (high level)

The detailed plan goes in `docs/plans/` after this spec is approved. High-level steps:

1. Create `.memory/` folder
2. Write `.memory/profile.md` from current CLAUDE.md `## Athlete Quick Reference` + `### Current PRs` + `### Target PRs` + `### Priority Stack`
3. Write `.memory/state.md` from current CLAUDE.md `### Known Physical Limiters` + `### Active Permanent Protocols` + `### Pending Structural Decisions` + `### Calendar`
4. Rewrite `CLAUDE.md` to the slimmed shape with the workflow integration edits (Edits A and B above)
5. Verify cross-references resolve (no orphaned "see CLAUDE.md" references that should now point at memory files)
6. Spot-check daily notes / phase files / weekly summaries for any "see CLAUDE.md" pointers that should now point at `.memory/state.md` or `.memory/profile.md`

## Risks and Mitigations

| Risk | Mitigation |
| --- | --- |
| Future Claude session forgets to read memory files and works without athlete context | The new `## Memory Files` section in CLAUDE.md is the explicit pointer; the "Before any work, read..." sentence in `## How to Help the Athlete` is the explicit instruction. CLAUDE.md is loaded by default in Claude Code sessions. |
| State drift — `state.md` and a Coach's Review in a daily note disagree | Coach's Review is the *event*; state.md is the *current state*. The Post-Workout Review Process step 5 makes the update mandatory at the moment the review is written. Disagreement = process failure, not a design failure. |
| Athlete browses Obsidian and can't find `.memory/` | `.memory/` is hidden by filesystem convention. If the athlete wants to browse, they enable "Show hidden files" in Obsidian. Alternative: use visible `Memory/` folder name (athlete decision deferred; default is hidden, can be revisited). |
| `state.md` grows unwieldy as old limiters accumulate | Closed limiters can be archived or deleted from `state.md` once they've been closed for 4+ weeks. Status conventions: `active` / `managing` / `closing` / `closed` make this explicit. (This is an operational choice, not a design issue.) |

## Open Questions for Athlete

None — all design decisions resolved during brainstorming. Ready for review.

## Acceptance Criteria

After migration, verify:

1. CLAUDE.md contains zero athlete-specific content (no PRs, no limiters, no protocols, no calendar dates, no priority stack).
2. CLAUDE.md is ≤ ~85 lines.
3. `.memory/profile.md` is readable end-to-end as a coherent athlete identity document.
4. `.memory/state.md` is readable end-to-end as a coherent current-state document; every section has a clear "when do I update this?" answer.
5. Post-Workout Review Process in CLAUDE.md includes the new step 5.
6. `## How to Help the Athlete` in CLAUDE.md begins with the "Before any work, read..." instruction.
7. No daily note, phase file, or weekly summary contains a stale "see CLAUDE.md" reference that should now point at memory.

## What Happens After This Spec

If approved: a corresponding implementation plan is written to `docs/plans/2026-04-24-claude-md-memory-split-plan.md` with file-by-file changes and a checklist. Athlete reviews the plan. On plan approval, the migration is executed.
