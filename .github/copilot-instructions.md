# Copilot instructions

House rules for GitHub Copilot (Agent Mode / CLI / code review) in this repository.
These apply to every request. Detailed, task-specific playbooks live as **skills** in
`.agents/skills/` — load the relevant one instead of improvising.

## Language / Idioma

**Sempre responda em português (português do Brasil).** Toda explicação, resumo, mensagem de
chat, descrição de PR e comentário voltado ao usuário deve ser em português. Mantenha em inglês
apenas: identificadores de código, nomes de arquivos/comandos, e termos técnicos consagrados
(ex.: commit, pull request, deploy).

## Where the code lives

- **All application source code lives in `src/`.** Treat `src/` as the project root for
  any feature work, refactor, review, or bug fix. When you explore the codebase, start there.
- Repository-level config (package manager files, linters, CI, tooling) lives at the repo root.
- Do not scatter application code outside `src/` unless a config file must sit at the root.

## How to work here

- **Prefer a skill over ad-hoc behavior.** Before writing code, check `.agents/skills/` for a
  matching playbook and follow it. Skills are invocable as slash commands (e.g. `/tdd`,
  `/code-review`) and some load automatically when the task matches their description.
- **Build features and fix bugs test-first** using the `tdd` skill (red → green → refactor).
- **Plan before building.** Turn loose requests into specs/tickets with `to-spec` / `to-tickets`,
  and pressure-test thinking with `grill-me` before committing to an approach.
- **Match the project's vocabulary.** If a `CONTEXT.md` exists at the repo root, read it so
  names in code, tests, and commits use the project's ubiquitous language. Respect any ADRs.
- **Stay aligned and concise.** Confirm intent when a request is ambiguous rather than guessing;
  don't pad responses. When reviewing, use `code-review` (standards + spec compliance).

## First-time setup

Run `/setup-matt-pocock-skills` **once per repository** to configure the issue tracker, triage
labels, and documentation locations these skills read from and write to.

## Skill catalog

Skills are grouped below. Full instructions are in each `.agents/skills/<name>/SKILL.md`.

**Planning & specs:** `grill-me`, `grill-with-docs`, `to-spec`, `to-tickets`, `to-questionnaire`,
`research`, `wayfinder`

**Building:** `tdd`, `implement`, `prototype`, `diagnosing-bugs`, `resolving-merge-conflicts`,
`domain-modeling`, `codebase-design`

**Quality & architecture:** `code-review`, `improve-codebase-architecture`, `triage`,
`setup-pre-commit`, `git-guardrails-claude-code`

**Knowledge & collaboration:** `handoff`, `teach`, `wait-what`, `writing-for-agents`, `ask-matt`

**Utilities:** `wizard`, `setup-matt-pocock-skills`, `migrate-to-shoehorn`, `scaffold-exercises`
