# 📘 Dicionário Técnico — 17 Agentic AI

> **Categoria:** Inteligência Artificial / Agentes / Automação  
> **Código:** 17  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** .NET / LLM / RAG / MCP / Tools / Multi-Agent Systems / Automação de Desenvolvimento  
> **Objetivo:** Consolidar os conceitos de Agentic AI e mostrar como agentes podem planejar, usar ferramentas, consultar conhecimento, manter estado, colaborar e executar workflows controlados.

---

# 1. O que é Agentic AI

Agentic AI descreve sistemas de IA capazes de perseguir um objetivo através de múltiplas etapas.

Em vez de:

```text
Prompt
 ↓
LLM
 ↓
Answer
```

temos:

```text
Goal
 ↓
Agent
 ↓
Plan
 ↓
Action
 ↓
Observation
 ↓
Decision
 ↓
Next Action
 ↓
Result
```

---

# 2. LLM x Agent

LLM:

```text
Input
 ↓
Generation
 ↓
Output
```

Agent:

```text
Goal
 ↓
Reason
 ↓
Use Tool
 ↓
Observe
 ↓
Update State
 ↓
Continue / Stop
```

O LLM pode ser um componente do agente.

---

# 3. Componentes principais

```text
Agent
├── Model
├── Instructions
├── Memory
├── Planning
├── Tools
├── Knowledge
├── Policies
├── State
└── Evaluation
```

---

# 4. Model

Pode ser:

```text
Cloud LLM
Local LLM
Specialized Model
```

A arquitetura deve abstrair o provider quando possível.

---

# 5. Instructions

Definem:

```text
role
objective
constraints
allowed tools
output format
stop conditions
```

---

# 6. Goal

Um agente deve trabalhar com objetivo claro.

Ruim:

```text
"Melhore o projeto."
```

Melhor:

```text
"Implemente a task AUTH-102 seguindo a arquitetura existente,
adicione testes e gere PR sem alterar contratos públicos."
```

---

# 7. Planning

```text
Goal
 ↓
Planner
 ↓
Tasks
 ↓
Execution
```

Exemplo:

```text
1. Ler requisitos
2. Mapear código
3. Definir impacto
4. Implementar
5. Testar
6. Revisar
7. Documentar
```

---

# 8. ReAct

Padrão conceitual:

```text
Reason
 ↓
Act
 ↓
Observe
 ↓
Reason
```

Não significa expor raciocínio interno ao usuário.

Na implementação, o importante é manter o ciclo de decisão/ação/observação.

---

# 9. Tool

Tool permite agir sobre sistemas externos.

Exemplos:

```text
Git
GitHub
Files
Database
Docker
Cloud
Search
CI/CD
Issue Tracker
```

---

# 10. Tool Calling

```text
Agent
 ↓
Select Tool
 ↓
Arguments
 ↓
Execute
 ↓
Result
```

Resultado retorna ao agente como observação.

---

# 11. Tool Contract

Cada ferramenta precisa de contrato claro.

```text
name
description
input schema
output schema
permissions
failure modes
```

---

# 12. Tool Router

```text
Task
 ↓
Router
 ├── GitHub
 ├── Files
 ├── Database
 ├── Docker
 └── Search
```

---

# 13. MCP

Model Context Protocol pode padronizar integração entre agentes e ferramentas/fontes.

```text
Agent
 ↓
MCP Client
 ↓
MCP Servers
 ├── GitHub
 ├── Files
 ├── Database
 └── Services
```

---

# 14. Connector

Connector encapsula integração.

```text
Agent
 ↓
Connector
 ↓
External System
```

---

# 15. Skill

Skill define uma capacidade reutilizável.

```text
Agent
 ↓
Skill
 ↓
Workflow
 ↓
Tools
```

Exemplo:

```text
tdd
seo-audit
research
architecture-review
```

---

# 16. Agent x Skill

```text
Agent
→ quem executa / papel

Skill
→ capacidade reutilizável
```

Exemplo:

```text
Developer Agent
+
TDD Skill
```

---

# 17. Agent x Tool

```text
Agent
→ decide

Tool
→ executa operação
```

---

# 18. Agent x Workflow

```text
Agent
→ participante

Workflow
→ sequência coordenada
```

---

# 19. Memory

Agente pode utilizar memória.

```text
Short-Term Memory
Long-Term Memory
Working State
```

---

# 20. Short-Term Memory

```text
current task
recent observations
current plan
temporary context
```

---

# 21. Long-Term Memory

