# Templates

## .okr.md

```yaml
---
objective: "<qualitative outcome>"
period: <duration, e.g. "6 weeks" or "2 weeks">
ends: <YYYY-MM-DD>
created: <YYYY-MM-DD>
---

## Key Results

### KR1: <measurable metric>
- Baseline: <starting value>
- Target: <goal value>
- Current: <current value>
- Status: <not_started | on_track | at_risk | off_track | done>
- Harness: <how to verify - SQL query, API call, manual check>
- Period: <duration or "sprint">

### KR2: <measurable metric>
- Baseline: <starting value>
- Target: <goal value>
- Current: <current value>
- Status: <status>
- Harness: <verification method>
- Period: <duration>

## Check-ins

### <YYYY-MM-DD>
- Overall: <status>
- KR1: <status> (<current>/<target>). <note>
- KR2: <status> (<current>/<target>). <note>
- Next: <priority action>

## Sprint Scores

### Sprint 1 (<dates>)
- KR2: <0.0-1.0> - <learning>
- Next sprint focus: <what changes>

## Final Score

### <YYYY-MM-DD>
- KR1: <0.0-1.0> - <reason>
- KR2: <0.0-1.0> - <reason>
- Average: <0.0-1.0>
- Verdict: <one line>

### Learnings
- <what worked>
- <what didn't>
- <what surprised you>

### Next Focus
<suggested objective for next period>
```

## Period Selection Guide

| Feedback Loop | Suggested Period |
|---------------|------------------|
| A/B test results | 1-2 weeks |
| User activation metrics | 2-4 weeks |
| Retention/churn | 4-8 weeks |
| Enterprise sales cycle | 8-12 weeks |
| Product-market fit | 6-12 weeks |
| Annual planning | 12 months |

Use sprint KRs (1-2 weeks) nested under longer objectives for fast iteration.

## Scoring Guide

| Score | Meaning |
|-------|---------|
| 1.0 | Target fully achieved or exceeded |
| 0.7 | Meaningful success (sweet spot for ambitious OKRs) |
| 0.5 | Partial progress |
| 0.3 | Some movement but weak traction |
| 0.0 | No meaningful progress |

## Status Guide

| Status | When to use |
|--------|-------------|
| not_started | KR created but no work begun |
| on_track | Progress ≥ 70% of expected pace, no blockers |
| at_risk | Progress 40-70% of pace, or blocker exists |
| off_track | Progress < 40%, or strategy needs to change |
| done | Target achieved |

## Good vs Bad Examples

### Objectives

Good: "Validate demand for premium pet food subscription"
Bad: "Build subscription features and launch marketing"

### Key Results

Good: "Get 200 subscribers with <5% monthly churn"
Bad: "Launch subscription feature"

### Harnesses

Good: `SELECT COUNT(*) FROM subscriptions WHERE status = 'active'`
Bad: "Check if subscriptions are working"

### Periods

Good: "2 weeks" (because we can measure conversion daily)
Bad: "Q2" (arbitrary calendar, no connection to feedback loop)
