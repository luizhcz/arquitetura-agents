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

Invoque com `/<nome>` no chat do Agent, ou deixe carregar sozinha quando a tarefa combinar.

### Planejamento & specs

| Skill | O que faz |
|---|---|
| `grill-me` | Entrevista implacável para afiar um plano ou design **antes** de escrever código. |
| `grill-with-docs` | Igual ao `grill-me`, mas vai gerando ADRs e glossário ao longo da conversa. |
| `to-spec` | Transforma a conversa atual numa **spec** e publica no issue tracker (sem entrevista, só síntese). |
| `to-tickets` | Quebra um plano/spec/conversa em **tickets** "tracer-bullet", cada um declarando suas dependências. |
| `to-questionnaire` | Transforma uma decisão que você não consegue responder num **questionário** para outra pessoa preencher. |
| `research` | Investiga uma pergunta em **fontes primárias** confiáveis e salva as descobertas em Markdown no repo. |
| `wayfinder` | Planeja um trabalho **enorme** (maior que uma sessão) como um mapa de "decision tickets" resolvidos um a um. |

### Construção

| Skill | O que faz |
|---|---|
| `tdd` | Desenvolvimento **test-first** (red → green → refactor), com testes que valem a pena manter. |
| `implement` | Implementa um trabalho a partir de uma **spec** ou conjunto de **tickets**. |
| `prototype` | Constrói um **protótipo descartável** para responder a uma dúvida de design (lógica ou UI). |
| `diagnosing-bugs` | Loop de **diagnóstico** para bugs difíceis e regressões de performance. |
| `resolving-merge-conflicts` | Resolve **conflitos** de merge/rebase em andamento. |
| `domain-modeling` | Constrói e refina o **modelo de domínio** / linguagem ubíqua e registra ADRs. |
| `codebase-design` | Vocabulário e técnicas para desenhar **"deep modules"** e interfaces testáveis/navegáveis. |

### Qualidade & arquitetura

| Skill | O que faz |
|---|---|
| `code-review` | Revisa o diff desde um ponto fixo em **dois eixos** (padrões do repo + aderência à spec), em sub-agentes paralelos. |
| `improve-codebase-architecture` | Varre o código atrás de oportunidades de "deepening", mostra um **relatório HTML** e aprofunda a escolhida. |
| `triage` | Move issues e PRs externos por uma **máquina de estados** de triagem, gerando briefs prontos para o agente. |
| `setup-pre-commit` | Configura **pre-commit hooks** (Husky + lint-staged: Prettier, type-check, testes). |
| `git-guardrails-claude-code` | Instala hooks que **bloqueiam comandos git perigosos** (push, reset --hard, clean, branch -D…). |

### Conhecimento & colaboração

| Skill | O que faz |
|---|---|
| `handoff` | Compacta a conversa atual num **documento de handoff** para outro agente continuar. |
| `teach` | **Ensina** uma skill ou conceito novo, dentro do workspace. |
| `wait-what` | "Pare — a última mensagem não funcionou": **re-explica** o ponto de outro jeito. |
| `writing-for-agents` | Como **escrever documentos para agentes** (criar/editar skills, `AGENTS.md`, `CLAUDE.md`). |
| `ask-matt` | **Roteador**: diz qual skill ou fluxo encaixa na sua situação. |

### Utilitários

| Skill | O que faz |
|---|---|
| `wizard` | Gera um **wizard bash interativo** para passos que só um humano faz (credenciais, dashboards, cutovers). |
| `setup-matt-pocock-skills` | Configura o repo para as skills (issue tracker, labels de triagem, docs). **Rode uma vez.** |
| `migrate-to-shoehorn` | Migra testes de `as` para `@total-typescript/shoehorn` (dados parciais de teste). |
| `scaffold-exercises` | Cria estrutura de **exercícios** (seções, problemas, soluções, explicações) que passa no lint. |

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
