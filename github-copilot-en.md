THIS FILE IS A ONE-TIME BOOTSTRAP SCRIPT. 
Do NOT modify application logic.
Only create Brain structure files.

Your mission:
Analyze this repository and implement a structured AI Brain using:

- .github/agents/
- .github/instructions/
- .github/adr/
- .github/devlog/
- .github/pull_request_template.md

Language rules:
- All documentation content must be in pt-BR.
- File and folder names must remain in English.

Hard limits:
- Max 8 agents (including orchestrator).
- Max 6 contextual instruction files.
- Exactly 2 always-on instruction files:
  - orchestration.instructions.md
  - global.instructions.md

------------------------------------------------------------
PHASE 0 - REPOSITORY DETECTION (READ-ONLY)
------------------------------------------------------------

Detect:

A) Repo topology
- Single project or monorepo
- Presence of /packages, /apps, pnpm-workspace, nx, turbo

B) Stack fingerprint
- Language(s)
- Framework(s)
- Build tools
- Package manager
- Test runner
- Lint/typecheck
- CI workflows

C) Classify primary type:
A: Console
B: Integration / Sync
C: Frontend-only
D: Backend API-only
E: Fullstack
F: Monorepo

D) Detect responsibilities by structural evidence:
- Business rules
- Integrations / jobs / queues
- AI / LLM / embeddings
- UI / frontend
- API / backend
- Database
- Observability

Do not create files yet.

------------------------------------------------------------
PHASE 1 - BRAIN STRUCTURE DECISION
------------------------------------------------------------

We will create:

.github/
  agents/
  instructions/

.github/
  adr/
  devlog/

------------------------------------------------------------
AGENTS (Selection Rules)
------------------------------------------------------------

Always create:
- orchestrator.agent.md
- planner.agent.md
- reviewer.agent.md

Conditionally create:

domain.agent.md (name: Domain)
→ if business/domain rules detected

integrations.agent.md (name: Integrations)
→ if integrations, jobs, queues, external APIs detected

ai.agent.md (name: Ai)
→ if LLM, embeddings, vector DB detected

frontend.agent.md (name: Frontend)
→ if React/Vue/Svelte/UI structure detected

backend.agent.md (name: Backend)
→ if Express/Nest/API/server detected

Max total agents: 8.

------------------------------------------------------------
INSTRUCTIONS
------------------------------------------------------------

Always create TWO always-on instructions:

1) orchestration.instructions.md
2) global.instructions.md

Contextual instruction files only if relevant:

- integrations.instructions.md
- ai.instructions.md
- frontend.instructions.md
- backend.instructions.md
- database.instructions.md
- quality.instructions.md

Max contextual files: 6.

------------------------------------------------------------
PHASE 1.5 - AUTO-ADR POLICY
------------------------------------------------------------

If any structural ambiguity requires decision:

- Conflicting folder conventions
- Multiple documentation roots
- Missing or inconsistent scripts
- Need to choose architecture interpretation
- Need to choose agent boundaries
- Monorepo ownership unclear

Then:

1) Create ADR:
.github/adr/0001-brain-bootstrap-decisions.md
(or next sequential number)

Status: Accepted

Include:
- Context
- Decision
- Consequences
- Alternatives considered

2) Reference it in DevLog entry.

If no ambiguity exists, do NOT create ADR.

------------------------------------------------------------
PHASE 2 - IMPLEMENTATION
------------------------------------------------------------

============================================================
A) CREATE .github/agents/
============================================================

1) orchestrator.agent.md

---
name: Orchestrator
description: Coordena a execução entre agentes e aplica o protocolo Brain.
argument-hint: "Descreva a tarefa ou solicitação"
tools: ['read','search','agent']
---

Body must define:

- Objetivo
- Quando usar (sempre como ponto de entrada)
- Algoritmo de decisão:
  1. Classificar pedido
  2. Determinar se requer planejamento
  3. Delegar a agente especializado
  4. Garantir revisão final
  5. Avaliar necessidade de ADR/DevLog