Pode armazenar conhecimento persistente autorizado.

Exemplos:

```text
architecture decisions
project conventions
validated patterns
user preferences
```

Precisa de governança.

---

# 22. Working State

```text
TaskId
CurrentStep
CompletedSteps
Artifacts
Errors
PendingActions
```

Permite retomar workflow.

---

# 23. RAG

RAG fornece conhecimento externo.

```text
Agent
 ↓
Retriever
 ↓
Knowledge Base
 ↓
Evidence
```

---

# 24. Agentic RAG

```text
Question
 ↓
Agent
 ↓
Choose Source
 ├── Vector DB
 ├── SQL
 ├── Files
 ├── Git
 └── Web
 ↓
Evidence
 ↓
Answer
```

---

# 25. Classic RAG x Agentic RAG

Classic:

```text
fixed retrieval
```

Agentic:

```text
agent chooses retrieval strategy
```

---

# 26. Multi-Agent

```text
Orchestrator
├── Requirements Agent
├── Architect Agent
├── Developer Agent
├── Tester Agent
├── Reviewer Agent
└── Documentation Agent
```

---

# 27. Specialized Agents

Cada agente deve ter responsabilidade delimitada.

Evitar:

```text
one agent does everything
```

Preferir:

```text
specialized roles
+
clear handoffs
```

---

# 28. Orchestrator

```text
Goal
 ↓
Orchestrator
 ↓
Select Agent
 ↓
Collect Result
 ↓
Next Agent
```

---

# 29. Requirements Agent

Responsabilidades:

```text
understand request
identify ambiguities
define scope
acceptance criteria
constraints
```

Saída:

```text
REQUIREMENTS.md
```

---

# 30. Architect Agent

Responsabilidades:

```text
architecture drivers
boundaries
technology choices
trade-offs
ADRs
diagrams
```

Saída:

```text
ARCHITECTURE_PLAN.md
```

---

# 31. Tech Lead Agent

Responsabilidades:

```text
break architecture into tasks
sequence work
dependencies
technical standards
```

Saída:

```text
EXECUTION_PLAN.md
```

---

# 32. Developer Agent

```text
Task
 ↓
Code
 ↓
Tests
 ↓
Local Validation
```

Não deve ignorar arquitetura existente.

---

# 33. Tester Agent

```text
Requirements
 ↓
Test Scenarios
 ↓
Unit / Integration / E2E
 ↓
Report
```

---

# 34. Reviewer Agent

Verifica:

```text
correctness
architecture
security
performance
maintainability
tests
```

---

# 35. Documentation Agent

Atualiza:

```text
README
architecture docs
API docs
ADRs
runbooks
release notes
```

---

# 36. Security Agent

Pode verificar:

```text
secrets
dependencies
auth
authorization
input validation
misconfiguration
```

---

# 37. DevOps Agent

Pode cuidar de:

```text
Docker
CI/CD
IaC
deploy
observability
environment configuration
```

---

# 38. Agent Handoff

```text
Requirements Agent
 ↓
Requirements Artifact
 ↓
Architect Agent
```

O handoff deve ser explícito e versionado.

---

# 39. Artifact-Driven Workflow

Em vez de depender apenas de conversa:

```text
Agent
 ↓
Artifact
 ↓
Next Agent
```

Exemplos:

```text
REQUIREMENTS.md
ARCHITECTURE_PLAN.md
EXECUTION_PLAN.md
TEST_REPORT.md
REVIEW_REPORT.md
```

---

# 40. Workflow completo

```text
USER
 ↓
REQUIREMENTS
 ↓
ARCHITECT
 ↓
TECH LEAD
 ↓
DEVELOPER
 ↓
TESTER
 ↓
REVIEWER
 ↓
DOCUMENTATION
 ↓
DONE
```

---

# 41. Quality Gates

Entre agentes:

```text
Agent
 ↓
Artifact
 ↓
Quality Gate
 ├── PASS → next
 └── FAIL → return
```

---

# 42. Requirements Gate

Verifica:

```text
scope
acceptance criteria
constraints
ambiguities
```

---

# 43. Architecture Gate

```text
boundaries
security
data
observability
testing
deployment
trade-offs
```

---

# 44. Development Gate

```text
build
tests
lint
architecture tests
security checks
```

---

# 45. Review Gate

```text
requirements satisfied?
architecture respected?
tests adequate?
documentation updated?
```

---

# 46. Loop

Agentes podem iterar.

