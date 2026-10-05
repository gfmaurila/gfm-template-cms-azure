# 📘 Dicionário Técnico — 18 Kit IA Dev

> **Categoria:** Engenharia de Software com IA / Agentic Development / Automação  
> **Código:** 18  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** Claude Code / Codex / Copilot / OpenCode / outras IAs de código  
> **Objetivo:** Consolidar a arquitetura, instalação, agentes, skills, workflows, quality gates, templates e regras operacionais do Kit IA Dev para reutilização em projetos de diferentes stacks.

---

# 1. O que é o Kit IA Dev

O **Kit IA Dev** é uma estrutura reutilizável para transformar uma IA de código em um fluxo organizado de engenharia de software.

A ideia não é simplesmente:

```text
Prompt
 ↓
IA
 ↓
Código
```

A proposta é:

```text
REQUISITOS
    ↓
ARQUITETURA
    ↓
PLANEJAMENTO
    ↓
IMPLEMENTAÇÃO
    ↓
TESTES
    ↓
REVISÃO
    ↓
DOCUMENTAÇÃO
    ↓
QUALITY GATES
```

---

# 2. Objetivo

O Kit deve permitir que diferentes ferramentas de IA trabalhem seguindo um padrão comum.

Exemplos:

```text
Claude Code
Codex
GitHub Copilot
OpenCode
Cursor
outra ferramenta de IA
```

O projeto não deve depender exclusivamente de um único fornecedor.

---

# 3. Componentes principais

```text
Kit IA Dev
├── Prompts
├── Agents
├── Skills
├── Templates
├── Workflows
├── Quality Gates
├── Documentation
└── Dictionary
```

---

# 4. Estrutura recomendada

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
```

---

# 5. 1-Prompts

Contém prompts reutilizáveis.

```text
1-Prompts/
├── bootstrap/
├── architecture/
├── development/
├── testing/
├── review/
└── documentation/
```

---

# 6. prompts.md

`prompts.md` funciona como o **orquestrador principal**.

Ele informa à IA:

```text
o que ler
em qual ordem trabalhar
quais agentes utilizar
quais skills aplicar
quais gates executar
quais artifacts produzir
```

---

# 7. Papel do prompts.md

```text
USER
 ↓
prompts.md
 ↓
PROJECT CONTEXT
 ↓
AGENTS
 ↓
SKILLS
 ↓
WORKFLOWS
 ↓
QUALITY GATES
 ↓
DELIVERABLES
```

---

# 8. Execução em etapas

Uma estratégia útil é possuir prompts de execução separados.

```text
1º prompt
→ instalar/analisar/preparar

2º prompt
→ construir/refatorar

