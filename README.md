# OKR Skill

An open-source skill that helps AI coding agents create and maintain OKRs.

Works with Claude Code, Cursor, Codex, or any agent that can read a skill file.

## What It Does

**Define**: Interviews you to create one Objective and 2-4 measurable Key Results. Pushes back on vague goals. Picks the right period based on your feedback loop.

**Check-in**: Reads `.okr.md`, updates progress, flags KRs as on_track/at_risk/off_track, recommends next actions.

**Score**: Grades each KR from 0.0 to 1.0, extracts learnings, rolls into next sprint or suggests next focus.

## Install

Copy this folder to your repo, then tell your agent:

```
Follow ./okr-skill/SKILL.md for OKR planning and check-ins.
```

Or reference it in your system prompt / rules file.

## Usage

```
Define OKRs for this project.
```

```
Check in on .okr.md - we now have 12 weekly active teams.
```

```
Score this period. Final: 14 teams, 3 pilots, 5% conversion.
```

## Period Selection

The period should match your feedback loop, not the calendar.

Ask: **"How long until you'll know if this worked?"**

- Landing page conversion? 1-2 weeks
- Enterprise sales cycle? 3 months  
- Product-market fit? 6-12 weeks

For longer objectives, use nested periods: a 3-month objective with 2-week sprint KRs.

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
- Harness: Count workspace_ids with >3 logins in past 7 days
- Period: 6 weeks

### KR2: Find winning landing page
- Baseline: 2% conversion
- Target: 8% conversion
- Current: 5%
- Status: on_track
- Harness: Posthog funnel /landing → /signup
- Period: 2 weeks (sprint)

## Check-ins

### 2026-04-15
- KR2 Sprint 1: scored 0.6. Best variant: social proof.
- Next sprint: test pricing variants.
```

## Why OKRs

The Objective is the outcome you want. Key Results are the metrics that prove you got there.

An OKR is not a todo list. "Build email integration" is a task. "Get 50 teams sending weekly digests" is a Key Result.

## Persistence

This skill works standalone with a local `.okr.md` file.

For multi-session persistence across agents and MCP integration, see [okr.io](https://okr.io).

## License

MIT