```text
Developer
 ↓
Tester
 ↓ FAIL
Developer
 ↓
Fix
 ↓
Tester
```

Limitar loops.

---

# 47. Max Steps

Configurar:

```text
maxSteps
```

Evita execução infinita.

---

# 48. Timeout

```text
Agent Task
 ↓
Timeout
 ↓
Stop / Retry / Escalate
```

---

# 49. Token Budget

Cada agente pode possuir orçamento.

```text
Planner → small
Developer → medium/high
Reviewer → medium
```

A política depende da tarefa.

---

# 50. Model Routing

```text
Task
 ↓
Router
 ├── Fast Model
 ├── Strong Model
 └── Local Model
```

---

# 51. Local Model

Pode ser utilizado para:

```text
classification
simple extraction
summaries
local/private workflows
```

dependendo da capacidade.

---

# 52. Strong Model

Reservar para:

```text
architecture
complex reasoning
large refactoring
difficult debugging
```

quando necessário.

---

# 53. Human in the Loop

```text
Agent
 ↓
Critical Decision
 ↓
Human Approval
 ↓
Continue
```

---

# 54. Ações que podem exigir aprovação

Exemplos:

```text
production deployment
delete resource
merge to main
send external communication
change billing
rotate secrets
database destructive migration
```

---

# 55. Permission Model

```text
Agent
 ↓
Policy
 ↓
Allowed Tools
 ↓
Allowed Actions
```

---

# 56. Least Privilege

Um Documentation Agent não precisa:

```text
delete production database
```

Permissões devem corresponder à função.

---

# 57. Read x Write

Classificar ferramentas:

```text
READ
WRITE
DESTRUCTIVE
```

---

# 58. Approval Boundary

```text
READ
→ automatic

WRITE
→ policy dependent

DESTRUCTIVE
→ explicit approval
```

A política real depende do ambiente.

---

# 59. Idempotência

Ações repetidas não devem duplicar efeitos.

Exemplo:

```text
Create PR
 ↓
PR already exists?
 ├── Yes → reuse
 └── No → create
```

---

# 60. Retry

```text
Transient Failure
 ↓
Backoff
 ↓
Retry
```

Não repetir ação destrutiva cegamente.

---

# 61. Compensation

Se workflow falhar:

```text
Step A
Step B
Step C FAIL
 ↓
Compensate B/A if required
```

---

# 62. Checkpoint

```text
Step 1 ✓
Step 2 ✓
Checkpoint
Step 3
```

Permite retomada.

---

# 63. Event-Driven Agents

```text
GitHub Issue Created
 ↓
Event
 ↓
Agent Workflow
```

Outros gatilhos:

```text
PR opened
build failed
document uploaded
incident detected
```

---

# 64. Scheduled Agents

```text
Schedule
 ↓
Agent
 ↓
Task
```

Exemplo:

```text
daily dependency review
weekly architecture report
```

---

# 65. Reactive Agent

```text
Event
 ↓
Agent
 ↓
Analyze
 ↓
Action
```

---

# 66. Proactive Agent

```text
Periodic Check
 ↓
Detect Condition
 ↓
Recommendation
```

Precisa de limites para não executar ações indesejadas.

---

# 67. Code Agent

```text
Issue
 ↓
Read Repository
 ↓
Plan
 ↓
Branch
 ↓
Implement
 ↓
Test
 ↓
Commit
 ↓
Push
 ↓
PR
```

---

# 68. GitFlow Agent

```text
develop
 ↓
feature/task-123
 ↓
commit
 ↓
push
 ↓
PR
 ↓
CI
```

---

# 69. PR Review Agent

```text
Diff
 ↓
Review
 ├── bugs
 ├── architecture
 ├── security
 ├── tests
 └── maintainability
 ↓
Report
```

---

# 70. CI Failure Agent

```text
Pipeline Failure
 ↓
Collect Logs
 ↓
Classify
 ↓
Find Root Cause
 ↓
Recommend / Fix
```

---

# 71. Incident Agent

```text
Alert
 ↓
Logs + Metrics + Traces
 ↓
Analysis
 ↓
Hypothesis
 ↓
Runbook
 ↓
Human Approval / Action
```

---

# 72. RAG Agent

```text
Question
 ↓
Plan Retrieval
 ↓
Search Sources
 ↓
Evaluate Evidence
 ↓
Answer with Sources
```

---

# 73. Database Agent

Pode:

```text
inspect schema
generate query
explain plan
analyze migrations
```

Writes devem seguir política rigorosa.

---