3º prompt
→ validar/finalizar
```

---

# 9. Primeiro Prompt

Objetivo:

```text
read project
read Kit
discover tool conventions
install agents/skills
map architecture
create execution plan
```

Não começar alterando código sem entender o projeto.

---

# 10. Segundo Prompt

Objetivo:

```text
execute planned tasks
implement features
run tests
apply quality gates
```

---

# 11. Terceiro Prompt

Objetivo:

```text
final review
run all tests
security checks
documentation
architecture validation
generate reports
```

---

# 12. 2-Agents

```text
2-Agents/
├── requirements/
├── architect/
├── tech-lead/
├── developer/
├── tester/
├── reviewer/
├── security/
├── devops/
└── documentation/
```

---

# 13. Agent

Agent representa um papel especializado.

```text
Agent
├── Role
├── Objective
├── Inputs
├── Skills
├── Tools
├── Rules
└── Outputs
```

---

# 14. AGENT.md

Estrutura possível:

```text
# Role
# Objective
# Responsibilities
# Inputs
# Outputs
# Skills
# Allowed Tools
# Constraints
# Quality Gates
# Definition of Done
```

---

# 15. Requirements Agent

Responsabilidades:

```text
understand request
analyze existing project
identify constraints
identify ambiguities
define acceptance criteria
```

Artifact:

```text
REQUIREMENTS.md
```

---

# 16. Architect Agent

Responsabilidades:

```text
analyze architecture
identify boundaries
choose patterns
evaluate trade-offs
define integrations
define security
define observability
generate diagrams
```

Artifact:

```text
ARCHITECTURE_PLAN.md
```

---

# 17. Tech Lead Agent

Responsabilidades:

```text
convert architecture into tasks
define sequence
define dependencies
define technical standards
estimate impact
```

Artifact:

```text
EXECUTION_PLAN.md
```

---

# 18. Developer Agent

Responsabilidades:

```text
implement task
follow architecture
write tests
run local validation
update code
```

---

# 19. Tester Agent

Responsabilidades:

```text
unit tests
integration tests
contract tests
E2E tests
edge cases
regression
```

Artifact:

```text
TEST_REPORT.md
```

---

# 20. Reviewer Agent

Responsabilidades:

```text
review code
review architecture
review tests
review maintainability
review security
```

Artifact:

```text
REVIEW_REPORT.md
```

---

# 21. Security Agent

Verifica:

```text
secrets
authentication
authorization
dependencies
input validation
security configuration
```

---

# 22. DevOps Agent

Responsabilidades:

```text
Docker
CI/CD
environments
IaC
cloud
observability
deployment
```

---

# 23. Documentation Agent

Atualiza:

```text
README
API docs
architecture
ADRs
runbooks
setup instructions
release notes
```

---

# 24. Agent Workflow

```text
Requirements
 ↓
Architect
 ↓
Tech Lead
 ↓
Developer
 ↓
Tester
 ↓
Reviewer
 ↓
Documentation
```

---

# 25. 3-Skills

Skills representam capacidades reutilizáveis.

```text
3-Skills/
├── tdd/
├── architecture-review/
├── improve-codebase-architecture/
├── research/
├── frontend-design/
├── seo-audit/
├── rag/
└── ...
```

---

# 26. SKILL.md

Cada skill deve possuir:

```text
# Name
# Purpose
# When to Use
# Inputs
# Steps
# Tools
# Outputs
# Rules
# Examples
# Quality Checks
```

---

# 27. Skill não é Agent

```text
Agent
→ papel

Skill
→ capacidade
```

Exemplo:

```text
Developer Agent
+
TDD Skill
```

---

# 28. Skills Avançadas

O pacote de Skills Avançadas complementa o Kit.

Fluxo:

```text
Kit IA Dev
+
Advanced Skills
+
Stack Templates
=
Project AI Environment
```

---

# 29. Descoberta de Skills

Antes de criar uma skill:

```text
Need
 ↓
Search Existing Skills
 ↓
Found?
 ├── Yes → reuse
 └── No → create
```

Evita duplicação.

---

# 30. Catálogo

Manter:

```text
PROJECT_SKILLS.md
```

ou:

```text
SKILLS_REGISTRY.md
```

---

# 31. Registro de Skill

Exemplo:

```text
Name: tdd
Purpose: test-driven development
Agents: developer, tester
Trigger: new feature / bug fix
Location: 3-Skills/tdd/
```

---

# 32. 4-Templates

Templates fornecem estruturas iniciais.

```text
4-Templates/
├── dotnet/
├── java/
├── node/
├── python/
├── laravel/
└── frontend/
```

---

# 33. Templates por Stack

O pacote:

```text
Order-Bump-Templates-por-Stack/
```

ou equivalente compactado:

```text
Kit-IA-Dev-Templates-por-Stack.zip
```

pode fornecer referências específicas por tecnologia.

---

# 34. Template não deve substituir análise

Fluxo correto:

```text
Requirements
 ↓
Select Template
 ↓
Adapt
 ↓
Validate
```

Não:

```text
Template
 ↓
