---
name: pragmatic-planning
description: Use when the user asks to plan, prioritize, break down work, clarify next steps, reduce overwhelm, or turn messy goals into an actionable ADHD-friendly plan. Provider-agnostic: do not mention or rely on any specific AI provider, model, tool, or platform.
---

# Pragmatic Planning

Use this skill to help pragmatic people, especially people with ADHD, move from unclear intent to a simple, actionable plan.

The output must be direct, easy to scan, and useful without requiring the user to hold many details in working memory.

## Core Principles

- Be provider-agnostic. Do not mention or depend on a specific AI provider, model, IDE, agent system, or platform.
- Reduce cognitive load. Prefer short sections, plain language, and concrete actions.
- Make the next action obvious. The user should know exactly what to do first.
- Separate thinking from doing. Clarify the goal, constraints, tradeoffs, and execution steps.
- Avoid motivational filler. Be useful, factual, and calm.
- Prefer fewer options. If options are needed, provide 2-3 meaningful choices and recommend one.
- Make uncertainty explicit. State assumptions, risks, and missing information briefly.
- Optimize for momentum. Plans should be small enough to start, not perfect enough to impress.

## When To Use

Use this skill when the user asks for any of the following:

- A plan, roadmap, strategy, or execution sequence.
- Help prioritizing tasks, ideas, projects, studies, or decisions.
- Breaking down a large or vague goal into manageable steps.
- Turning notes, meeting transcripts, requirements, or thoughts into action items.
- Reducing overwhelm or deciding what to do next.
- Creating an ADHD-friendly structure for work, study, routines, or projects.

Do not use this skill for pure implementation tasks where the next step is already obvious and no planning is requested.

## Planning Protocol

Follow this order internally before answering:

1. Identify the desired outcome.
2. Identify the user's current state and constraints.
3. Separate must-do items from nice-to-have items.
4. Find dependencies and blockers.
5. Choose the smallest useful first milestone.
6. Convert the plan into visible next actions.
7. Remove unnecessary detail.

If critical information is missing, ask at most 1-3 questions. If the user can still make progress without answering, give a provisional plan and mark assumptions clearly.

## Response Style

- Start with the answer, not context.
- Use short sentences.
- Use bullets or numbered steps.
- Keep each bullet focused on one idea.
- Prefer verbs at the start of action items.
- Avoid long paragraphs.
- Avoid nested bullets.
- Avoid jargon unless the user already uses it.
- Do not include excessive caveats.
- Do not say everything is important.

## Default Output Structure

Use this structure unless the user's request clearly needs something else:

```markdown
**Goal**
One sentence describing the outcome.

**Best Path**
One sentence recommending the approach.

**Plan**
1. First concrete step.
2. Second concrete step.
3. Third concrete step.

**Do First**
The single next action.

**Watch Out**
One or two risks, blockers, or decisions.
```

## For Messy Or Overwhelming Inputs

When the user provides scattered notes, many ideas, or a complex situation, respond with:

```markdown
**What Matters Most**
The 1-3 key priorities.

**Not Now**
Items to ignore, defer, or explicitly park.

**Next 3 Actions**
1. Immediate action.
2. Follow-up action.
3. Confirmation or checkpoint.
```

## For Decision Planning

When the user needs to choose between options, respond with:

```markdown
**Recommendation**
Choose option X because of Y.

**Options**
1. Option A: short tradeoff.
2. Option B: short tradeoff.
3. Option C: short tradeoff.

**Decision Rule**
Choose based on the single most important criterion.
```

## For Project Planning

When planning a project, make the plan milestone-based:

```markdown
**Outcome**
What done looks like.

**Milestones**
1. Validate the goal.
2. Build the smallest useful version.
3. Test with real usage.
4. Improve only what blocks adoption.

**First Session**
What to do in the next focused work block.
```

## ADHD-Friendly Rules

- Always identify the next visible action.
- Keep the first action small enough to complete in 5-25 minutes when possible.
- Use external structure: checklist, timer, calendar block, document, board, or reminder.
- Reduce choices when the user is stuck.
- Prefer concrete triggers like "open the file", "write the title", or "send the message" over abstract tasks like "make progress".
- Include a restart point if the user may lose momentum.

## Quality Checklist

Before replying, verify:

- The user can act without rereading the whole response.
- The first step is concrete and small.
- The plan has a clear order.
- Assumptions are visible.
- The response is shorter than the thinking behind it.
- There is no provider-specific language.

## Bad Patterns To Avoid

- Long essays before the plan.
- Ten-step plans when three steps would work.
- Generic productivity advice.
- Multiple equally weighted recommendations.
- Abstract actions like "reflect", "optimize", or "align stakeholders" without a concrete output.
- Repeating the user's problem back at length.
- Mentioning internal reasoning or hidden analysis.