# 74. Cloud Agent

```text
IaC
 ↓
Plan
 ↓
Security Review
 ↓
Cost Review
 ↓
Approval
 ↓
Apply
```

---

# 75. Observability Agent

```text
Metrics
Logs
Traces
 ↓
Agent
 ↓
Anomaly / Explanation
```

---

# 76. Documentation Agent

```text
Code Changes
 ↓
Detect Documentation Impact
 ↓
Update Docs
```

---

# 77. Content Agent

```text
Topic
 ↓
Research
 ↓
Draft
 ↓
Review
 ↓
Human Approval
```

---

# 78. Agent Communication

Evitar agentes trocando mensagens livres sem contrato.

Preferir:

```text
Typed Artifact
Structured Result
Defined Schema
```

---

# 79. Structured Output

```text
Agent
 ↓
JSON Schema
 ↓
Validation
 ↓
Next Step
```

---

# 80. Agent State Model

Exemplo:

```json
{
  "taskId": "AUTH-102",
  "status": "testing",
  "completedSteps": 5,
  "pendingSteps": 2
}
```

---

# 81. Decision Layer

```text
Agent
 ↓
Decision
 ↓
Policy
 ↓
Action
```

Separar decisão de execução.

---

# 82. Guardrails

```text
Input Validation
Output Validation
Tool Policy
Budget
Max Steps
Timeout
Approval
```

---

# 83. Prompt Injection

Especialmente em agentes com RAG/tools:

```text
External Content
 ↓
"Delete all files"
```

Isso é dado, não autorização.

---

# 84. Tool Injection

Nunca permitir que conteúdo recuperado altere permissões do agente.

```text
Document Instructions
≠
System Policy
```

---

# 85. Secret Protection

Agente não deve:

```text
print secrets
commit secrets
send secrets to model unnecessarily
```

---

# 86. Sandboxing

Code execution deve ocorrer em ambiente controlado quando possível.

```text
Agent
 ↓
Sandbox
 ↓
Command
```

---

# 87. Audit Trail

Registrar:

```text
Agent
Task
Tool
Arguments summary
Result
Timestamp
Approval
CorrelationId
```

Sem registrar secrets.

---

# 88. Observabilidade

```text
Workflow
 ↓
Trace
 ├── Agent A
 ├── Tool X
 ├── Agent B
 └── Gate
```

---

# 89. Métricas

```text
task success rate
tool failure rate
average steps
latency
token usage
human intervention
rework rate
```

---

# 90. Agent Evaluation

Avaliar:

```text
correctness
task completion
tool selection
policy compliance
cost
latency
```

---

# 91. Golden Tasks

Criar conjunto fixo:

```text
Task
Expected Actions
Expected Result
Forbidden Actions
```

Executar regressão.

---

# 92. Deterministic Tests

Componentes devem ser testáveis sem LLM real.

```text
FakeModel
FakeTool
FakeMemory
```

---

# 93. Integration Tests

```text
Agent
 ↓
Sandbox Tools
 ↓
Test Repository
```

---

# 94. Agent Simulation

Antes de produção:

```text
Real Workflow
+
Fake Side Effects
```

Exemplo:

```text
deploy → simulated
email → draft only
delete → blocked
```

---

# 95. Multi-Agent Failure

Problemas comuns:

```text
agent loops
duplicate work
conflicting changes
context loss
unclear ownership
```

---

# 96. Ownership

Cada artifact deve possuir owner.

```text
REQUIREMENTS.md
→ Requirements Agent

ARCHITECTURE_PLAN.md
→ Architect Agent
```

---

# 97. Shared Context

Agentes devem compartilhar somente o necessário.

```text
Project Context
+
Task Context
+
Relevant Artifacts
```

Evitar carregar o repositório inteiro sem necessidade.

---

# 98. Context Engineering

Selecionar contexto é parte crítica.

```text
Retrieve
 ↓
Filter
 ↓
Rank
 ↓
Compress
 ↓
Provide
```

---

# 99. Context Window

Orçamento inclui:

```text
instructions
memory
documents
tool outputs
task
response
```

---

# 100. Context Compression

```text
Large Tool Output
 ↓
Summarize
 ↓
Relevant Facts
```

---

# 101. RTK / Output Compression

Ferramentas de resumo de terminal podem reduzir:

```text
test logs
git output
docker output
```

antes de devolver ao agente.

---

# 102. Parallel Agents

Tarefas independentes podem rodar em paralelo.

