# CLAUDE.md / `.memory/` Split — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Migrate athlete-specific content from `CLAUDE.md` to two new memory files (`.memory/profile.md` for stable identity, `.memory/state.md` for fluid state), leaving `CLAUDE.md` as a pure workflow + project structure document.

**Architecture:** Three-file separation. CLAUDE.md gets a new "Memory Files" section pointing at `.memory/`, plus a Post-Workout Review Process step that updates state.md when reviews surface state changes. No new tooling — plain markdown migration.

**Tech Stack:** Obsidian vault (markdown), git for version control, no code dependencies.

**Spec:** `docs/specs/2026-04-24-claude-md-memory-split-design.md`

---

## File Structure

| File | Action | Purpose |
| --- | --- | --- |
| `.memory/profile.md` | CREATE | Stable athlete identity (demographics, PRs, target PRs, priority stack, program timeline) |
| `.memory/state.md` | CREATE | Current operating state (active limiters, active protocols, calendar, pending decisions, recent state notes) |
| `CLAUDE.md` | REWRITE | Slimmed to pure workflow + stable project structure; adds Memory Files section + Post-Workout Review step 5 |

No daily notes, phase files, weekly summaries, or other Training Program content is touched. Pre-execution grep confirmed zero stale "see CLAUDE.md" references in any training file.

---

## Task 1: Create `.memory/profile.md`

**Files:**
- Create: `.memory/profile.md`

- [ ] **Step 1: Write the file with full content**

```markdown
# Athlete Profile

> **Last updated:** 2026-04-24 (initial migration from CLAUDE.md)
> **Update trigger:** test weeks (Wk 8, 16, 24) when PRs are retested, OR explicit priority/schedule change discussion.

## Identity
- **Height:** 181 cm
- **Weight:** 92 kg (baseline)
- **Age:** 31
- **Sex:** M
- **Dominance:** right-dominant

## Training Background
- 4+ years bodybuilding
- 2+ years CrossFit
- Self-coached

## Schedule
- Trains Mon–Fri ~1 hr + 15–20 min accessory
- Rests weekends

## Current PRs

> Last PR retest: 2026-03 (program start)

| Lift | PR |
| --- | --- |
| Back Squat | 190 kg (low bar) |
| Front Squat | 160 kg |
| Deadlift | 200 kg |
| Snatch | 105 kg |
| Clean | 140 kg |
| Jerk | ~120 kg |
| Bench | 110 kg |
| Fran | 4:30 |

## Target PRs

| Lift | Target |
| --- | --- |
| Back Squat | 200+ |
| Front Squat | 170+ |
| Snatch | 120 |
| C&J | 140+ |

**Skill unlocks:** ring muscle-ups, handstand walk

## Priority Stack

1. Olympic lifting numbers (primary driver)
2. Squat strength (supports everything)
3. Left knee / asymmetry rehab (background, non-negotiable)
4. Gymnastics unlocks (secondary)
5. Conditioning (maintained, not focused)

## Program Timeline

- **Start:** 2026-03-30
- **End:** 2026-09-20
- **Duration:** 24 weeks (3 phases × 8 weeks)
```

- [ ] **Step 2: Verify file exists and content matches**

Run: `wc -l ".memory/profile.md"`
Expected: ~50 lines

Run: `head -5 ".memory/profile.md"`
Expected: shows the H1 + Last updated line

- [ ] **Step 3: Spot-check that the migration captured the full source content**

Run: `grep -c "190 kg\|181 cm\|92 kg\|right-dominant\|Olympic lifting" ".memory/profile.md"`
Expected: ≥4 matches (confirms key facts present)

---

## Task 2: Create `.memory/state.md`

**Files:**
- Create: `.memory/state.md`

- [ ] **Step 1: Write the file with full content**