Copy Everything
```

---

# 35. Exemplo .NET

```text
backend/
├── Domain/
├── Application/
├── Infrastructure/
├── Api/
└── CrossCutting/
```

Pode ser adaptado para:

```text
Clean Architecture
Vertical Slice
CQRS
DDD
```

---

# 36. Exemplo Frontend

```text
frontend/
├── src/
│   ├── app/
│   ├── features/
│   ├── components/
│   ├── services/
│   └── shared/
└── tests/
```

---

# 37. 5-Workflows

```text
5-Workflows/
├── project-bootstrap/
├── feature-development/
├── bug-fix/
├── refactoring/
├── release/
├── architecture-review/
└── documentation/
```

---

# 38. Workflow

Workflow define sequência.

```text
Trigger
 ↓
Steps
 ↓
Agents
 ↓
Skills
 ↓
Gates
 ↓
Artifacts
```

---

# 39. Feature Workflow

```text
Issue
 ↓
Requirements
 ↓
Architecture Impact
 ↓
Task Plan
 ↓
Branch
 ↓
Implementation
 ↓
Tests
 ↓
Review
 ↓
PR
```

---

# 40. Bug Fix Workflow

```text
Bug
 ↓
Reproduce
 ↓
Root Cause
 ↓
Regression Test
 ↓
Fix
 ↓
Run Tests
 ↓
Review
```

---

# 41. Refactoring Workflow

```text
Current Architecture
 ↓
Problems
 ↓
Target Architecture
 ↓
Incremental Plan
 ↓
Tests
 ↓
Refactor
 ↓
Regression
```

---

# 42. Release Workflow

```text
develop
 ↓
hml
 ↓
release/x.y.z
 ↓
validation
 ↓
main
 ↓
production
```

---

# 43. 6-Quality-Gates

```text
6-Quality-Gates/
├── requirements/
├── architecture/
├── code/
├── tests/
├── security/
├── performance/
├── documentation/
└── release/
```

---

# 44. Quality Gate

Gate impede avanço quando critérios obrigatórios não são atendidos.

```text
Artifact
 ↓
Gate
 ├── PASS
 └── FAIL
```

---

# 45. Requirements Gate

```text
scope defined?
acceptance criteria?
constraints?
dependencies?
```

---

# 46. Architecture Gate

```text
SOLID?
boundaries?
security?
observability?
data ownership?
trade-offs documented?
```

---

# 47. Code Gate

```text
build passes
lint passes
architecture rules
no obvious duplication
clean code
```

---

# 48. Test Gate

```text
unit
integration
architecture
contract
E2E when required
```

---

# 49. Security Gate

```text
secret scan
dependency scan
SAST
container scan
IaC scan
```

---

# 50. Documentation Gate

```text
README updated?
architecture updated?
API docs?
ADRs?
runbook?
```

---

# 51. Release Gate

```text
tests
security
version
migration
rollback
release notes
```

---

# 52. 7-Documentation

```text
7-Documentation/
├── architecture/
├── standards/
├── guides/
├── runbooks/
├── ADR/
└── examples/
```

---

# 53. Documentação como código

Documentação deve acompanhar o repositório.

```text
Code Change
 ↓
Documentation Impact
 ↓
Update
```

---

# 54. 8-Dictionary

Este conjunto de documentos.

```text
8-Dictionary/
├── 01-estrutura-de-projeto.md
├── 02-rag.md
├── ...
└── 18-kit-ia-dev.md
```

---

# 55. Dicionário técnico

Objetivo:

```text
shared vocabulary
architecture reference
agent knowledge
training material
prompt support
```

---

# 56. Estrutura no projeto

O Kit pode ser instalado dentro do repositório conforme convenções da ferramenta.

Exemplo conceitual:

```text
project/
├── .ai/
│   ├── agents/
│   ├── skills/
│   ├── workflows/
│   └── rules/
├── docs/
├── backend/
├── frontend/
├── tests/
└── prompts.md
```

---

# 57. Descobrir caminho correto

Cada ferramenta pode possuir convenções diferentes.

Portanto:

```text
1. Detect tool
2. Read tool documentation/config
3. Locate Agent Skills path
4. Install compatible structure
```

Não assumir caminho fixo sem verificar.

---

# 58. COMO-INSTALAR.md

O pacote pode manter:

```text
3-Skills/COMO-INSTALAR.md
```

como referência de instalação.

---

# 59. Instalação

Fluxo:

```text
Kit ZIP
 ↓
