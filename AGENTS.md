# AGENTS.md

Cross-agent instructions (Copilot, Codex, Cursor, Claude Code, and other AGENTS.md-aware tools).
GitHub Copilot's primary config is `.github/copilot-instructions.md`; this file mirrors the
essentials for agents that read `AGENTS.md`.

## Language / Idioma

**Sempre responda em português (português do Brasil).** Mantenha em inglês apenas identificadores
de código, nomes de arquivos/comandos e termos técnicos consagrados.

## Project layout

- **`src/`** — all application source code. This is where feature work, refactors, and fixes go.
- **`.agents/skills/`** — the [Matt Pocock skills](https://github.com/mattpocock/skills) library
  (SKILL.md playbooks). A single shared copy read by **both** GitHub Copilot and Cursor (and Codex).
  House rules live in `.github/copilot-instructions.md` (Copilot) and `.cursor/rules/project.mdc` (Cursor).
- Root — tooling and repo config.

## Conventions

- Load the matching skill from `.agents/skills/` before improvising; follow it.
- Build test-first (`tdd`). Plan with `to-spec` / `to-tickets`. Review with `code-review`.
- Read `CONTEXT.md` (if present) for the project's ubiquitous language and respect ADRs.
- Run `/setup-matt-pocock-skills` once per repository to wire up issue tracking and docs.