```markdown
# Athlete State

> **Last updated:** 2026-04-24 (initial migration from CLAUDE.md, post Wk 4 Fri Coach's Review)
> **Update trigger:** every Coach's Review when state changes — new finding, limiter status change (active → managing → closing → closed), protocol added/removed/modified, calendar shift, decision created/changed/resolved.

---

## Active Limiters

### Left knee patellar tracking issue
- **Status:** managing (jerk-dip-only pattern; fix in place)
- **Pattern:** pain with vertical-torso / knee-forward positions under heavy load. Confirmed Wk 3: aggravation ONLY on jerk dip (COM forward drift). All other movements — squats, cleans, deadlifts, BSS — are 5/5 pain-free across all of Wk 3 and Wk 4.
- **Fix in place:** wider jerk stance (+5 cm outside hip-width) — now the permanent default
- **Asymmetry:** left side still weaker than right
- **Weekly corrective:** BSS at 15 kg @ 3-sec tempo (confirmed Wk 3 Sat); 17 kg test scheduled Wk 5 Wed/Fri

### Thoracic mobility restriction
- **Status:** managing (improving)
- **Pattern:** bilateral, worse on left. Limits front rack — elbows can't get high enough under heavy load, left arm more rigid. Caps jerk dip mechanics and clean receiving position.
- **Progress:** front rack elbow height visibly higher than Wk 1 baseline; clean-grip front squat now stable at 104 kg with no rounding
- **Active accessories:** thoracic extension over bench (3×10 breaths), banded overhead distraction (extra time on left), front rack stretch with barbell

### Chronic lumbar stiffness / anterior pelvic tilt (bilateral central pattern)
- **Status:** RESOLVED as of Wk 3 (2026-04-17)
- **Original pattern:** 3-4 year history, lower lumbar region
- **Resolution evidence:** constraint absent during 107 kg 5×5 front squat with 3-0-0 tempo Wk 3 Thu; held through Wk 4
- **Mechanism that resolved it:** consistent 90/90 breathing from Wk 2 + wider stance
- **Watch:** may resurface under Phase 2 loads (130 kg+)
- **Maintenance:** keep 90/90 breathing as the first item in every warm-up

### Right erector spinae chronic tonus
- **Status:** managing (chronic, not progressive — characterized 2026-04-24)
- **Pattern:** right-side lower lumbar discomfort close to spine. Pre-existing pattern that predates the program; dissipated in early Phase 1, resurfaced under peak volume Wk 3 + belt-less squatting Wk 4 Mon/Thu.
- **Diagnostic results (Wk 4 Fri 4-test self-screen):** mild palpation tenderness (R 1–2/10 vs L); mild stretch on trunk flexion (superficial — feels muscular not joint); NO worsening with extension; NO change with single-leg stand; NO reproduction at bodyweight squat.
- **Verdict:** muscular, not joint, not disc, not radicular
- **Management:** belt on for working sets (BS ≥80, FS ≥75, Clean ≥85); daily right erector foam roll 60 sec + couch stretch 60 sec each side in warm-up; pre-bed cat-cow + child's pose + supine spinal rotation on training days
- **Red flags (would change plan):** sharp/electrical pain, referral into glute/leg, worse with cough/sneeze, can't tolerate sitting → stop loading and see clinician

### Anterior shoulder pull on heavy squat clean
- **Status:** closed pending Wk 5 Wed Apr 29 final 100+ kg confirm
- **Original finding (Wk 3 Fri):** stretch/pull sensation on anterior shoulder during pull-under at ~98 kg
- **Closure data (3 fresh data points absent):** Wk 3 Sat 85 kg, Wk 4 Wed 100 kg, Wk 4 Fri 90 kg
- **Verdict:** Wk 3 Friday occurrence was load + fatigue + decayed pull-under pattern — NOT structural
- **Athlete insight (Wk 4 Wed):** bar-lowering / catch-at-pelvis on the descent identified as probable additional aggravator
- **Permanent cue carried forward:** drop bar from front rack to platform at clean ≥80%

### Left hip ER (external rotation) stiffness
- **Status:** closing
- **Pattern:** "rust gear" sensation in left hip ER (Wk 3 Sat finding)
- **Progress:** reduced after pigeon stretch by Wk 4 Wed
- **Maintenance:** pigeon stretch + 90/90 hip rotation in accessory window
- **Next check:** if stays clean through Wk 5, comes off active list

### Snatch efficiency gap
- **Status:** active (technique-limited, confirmed)
- **Pattern:** 55% snatch-to-squat ratio (105/190)
- **Diagnosis:** technique-limited NOT strength-limited — 84 kg single at RPE 7 in Wk 3
- **Recent confirmation:** Wk 4 Fri 73 kg flat-RPE across all working sets confirms position quality holds at moderate load
- **Lever:** positional/timing improvements

---

## Active Permanent Protocols

These apply to every training day from Wk 5 onward (carried from Wk 4 review 2026-04-24):

1. **Belt rule:** belt ON for all working sets at: BS ≥80 kg, FS ≥75 kg, Clean ≥85 kg. Belt-less only for warm-ups and accessories.
2. **Pre-session fueling:** 500 ml water + ~30 g carbs (banana / rice cake / equivalent) in the 60–90 min pre-training window.
3. **Daily warm-up additions** (every training day, before prescribed warm-up):
   - 60 sec right lumbar erector foam roll (gentle)
   - 60 sec couch stretch each side
4. **Heavy clean stand-up breathing protocol** (any clean ≥85 kg): controlled exhale through pursed lips during the rise from the squat catch (~50% of breath out by the time standing); never Valsalva-and-release at the top; own the 1-sec pause between clean and jerk; never chain them. *Addresses the Wk 4 Fri near-syncope at 90 kg C&J.*
5. **Bar drop protocol:** at clean ≥80% drop the bar from front rack to platform between reps; do not control descent to thigh/pelvis. *Addresses bar-lowering as anterior shoulder aggravator.*
6. **Pre-bed mobility (training days only):** 5 min cat-cow + child's pose + supine spinal rotation.
7. **Wider jerk stance default:** +5 cm outside hip-width on all jerk work (rack and from clean).
8. **Bodyweight tracking:** first thing in the morning, post-pee, pre-food, naked. Baseline 92 kg.

---

## Calendar (current — adjusted for Wk 5 trip)

| Week | Dates | Notes |
| --- | --- | --- |
| Wk 5 | Apr 27–May 8 | Split by trip Apr 30–May 5; 6 lifting days (3+3) |
| Wk 6 | **May 11–17** (shifted +1 wk from original) | Full prescribed |
| Wk 7 | May 18–24 | Full prescribed |
| **Wk 8 (test week)** | **May 25–31** | Originally May 18–24; shifted +1 wk |

See `Training Program/Phase 1 - Weeks 5-8.md` (Wk 5 callout) for trip accommodation details and `Training Program/Week 5/Trip Mobility Protocol (2026-04-30 to 2026-05-05).md` for the daily trip mobility protocol.

---

## Pending Decisions

### Squat clean at the box (Wednesdays)
- **Context:** three weeks of Phase 1 ran power-clean-dominant box sessions; recurring structural gap
- **Decision needed by:** when box Wednesdays resume in Wk 6+
- **Options:**
  - (a) Clean with wider (jerk) grip at the box
  - (b) Mandatory 4–5 squat clean singles at 90–100 kg after every box Wednesday (15–20 min add-on)
  - (c) Accept box as power-clean session, add extra squat clean set to Friday and Monday
- **Coach's recommendation:** (b) — minimal friction, doesn't disrupt box schedule, adds ~15 quality squat clean reps per week
- **Note:** Wk 5 Wed Apr 29 is at the gym (not the box) — squat clean is the prescribed primary lift, no add-on needed this week

---

## Recent State Notes

- **Bodyweight 91.8 kg** (Wk 4 Thu Apr 23) — single reading, ~200 g below 92 kg baseline. Monitoring trend over coming weeks; if trends below 91 kg, food intake needs attention before Phase 2 loads start climbing.
- **Sleep deficit pattern Wk 4 Mon + Thu** — both sessions came in 1+ RPE point above target with poor sleep cited; Friday's 8-hour sleep cleared it. Watch.
```

