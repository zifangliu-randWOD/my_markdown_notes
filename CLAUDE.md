# Training Program Vault

## What This Is
An Obsidian vault containing a 24-week Oly-First Periodized CrossFit training program, designed March 2026. The program runs from 2026-03-30 to 2026-09-20.

## Athlete Quick Reference
- 181cm, 92kg, 31M, right-dominant
- 4+ years bodybuilding, 2+ years CrossFit, self-coached
- Trains Mon-Fri ~1hr + 15-20min accessory, rest weekends

### Current PRs (at program start, March 2026)
- Back Squat: 190kg (low bar) | Front Squat: 160kg | Deadlift: 200kg
- Snatch: 105kg | Clean: 140kg | Jerk: ~120kg
- Bench: 110kg | Fran: 4:30

### Target PRs
- Back Squat: 200+ | Front Squat: 170+ | Snatch: 120 | C&J: 140+
- Unlock: ring muscle-ups, handstand walk

### Known Physical Limiters
- **Left knee patellar tracking issue**: pain with vertical torso/knee-forward positions under heavy load. Manageable with tempo and foot positioning. Likely VMO/quad imbalance. Left side clearly weaker than right.
- **Thoracic mobility restriction**: bilateral, worse on left. Limits front rack position — elbows can't get high enough under heavy load, left arm more rigid. Directly caps jerk dip mechanics and clean receiving position.
- **Chronic lumbar stiffness / anterior pelvic tilt**: 3-4 year history, lower lumbar region. Constraint at parallel depth during controlled front squats under load; absent at full depth with fast drop or at bodyweight. Connected to hamstring tightness. Managed with 90/90 breathing (daily warm-up from Week 2). Monitor as front squat loads climb.
- **Snatch efficiency gap**: 55% snatch-to-squat ratio (105/190). Positional/timing improvements are the biggest lever, not raw strength.

### Priority Stack
1. Olympic lifting numbers (primary driver)
2. Squat strength (supports everything)
3. Left knee / asymmetry rehab (background, non-negotiable)
4. Gymnastics unlocks (secondary)
5. Conditioning (maintained, not focused)

## Program Design
- **Approach**: Oly-First Periodization — "Position Before Load, Load Before Speed"
- **Phase 1 (Wk 1-8)**: Positional Foundation — technique volume, hypertrophy, rehab ramp-up
- **Phase 2 (Wk 9-16)**: Strength-Speed — heavier Oly, squat intensity climbs
- **Phase 3 (Wk 17-24)**: Peaking & Expression — heavy singles, test weeks
- **Deload weeks**: 4, 8, 12, 16, 20
- **Test weeks**: 8, 16, 24
- Percentages recalculated after each test week based on new maxes

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
    └── YYYY-MM-DD Day - Movement.md
```

## How to Help the Athlete
- **Program updates**: check current week/phase, read the relevant phase file, understand what's been done and what's coming. Check daily notes for RPE, knee status, and reflection notes.
- **Performance diagnosis**: compare test week results (Weeks 8, 16, 24) in `Protocols & Reference.md` PR log. Check snatch daily max log for trends. Look at weekly reflections for patterns.
- **Training compliance**: daily notes have checkboxes — count completed vs planned. Weekly reflections capture what was missed and why.
- **Knee/mobility assessment**: each daily note tracks left knee feel (1-5) and front rack feel. The PR log in Protocols & Reference has a knee pain tracker table across weeks.
- **Adjusting the program**: if the athlete asks to modify, understand which phase/week they're in, what their recent test results were, and what their reflections say. Adjust percentages, volume, or exercise selection accordingly. Never change the priority stack without discussion.

### Post-Workout Review Process
When the athlete shares a daily note with workout results (completed checkboxes, filled tracking tables, and log entries), perform this review automatically:

1. **Fix grammar and formatting** — clean up notes, fix table data (correct weights, add missing rows for extra sets), standardize language. Preserve the athlete's intent and observations.
2. **Adjust future programming if needed** — if weights were too heavy/light (RPE off target by 2+ points) or new limiters appeared, update upcoming sessions in the phase file. Note what was changed and why.
3. **Add Coach's Review** (`> [!note] Coach's Review — Day N`) at the bottom of the daily note:
   - Analyze each lift's performance vs expectations (RPE target vs actual, completed vs prescribed)
   - Note emerging patterns across sessions (e.g., consistent weight overestimation, left-right asymmetry trends)
   - Flag concerns about knee status, mobility, or recovery
   - Summarize what was adjusted and what to watch for in upcoming sessions
   - Keep it honest and specific — reference actual numbers, not generic encouragement
4. **Cross-reference recent sessions** — check the last 2-3 daily notes for trends (is RPE trending up/down? Is knee status stable? Are the same issues recurring?)

## Conventions
- All percentages reference current test maxes (updated after Weeks 8, 16, 24)
- Daily notes use frontmatter: date, week, phase, day, training, tags
- Checkboxes (`- [ ]`) for completion tracking (obsidian-tasks compatible)
- Callout blocks (`> [!note]`) for weekly reflections
- RPE scale: 1-10 (10 = max effort)
- Knee pain scale: 1-5 (5 = no pain)
- Front rack feel: 1-5 (5 = no restriction)

### Daily Note Template Requirements
Every daily training note must include:
- A **Day Focus tip** (`> [!tip]`) at the top — 2-3 sentences framing the session's intent and what to focus on
- **Coaching callout blocks** (`> [!info]-` collapsed) after each section (warm-up, each primary/secondary lift, gymnastics skill, accessories) containing:
  - **Why** this movement is in the program, tied to the athlete's specific limiters and goals
  - **How to execute** with detailed cues and setup instructions
  - **Athlete-specific notes** referencing left knee, thoracic restriction, or other relevant limiters
  - **Expected RPE/feel** at the prescribed load so the athlete can self-calibrate
- These callouts use the collapsed format (`> [!info]-`) so they don't clutter the page but are always available for reference