- Fluxo padrão:
  User → Orchestrator → Planner → Specialist → Reviewer
- Anti-padrões
- Definition of Done

------------------------------------------------------------

2) planner.agent.md

---
name: Planner
tools: ['read','search','edit','todo']
---

Responsável por:
- Plano técnico
- Critérios de aceite
- Identificação de riscos
- Avaliação de ADR necessário

------------------------------------------------------------

3) reviewer.agent.md

---
name: Reviewer
tools: ['read','search']
---

Responsável por:
- Segurança
- Performance
- Consistência arquitetural
- Conformidade com instructions
- Avaliar se DevLog/ADR foram considerados

------------------------------------------------------------

Create specialized agents only if heuristics matched.

Each specialized agent must follow the pattern:

---
name: <AgentName>
description: <Description of what the agent does>
argument-hint: "<Argument hint>"
tools: ['read','search','edit',...]
---

Body must include:
- Objetivo
- Quando usar
- Entradas esperadas
- Saídas produzidas
- Checklist de verificação
- Anti-padrões
- Definition of Done

============================================================
B) CREATE .github/instructions/
============================================================

1) orchestration.instructions.md

Header:

---
alwaysApply: true
always_on: true
trigger: always_on
applyTo: "**"
description: Agent orchestration protocol
---

Must define:

- Sempre classificar pedido antes de agir
- Nunca implementar sem planejamento se:
  - Nova feature
  - Alteração arquitetural
  - Mudança multi-arquivo
- Sempre passar pelo reviewer antes de finalizar
- Avaliar ADR quando decisão estrutural for tomada
- Atualizar DevLog quando mudança funcional relevante
- Não ignorar agente especializado aplicável

------------------------------------------------------------

2) global.instructions.md

Header:

---
alwaysApply: true
always_on: true
trigger: always_on
applyTo: "**"
description: Global architecture and operating rules
---

Must include:

- Missão do repositório
- Arquitetura detectada
- Mapa de pastas
- Comandos essenciais
- Regras de ouro (10–15)
- Segurança (OWASP principles se aplicável)
- Política ADR
- Política DevLog
- Política PR

------------------------------------------------------------

3) Contextual instruction files (if relevant)

Header:

---
description: Loaded when working on <scope>
applyTo: "<glob pattern>"
---

Include:
- Escopo
- Padrões
- Armadilhas
- Checklist

============================================================
C) CREATE ADR STRUCTURE
============================================================

.github/adr/README.md
.github/adr/0000-template.md

Template must include:
- Title
- Status
- Context
- Decision
- Consequences
- Alternatives considered
- Links

============================================================
D) CREATE DEVLOG STRUCTURE
============================================================

.github/devlog/README.md

Include Decision Matrix:

- PR → detalhe técnico
- DevLog → resumo funcional
- ADR → decisão estrutural

Rule:

If it changes how system is built → ADR.
If it changes what system does → DevLog.
If only technical implementation → PR.

Create:
.github/devlog/YYYY-MM.md

Add entry:

"Brain bootstrap created: agents, instructions, ADR template, PR template."

If ADR created, reference it.

============================================================
E) CREATE PR TEMPLATE
============================================================

.github/pull_request_template.md

Include:

- O que / Por que
- Como testar
- Impacto
- Riscos & rollback
- Observabilidade
- Segurança / Privacidade checklist
- Checkboxes:
  - [ ] ADR necessário?
  - [ ] DevLog atualizado?
  - [ ] Testes adicionados?

------------------------------------------------------------
PHASE 3 - FINAL VALIDATION
------------------------------------------------------------

Ensure:

- Only relevant agents created
- Only 2 always-on instruction files exist
- No duplication
- Correct paths
- Hard limits respected

Print summary in chat:

1) Repo classification
2) Responsibilities detected
3) Agents created and why
4) Instruction files created and why
5) Whether Auto-ADR triggered
6) Files created

STOP.
