# Igor Albuquerque Skills

Open source skills for AI coding assistants that support `SKILL.md` files.

Versão em português abaixo: [Português](#português)

## English

This repository contains ready-to-use skills for AI coding assistants. Install them once to give your assistant clearer instructions for specific tasks, such as reviewing code or creating practical work plans.

These skills are practical, direct, and provider-agnostic. They do not depend on a specific model, company, editor, or platform.

## Available Skills

- `code-review`: pragmatic code review focused on bugs, regressions, security risks, missing tests, and maintainability issues.
- `llm-style-cleanup`: edits AI-generated or AI-assisted text to remove LLM writing patterns, overused em dashes, generic filler, and formulaic phrasing without changing the meaning.
- `meeting-transcript-summary`: direct, ADHD-friendly meeting transcript summaries with key points, topics, decisions, action items, open questions, and next steps.
- `pragmatic-planning`: direct, ADHD-friendly planning that turns messy ideas into clear next actions.

## Installation

Clone this repository into a directory your AI assistant can read.

### Claude

If your Claude client supports custom skills from `~/.claude/skills`, clone this repository there:

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/igorcalbuquerque/igoralbuquerqueskills.git ~/.claude/skills/igoralbuquerqueskills
```

Restart Claude after installing so it can reload the skills.

### Claude Code

Claude Code can use skills from `~/.claude/skills`:

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/igorcalbuquerque/igoralbuquerqueskills.git ~/.claude/skills/igoralbuquerqueskills
```

Then restart Claude Code and ask for the task normally, for example: "Review this PR" or "Help me plan this project".

### ChatGPT

ChatGPT does not automatically load local `SKILL.md` folders in every environment. You can still use these skills as reusable instructions:

```bash
git clone https://github.com/igorcalbuquerque/igoralbuquerqueskills.git
```

Then copy the content of the skill you want into your ChatGPT instructions, a project instruction, or the start of a conversation:

```text
Use the instructions from code-review/SKILL.md to review this diff.
```

### Codex

Codex environments may not automatically scan `SKILL.md` files. Clone the repository into your workspace and reference the skill file when asking for help:

```bash
git clone https://github.com/igorcalbuquerque/igoralbuquerqueskills.git
```

Example prompt:

```text
Use igoralbuquerqueskills/code-review/SKILL.md as review guidance for this change.
```

### Other Assistants

For assistants that scan `~/.agents/skills`:

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/igorcalbuquerque/igoralbuquerqueskills.git ~/.agents/skills/igoralbuquerqueskills
```

### opencode

If you use opencode, you can also reference this repository from your `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "skills": {
    "paths": ["/absolute/path/to/igoralbuquerqueskills"]
  }
}
```

Restart your assistant after installing or changing skills so it reloads them.

## How to Use

After installation, ask your assistant normally:

- "Review this PR."
- "Do a code review of this diff."
- "Remove the LLM-style wording from this draft."
- "Summarize this meeting transcript into topics, decisions, and action items."
- "Help me turn these ideas into a plan."
- "Break this project into simple next actions."

The assistant should choose the right skill when your request matches the skill description.

## Structure

Each skill lives in its own directory with a `SKILL.md` file:

```text
code-review/SKILL.md
llm-style-cleanup/SKILL.md
meeting-transcript-summary/SKILL.md
pragmatic-planning/SKILL.md
```

## Contributing

Contributions are welcome.

When contributing, keep skills:

- Clear and practical.
- Easy to read.
- Focused on one specific use case.
- Provider-agnostic whenever possible.

See `CONTRIBUTING.md` for details.

## License

MIT. See `LICENSE`.

---

## Português

Skills de código aberto para assistentes de IA que suportam arquivos `SKILL.md`.

Este repositório reúne skills prontas para uso em assistentes de IA de programação. Instale uma vez para dar ao seu assistente instruções mais claras para tarefas específicas, como revisar código ou montar planos de trabalho.

As skills foram escritas para serem práticas, diretas e independentes de provedor. Elas não dependem de um modelo, empresa, editor ou plataforma específica.

## Skills Disponíveis

- `code-review`: revisão de código pragmática, focada em bugs, regressões, riscos de segurança, testes ausentes e problemas de manutenção.
- `llm-style-cleanup`: edição de textos gerados ou assistidos por IA para remover vícios de linguagem de LLM, travessões em excesso, termos genéricos e frases formulaicas sem mudar o significado.
- `meeting-transcript-summary`: resumo direto e amigável para TDAH de transcrições de reuniões, com pontos principais, tópicos, decisões, tarefas, perguntas em aberto e próximos passos.
- `pragmatic-planning`: planejamento direto e amigável para TDAH que transforma ideias confusas em próximas ações claras.

## Como Instalar

Clone este repositório em uma pasta que seu assistente de IA consiga ler.

### Claude

Se o seu cliente Claude suporta skills em `~/.claude/skills`, clone este repositório lá:

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/igorcalbuquerque/igoralbuquerqueskills.git ~/.claude/skills/igoralbuquerqueskills
```