Extract
 ↓
Read Installation Guide
 ↓
Detect AI Tool
 ↓
Install Agents
 ↓
Install Skills
 ↓
Install Workflows
 ↓
Configure Project
 ↓
Validate
```

---

# 60. Bootstrap

Primeiro passo da IA:

```text
read prompts.md
```

Depois:

```text
read project docs
read architecture
read skills registry
read workflow
```

---

# 61. Project Contract

Arquivo recomendado:

```text
PROJECT.md
```

Contém:

```text
project name
goal
stack
architecture
environments
commands
rules
constraints
```

---

# 62. PROJECT_STRUCTURE.md

Define estrutura esperada.

```text
folder
purpose
ownership
allowed dependencies
```

Funciona como contrato arquitetural.

---

# 63. PROJECT_SKILLS.md

Lista skills disponíveis.

```text
skill
purpose
trigger
agent
path
```

---

# 64. SEED_FAKE_DATA.md

Quando o projeto utiliza dados fake:

```text
entities
volumes
relationships
roles
permissions
scenarios
```

Nunca documentar senhas reais.

---

# 65. Environment Strategy

```text
TEST
DEV
HML
PROD
```

Cada ambiente possui configuração isolada.

---

# 66. .env

Frontend:

```text
.env.development
.env.hml
.env.production
```

Sem secrets reais versionados.

---

# 67. appsettings

Backend:

```text
appsettings.json
appsettings.Development.json
appsettings.Hml.json
appsettings.Production.json
```

Secrets devem vir de mecanismo seguro.

---

# 68. Docker

```text
docker/
├── compose/
├── api/
├── frontend/
├── databases/
└── observability/
```

---

# 69. Docker Compose

Objetivo:

```text
one command
 ↓
environment
```

Exemplo conceitual:

```text
docker compose up
```

---

# 70. Testes via Docker

Requisito recomendado:

```text
docker compose run tests
```

ou comando equivalente definido pelo projeto.

---

# 71. Bancos separados

```text
TEST DB
DEV DB
HML DB
PROD DB
```

Nunca executar teste automatizado destrutivo contra produção.

---

# 72. Seed

```text
Migration
 ↓
Seed
 ↓
