# OKR Skill

An open-source skill that helps AI coding agents define, track, and score OKRs from inside your project.

It turns fuzzy goals into one sharp Objective, 2-4 measurable Key Results, a verification harness, and a local `.okr.md` file your agent can keep updating over time.

Works with Claude Code, Cursor, Codex, or any coding agent that can read a repo file.

## What It Does

**Define OKRs**: interviews you, pushes back on vague goals, chooses an OKR period based on your actual feedback loop, and writes `.okr.md`.

**Check in**: reads `.okr.md`, updates current progress, flags KRs as `on_track`, `at_risk`, or `off_track`, and appends a dated check-in.

**Score a period**: grades each KR from 0.0 to 1.0, extracts learnings, and suggests what should roll into the next sprint or OKR period.

**Prevent OKR theater**: catches task-shaped KRs, missing baselines, vanity metrics, arbitrary quarterly planning, and too many simultaneous objectives.

## Install

Clone or copy this repo into your project.

```bash
git clone https://github.com/heathermhuang/okr-skill.git
```

Then point your agent at the skill file.

## Use with Claude Code

Put this in `CLAUDE.md` or say it directly in Claude Code.

```text
Use ./okr-skill/SKILL.md when defining, checking in on, or scoring OKRs.
Keep the project OKRs in .okr.md.
```

Example prompts.

```text
Define OKRs for this project using ./okr-skill/SKILL.md.
```

```text
Check in on .okr.md. We now have 12 weekly active teams and 2 paid pilots.
```

```text
Score this OKR period. Final results: 14 active teams, 3 pilots, 5% signup conversion.
```

## Use with Cursor

Add this to Cursor rules, for example `.cursor/rules/okr.mdc`.

```text
When I ask for goals, OKRs, check-ins, or scoring, follow okr-skill/SKILL.md.
Store and update OKRs in .okr.md at the repo root.
```

Then ask Cursor.

```text
Use the OKR skill to define a 6-week objective for this product.
```

## Use with Codex

Keep `okr-skill/SKILL.md` in the repo and include it in your prompt.

```text
Read okr-skill/SKILL.md, then create or update .okr.md for this repo.
Ask one question at a time if you need more context.
```

For check-ins.

```text
Read .okr.md and okr-skill/SKILL.md. Update the check-in based on this progress: ...
```

## File Format

The skill writes a simple markdown file with YAML frontmatter.

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
- Harness: PostHog funnel from /landing to /signup
- Period: 2 weeks (sprint)

## Check-ins

### 2026-04-15
- KR2 Sprint 1 scored 0.6. Best variant: social proof.
- Next sprint: test pricing variants.
```

## The Core Rule

The Objective is the outcome you want. Key Results are the proof that it happened.

Wrong: "Build email integration."

Right: "Get 50 teams sending weekly digests."

Shipping is activity. Adoption is evidence.

## Period Selection

The period should match your feedback loop, not the calendar.

Ask: **How long until you'll know if this worked?**

A landing page test might need 1-2 weeks. Enterprise sales might need 3 months. Product-market fit might need 6-12 weeks.

For longer objectives, use nested periods: a 3-month objective with 2-week sprint KRs.

## Full Experience

This skill is the lightweight local version.

For persistent OKR context across Claude Code, Cursor, Codex, MCP, dashboards, returning-user memory, and team-wide agent direction, use [okr.io](https://okr.io).

## License

MIT
