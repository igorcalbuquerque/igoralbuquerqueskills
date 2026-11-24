---
name: postmortem
description: Use after an incident, outage, failed deploy, data loss, security event, or any production bug that hurt users, when the user asks what happened, why it happened, how to stop it happening again, or asks for a postmortem, incident report, or root cause analysis. Builds a blameless report with a sourced timeline, impact, root cause chain, and actions that change the system.
---

# Postmortem

You write a **blameless** postmortem: the goal is to find the gaps in the system that let the incident happen and close them, so the same failure cannot come back. People acted on what they knew at the time. The question is why the system let a reasonable action cause harm, and why nobody noticed sooner.

This skill is provider-agnostic. Work from the evidence the user and the environment give you: logs, commits, deploy history, alerts, tickets, chat messages, dashboards.

## Workflow

1. **Collect evidence.** Gather every source in reach: logs, commit and deploy history, CI runs, alerts, monitoring, tickets, messages. Note the timezone of each source and convert every time to one zone. Done when each phase of the incident (start, detection, mitigation, resolution) has at least one source, or you know which one is missing.
2. **Timeline.** One line per event, in order, each with its time and its source. Mark anything you deduced instead of read as `[inference]`. The four phases above are always on the timeline, even when the time is an estimate.
3. **Impact.** Who was affected, how many, for how long, and what they could not do. Say whether data was lost, corrupted, or exposed, and whether that is confirmed or still unknown. Use numbers from the sources; when there is no number, say so.
4. **Root cause.** Ask "why" from the visible failure down, one link at a time, until you reach a gap in the system: a missing test, check, guard, alert, limit, review step, or documentation. Stop there. A person's mistake is a link in the chain, never its end: the next "why" asks what let that mistake reach production. Most incidents have more than one **contributing factor**; list each one that, if absent, would have prevented or shortened the incident.
5. **Detection and response.** Two questions with their own answers: why it took the time it took to notice, and why it took the time it took to fix. These often produce the most valuable actions.
6. **Actions.** Each action changes the system: a test, a guard in code, an alert, a limit, a rollback path, a checklist step enforced by tooling. Each one names the contributing factor it closes, an owner (or `owner: TBD`), and a done-when that someone can check. Rank them by how much recurrence risk they remove for their cost. At most five; the rest go to a `+N more` line.
7. **Lesson.** One or two sentences someone could put in the project's docs or memory and that would change what the next person does. Write it as a rule with its reason.

If the incident is still ongoing, stop after the timeline and impact, say the postmortem is waiting for resolution, and list the evidence to keep (logs that rotate, temporary dashboards).

## Output Format

Use this template. Keep it to what a reader needs to understand the incident and act; it should fit on two screens.

```markdown
# Postmortem: <what users experienced, in plain words>

**Date:** YYYY-MM-DD · **Duration:** <start to resolution> · **Severity:** <project scale, or Critical/High/Medium/Low>

## Summary
<Two or three sentences: what broke, for whom, why, and how it was fixed.>

## Impact
<Who, how many, how long, what they could not do. Data lost, corrupted, or exposed: yes/no/unknown.>

## Timeline (<timezone>)
| Time | Event | Source |
|---|---|---|
| 14:02 | Deploy of `a1b2c3d` to production | deploy log |
| 14:05 | First 500 on `/checkout` | app logs |
| 14:31 | Alert fires | monitoring |
| 14:40 | Rollback to `9f8e7d6` | deploy log |

## Root cause
1. <visible failure>
2. because <...>
3. because <...> ← system gap

Contributing factors: <each one in a short clause>.

## Detection and response
- Noticed after <N min> because <...>.
- Fixed after <N min> because <...>.

## Actions
| # | Action | Closes | Owner | Done when |
|---|---|---|---|---|
| 1 | Add a migration test against a copy of the production schema | factor 1 | TBD | CI runs it on every PR |

## Lesson
<Rule + reason, one or two sentences.>
```

## Rules

- Every time and every number comes from a source. What you could not confirm is marked `[inference]` or listed as unknown, so the reader knows which parts to check.
- Name roles and systems, not people: "the deploy", "the on-call engineer", "the migration".
- Write actions as changes to the system. An action such as "be more careful" or "remember to check" is a sign the chain stopped one link too early: ask what tool or guard would make the check automatic.
- Keep secrets, tokens, and personal data out of the report, even when they appear in the logs you quote.
- If the project has a postmortem folder or template, write there and follow its format; this template is the default.
