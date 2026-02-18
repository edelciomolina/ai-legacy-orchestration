ESTE ARQUIVO É UM SCRIPT DE BOOTSTRAP ÚNICO. 
NÃO modifique a lógica da aplicação.
Crie apenas arquivos de estrutura Brain.

Sua missão:
Analise este repositório e implemente um Brain estruturado de IA usando:

- .github/agents/
- .github/instructions/
- .github/adr/
- .github/devlog/
- .github/pull_request_template.md

Regras de linguagem:
- Todo conteúdo de documentação deve estar em pt-BR.
- Nomes de arquivos e pastas devem permanecer em inglês.

Limites rígidos:
- Máximo 8 agentes (incluindo orquestrador).
- Máximo 6 arquivos de instrução contextual.
- Exatamente 2 arquivos de instrução sempre ativas:
  - orchestration.instructions.md
  - global.instructions.md

------------------------------------------------------------
FASE 0 - DETECÇÃO DE REPOSITÓRIO (SOMENTE LEITURA)
------------------------------------------------------------

Detectar:

A) Topologia do repositório
- Projeto único ou monorepo
- Presença de /packages, /apps, pnpm-workspace, nx, turbo

B) Impressão das tecnologias
- Linguagem(s)
- Framework(s)
- Ferramentas de build
- Gerenciador de pacotes
- Test runner
- Lint/typecheck
- Workflows de CI

C) Classificar tipo primário:
A: Console
B: Integração / Sincronização
C: Frontend apenas
D: Backend API apenas
E: Fullstack
F: Monorepo

D) Detectar responsabilidades por evidência estrutural:
- Regras de negócio
- Integrações / jobs / filas
- IA / LLM / embeddings
- UI / frontend
- API / backend
- Banco de dados
- Observabilidade

Não crie arquivos ainda.

------------------------------------------------------------
FASE 1 - DECISÃO DE ESTRUTURA BRAIN
------------------------------------------------------------

Criaremos:

.github/
  agents/
  instructions/

.github/
  adr/
  devlog/

------------------------------------------------------------
AGENTES (Regras de Seleção)
------------------------------------------------------------

Sempre criar:
- orchestrator.agent.md
- planner.agent.md
- reviewer.agent.md

Criar condicionalmente:

domain.agent.md (name: Domain)
→ se regras de negócio/domínio detectadas

integrations.agent.md (name: Integrations)
→ se integrações, jobs, filas, APIs externas detectadas

ai.agent.md (name: Ai)
→ se LLM, embeddings, vector DB detectados

frontend.agent.md (name: Frontend)
→ se React/Vue/Svelte/estrutura UI detectada

backend.agent.md (name: Backend)
→ se Express/Nest/API/servidor detectado

Total máximo de agentes: 8.

------------------------------------------------------------
INSTRUÇÕES
------------------------------------------------------------

Sempre criar DUAS instruções sempre ativas:

1) orchestration.instructions.md
2) global.instructions.md

Arquivos de instrução contextual apenas se relevante:

- integrations.instructions.md
- ai.instructions.md
- frontend.instructions.md
- backend.instructions.md
- database.instructions.md
- quality.instructions.md

Máximo de arquivos contextuais: 6.

------------------------------------------------------------
FASE 1.5 - POLÍTICA AUTO-ADR
------------------------------------------------------------

Se qualquer ambiguidade estrutural exigir decisão:

- Convenções de pasta conflitantes
- Múltiplas raízes de documentação
- Scripts ausentes ou inconsistentes
- Necessidade de escolher interpretação de arquitetura
- Necessidade de escolher limites de agentes
- Propriedade de monorepo pouco clara

Então:

1) Criar ADR:
.github/adr/0001-brain-bootstrap-decisions.md
(ou próximo número sequencial)

Status: Aceito

Incluir:
- Contexto
- Decisão
- Consequências
- Alternativas consideradas

2) Referenciar na entrada do DevLog.

Se não houver ambiguidade, NÃO crie ADR.

------------------------------------------------------------
FASE 2 - IMPLEMENTAÇÃO
------------------------------------------------------------

