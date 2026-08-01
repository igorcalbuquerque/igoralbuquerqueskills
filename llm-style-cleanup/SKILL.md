---
name: llm-style-cleanup
description: Use when editing AI-generated text, assistant responses, documentation, emails, or drafts to remove LLM writing patterns, overused em dashes, generic filler, formulaic phrasing, and artificial polish while preserving meaning and clarity.
---

# LLM Style Cleanup

Use this skill to make AI-generated or AI-assisted writing sound more natural, direct, and human-edited without changing its meaning.

The goal is not to make text casual. The goal is to remove recognizable LLM habits, unnecessary polish, and formulaic structure while preserving clarity, accuracy, and the author's intended tone.

## Core Principles

- Be provider-agnostic. Do not mention or depend on a specific AI provider, model, product, editor, or platform.
- Preserve meaning. Do not add, remove, soften, or strengthen claims unless the user asks for that.
- Prefer small edits. Remove the pattern without rewriting the whole text when a local edit is enough.
- Keep the user's voice. Do not replace one generic style with another.
- Prioritize readability over cleverness. Natural writing should still be clear and useful.
- Avoid overcorrecting. Some punctuation, structure, or polish is fine when it serves the text.

## When To Use

Use this skill when the user asks to:

- Remove AI tone, LLM style, chatbot voice, or generic assistant phrasing.
- Make text sound more human, natural, direct, or less robotic.
- Clean up a draft, response, document, email, README, article, or message generated with AI help.
- Reduce overused em dashes, generic transitions, artificial balance, or formulaic conclusions.
- Edit text for voice and style while preserving the original meaning.

Do not use this skill for code formatting, factual review, translation, or deep copywriting unless the user also asks to remove LLM-like writing patterns.

## Cleanup Targets

Look for these patterns and remove or rewrite them when they feel excessive, formulaic, or unnecessary:

- Overused em dashes: repeated `—` as the default rhythm of every sentence.
- Generic openings: "Sure", "Certainly", "Great question", "Absolutely", "I'd be happy to".
- Framing filler: "It's worth noting that", "It's important to note that", "In today's fast-paced world".
- Artificial contrast: "not only X, but also Y" when a simpler sentence works.
- Formulaic conclusions: "In conclusion", "Overall", "To summarize" when the ending is already clear.
- Excessive caveats: repeated "may", "might", "can help", "depending on your needs" without useful precision.
- Corporate polish: "seamlessly", "robust", "leverage", "empower", "unlock", "enhance" when vague.
- Symmetric list padding: three balanced bullets that say nearly the same thing.
- Restating the prompt: long introductions that repeat what the user already said.
- Over-explaining intent: "This ensures that" or "This helps to" after obvious statements.

## Rewrite Rules

- Replace repeated em dashes with periods, commas, colons, parentheses, or shorter sentences when appropriate.
- Delete filler openings unless they add real tone or relationship context.
- Convert vague qualifiers into specific wording, or remove them if they do not change the meaning.
- Break predictable LLM cadence by varying sentence length naturally.
- Prefer concrete verbs over abstract assistant language.
- Keep useful structure, headings, and lists when they improve scanability.
- Do not flatten personality. If the original has humor, warmth, urgency, or authority, preserve it.
- Do not remove all nuance. Keep caveats that are legally, technically, or factually important.

## Output Modes

If the user asks for a rewrite, return only the cleaned-up version unless comparison is useful.

If the user asks what changed, use this structure:

```markdown
**Cleaned Version**
Edited text.

**What Changed**
- Removed repeated LLM-style phrasing.
- Replaced unnecessary em dashes with cleaner punctuation.
- Preserved the original meaning and tone.
```

If the text is long, preserve the original section order and headings unless they are part of the problem.

## Before And After Examples

### Em Dash Overuse

Before:

```text
This workflow is simple — it keeps the team aligned — and it reduces confusion — especially during handoffs.
```

After:

```text
This workflow keeps the team aligned and reduces confusion, especially during handoffs.
```

### Generic Assistant Voice

Before:

```text
Great question. It's important to note that this approach can help improve productivity by allowing teams to better leverage their existing processes.
```

After:

```text
This approach can improve productivity by fitting into the team's existing process.
```

### Formulaic Balance

Before:

```text
The tool is not only useful for planning, but also for execution, making it a robust solution for teams of all sizes.
```

After:

```text
The tool supports planning and execution for teams that need both in one place.
```

## Quality Checklist

Before replying, verify:

- The meaning is unchanged.
- The text sounds edited, not generically rewritten.
- Repeated em dashes and formulaic transitions are reduced.
- Filler openings and unnecessary conclusions are removed.
- Technical accuracy and important caveats are preserved.
- The final text matches the likely audience and context.
- No provider-specific language is included.

## Bad Patterns To Avoid

- Rewriting everything just to make it different.
- Making professional text too casual.
- Removing all structure when headings or bullets help.
- Replacing clear wording with slang or forced personality.
- Deleting factual caveats that protect accuracy.
- Adding new claims, examples, or promises not present in the source.
- Calling out that the text was AI-generated unless the user asks for that analysis.
