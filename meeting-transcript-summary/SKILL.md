---
name: meeting-transcript-summary
description: Use when reading meeting transcripts, call notes, interview notes, or recorded discussion text to extract key points, topics, decisions, action items, open questions, and a direct ADHD-friendly summary.
---

# Meeting Transcript Summary

Use this skill to turn meeting transcripts, call notes, interview notes, or messy discussion text into a direct, practical summary that is easy to scan and act on.

The output must reduce cognitive load for pragmatic readers and people with ADHD. Make the important information visible without forcing the user to reread the whole transcript.

## Core Principles

- Be provider-agnostic. Do not mention or depend on a specific AI provider, model, tool, platform, or meeting app.
- Prioritize signal over completeness. Capture what matters, not every detail.
- Make actions visible. Separate tasks from discussion, context, and decisions.
- Be concrete. Prefer names, dates, outcomes, blockers, and next steps over vague summaries.
- Do not invent information. If an owner, deadline, decision, or context is unclear, mark it as unclear.
- Keep the response easy to scan. Use short sections, bullets, and plain language.
- Avoid motivational filler, long introductions, and generic productivity advice.

## When To Use

Use this skill when the user provides or references:

- Meeting transcripts.
- Call recordings converted to text.
- Interview notes.
- Standup notes.
- Planning or alignment meeting notes.
- Discovery calls or customer conversation notes.
- Messy discussion text that needs to become a clear summary and task list.

Do not use this skill for live meeting facilitation unless the user asks to structure notes or create an agenda from transcript-like material.

## Analysis Protocol

Before answering, identify:

1. The meeting purpose or likely objective.
2. The main topics discussed.
3. The key points under each topic.
4. Explicit decisions.
5. Proposed or implied action items.
6. Owners, deadlines, dependencies, and blockers.
7. Open questions and unresolved disagreements.
8. Important context the user may need later.

If the transcript is long or messy, do not summarize chronologically unless chronology is important. Organize by meaning and actionability.

## Default Output Structure

Use this structure unless the user asks for another format:

```markdown
**Executive Summary**
1-3 bullets with the most important takeaway.

**Main Topics**
- Topic: short explanation of what was discussed.

**Key Points**
- Point that matters.
- Point that matters.

**Decisions**
- Decision made. Owner: name or unclear. Date/context: date or unclear.

**Action Items**
- Task: concrete action. Owner: name or unclear. Due date: date or unclear.

**Open Questions**
- Question that still needs an answer.

**Risks Or Blockers**
- Risk, dependency, disagreement, or blocker.

**Important Context**
- Background detail that helps future readers understand the meeting.

**Suggested Next Step**
The single most useful next action.
```

Omit sections that are truly empty, but do not omit `Action Items` if there are tasks. If there are no tasks, write `No clear action items found.`

## Action Item Rules

- Start each task with a verb.
- Include the owner when stated.
- Include the due date when stated.
- If ownership is implied but not explicit, write `Owner: likely [name/team]` and keep the task marked as inferred.
- If a task is vague, rewrite it into the smallest useful concrete action without changing its meaning.
- Separate confirmed tasks from possible follow-ups when needed.

Use this format:

```markdown
- Task: Send the revised proposal to the client. Owner: Mariana. Due date: Friday.
- Task: Confirm the integration requirements. Owner: unclear. Due date: unclear.
- Possible follow-up: Schedule a technical review if the API scope changes. Owner: likely engineering. Due date: unclear.
```

## Handling Uncertainty

- Use `unclear` when the transcript does not provide enough information.
- Use `inferred` only when the implication is strong and useful.
- Do not turn casual ideas into confirmed decisions.
- Do not assign tasks to people unless the transcript supports it.
- If there are conflicting statements, show the conflict briefly instead of choosing a side.

## ADHD-Friendly Response Rules

- Start with the most useful summary, not context.
- Keep paragraphs short.
- Prefer bullets over prose.
- Use direct labels like `Decision`, `Task`, `Owner`, and `Due date`.
- Highlight the single next step at the end.
- Avoid dumping every minor point from the transcript.
- Make it possible to act after reading only the summary, action items, and next step.

## Quality Checklist

Before replying, verify:

- The main takeaway is obvious.
- Topics are grouped logically.
- Decisions are not mixed with discussion.
- Tasks are concrete and separated from ideas.
- Owners and deadlines are preserved or marked as unclear.
- Open questions and blockers are visible.
- The response is shorter and clearer than the transcript.
- No provider-specific language is included.

## Bad Patterns To Avoid

- Chronological summaries that hide what matters.
- Long paragraphs copied or paraphrased from the transcript.
- Generic statements like "the team discussed several things".
- Invented owners, deadlines, or decisions.
- Too many equally weighted details.
- Repeating the transcript instead of extracting structure.
- Ending without a concrete next step.
