# Agent Startup Guide

This vault is an Obsidian training-program workspace for a 24-week Oly-first periodized CrossFit plan. Use this file as the quick startup map, then read the live source files before changing programming or writing reviews.

## Always Read First

Before working on programming, session reviews, athlete state, or training decisions:

1. Read `.memory/profile.md` for stable athlete identity, PRs, targets, priorities, and timeline.
2. Read `.memory/state.md` for current limiters, active protocols, calendar shifts, and pending decisions.
3. Read the relevant phase file in `Training Program/`.
4. For post-workout reviews, inspect `git diff` first to see what the athlete changed.

`CLAUDE.md` remains the full operating guide. This file is a condensed startup companion, not a replacement for the memory files.

## Vault Context

- Program: 24-week Oly-First Periodized CrossFit training program.
- Program dates: 2026-03-30 to 2026-09-20.
- Philosophy: "Position Before Load, Load Before Speed."
- Phase 1, Weeks 1-8: Positional Foundation.
- Phase 2, Weeks 9-16: Strength-Speed.
- Phase 3, Weeks 17-24: Peaking and Expression.
- Deload weeks: 4, 8, 12, 16, 20.
- Test weeks: 8, 16, 24.
- Percentages reference current test maxes in `.memory/profile.md`.

## Athlete Snapshot

Live source: `.memory/profile.md`.

- Male, 31, 181 cm, baseline 92 kg, right-dominant.
- Background: 4+ years bodybuilding, 2+ years CrossFit, self-coached.
- Schedule: Mon-Fri, about 1 hr training plus 15-20 min accessory; weekends rest.
- Current PRs at program start: BS 190 kg, FS 160 kg, DL 200 kg, snatch 105 kg, clean 140 kg, jerk about 120 kg, bench 110 kg, Fran 4:30.
- Targets: BS 200+, FS 170+, snatch 120, C&J 140+, ring muscle-up, handstand walk.

Priority stack:

1. Olympic lifting numbers.
2. Squat strength.
3. Left knee / asymmetry rehab.
4. Gymnastics unlocks.
5. Conditioning maintenance.

Do not change the priority stack without explicit discussion.

## Current State Snapshot

Live source: `.memory/state.md`. Refresh this from the live file every session.

Active limiters as of 2026-04-24:

- Left knee patellar tracking issue: managing. Pattern is jerk-dip-specific under heavy vertical-torso/knee-forward loading. Wider jerk stance, about +5 cm outside hip-width, is the permanent default. Squats, cleans, deadlifts, and BSS were pain-free through Weeks 3-4.
- Thoracic mobility restriction: managing and improving. Bilateral, worse on left. Limits front rack, jerk mechanics, clean receive, and overhead positions.
- Chronic lumbar stiffness / anterior pelvic tilt: resolved as of Wk 3, maintained with 90/90 breathing.
- Right erector spinae chronic tonus: managing. Muscular, not joint/disc/radicular per Wk 4 self-screen. Use belt and daily soft-tissue/mobility protocol.
- Anterior shoulder pull on heavy squat clean: closed pending Wk 5 Apr 29 final 100+ kg confirm. Likely load + fatigue + decayed pull-under pattern, with bar-lowering/catch-at-pelvis as probable aggravator.
- Left hip ER stiffness: closing. Maintain pigeon stretch and 90/90 hip rotation.
- Snatch efficiency gap: active, technique-limited. Snatch-to-squat ratio is 105/190; lever is positional/timing improvement.

## Active Protocols

Live source: `.memory/state.md`.

- Belt ON for working sets at BS >= 80 kg, FS >= 75 kg, Clean >= 85 kg.
- Pre-session fueling: 500 ml water plus about 30 g carbs in the 60-90 min pre-training window.
- Daily warm-up additions: right lumbar erector foam roll 60 sec, couch stretch 60 sec each side, and 90/90 breathing.
- Heavy clean stand-up breathing for clean >= 85 kg: controlled exhale through pursed lips during the rise, about 50% out by standing; own the 1-sec pause between clean and jerk; never chain clean and jerk.
- Bar drop protocol: at clean >= 80%, drop from front rack to platform. Do not catch at pelvis or control to thigh.
- Pre-bed mobility on training days: 5 min cat-cow, child's pose, supine spinal rotation.
- Wider jerk stance default on all jerk work.
- Bodyweight tracking: morning, post-pee, pre-food, naked. Baseline 92 kg.

## Current Calendar Snapshot

Live source: `.memory/state.md`.

- Wk 5: Apr 27-May 8, split by trip Apr 30-May 5, six lifting days total.
- Wk 6: May 11-17.
- Wk 7: May 18-24.
- Wk 8 test week: May 25-31.

Trip protocol lives at `Training Program/Week 5/Trip Mobility Protocol (2026-04-30 to 2026-05-05).md`.

## Pending Decision

Squat clean at the box on Wednesdays:

- Context: early Phase 1 box Wednesdays were power-clean-dominant, creating a squat-clean exposure gap.
- Decision needed when box Wednesdays resume in Wk 6+.
- Coach recommendation in state: mandatory 4-5 squat clean singles at 90-100 kg after box Wednesday.

## Programming Rules

- Check current week/phase and the relevant phase file before editing daily notes.
- Daily notes and phase files reference `.memory/*`; do not duplicate all athlete-specific content inline unless needed for a coaching cue.
- When modifying future exercises/progressions, propagate the change to the relevant phase file, because phase files are the programming source of truth.
- Keep percentages tied to current PRs in `.memory/profile.md`.
- Keep changes scoped. Preserve the athlete's notes and intent.
- Use Week 4 daily notes as the detail standard for Week 5+ daily coaching notes.

## Daily Note Standard

Every daily training note should include:

- Frontmatter: date, week, phase, day, training, tags.
- A `> [!tip] Day Focus` at the top with session intent, not generic motivation.
- Collapsed `> [!info]-` coaching callouts after warm-up, primary lifts, secondary lifts, gymnastics, and accessory blocks.
- Each coaching callout should explain why the movement is in the program, how to execute it, athlete-specific notes, expected RPE/feel, and decision rules if the response is off-target.
- Tracking tables for sets, loads, RPE, notes, and relevant limiter status.
- Daily log fields for RPE, left knee, right lumbar, front rack/shoulder where relevant, fueling, pre-bed mobility, and general notes.

## Post-Workout Review Workflow

When the athlete fills in a daily note:

1. Start with `git diff` or `git diff --staged`.
2. Clean grammar, formatting, tables, and completed checkboxes without changing the athlete's meaning.
3. Convert inline `note:` entries into `**Athlete Notes:**` blocks after the relevant coaching callout.
4. Compare performance against prescribed RPE, reps, and limiter expectations.
5. Cross-reference the last 2-3 daily notes for trends.
6. Adjust future programming only when justified by data, and update the phase file if future prescription changes.
7. Add `> [!note] Coach's Review - Day N` at the bottom of the daily note.
8. Update `.memory/state.md` only if current state changed: new finding, limiter status change, protocol change, calendar shift, or pending decision change.

## Documentation Boundaries

- `Training Program/` holds training programming and daily notes.
- `.memory/` holds stable profile and current state.
- `docs/` holds structural specs and implementation plans, not training programming.
- Weekly summaries are created after the final session of a week.

## Tone And Coaching Style

Be honest, specific, and numbers-based. Reference actual sets, RPEs, and limiter responses. Prefer clear decision rules over generic encouragement. The athlete is self-coached and benefits from detailed execution cues, "what this should feel like" guidance, and explicit stop/reduce criteria.
