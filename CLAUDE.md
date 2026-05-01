# Training Program Vault

## What This Is
An Obsidian vault containing a 24-week Oly-First Periodized CrossFit training program, designed March 2026. The program runs from 2026-03-30 to 2026-09-20.

## Memory Files

This vault uses two memory files for athlete-specific content. **Read both at the start of any session before working on programming or reviews.**

- **`.memory/profile.md`** — stable athlete identity (demographics, current PRs, target PRs, priority stack, program timeline). Updated only at test weeks or by explicit decision.
- **`.memory/state.md`** — current operating state (active limiters, active protocols, calendar, pending decisions, recent state notes). Updated after every Coach's Review when state changes.

Daily notes, phase files, and weekly summaries reference these — they should not duplicate athlete-specific content inline.

## Program Design
- **Approach**: Oly-First Periodization — "Position Before Load, Load Before Speed"
- **Phase 1 (Wk 1-8)**: Positional Foundation — technique volume, hypertrophy, rehab ramp-up
- **Phase 2 (Wk 9-16)**: Strength-Speed — heavier Oly, squat intensity climbs
- **Phase 3 (Wk 17-24)**: Peaking & Expression — heavy singles, test weeks
- **Deload weeks**: 4, 8, 12, 16, 20
- **Test weeks**: 8, 16, 24
- Percentages reference current test maxes (updated after Weeks 8, 16, 24 — see `.memory/profile.md`)

## Vault Structure
```
Training Program/
├── 00 - Program Overview.md        ← Hub file: philosophy, macrocycle, links
├── Phase 1 - Weeks 1-4.md          ← Week-by-week with tracking
├── Phase 1 - Weeks 5-8.md
├── Phase 2 - Week 9.md
├── Phase 2 - Weeks 10-11.md
├── Phase 2 - Weeks 12-13.md
├── Phase 2 - Weeks 14-15.md
├── Phase 2 - Week 16.md
├── Phase 3 - Week 17.md
├── Phase 3 - Weeks 18-19.md
├── Phase 3 - Weeks 20-21.md
├── Phase 3 - Weeks 22-24.md
├── Protocols & Reference.md        ← Mobility library, gymnastics progressions, PR log
└── Week N/                          ← Daily training notes organized by week
    ├── YYYY-MM-DD Day - Movement.md
    └── Week N Summary.md            ← End-of-week analysis (created after final session)

.memory/
├── profile.md                       ← Stable athlete identity (PRs, demographics, priorities)
└── state.md                         ← Current operating state (limiters, protocols, calendar)

docs/
├── README.md
├── specs/                           ← Design documents
└── plans/                           ← Implementation plans
```

## How to Help the Athlete

**Before any work, read `.memory/state.md` for current athlete state (limiters, protocols, calendar, decisions) and `.memory/profile.md` for stable context (PRs, demographics, priority stack). Daily notes and phase files reference these — do not duplicate their contents.**

- **Program updates**: check current week/phase, read the relevant phase file, understand what's been done and what's coming. Check daily notes for RPE, knee status, and reflection notes.
- **Performance diagnosis**: compare test week results (Weeks 8, 16, 24) in `Protocols & Reference.md` PR log. Check snatch daily max log for trends. Look at weekly reflections for patterns.
- **Training compliance**: daily notes have checkboxes — count completed vs planned. Weekly reflections capture what was missed and why.
- **Knee/mobility assessment**: each daily note tracks left knee feel (1-5) and front rack feel. The PR log in Protocols & Reference has a knee pain tracker table across weeks.
- **Adjusting the program**: if the athlete asks to modify, understand which phase/week they're in, what their recent test results were (`.memory/profile.md`), and what their reflections say. Adjust percentages, volume, or exercise selection accordingly. Never change the priority stack without discussion. **When modifying exercises or progressions for future sessions, always propagate the change to the relevant phase file** (e.g., `Phase 1 - Weeks 1-4.md`) — this is the source of truth used to generate weekly sessions.

### Post-Workout Review Process
When the athlete shares a daily note with workout results (completed checkboxes, filled tracking tables, and log entries), perform this review automatically:

