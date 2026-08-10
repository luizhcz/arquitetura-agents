# arquitetura-agents

Template base para novos projetos, já configurado com as **skills do [Matt Pocock](https://github.com/mattpocock/skills)**
rodando no **GitHub Copilot** e no **Cursor** (uma cópia única, compartilhada). Clone/copie esta
pasta ao iniciar um projeto: o agente passa a ter os playbooks de engenharia do Matt (TDD, code
review, specs, triage…) e é orientado a trabalhar sobre o código em **`src/`**.

## Estrutura

```
.
├── .agents/
│   └── skills/                    # 29 skills do Matt Pocock — CÓPIA ÚNICA (Copilot + Cursor)
│       ├── tdd/SKILL.md
│       ├── code-review/SKILL.md
│       └── ...
├── .github/
│   └── copilot-instructions.md   # regras da casa do Copilot: código em src/, use as skills
├── .cursor/
│   └── rules/project.mdc          # regras da casa do Cursor (alwaysApply)
├── src/                           # ← seu código de aplicação vai aqui
├── AGENTS.md                      # espelho das regras para outros agentes (Codex, Claude Code…)
├── CONTEXT.md                     # linguagem ubíqua do projeto (preencha ao começar)
└── README.md
```

## Como as skills são descobertas

As 29 skills ficam numa **cópia única** em **`.agents/skills/`** — diretório que **tanto o
GitHub Copilot quanto o Cursor** leem nativamente (e o Codex também). Cada skill é uma pasta cujo
**nome é igual ao campo `name`** do `SKILL.md` (requisito de ambos) — já está tudo assim.

As "regras da casa" (respostas em pt-BR, código em `src/`, use as skills) ficam separadas por
ferramenta, mas com o mesmo conteúdo:

- **Copilot** → `.github/copilot-instructions.md`
- **Cursor** → `.cursor/rules/project.mdc` (`alwaysApply`)
- **Outros agentes** → `AGENTS.md`

### Invocação

- **Slash command:** digite `/` no chat do Agent e busque a skill (`/tdd`, `/code-review`,
  `/to-spec`…).
- **Automático:** o agente carrega a skill quando a tarefa combina com a `description` dela.

Funciona no Copilot em **Agent Mode (VS Code / JetBrains)**, **Copilot CLI**, **code review** e
no **cloud agent**; e no **Cursor** (editor e CLI). Como tudo segue o padrão `SKILL.md`, também
funciona em Claude Code (via `.claude/skills/` ou `AGENTS.md`).

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

e aponte a instalação para `.agents/skills/` (ou re-copie de
https://github.com/mattpocock/skills para lá). Como há **uma única cópia**, não é preciso
sincronizar nada entre ferramentas.

## Créditos & licença

As skills em `.agents/skills/` são de **Matt Pocock**, distribuídas sob **licença MIT**
(preservada em `.agents/skills/LICENSE`). Repositório original:
https://github.com/mattpocock/skills
