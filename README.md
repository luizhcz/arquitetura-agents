# arquitetura-agents

Template base para novos projetos, já configurado com as **skills do [Matt Pocock](https://github.com/mattpocock/skills)**
rodando no **GitHub Copilot**. Clone/copie esta pasta ao iniciar um projeto: o Copilot passa a
ter os playbooks de engenharia do Matt (TDD, code review, specs, triage…) e é orientado a
trabalhar sobre o código em **`src/`**.

## Estrutura

```
.
├── .github/
│   ├── copilot-instructions.md   # regras da casa: código fica em src/, use as skills
│   └── skills/                    # 29 skills do Matt Pocock (layout que o Copilot exige)
│       ├── tdd/SKILL.md
│       ├── code-review/SKILL.md
│       └── ...
├── src/                           # ← seu código de aplicação vai aqui
├── AGENTS.md                      # espelho das regras para outros agentes (Codex, Cursor…)
├── CONTEXT.md                     # linguagem ubíqua do projeto (preencha ao começar)
└── README.md
```

## Como o Copilot enxerga as skills

O Copilot descobre skills automaticamente em `.github/skills/`. Cada skill é uma pasta cujo
**nome é igual ao campo `name`** do `SKILL.md` (requisito do Copilot) — já está tudo assim.

- **Slash command:** digite `/tdd`, `/code-review`, `/to-spec` etc. no chat do Copilot.
- **Automático:** skills como `tdd`, `code-review`, `diagnosing-bugs` carregam sozinhas quando
  a tarefa combina com a `description` delas.

Funciona no Copilot em **Agent Mode (VS Code / JetBrains)**, **Copilot CLI**, **code review** e
no **cloud agent**. Como os arquivos seguem o padrão `SKILL.md`, também funcionam em Claude Code,
Codex e Cursor (que leem `.claude/skills/`, `.agents/skills/` ou o `AGENTS.md`).

## Primeiros passos num projeto novo

1. Copie este template para a pasta do projeto novo.
2. Coloque o código da aplicação em **`src/`**.
3. No Copilot, rode uma vez: **`/setup-matt-pocock-skills`** — configura issue tracker, labels de
   triagem e locais de documentação que as skills usam.
4. Preencha o **`CONTEXT.md`** (ou rode `/domain-modeling`) com o vocabulário do projeto.
5. Comece a construir test-first com **`/tdd`**.

## Skills incluídas (29)

**Planejamento & specs:** `grill-me`, `grill-with-docs`, `to-spec`, `to-tickets`,
`to-questionnaire`, `research`, `wayfinder`

**Construção:** `tdd`, `implement`, `prototype`, `diagnosing-bugs`, `resolving-merge-conflicts`,
`domain-modeling`, `codebase-design`

**Qualidade & arquitetura:** `code-review`, `improve-codebase-architecture`, `triage`,
`setup-pre-commit`, `git-guardrails-claude-code`

**Conhecimento & colaboração:** `handoff`, `teach`, `wait-what`, `writing-for-agents`, `ask-matt`

**Utilitários:** `wizard`, `setup-matt-pocock-skills`, `migrate-to-shoehorn`, `scaffold-exercises`

> Não foram incluídas as skills `in-progress/` (ainda em desenvolvimento no repositório do Matt)
> nem as `deprecated/`.

## Atualizar as skills

As skills são **vendorizadas** (cópia local, editável). Para trazer a versão mais recente:

```bash
npx skills@latest add mattpocock/skills
```

ou re-copie de https://github.com/mattpocock/skills para `.github/skills/`.

## Créditos & licença

As skills em `.github/skills/` são de **Matt Pocock**, distribuídas sob **licença MIT**
(preservada em `.github/skills/LICENSE`). Repositório original:
https://github.com/mattpocock/skills