Fake Data
```

Somente em ambientes permitidos.

---

# 73. Fake Data

Exemplo:

```text
1000 users
roles
permissions
content
relationships
audit examples
```

---

# 74. GitFlow

```text
main
develop
hml
feature/task-*
release/*
```

---

# 75. Feature Branch

```text
develop
 ↓
feature/task-123
```

---

# 76. AI Git Workflow

```text
Task
 ↓
Create Branch
 ↓
Implement
 ↓
Test
 ↓
Commit
 ↓
Push
 ↓
Create PR
 ↓
AI Review
 ↓
CI
```

---

# 77. Pull Request

PR deve conter:

```text
summary
changes
tests
risks
migration
screenshots when relevant
```

---

# 78. Release

```text
develop
 ↓
hml
 ↓
release/1.0.0
 ↓
main
```

Versionamento real deve seguir convenção do projeto.

---

# 79. CI/CD

```text
PR
 ↓
Build
 ↓
Tests
 ↓
Security
 ↓
Quality Gate
 ↓
Artifact
 ↓
Environment
```

---

# 80. Definition of Done

Uma task só termina quando:

```text
code complete
tests passing
review complete
documentation updated
quality gates passed
```

---

# 81. SOLID

Kit deve orientar:

```text
SRP
OCP
LSP
ISP
DIP
```

---

# 82. Clean Code

```text
clear names
small responsibilities
explicit dependencies
testable design
```

---

# 83. Clean Architecture

```text
Domain
 ↑
Application
 ↑
Infrastructure / API
```

Dependências devem respeitar regras definidas.

---

# 84. DDD

Aplicar quando o domínio justificar.

```text
Entities
Value Objects
Aggregates
Domain Events
Bounded Contexts
```

---

# 85. CQRS

```text
Commands
→ writes

Queries
→ reads
```

---

# 86. Vertical Slice

```text
Features/
├── CreateUser/
├── UpdateUser/
└── GetUser/
```

---

# 87. Domain Events

```text
Domain
 ↓
Event
 ↓
Application Handler
```

Domínio não deve depender diretamente de broker.

---

# 88. Outbox

```text
Business Transaction
+
Outbox
 ↓
Publisher
 ↓
Broker
```

---

# 89. Cache

```text
Query
 ↓
Redis
 ├── HIT
 └── MISS → DB → Cache
```

---

# 90. Mensageria

Possíveis adapters:

```text
RabbitMQ
Kafka
SQS
SNS
Service Bus
```

Core deve permanecer desacoplado quando possível.

---

# 91. Observabilidade

```text
Logs
Metrics
Traces
Health Checks
Correlation ID
```

---

# 92. OpenTelemetry

Instrumentar:

```text
HTTP
Database
Redis
Messaging
External APIs
AI
```

---

# 93. Cloud Ready

```text
Local
 ↓
Docker
 ↓
Cloud-ready adapters
 ↓
AWS / Azure
```

---

# 94. AWS

Competências/templates podem contemplar:

```text
SQS
SNS
Lambda
S3
EC2
ECS
```

---

# 95. Azure

Possíveis equivalentes:

```text
Service Bus
Event Grid
Functions
Blob Storage
VM
Container Apps / AKS
```

---

# 96. IaC

```text
Terraform
CloudFormation
Bicep
```

Conforme target.

---

# 97. Arquitetura Draw.io

Depois de estruturar o projeto:

```text
prompts.md
 ↓
project structure
 ↓
architecture analysis
 ↓
draw.io diagrams
```

---

# 98. Diagramas recomendados

```text
Context
Containers
Backend
Frontend
Infrastructure
Data
Messaging
Git Flow
CI/CD
```

---

# 99. C4

```text
Context
Container
Component
```

Pode servir como modelo conceitual para os desenhos.

---

# 100. ADR

```text
docs/adr/
```

Registrar decisões relevantes.

---

# 101. AI Context

Não enviar todo o projeto indiscriminadamente.

```text
Task
 ↓
Relevant Files
 ↓
Relevant Docs
 ↓
Relevant Skills
```

---

# 102. Context Engineering

```text
Search
 ↓
Filter
 ↓
Rank
 ↓
Compress
 ↓
Context
```

---

# 103. RTK

Ferramentas de compactação de saída podem reduzir contexto de:

```text
npm test
dotnet test
git diff
docker logs
```

---

# 104. Token Economy

```text
small context
+
relevant context
+
structured artifacts
=
lower token waste
```

---

# 105. LLM Router

Tarefas simples:

```text
fast/cheap model
```

Tarefas complexas:

```text
stronger model
```

Quando a ferramenta permitir.

---

# 106. LLM Local

Pode apoiar:

```text
private processing
classification
summaries
local development
```

---

# 107. RAG

Kit pode incluir RAG para conhecimento de projeto.

```text
Docs
Code
ADRs
 ↓
RAG
 ↓
Agents
```

---

# 108. Agentic RAG

```text
Agent
 ↓
Choose Source
 ↓
Retrieve
 ↓
Evaluate
 ↓
Continue
```

---

# 109. MCP

```text
Agents
 ↓
MCP
 ↓
GitHub / Files / DB / Tools
```

---

# 110. Plugins

Plugins podem ampliar capacidades.

```text
Agent
 ↓
Plugin
 ↓
External Service
```

---

# 111. Connectors

```text
GitHub
Drive
Database
Cloud
Observability
Project Management
```

Devem possuir permissões controladas.

---

# 112. Human in the Loop

Ações críticas:

```text
merge main
production deploy
destructive migration
delete cloud resource
external communication
```

podem exigir aprovação explícita.

---

# 113. Least Privilege

Cada agente recebe apenas ferramentas necessárias.

```text
Documentation Agent
→ docs access

DevOps Agent
→ infrastructure access
```

---

# 114. Security

Kit deve proibir:

```text
hardcoded secrets
real passwords in docs
unvalidated external input
unrestricted destructive tools
```

---

# 115. Audit

Registrar ações relevantes:

```text
agent
task
tool
result
timestamp
approval
```

---

# 116. Agent Observability

```text
Workflow Trace
├── Agent
├── Skill
├── Tool
├── Gate
└── Result
```

---

# 117. Agent Tests

```text
Golden Tasks
Fake Tools
Fake LLM
Expected Artifacts
Forbidden Actions
```

---

# 118. Quality of AI Output

Não validar apenas:

```text
"compilou"
```

Validar:

```text
requirements
architecture
tests
security
maintainability
documentation
```

---

# 119. AI Review

IA pode revisar PR, mas não substitui políticas determinísticas.

```text
AI Review
+
CI
+
Static Analysis
+
Tests
```

---

# 120. Project Bootstrap Workflow

```text
Read Kit
 ↓
Read Project
 ↓
Detect Stack
 ↓
Detect Existing Architecture
 ↓
Install Skills
 ↓
Configure Agents
 ↓
Generate Project Docs
 ↓
Validate
```

---

# 121. New Project Workflow

```text
Idea
 ↓
Requirements
 ↓
Architecture
 ↓
Project Structure
 ↓
Docker
 ↓
Tests
 ↓
CI/CD
 ↓
Documentation
```

---

# 122. Existing Project Workflow

```text
Existing Repository
 ↓
Inventory
 ↓
Architecture Map
 ↓
Gap Analysis
 ↓
Refactoring Plan
 ↓
Incremental Changes
```

---

# 123. Nunca apagar contexto útil

Antes de refatorar:

```text
read existing docs
read code
read tests
read diagrams
read references
```

---

# 124. References Folder

```text
references/
├── screens/
├── diagrams/
├── specifications/
└── examples/
```

A IA deve consultar referências antes de inventar interface ou arquitetura.

---

# 125. Screenshot-Driven Development

```text
Reference Screens
 ↓
Analyze Components
 ↓
Extract Layout
 ↓
Implement
 ↓
Visual Compare
```

---

# 126. Task Management

```text
tasks/
├── backlog/
├── doing/
├── review/
└── done/
```

ou integração com issue tracker.

---

# 127. Task Artifact

```text
Task ID
Description
Acceptance Criteria
Dependencies
Files
Tests
Status
```

---

# 128. Gate Artifact

```text
Gate
Result
Evidence
Failures
Required Fixes
```

---

# 129. Report Artifact

Exemplos:

```text
TEST_REPORT.md
REVIEW_REPORT.md
SECURITY_REPORT.md
ARCHITECTURE_REPORT.md
```

---

# 130. Recovery

Se execução for interrompida:

```text
STATUS.md
```

pode registrar:

```text
completed
pending
current task
failures
next action
```

---

# 131. Resumo de Pendências

Ao atingir limite de contexto ou interromper trabalho, produzir:

```text
what was completed
what remains
known issues
commands to resume
```

---

# 132. Multi-Stack

Kit deve ser genérico.

```text
Core Kit
 ↓
Stack Adapter
 ├── .NET
 ├── Java
 ├── Node
 ├── Python
 └── Laravel
```

---

# 133. Stack Adapter

Define:

```text
build command
test command
folder conventions
framework patterns
Docker
CI/CD
```

---

# 134. .NET Adapter

Pode conhecer:

```text
dotnet restore
dotnet build
dotnet test
ASP.NET Core
EF Core
Dapper
xUnit
FluentValidation
```

---

# 135. React Adapter

```text
npm ci
npm run build
npm test
lint
typecheck
```

---

# 136. Java Adapter

```text
Gradle
Spring Boot
JUnit
Flyway
Testcontainers
```

---

# 137. Python Adapter

```text
FastAPI
pytest
SQLAlchemy
Alembic
```

---

# 138. Node Adapter

```text
Fastify
Prisma
Vitest
```

---

# 139. Template Selection

```text
Project Requirements
 ↓
Stack
 ↓
Architecture
 ↓
Best Template
```

---

# 140. Não misturar tudo

Um template não precisa conter:

```text
Kafka
RabbitMQ
Redis
MongoDB
Kubernetes
RAG
Agents
```

se o projeto não necessita.

Kit fornece opções; arquitetura seleciona.

---

# 141. Progressive Complexity

```text
Simple
 ↓
Measure
 ↓
Need Identified
 ↓
Add Capability
```

---

# 142. YAGNI

Não implementar capacidade apenas porque está disponível no Kit.

---

# 143. SOLID + AI

Agente deve verificar se geração automática respeita:

```text
SRP
OCP
LSP
ISP
DIP
```

---

# 144. Architecture Tests

Automatizar regras como:

```text
Domain cannot depend on Infrastructure
```

---

# 145. Definition of Ready

Antes de implementar:

```text
requirement clear
acceptance criteria
dependencies known
architecture impact reviewed
```

---

# 146. Definition of Done

Depois:

```text
implementation
tests
review
docs
CI
quality gates
```

---

# 147. Governance

Kit precisa de versionamento.

Exemplo:

```text
Kit IA Dev v1
v2
v3
```

Mudanças precisam de changelog.

---

# 148. CHANGELOG

```text
Added
Changed
Deprecated
Removed
Fixed
Security
```

---

# 149. Versionamento de Skills

Skill pode possuir:

```text
name
version
compatibility
lastUpdated
```

---

# 150. Compatibility Matrix

```text
Skill
Claude Code
Codex
Copilot
OpenCode
```

Indicar adaptações quando necessárias.

---

# 151. Tool-Specific Adapter

```text
Core Skill
 ↓
Claude Adapter
Codex Adapter
OpenCode Adapter
```

Evita duplicar conhecimento principal.

---

# 152. Instalação segura

Nunca permitir script de instalação executar comandos destrutivos sem revisão.

```text
inspect
 ↓
plan
 ↓
confirm critical changes
 ↓
install
```

---

# 153. Backup

Antes de grandes refatorações:

```text
clean Git status
commit/checkpoint
branch
```

Permite rollback.

---

# 154. Git como checkpoint

```text
Task Start
 ↓
Feature Branch
 ↓
Small Commits
 ↓
PR
```

---

# 155. Commit

Mensagem deve explicar alteração.

Exemplo:

```text
feat(auth): add refresh token rotation
```

---

# 156. AI Commit Policy

IA não deve incluir:

```text
secrets
generated garbage
temporary files
local environment files
```

---

# 157. PR Validation

```text
AI Review
 ↓
CI
 ↓
Quality Gates
 ↓
Approval
```

---

# 158. Architecture Diagram Workflow

```text
Code Structure
 ↓
Architect Agent
 ↓
Draw.io
 ↓
Review
 ↓
docs/architecture
```

---

# 159. Diagramas devem refletir realidade

Não manter:

```text
beautiful diagram
≠
actual system
```

Atualizar com mudanças arquiteturais.

---

# 160. Document-Driven Engineering

Artifacts importantes funcionam como contratos:

```text
REQUIREMENTS.md
PROJECT_STRUCTURE.md
ARCHITECTURE_PLAN.md
EXECUTION_PLAN.md
PROJECT_SKILLS.md
```

---

# 161. Agentic Engineering

O Kit transforma engenharia assistida por IA em:

```text
CONTEXT
+
ROLES
+
SKILLS
+
WORKFLOWS
+
TOOLS
+
GATES
+
EVIDENCE
```

---

# 162. Exemplo de fluxo completo

```text
USER REQUEST
      ↓
prompts.md
      ↓
REQUIREMENTS AGENT
      ↓
REQUIREMENTS.md
      ↓
GATE
      ↓
ARCHITECT AGENT
      ↓
ARCHITECTURE_PLAN.md
      ↓
GATE
      ↓
TECH LEAD
      ↓
EXECUTION_PLAN.md
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
      ↓
PR / RELEASE
```

---

# 163. Exemplo para projeto .NET + React

```text
React Site
React Admin
     ↓
ASP.NET APIs
     ↓
Application
     ↓
Domain
     ↓
Infrastructure
     ↓
MySQL / Redis / MongoDB
     ↓
Messaging
```

Kit adiciona:

```text
Agents
Skills
Tests
Docker
CI/CD
Observability
Documentation
```

---

# 164. Exemplo de Agentic Development

```text
Task
 ↓
Requirements
 ↓
Architect
 ↓
Developer
 ↓
dotnet test
 ↓
Reviewer
 ↓
Git Commit
 ↓
Push
 ↓
PR
```

---

# 165. Quality Gates globais

- [ ] requisitos claros;
- [ ] arquitetura validada;
- [ ] SOLID;
- [ ] build;
- [ ] unit tests;
- [ ] integration tests;
- [ ] security checks;
- [ ] observabilidade;
- [ ] Docker;
- [ ] documentação;
- [ ] diagramas;
- [ ] CI/CD;
- [ ] PR review;
- [ ] sem secrets;
- [ ] Definition of Done.

---

# 166. Anti-patterns

Evitar:

```text
mega prompt sem estrutura
IA codificando antes de ler projeto
agente com permissão ilimitada
skills duplicadas
template copiado sem adaptação
quality gate apenas textual
documentação desatualizada
testes ignorados
commit direto em main
segredos em arquivos
arquitetura definida por hype
```

---

# 167. Regras do Kit

1. Ler antes de alterar.
2. Planejar antes de implementar.
3. Preservar arquitetura válida existente.
4. Usar a skill correta.
5. Usar o agente correto.
6. Criar artifacts persistentes.
7. Executar testes.
8. Executar Quality Gates.
9. Não expor secrets.
10. Documentar decisões.
11. Usar Git como checkpoint.
12. Criar PR.
13. Não considerar task concluída sem evidência.

---

# 168. Relação com o Dicionário

```text
01   Estrutura de Projeto
01.1 Estrutura de Projeto
01.2 Agentic Workflow
02   RAG
02.1 RAG
02.2 RAG .NET
03   Plugins
04   Frameworks de Análise/Gestão
05   Conectores e Funções
06   Skills de Escritório
07   LinkedIn Manager Agent
08   Free LLM API / Token
09   Skills
10   LLM Local
11   CI/CD
12   SEO / AEO
13   Projetar Microsserviços
14   LLM vs Jev
15   RAG System
16   Arquitetura e Aplicações
17   Agentic AI
18   Kit IA Dev
```

---

# 169. Visão consolidada

```text
                        KIT IA DEV
                            │
        ┌───────────────────┼────────────────────┐
        │                   │                    │
      AGENTS              SKILLS              TEMPLATES
        │                   │                    │
        └───────────────────┼────────────────────┘
                            │
                        WORKFLOWS
                            │
                      QUALITY GATES
                            │
                         PROJECT
                            │
            ┌───────────────┼───────────────┐
            │               │               │
          CODE            TESTS           DOCS
            │               │               │
            └───────────────┼───────────────┘
                            │
                          CI/CD
                            │
                        PR/RELEASE
```

---

# 170. Resumo

O Kit IA Dev não deve ser apenas uma coleção de prompts.

Ele deve funcionar como um **sistema operacional de engenharia assistida por IA**:

```text
PROMPTS
+
AGENTS
+
SKILLS
+
TEMPLATES
+
WORKFLOWS
+
QUALITY GATES
+
DOCUMENTATION
+
TECHNICAL DICTIONARY
```

O princípio central é transformar IA de código em um processo de engenharia controlado, reproduzível, testável e auditável.

A IA deixa de atuar apenas como:

```text
code generator
```

e passa a atuar dentro de um processo:

```text
REQUIREMENTS
→ ARCHITECTURE
→ PLAN
→ IMPLEMENT
→ TEST
→ REVIEW
→ DOCUMENT
→ VALIDATE
→ DELIVER
```

---

# 📁 Arquivo

```text
18-kit-ia-dev.md
```