```text
Orchestrator
 ├── Security Review
 ├── Test Review
 └── Documentation Review
```

Depois:

```text
Aggregator
```

---

# 103. Não paralelizar dependências

Errado:

```text
Developer
and
Tester

at same time before code exists
```

O DAG do workflow deve respeitar dependências.

---

# 104. DAG

```text
Requirements
      ↓
Architecture
      ↓
Development
     / Tests  Docs
     \ /
Review
```

---

# 105. Agent Workflow Engine

Pode controlar:

```text
states
transitions
retry
timeout
parallelism
approval
checkpoints
```

---

# 106. State Machine

```text
PLANNED
 ↓
RUNNING
 ↓
TESTING
 ↓
REVIEW
 ↓
DONE
```

Falha:

```text
FAILED
```

---

# 107. Event Log

```text
TaskCreated
PlanGenerated
CodeChanged
TestsPassed
ReviewApproved
```

Permite rastreabilidade.

---

# 108. Agentic AI + CQRS

Conceitualmente:

```text
Agent Command
 ↓
Action Handler
 ↓
State Change

Agent Query
 ↓
Read State
```

Útil para separar leitura e ação no runtime.

---

# 109. Agentic AI + Event Sourcing

Em casos avançados:

```text
Agent Events
 ↓
Event Store
 ↓
Rebuild State
```

Só usar se houver necessidade real.

---

# 110. Agentic AI + Messaging

```text
Task
 ↓
Queue
 ↓
Agent Worker
 ↓
Result Event
```

Útil para workflows assíncronos.

---

# 111. AWS

Possível arquitetura:

```text
API
 ↓
SQS
 ↓
Agent Worker on ECS
 ↓
LLM / Tools
 ↓
SNS
```

---

# 112. Lambda

Pode executar tarefas agentic curtas e compatíveis com limites serverless.

Workflows longos podem exigir outra estratégia.

---

# 113. Step Functions

Em AWS, pode coordenar workflows explícitos:

```text
Step A
 ↓
Step B
 ↓
Approval
 ↓
Step C
```

Pode complementar agentes.

---

# 114. Azure

Equivalentes podem envolver:

```text
Service Bus
Functions
Container Apps
Durable Functions
Logic Apps
```

dependendo do cenário.

---

# 115. .NET Architecture

```text
AI/
├── Abstractions/
├── Agents/
├── Orchestration/
├── Planning/
├── Memory/
├── RAG/
├── Tools/
├── Policies/
├── Skills/
├── Evaluation/
└── Observability/
```

---

# 116. IAgent

```csharp
public interface IAgent<TInput, TOutput>
{
    Task<TOutput> ExecuteAsync(
        TInput input,
        CancellationToken cancellationToken);
}
```

---

# 117. ITool

```csharp
public interface ITool<TInput, TOutput>
{
    Task<TOutput> ExecuteAsync(
        TInput input,
        CancellationToken cancellationToken);
}
```

---

# 118. IPolicy

```csharp
public interface IActionPolicy
{
    Task<PolicyResult> AuthorizeAsync(
        AgentAction action,
        CancellationToken cancellationToken);
}
```

---

# 119. Orchestrator

```text
IWorkflowOrchestrator
 ↓
Agents
 ↓
Gates
 ↓
Artifacts
```

---

# 120. prompts.md

No Kit IA Dev:

```text
prompts.md
 ↓
Orchestrator
 ↓
Workflow
 ↓
Agents
```

Deve definir ordem e regras gerais.

---

# 121. PROJECT.md

Pode fornecer:

```text
project goals
stack
environments
architecture constraints
commands
quality rules
```

---

# 122. PROJECT_SKILLS.md

Catálogo:

```text
skill
purpose
agent
trigger
inputs
outputs
```

---

# 123. Agent Folder

```text
agents/
└── architect/
    ├── AGENT.md
    ├── prompts/
    ├── rules/
    └── templates/
```

---

# 124. Skill Folder

```text
skills/
└── tdd/
    ├── SKILL.md
    ├── references/
    ├── examples/
    └── templates/
```

---

# 125. Workflow Folder

```text
workflows/
└── feature-development/
    ├── WORKFLOW.md
    ├── gates/
    └── templates/
```

---

# 126. Quality Gate Folder

```text
quality-gates/
├── requirements/
├── architecture/
├── development/
├── testing/
└── review/
```

---

# 127. Definition of Done

```text
Requirement satisfied
+
Code
+
Tests
+
Review
+
Documentation
+
CI
```

---

