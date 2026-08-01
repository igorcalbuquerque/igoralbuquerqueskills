# Igor Albuquerque Skills

Open source skills for AI coding assistants that support `SKILL.md` files.

The skills in this repository are written to be portable and provider-agnostic. They avoid depending on a specific model, vendor, editor, hosted service, or platform unless the user explicitly asks for that context.

## Skills

- `code-review`: pragmatic code review focused on bugs, regressions, security risks, missing tests, and maintainability issues.
- `pragmatic-planning`: direct, ADHD-friendly planning for turning messy goals into clear next actions.

## Installation

Clone this repository into a directory scanned by your AI coding assistant.

For assistants that scan `~/.agents/skills` recursively:

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/igorcalbuquerque/igoralbuquerqueskills.git ~/.agents/skills/igoralbuquerqueskills
```

For opencode, you can also reference the cloned repository from your `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "skills": {
    "paths": ["/absolute/path/to/igoralbuquerqueskills"]
  }
}
```

Restart your assistant after installing or changing skills so it reloads them.

## Repository Structure

Each skill lives in its own directory and must include a `SKILL.md` file:

```text
code-review/SKILL.md
pragmatic-planning/SKILL.md
```

## Contributing

Contributions are welcome. Keep skills:

- Clear and practical.
- Provider-agnostic when possible.
- Focused on specific trigger cases.
- Easy to scan and use.

See `CONTRIBUTING.md` for details.

## License

MIT. See `LICENSE`.