============================================================
A) CRIAR .github/agents/
============================================================

1) orchestrator.agent.md

---
name: Orchestrator
description: Coordena a execução entre agentes e aplica o protocolo Brain.
argument-hint: "Descreva a tarefa ou solicitação"
+tools:
  [
    "vscode/getProjectSetupInfo",
    "vscode/installExtension",
    "vscode/newWorkspace",
    "vscode/openSimpleBrowser",
    "vscode/runCommand",
    "vscode/askQuestions",
    "vscode/vscodeAPI",
    "vscode/extensions",
    "execute/runNotebookCell",
    "execute/testFailure",
    "execute/getTerminalOutput",
    "execute/awaitTerminal",
    "execute/killTerminal",
    "execute/createAndRunTask",
    "execute/runInTerminal",
    "execute/runTests",
    "read/getNotebookSummary",
    "read/problems",
    "read/readFile",
    "read/terminalSelection",
    "read/terminalLastCommand",
    "agent/runSubagent",
    "edit/createDirectory",
    "edit/createFile",
    "edit/createJupyterNotebook",
    "edit/editFiles",
    "edit/editNotebook",
    "search/changes",
    "search/codebase",
    "search/fileSearch",
    "search/listDirectory",
    "search/searchResults",
    "search/textSearch",
    "search/usages",
    "search/searchSubagent",
    "web/fetch",
    "web/githubRepo",
    "todo"
  ]
---

O corpo deve definir:

- Objetivo
- Quando usar (sempre como ponto de entrada)
- Algoritmo de decisão:
  1. Classificar pedido
  2. Determinar se requer planejamento
  3. Delegar a agente especializado
  4. Garantir revisão final
  5. Avaliar necessidade de ADR/DevLog
- Fluxo padrão:
  Usuário → Orquestrador → Planejador → Especialista → Revisor
- Anti-padrões
- Definition of Done

------------------------------------------------------------

2) planner.agent.md

---
name: Planner
+tools:
  [
    "vscode/getProjectSetupInfo",
    "vscode/installExtension",
    "vscode/newWorkspace",
    "vscode/openSimpleBrowser",
    "vscode/runCommand",
    "vscode/askQuestions",
    "vscode/vscodeAPI",
    "vscode/extensions",
    "execute/runNotebookCell",
    "execute/testFailure",
    "execute/getTerminalOutput",
    "execute/awaitTerminal",
    "execute/killTerminal",
    "execute/createAndRunTask",
    "execute/runInTerminal",
    "execute/runTests",
    "read/getNotebookSummary",
    "read/problems",
    "read/readFile",
    "read/terminalSelection",
    "read/terminalLastCommand",
    "agent/runSubagent",
    "edit/createDirectory",
    "edit/createFile",
    "edit/createJupyterNotebook",
    "edit/editFiles",
    "edit/editNotebook",
    "search/changes",
    "search/codebase",
    "search/fileSearch",
    "search/listDirectory",
    "search/searchResults",
    "search/textSearch",
    "search/usages",
    "search/searchSubagent",
    "web/fetch",
    "web/githubRepo",
    "todo"
  ]
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
tools: ["read","search"]
---

Responsável por:
- Segurança
- Performance
- Consistência arquitetural
- Conformidade com instruções
- Avaliar se DevLog/ADR foram considerados

------------------------------------------------------------

Criar agentes especializados apenas se heurísticos coincidirem.

Cada agente especializado deve seguir o padrão:

---
name: <AgentName>
description: <Descrição do que o agente faz>
argument-hint: "<Dica de argumento>"
+tools:
  [
    "vscode/getProjectSetupInfo",
    "vscode/installExtension",
    "vscode/newWorkspace",
    "vscode/openSimpleBrowser",
    "vscode/runCommand",
    "vscode/askQuestions",
    "vscode/vscodeAPI",
    "vscode/extensions",
    "execute/runNotebookCell",
    "execute/testFailure",
    "execute/getTerminalOutput",
    "execute/awaitTerminal",
    "execute/killTerminal",
    "execute/createAndRunTask",
    "execute/runInTerminal",
    "execute/runTests",
    "read/getNotebookSummary",
    "read/problems",
    "read/readFile",
    "read/terminalSelection",
    "read/terminalLastCommand",
    "agent/runSubagent",
    "edit/createDirectory",
    "edit/createFile",
    "edit/createJupyterNotebook",
    "edit/editFiles",
    "edit/editNotebook",
    "search/changes",
    "search/codebase",
    "search/fileSearch",
    "search/listDirectory",
    "search/searchResults",
    "search/textSearch",
    "search/usages",
    "search/searchSubagent",
    "web/fetch",
    "web/githubRepo",
    "todo"
  ]
---

O corpo deve incluir:
- Objetivo
- Quando usar
- Entradas esperadas
- Saídas produzidas
- Checklist de verificação
- Anti-padrões
- Definition of Done

============================================================
B) CRIAR .github/instructions/
============================================================

1) orchestration.instructions.md

Cabeçalho:

---
alwaysApply: true
always_on: true
trigger: always_on
applyTo: "**"
description: Protocolo de orquestração de agentes
---

Deve definir:

- Sempre classificar pedido antes de agir
- Nunca implementar sem planejamento se:
  - Nova feature
  - Alteração arquitetural
  - Mudança multi-arquivo
- Sempre passar pelo revisor antes de finalizar
- Avaliar ADR quando decisão estrutural for tomada
- Atualizar DevLog quando mudança funcional relevante
- Não ignorar agente especializado aplicável

------------------------------------------------------------

2) global.instructions.md

Cabeçalho:

---
alwaysApply: true
always_on: true
trigger: always_on
applyTo: "**"
description: Regras globais de arquitetura e funcionamento
---

Deve incluir:

- Missão do repositório
- Arquitetura detectada
- Mapa de pastas
- Comandos essenciais
- Regras de ouro (10–15)
- Segurança (princípios OWASP se aplicável)
- Política ADR
- Política DevLog
- Política PR

------------------------------------------------------------

3) Arquivos de instrução contextual (se relevante)

Cabeçalho:

---
description: Carregado ao trabalhar em <escopo>
applyTo: "<padrão glob>"
---

Incluir:
- Escopo
- Padrões
- Armadilhas
- Checklist

============================================================
C) CRIAR ESTRUTURA DE ADR
============================================================

.github/adr/README.md
.github/adr/0000-template.md

Modelo deve incluir:
- Título
- Status
- Contexto
- Decisão
- Consequências
- Alternativas consideradas
- Links

============================================================
D) CRIAR ESTRUTURA DE DEVLOG
============================================================

.github/devlog/README.md

Incluir Matriz de Decisão:

- PR → detalhe técnico
- DevLog → resumo funcional
- ADR → decisão estrutural

Regra:

Se muda como o sistema é construído → ADR.
Se muda o que o sistema faz → DevLog.
Se apenas implementação técnica → PR.

Criar:
.github/devlog/YYYY-MM.md

Adicionar entrada:

"Bootstrap do Brain criado: agentes, instruções, modelo de ADR, modelo de PR."

Se ADR criado, referenciar.

============================================================
E) CRIAR MODELO DE PR
============================================================

.github/pull_request_template.md

Incluir:

- O que / Por quê
- Como testar
- Impacto
- Riscos & rollback
- Observabilidade
- Checklist de segurança / privacidade
- Checkboxes:
  - [ ] ADR necessário?
  - [ ] DevLog atualizado?
  - [ ] Testes adicionados?

------------------------------------------------------------
FASE 3 - VALIDAÇÃO FINAL
------------------------------------------------------------

Garantir:

- Apenas agentes relevantes criados
- Apenas 2 arquivos de instrução sempre ativas existem
- Sem duplicação
- Caminhos corretos
- Limites rígidos respeitados

Imprimir resumo no chat:

1) Classificação do repositório
2) Responsabilidades detectadas
3) Agentes criados e por quê
4) Arquivos de instruções criados e por quê
5) Se Auto-ADR foi acionado
6) Arquivos criados

PARE.