0. **Locate changes efficiently** — check `git diff` (unstaged) or `git diff --staged` (staged) first to see only what the athlete changed, rather than reading the full file. This saves tokens and focuses attention on the actual session data. Fall back to reading the full file only if the diff is empty or context is needed.
1. **Fix grammar and formatting** — clean up notes, fix table data (correct weights, add missing rows for extra sets), standardize language. Convert any inline athlete `note:` entries (e.g. `note: felt good`) to `**Athlete Notes:**` blocks placed after the relevant section's coaching callout. Preserve the athlete's intent and observations.
2. **Adjust future programming if needed** — if weights were too heavy/light (RPE off target by 2+ points) or new limiters appeared, update upcoming sessions in the phase file. Note what was changed and why.
3. **Add Coach's Review** (`> [!note] Coach's Review — Day N`) at the bottom of the daily note:
   - Analyze each lift's performance vs expectations (RPE target vs actual, completed vs prescribed)
   - Note emerging patterns across sessions (e.g., consistent weight overestimation, left-right asymmetry trends)
   - Flag concerns about knee status, mobility, or recovery
   - Summarize what was adjusted and what to watch for in upcoming sessions
   - Keep it honest and specific — reference actual numbers, not generic encouragement
4. **Cross-reference recent sessions** — check the last 2-3 daily notes for trends (is RPE trending up/down? Is knee status stable? Are the same issues recurring?)
5. **Update `.memory/state.md` if state changed** — if the review surfaced a new finding, closed a limiter, modified a protocol, shifted the calendar, or made/created a pending decision, edit the relevant section of `state.md` and refresh its `Last updated:` stamp. Coach's reviews stay in the daily note (history); state.md holds current state only.

## Conventions
- All percentages reference current test maxes (updated after Weeks 8, 16, 24 — see `.memory/profile.md`)
- Daily notes use frontmatter: date, week, phase, day, training, tags
- Checkboxes (`- [ ]`) for completion tracking (obsidian-tasks compatible)
- Callout blocks (`> [!note]`) for weekly reflections
- RPE scale: 1-10 (10 = max effort)
- Knee pain scale: 1-5 (5 = no pain)
- Front rack feel: 1-5 (5 = no restriction)

### Daily Note Template Requirements
Every daily training note must include:
- A **Day Focus tip** (`> [!tip]`) at the top — 2-3 sentences framing the session's intent and what to focus on
- **Coaching callout blocks** (`> [!info]-` collapsed) after each section (warm-up, each primary/secondary lift, gymnastics skill, accessories)
- These callouts use the collapsed format (`> [!info]-`) so they don't clutter the page but are always available for reference

#### Day Focus tip standard
The tip is not a generic summary of what's in the session. It must answer: *what is the one or two things the athlete should hold in mind before starting?* Useful tips include:
- The session's place in the training arc (e.g. "this is the first time you're seeing this weight — here's what to expect")
- A specific technical cue carried forward from the last session's Coach's Review
- A load-management warning if accumulated fatigue, a new finding, or a recent limiter makes an auto-regulation note necessary
- What "success" looks like for this session in concrete terms (RPE target, movement quality marker, not just "do the work")

Keep it 2–4 sentences. It should read like something a coach would say to an athlete in the 2 minutes before they touch the bar — specific, grounded in recent history, actionable.

#### Coaching callout standard
Each callout covers one movement or section. Generic execution descriptions are not sufficient. Every callout must include:

**Why this movement is in the program right now** — tied to the athlete's specific limiters and goals from `.memory/state.md`. Not "this builds leg strength" but "this is in the program because your snatch-to-squat ratio is 55% and the limiting factor is positional timing, not strength — this drill isolates the third pull without the squat catch so you can drill turnover speed in isolation." If the movement is a corrective, name the limiter it addresses and why this exercise specifically targets it.

**How to execute** — specific setup instructions and movement cues. Include: starting position, grip width or stance, tempo if prescribed, what the movement should feel like at each phase, and the 1–2 cues that distinguish a good rep from a mediocre one. Do not just describe the movement mechanically — explain what the athlete should be thinking about during it.

**Athlete-specific notes** — reference the active limiters from `.memory/state.md` as they apply to this movement. How does the left knee behave in this pattern? Does the thoracic restriction show up in the catch or overhead position? Is this movement contraindicated, modified, or specifically beneficial given the current limiter status? This section makes the callout specific to this athlete rather than generic coaching content.

**Expected feel / RPE** — what should the prescribed load feel like? Give a specific RPE and describe what that RPE feels like in this movement at this weight. Include a calibration cue: "if it feels heavier than this, here's why and what to do." This allows the athlete to self-regulate without waiting for a review.

**Stop signals or adjustment conditions** — for any movement where a limiter could be aggravated, state the specific signal to stop or modify: what sensation, at what point in the movement, means to back off. "Stop if it hurts" is not sufficient — name the sensation (sharp vs dull, localized vs diffuse, which structure) and the appropriate response.