- [ ] **Step 2: Verify file exists and is well-formed**

Run: `wc -l ".memory/state.md"`
Expected: ~110 lines

Run: `grep -c "^### " ".memory/state.md"`
Expected: ≥7 (one heading per active limiter)

- [ ] **Step 3: Spot-check coverage of each migrated section**

Run: `grep -c "Active Limiters\|Active Permanent Protocols\|Calendar\|Pending Decisions\|Recent State Notes" ".memory/state.md"`
Expected: 5 matches (one per top-level section)

---

## Task 3: Rewrite `CLAUDE.md` to slimmed version

**Files:**
- Modify: `CLAUDE.md` (full replacement — old: 138 lines mixing 4 categories; new: ~80 lines, pure workflow + structure)

- [ ] **Step 1: Replace entire CLAUDE.md with the slimmed version**

The new full content of `CLAUDE.md`:

```markdown
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
\```
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
\```

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
- **Coaching callout blocks** (`> [!info]-` collapsed) after each section (warm-up, each primary/secondary lift, gymnastics skill, accessories) containing:
  - **Why** this movement is in the program, tied to the athlete's specific limiters and goals (consult `.memory/state.md` for current limiters)
  - **How to execute** with detailed cues and setup instructions
  - **Athlete-specific notes** referencing left knee, thoracic restriction, or other relevant limiters
  - **Expected RPE/feel** at the prescribed load so the athlete can self-calibrate
- These callouts use the collapsed format (`> [!info]-`) so they don't clutter the page but are always available for reference
```

