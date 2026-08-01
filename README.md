# Igor Albuquerque Skills

Skills open source para assistentes de IA que suportam arquivos `SKILL.md`.

Versão em inglês abaixo: [English](#english)

## Português

Este repositório reúne skills prontas para usar em assistentes de IA de programação. A ideia é simples: instalar uma vez e dar ao seu assistente instruções melhores para tarefas específicas, como revisar código ou montar planos de trabalho.

As skills foram escritas para serem práticas, diretas e independentes de provedor. Elas evitam depender de um modelo, empresa, editor ou plataforma específica.

## Skills Disponíveis

- `code-review`: revisão de código pragmática, focada em bugs, regressões, riscos de segurança, testes ausentes e problemas reais de manutenção.
- `pragmatic-planning`: planejamento direto e amigável para TDAH, ajudando a transformar ideias confusas em próximas ações claras.

## Como Instalar

Clone este repositório em uma pasta que seu assistente de IA consiga ler.

Para assistentes que leem skills em `~/.agents/skills`:

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/igorcalbuquerque/igoralbuquerqueskills.git ~/.agents/skills/igoralbuquerqueskills
```

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
- "Me ajude a transformar essas ideias em um plano."
- "Quebre esse projeto em próximas ações simples."

O assistente deve escolher a skill certa quando o pedido combinar com a descrição dela.

## Estrutura

Cada skill fica em uma pasta própria com um arquivo `SKILL.md`:

```text
code-review/SKILL.md
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

---

## English

Open source skills for AI coding assistants that support `SKILL.md` files.

This repository contains ready-to-use skills for AI coding assistants. The goal is simple: install once and give your assistant better instructions for specific tasks, such as reviewing code or creating practical work plans.

These skills are practical, direct, and provider-agnostic. They avoid depending on a specific model, company, editor, or platform.

## Available Skills

- `code-review`: pragmatic code review focused on bugs, regressions, security risks, missing tests, and real maintainability issues.
- `pragmatic-planning`: direct, ADHD-friendly planning that turns messy ideas into clear next actions.

## Installation

Clone this repository into a directory your AI assistant can read.

For assistants that scan `~/.agents/skills`:

```bash
mkdir -p ~/.agents/skills
git clone https://github.com/igorcalbuquerque/igoralbuquerqueskills.git ~/.agents/skills/igoralbuquerqueskills
```

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

## How To Use

After installation, ask your assistant normally:

- "Review this PR."
- "Do a code review of this diff."
- "Help me turn these ideas into a plan."
- "Break this project into simple next actions."

The assistant should choose the right skill when your request matches the skill description.

## Structure

Each skill lives in its own directory with a `SKILL.md` file:

```text
code-review/SKILL.md
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
