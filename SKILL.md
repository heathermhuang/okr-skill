---
name: okr
description: Define, track, and score OKRs. Turns fuzzy goals into measurable outcomes.
triggers:
  - plan goals
  - set goals
  - define OKRs
  - check-in
  - score OKRs
  - close period
writes_to: .okr.md
---

# OKR Skill

Create and maintain OKRs in a `.okr.md` file at the repo root. Works standalone. For multi-session persistence, MCP integration, and dashboards, see okr.io.

## The One Rule

An OKR is not a todo list.

The **Objective** is the outcome you want. It should be memorable, ambitious, and qualitative.

**Key Results** are the measurable proof that the outcome happened. They are metrics, not tasks.

Wrong: "Launch email integration" (that's a task)
Right: "Get 50 teams sending weekly digests" (that's proof the integration works)

## Period Selection

The period should match your feedback loop, not the calendar.

Ask: **"How long until you'll know if this worked?"**

- If you can measure landing page conversion in 3 days → 1-2 week period
- If you're closing enterprise deals with 90-day sales cycles → 3 month period
- If you're validating product-market fit → 6-12 week period

AI agents compress execution, not validation. You can build fast, but customer decisions still take time.

For longer objectives, use **nested periods**: a 3-month objective with 2-week sprint KRs. Score the sprints, roll learnings into the next sprint.

## File Format

```yaml
---
objective: "Validate demand for API security monitoring"
period: 6 weeks
ends: 2026-05-15
created: 2026-04-01
---

## Key Results

### KR1: Get 15 beta teams using weekly
- Baseline: 0
- Target: 15
- Current: 6
- Status: on_track
- Harness: SELECT COUNT(*) FROM (SELECT workspace_id FROM logins WHERE created_at > NOW() - INTERVAL '7 days' GROUP BY workspace_id HAVING COUNT(*) > 3)
- Period: 6 weeks

### KR2: Find winning landing page
- Baseline: 2% conversion
- Target: 8% conversion
- Current: 5%
- Status: on_track
- Harness: Posthog funnel from /landing to /signup
- Period: 2 weeks (sprint)

### KR3: Close 3 paid pilots
- Baseline: 0
- Target: 3
- Current: 1
- Status: at_risk
- Harness: Count signed agreements with payment terms attached
- Period: 6 weeks

## Check-ins

### 2026-04-15 (Sprint 1 complete)
- KR2 scored: 0.6 (5% vs 8% target). Best variant: social proof above fold.
- Rolling into Sprint 2: test pricing page variants.

### 2026-04-20
- Overall: at_risk
- KR1: on_track (6/15). Demo pipeline healthy.
- KR3: at_risk (1/3). Procurement blocked at two accounts.
- Next: Unblock procurement with CFO intros.
```

## Mode Detection

**Define** - User says: plan, goals, OKRs, roadmap, align
**Check-in** - User says: update, progress, status, review, on track
**Score** - User says: grade, score, close, learnings, retrospective

If unclear, ask: "Are we defining new OKRs, checking in on existing ones, or scoring?"

## Define Mode

Ask one question at a time:

1. What are you building?
2. Who is it for?
3. What would success look like?
4. How long until you'll know if it worked?

Push back on vague answers. "More users" → "How many? What makes someone a real user vs a signup who never returns?"

For question 4: find the feedback loop. If they say "a quarter" but the harness could return signal in a week, suggest a shorter period with sprint KRs.

Generate:

- 1 Objective (outcome, not activity)
- 2-4 Key Results (metrics, not tasks)
- For each KR: baseline, target, harness, period

The **harness** is how you verify the KR. It should be concrete enough that someone else could check it. Good: "Count rows in payments table where status = 'completed'". Bad: "Check if revenue increased".

The **period** is how long until you score this KR. Sprint KRs (1-2 weeks) for fast feedback loops. Longer periods for slow external cycles.

Write to `.okr.md`. Show the user a summary.

### Quality Check

Before saving, verify:

- Objective is outcome-oriented ("Validate demand" not "Build features")
- Each KR is measurable by the harness
- KRs are leading indicators, not vanity metrics (weekly active users > total signups)
- Total KRs ≤ 4 (focus beats coverage)
- Period matches feedback loop speed (not arbitrary calendar)

## Check-in Mode

Read `.okr.md`. For each KR:

1. Get current value (compute from data if possible, ask if not)
2. Compare to target and time elapsed in period
3. Classify: `on_track`, `at_risk`, `off_track`

Status rules:
- **on_track**: Progress ≥ 70% of expected pace, no major blockers
- **at_risk**: Progress 40-70% of pace, or blocker needs attention
- **off_track**: Progress < 40%, or KR needs scope/strategy change

For sprint KRs at period end: score them immediately and start the next sprint.

Append a dated check-in to the file. Include blockers and next actions.

## Score Mode

At period end, score each KR from 0.0 to 1.0:

- **1.0**: Target fully hit or exceeded
- **0.7**: Target meaningfully achieved (this is success for ambitious OKRs)
- **0.3-0.6**: Partial progress
- **0.0-0.2**: Missed

For numeric KRs: `score = current / target` (capped at 1.0)

For binary KRs (shipped/not shipped): 1.0 if shipped and harness passes, 0.0 if not

Don't punish ambitious misses. Do call out sandbagging if every KR hits 1.0 easily.

Extract learnings: What worked? What didn't? What would you do differently?

For sprint KRs: roll learnings into the next sprint definition.
For objective-level scoring: suggest the next focus based on what you learned.

## Anti-Patterns

**Multiple objectives**: One sharp objective beats three vague ones. If you need multiple, you probably need multiple OKR files or teams.

**Tasks disguised as KRs**: "Build onboarding flow" is a task. "Get 80% of new users to complete onboarding" is a KR.

**No harness**: If you can't verify it, it's not measurable. Define the instrumentation needed.

**Calendar-driven periods**: "Quarterly" is arbitrary. Match the period to when you'll actually have signal.

**Waterfall planning**: Don't dump 12 weeks of tasks upfront. Use sprint KRs, check in often, adapt.

**Vanity metrics**: Total signups, page views, and lines of code don't prove value. Active usage, retention, and revenue do.