> **Note for the engineer:** the triple backticks inside the Vault Structure block above are escaped as `\`\`\`` in this plan to prevent breaking the outer code fence. When writing the actual file, use real triple backticks `\`\`\``.

- [ ] **Step 2: Verify line count and absence of athlete-specific content**

Run: `wc -l "CLAUDE.md"`
Expected: 80–90 lines (down from 138)

Run: `grep -c "190 kg\|181 cm\|92 kg\|Olympic lifting numbers (primary driver)\|Belt rule\|right-dominant" "CLAUDE.md"`
Expected: **0 matches** (no athlete-specific content; the only "kg" references should be the abstract phase descriptions if any)

If the grep returns >0, the rewrite leaked athlete content — re-check the rewrite against the spec's "Removed from CLAUDE.md" table and fix.

- [ ] **Step 3: Verify the two integration edits are present**

Run: `grep -c "Before any work, read" "CLAUDE.md"`
Expected: 1 match (Edit A — opening of How to Help the Athlete)

Run: `grep -c "Update \`.memory/state.md\` if state changed" "CLAUDE.md"`
Expected: 1 match (Edit B — Post-Workout Review Process step 5)

Run: `grep -c "## Memory Files" "CLAUDE.md"`
Expected: 1 match (new section)

---

## Task 4: Verify cross-references and acceptance criteria

**Files:** read-only audit across the vault

- [ ] **Step 1: Confirm no stale "see CLAUDE.md" pointers exist in training files**

Run: `rg "see CLAUDE\.md|see Athlete Quick Reference|see Known Physical Limiters|see Active Permanent Protocols|see Priority Stack|see Pending Structural Decisions" "Training Program/" || echo "no matches (expected)"`
Expected: `no matches (expected)`

If matches appear: fix each one to point at `.memory/state.md` or `.memory/profile.md` as appropriate.

- [ ] **Step 2: Confirm no athlete-specific limiter / protocol content lives in CLAUDE.md**

Run: `grep -E "Left knee patellar|Thoracic mobility restriction|right erector spinae|Anterior shoulder pull|Snatch efficiency gap|Belt rule:|Pre-session fueling:" "CLAUDE.md" || echo "no matches (expected)"`
Expected: `no matches (expected)`