# 128. Autonomous x Controlled

Níveis possíveis:

```text
Level 0 → assistant only
Level 1 → recommends actions
Level 2 → executes safe reads
Level 3 → executes controlled writes
Level 4 → autonomous within strict policies
```

Não maximizar autonomia sem necessidade.

---

# 129. Progressive Autonomy

Estratégia recomendada:

```text
Observe
 ↓
Recommend
 ↓
Execute in Sandbox
 ↓
Execute with Approval
 ↓
Automate Safe Actions
```

---

# 130. Anti-patterns

Evitar:

```text
agent with unlimited permissions
one mega-agent
no max steps
no timeout
no audit
no quality gates
tools without schemas
free-form agent handoffs
LLM output directly executing destructive actions
memory without governance
multi-agent without clear ownership
```

---

# 131. Quality Gates

- [ ] objetivo definido;
- [ ] papel do agente definido;
- [ ] ferramentas permitidas;
- [ ] permissões mínimas;
- [ ] input/output estruturados;
- [ ] max steps;
- [ ] timeout;
- [ ] token/cost budget;
- [ ] stop condition;
- [ ] human approval para ações críticas;
- [ ] audit trail;
- [ ] observabilidade;
- [ ] testes;
- [ ] evaluation dataset;
- [ ] fallback.

---

# 132. Estrutura no Kit IA Dev

```text
Kit-IA-Dev/
├── 1-Prompts/
├── 2-Agents/
├── 3-Skills/
├── 4-Templates/
├── 5-Workflows/
├── 6-Quality-Gates/
├── 7-Documentation/
└── 8-Dictionary/
    └── 17-agentic-ai.md
```

---

# 133. Workflow principal do Kit

```text
USER REQUEST
      ↓
REQUIREMENTS AGENT
      ↓
REQUIREMENTS GATE
      ↓
ARCHITECT AGENT
      ↓
ARCHITECTURE GATE
      ↓
TECH LEAD
      ↓
DEVELOPER
      ↓
TESTER
      ↓
REVIEWER
      ↓
DOCUMENTATION
      ↓
FINAL QUALITY GATE
```

---

# 134. Exemplo — Feature .NET

```text
Issue:
"Implementar refresh token"

Requirements Agent
 ↓
Acceptance Criteria

Architect
 ↓
Security / Data Design

Developer
 ↓
Implementation

Tester
 ↓
Unit + Integration

Reviewer
 ↓
Security + Architecture

Documentation
 ↓
README / API Docs
```

---

# 135. Exemplo — Falha CI

```text
CI Failed
 ↓
Agent reads logs
 ↓
Classifies error
 ↓
Finds affected project
 ↓
Proposes fix
 ↓
Runs tests
 ↓
Updates PR
```

---

# 136. Exemplo — RAG

```text
User Question
 ↓
RAG Agent
 ↓
Search Docs
 ↓
Search Code
 ↓
Aggregate Evidence
 ↓
Answer with Sources
```

---

# 137. Exemplo — Cloud

```text
Infrastructure Requirement
 ↓
Cloud Agent
 ↓
Generate IaC
 ↓
Plan
 ↓
Security Gate
 ↓
Cost Gate
 ↓
Human Approval
 ↓
Apply
```

---

# 138. Regra principal

```text
AGENT
does not equal
UNCONTROLLED AUTONOMY
```

Um sistema Agentic AI profissional precisa de:

```text
GOALS
+
TOOLS
+
STATE
+
POLICIES
+
QUALITY GATES
+
OBSERVABILITY
+
HUMAN CONTROL
```

---

# 139. Relação com outros itens

```text
01.2 - Agentic Workflow
02 - RAG
03 - Plugins
05 - Conectores e Funções
09 - Skills
10 - LLM Local
11 - CI/CD
14 - LLM vs Jev
15 - RAG System
16 - Arquitetura e Aplicações
18 - Kit IA Dev
```

---

# 140. Resumo

Agentic AI transforma o modelo de:

```text
PROMPT → RESPONSE
```

para:

```text
GOAL
 ↓
PLAN
 ↓
TOOLS
 ↓
OBSERVATIONS
 ↓
DECISIONS
 ↓
QUALITY GATES
 ↓
RESULT
```

No Kit IA Dev, agentes devem ser especializados, orientados a artifacts, limitados por políticas, testáveis e observáveis. A autonomia deve crescer progressivamente conforme o risco e a maturidade do workflow.

---

# 📁 Arquivo

```text
17-agentic-ai.md
```
