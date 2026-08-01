# Contributing

Thanks for helping improve these skills.

## Guidelines

- Keep each skill focused on a clear use case.
- Write descriptions with concrete trigger words so assistants know when to use the skill.
- Avoid depending on a specific provider, model, IDE, or hosted service unless the skill is explicitly about that tool.
- Prefer direct, actionable instructions over broad advice.
- Keep examples short and easy to adapt.

## Skill Format

Each skill should live in its own directory:

```text
skill-name/SKILL.md
```

Use frontmatter like this:

```markdown
---
name: skill-name
description: Use when the user asks for a specific thing this skill handles.
---
```

The `name` should match the directory name and use lowercase hyphen-separated words.