- [ ] **Step 3: Confirm `.memory/profile.md` and `.memory/state.md` exist and are non-empty**

Run: `ls -la ".memory/" && wc -l ".memory/profile.md" ".memory/state.md"`
Expected: both files exist; profile.md ~50 lines; state.md ~110 lines

- [ ] **Step 4: Walk the spec's 7 acceptance criteria**

Manually verify each:
1. CLAUDE.md contains zero athlete-specific content (no PRs, no limiters, no protocols, no calendar dates, no priority stack) — confirmed by Step 2 above
2. CLAUDE.md is ≤ ~85 lines — confirmed by Task 3 Step 2
3. `.memory/profile.md` is readable end-to-end as a coherent athlete identity document — read it and confirm
4. `.memory/state.md` is readable end-to-end as a coherent current-state document; every section has a clear "when do I update this?" answer — read it and confirm both the per-file footer and the per-limiter status fields
5. Post-Workout Review Process in CLAUDE.md includes the new step 5 — confirmed by Task 3 Step 3
6. `## How to Help the Athlete` in CLAUDE.md begins with the "Before any work, read..." instruction — confirmed by Task 3 Step 3
7. No daily note, phase file, or weekly summary contains a stale "see CLAUDE.md" reference that should now point at memory — confirmed by Step 1 above

If any criterion fails, fix it before proceeding to Task 5.

---

## Task 5: Commit

**Files:** git operations

- [ ] **Step 1: Verify the working tree state**

Run: `git status`
Expected output should include:
- Untracked files: `.memory/profile.md`, `.memory/state.md`
- Modified: `CLAUDE.md`
- (Possibly also: untracked `docs/` if not already tracked — that's expected from earlier work)

- [ ] **Step 2: Stage the migration files**

Run:
```bash
git add CLAUDE.md ".memory/profile.md" ".memory/state.md" docs/specs/2026-04-24-claude-md-memory-split-design.md docs/plans/2026-04-24-claude-md-memory-split-plan.md docs/README.md
```

Expected: no errors. If `docs/` files are already tracked, the `git add` is a no-op for them.

- [ ] **Step 3: Commit with a meaningful message**

Run:
```bash
git commit -m "$(cat <<'EOF'
refactor: split CLAUDE.md into workflow + .memory/ files

Migrate athlete-specific content out of CLAUDE.md into two new files:
- .memory/profile.md — stable identity (demographics, PRs, target PRs, priority stack, program timeline)
- .memory/state.md — current operating state (active limiters, active protocols, calendar, pending decisions, recent state notes)

CLAUDE.md slims from 138 → ~80 lines, becomes pure workflow + project structure. Adds:
- New ## Memory Files section pointing at .memory/
- "Before any work, read .memory/..." instruction at top of How to Help the Athlete
- Post-Workout Review Process step 5: update .memory/state.md when reviews surface state changes

Spec: docs/specs/2026-04-24-claude-md-memory-split-design.md
Plan: docs/plans/2026-04-24-claude-md-memory-split-plan.md

EOF
)"
```

Expected: commit succeeds with a single commit hash.

- [ ] **Step 4: Verify the commit landed**

Run: `git log -1 --stat`
Expected output: shows the new commit with the migration files listed (3 new files: `.memory/profile.md`, `.memory/state.md`, plus `CLAUDE.md` modified, plus the docs files).

---

## Done — what to look at after execution

- Athlete reads `.memory/state.md` end-to-end to confirm it looks like a useful "what's true right now" document
- Athlete reads the slimmed `CLAUDE.md` to confirm it reads as workflow guidance, not detailed instructions
- Future Coach's Reviews now have step 5 explicitly in the workflow, so state.md stays current

If anything in the migrated content needs adjustment (a limiter status is wrong, a protocol is mis-stated, etc.), edit the relevant memory file directly — no need to re-run this plan.