Reinicie o Claude depois da instalação para ele recarregar as skills.

### Claude Code

Claude Code pode usar skills em `~/.claude/skills`:

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/igorcalbuquerque/igoralbuquerqueskills.git ~/.claude/skills/igoralbuquerqueskills
```

Depois reinicie o Claude Code e peça a tarefa normalmente, por exemplo: "Revise este PR" ou "Me ajude a planejar este projeto".

### ChatGPT

O ChatGPT não carrega automaticamente pastas locais com `SKILL.md` em todos os ambientes. Mesmo assim, você pode usar estas skills como instruções reutilizáveis:

```bash
git clone https://github.com/igorcalbuquerque/igoralbuquerqueskills.git
```

Depois copie o conteúdo da skill desejada para as instruções do ChatGPT, instruções de projeto ou início de uma conversa:

```text
Use as instruções de code-review/SKILL.md para revisar este diff.
```

### Codex

Ambientes Codex podem não ler arquivos `SKILL.md` automaticamente. Clone o repositório no seu workspace e referencie o arquivo da skill ao pedir ajuda:

```bash
git clone https://github.com/igorcalbuquerque/igoralbuquerqueskills.git
```

Exemplo de prompt:

```text
Use igoralbuquerqueskills/code-review/SKILL.md como guia de revisão para esta alteração.
```

### Outros Assistentes

Para assistentes que leem skills em `~/.agents/skills`:

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/igorcalbuquerque/igoralbuquerqueskills.git ~/.agents/skills/igoralbuquerqueskills
```

### opencode

Se você usa opencode, também pode apontar para este repositório no seu `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "skills": {
    "paths": ["/caminho/absoluto/para/igoralbuquerqueskills"]
  }
}
```

Depois de instalar ou alterar uma skill, reinicie o assistente para ele recarregar os arquivos.

## Como Usar

Depois da instalação, peça normalmente ao seu assistente:

- "Revise este PR."
- "Faça uma revisão de código deste diff."
- "Remova os vícios de linguagem de LLM deste rascunho."
- "Resuma esta transcrição de reunião em tópicos, decisões e tarefas."
- "Me ajude a transformar essas ideias em um plano."
- "Quebre esse projeto em próximas ações simples."

O assistente deve escolher a skill certa quando o pedido combinar com a descrição dela.

## Estrutura

Cada skill fica em uma pasta própria com um arquivo `SKILL.md`:

```text
code-review/SKILL.md
llm-style-cleanup/SKILL.md
meeting-transcript-summary/SKILL.md
pragmatic-planning/SKILL.md
```

## Contribuindo

Contribuições são bem-vindas.

Ao contribuir, mantenha as skills:

- Claras e práticas.
- Fáceis de ler.
- Focadas em um caso de uso específico.
- Independentes de provedor sempre que possível.

Veja `CONTRIBUTING.md` para mais detalhes.

## Licença

MIT. Veja `LICENSE`.
