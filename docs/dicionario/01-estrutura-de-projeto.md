# 📘 Dicionário Técnico — 01 Estrutura de Projeto

> **Categoria:** Arquitetura / Organização de Projeto  
> **Código:** 01  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** Projetos .NET / React / APIs / IA / Cloud  
> **Objetivo:** Padronizar como projetos devem ser analisados, planejados, estruturados, implementados, testados e documentados.

## 1. O que é uma Estrutura de Projeto

A estrutura de projeto define como código, documentação, infraestrutura, testes, automações e recursos de IA são organizados dentro de um repositório.

Ela funciona como um contrato para desenvolvedores, arquitetos, Tech Leads, agentes de IA, Claude Code, Codex, Copilot, OpenCode, CI/CD, Docker e ferramentas de análise.

Uma boa estrutura permite entender rapidamente onde estão o código, regras de negócio, integrações, testes, Docker, infraestrutura, documentos, prompts, agentes e skills.

## 2. Objetivo da Padronização

A estrutura deve permitir que projetos diferentes utilizem o mesmo padrão operacional:

```text
Kit IA Dev
     │
     ▼
prompts.md
     │
     ▼
Requirements Agent
     │
     ▼
Architect Agent
     │
     ▼
Tech Lead Agent
     │
     ▼
Developer Agent
     │
     ▼
Tester Agent
     │
     ▼
Reviewer Agent
     │
     ▼
Documentation Agent
```

O Kit IA Dev pode ser reutilizado em APIs .NET, microsserviços, Modular Monolith, React, Cloud, AWS, Azure, IA, RAG, Agentic AI, SaaS e Micro SaaS.

## 3. Estrutura Base Recomendada

```text
project-root/
├── backend/
├── frontend/
├── tests/
├── docker/
├── infrastructure/
├── docs/
├── scripts/
├── tools/
├── references/
├── agents/
├── skills/
├── prompts/
├── reports/
├── .github/
├── .env.example
├── docker-compose.yml
├── prompts.md
├── PROJECT.md
├── PROJECT_STRUCTURE.md
├── PROJECT_SKILLS.md
└── README.md
```

## 4. Backend

```text
backend/
├── src/
│   ├── Api/
│   ├── Application/
│   ├── Domain/
│   ├── Infrastructure/
│   └── CrossCutting/
└── tests/
    ├── UnitTests/
    ├── IntegrationTests/
    └── ArchitectureTests/
```

## 5. Domain

O Domain representa o núcleo das regras de negócio.

```text
Domain/
├── Entities/
├── ValueObjects/
├── Aggregates/
├── Events/
├── Exceptions/
├── Enums/
├── Specifications/
└── Interfaces/
```

O Domain não deve depender de Entity Framework, Redis, Kafka, RabbitMQ, AWS, Azure ou APIs externas.

## 6. Application

A camada Application orquestra os casos de uso.

```text
Application/
├── Commands/
├── Queries/
├── Handlers/
├── DTOs/
├── Validators/
├── Interfaces/
└── Behaviors/
```

Exemplo CQRS:

```text
Users/
├── Commands/
│   ├── CreateUser/
│   ├── UpdateUser/
│   └── DeleteUser/
└── Queries/
    ├── GetUser/
    └── GetUsers/
```

## 7. Infrastructure

Implementa integrações externas.

```text
Infrastructure/
├── Persistence/
├── Cache/
├── Messaging/
├── Storage/
├── Email/
├── Authentication/
├── Observability/
└── ExternalServices/
```

Pode integrar MySQL, SQL Server, PostgreSQL, MongoDB, Redis, Kafka, RabbitMQ, SQS, SNS, S3 e Azure Service Bus.

## 8. API

```text
Api/
├── Endpoints/
├── Middleware/
├── Filters/
├── Authentication/
├── Authorization/
├── Extensions/
└── Configuration/
```

Exemplo:

```text
POST   /api/users
GET    /api/users
GET    /api/users/{id}
PUT    /api/users/{id}
DELETE /api/users/{id}
```

## 9. Vertical Slice Architecture

```text
Features/
└── Users/
    ├── Create/
    │   ├── Command.cs
    │   ├── Handler.cs
    │   ├── Validator.cs
    │   └── Endpoint.cs
    ├── GetById/
    │   ├── Query.cs
    │   ├── Handler.cs
    │   └── Endpoint.cs
    └── Delete/
        ├── Command.cs
        ├── Handler.cs
        └── Endpoint.cs
```

Facilita manutenção, testes, evolução, trabalho paralelo e atuação de agentes de IA.

## 10. CQRS

CQRS significa **Command Query Responsibility Segregation**.

```text
WRITE → Commands
READ  → Queries
```

Fluxo:

```text
Request
   ↓
Command / Query
   ↓
Handler
   ↓
Domain
   ↓
Infrastructure
```

## 11. Domain Events

Representam acontecimentos importantes do negócio, como UserCreated, OrderCreated, PaymentApproved, PasswordChanged e DocumentUploaded.

```text
Domain
   ↓
Domain Event
   ↓
Event Handler
   ├── Cache
   ├── Email
   ├── Audit
   └── Messaging
```

## 12. SOLID

- **S** — Single Responsibility Principle
- **O** — Open/Closed Principle
- **L** — Liskov Substitution Principle
- **I** — Interface Segregation Principle
- **D** — Dependency Inversion Principle

Objetivo: baixo acoplamento, alta coesão, facilidade de testes e manutenção.

## 13. Frontend

```text
frontend/
├── site/
└── admin/
```

Estrutura React:

```text
src/
├── components/
├── pages/
├── features/
├── services/
├── hooks/
├── contexts/
├── routes/
├── models/
├── utils/
└── assets/
```

## 14. Docker

```text
docker/
├── api/
├── frontend/
├── mysql/
├── redis/
├── mongo/
├── kafka/
├── rabbitmq/
└── observability/
```

Execução:

```bash
docker compose up -d
```

Meta: `git clone → docker compose up → ambiente funcionando`.

## 15. Ambientes

Ambientes recomendados:

```text
TEST
DEV
HML
PROD
```

Backend:

```text
appsettings.Test.json
appsettings.Development.json
appsettings.Homologation.json
appsettings.Production.json
```

Frontend:

```text
.env.test
.env.dev
.env.hml
.env.prod
```

## 16. Testes

```text
tests/
├── unit/
├── integration/
├── architecture/
├── contract/
└── e2e/
```

A maior cobertura deve estar nos testes unitários, complementada por integração, arquitetura, contratos e E2E.

## 17. Observabilidade

A aplicação deve fornecer logs, métricas, traces e health checks.

```text
Application
     ↓
OpenTelemetry
     ↓
Logs + Metrics + Traces
```

Ferramentas possíveis: OpenTelemetry, Prometheus, Grafana, Jaeger, Seq e Elastic.

## 18. Infrastructure as Code

```text
infrastructure/
├── aws/
├── azure/
├── terraform/
├── kubernetes/
└── localstack/
```

Evolução sugerida:

```text
LOCAL → DOCKER → LOCALSTACK → KUBERNETES → CLOUD
```

## 19. Documentação

```text
docs/
├── architecture/
├── diagrams/
├── requirements/
├── decisions/
├── api/
├── infrastructure/
├── security/
└── testing/
```

Arquivos importantes:

```text
README.md
PROJECT.md
PROJECT_STRUCTURE.md
ARCHITECTURE.md
REQUIREMENTS.md
EXECUTION_PLAN.md
TEST_PLAN.md
SECURITY.md
```

## 20. Diagramas

Ferramenta recomendada: **draw.io**.

Diagramas importantes:

- System Context
- Container Diagram
- Component Diagram
- Backend Architecture
- Frontend Architecture
- Infrastructure
- Database ER
- UML
- CI/CD
- Git Flow
- Cloud Architecture
- Messaging
- RAG
- Agentic AI

## 21. Git Flow

Branches principais:

```text
main
develop
hml
```

Fluxo:

```text
feature/task
     ↓
develop
     ↓
hml
     ↓
release/1.0.0
     ↓
main
```

Fluxo da IA:

```text
criar branch
    ↓
implementar task
    ↓
executar testes
    ↓
commit
    ↓
push
    ↓
criar Pull Request
    ↓
Code Review
    ↓
Quality Gate
```

## 22. Estrutura de IA

```text
.ai/
├── agents/
├── skills/
├── prompts/
├── workflows/
├── rules/
├── templates/
└── memory/
```

## 23. Agentes

Agentes recomendados:

- Requirements Agent
- Architect Agent
- Tech Lead Agent
- Developer Agent
- Tester Agent
- Reviewer Agent
- Security Agent
- DevOps Agent
- Documentation Agent

Fluxo:

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

## 24. Skills

```text
skills/
├── dotnet/
├── architecture/
├── testing/
├── docker/
├── aws/
├── azure/
├── database/
├── security/
├── observability/
└── documentation/
```

Cada skill pode seguir o padrão:

```text
skill-name/
└── SKILL.md
```

## 25. prompts.md

O `prompts.md` funciona como ponto inicial de execução do Kit IA Dev.

```text
prompts.md
    ↓
ler projeto
    ↓
analisar requisitos
    ↓
analisar estrutura existente
    ↓
identificar gaps
    ↓
criar plano
    ↓
acionar agentes
    ↓
executar tasks
    ↓
executar testes
    ↓
validar quality gates
    ↓
documentar
```

## 26. Quality Gates

```text
Build
  ↓
Unit Tests
  ↓
Integration Tests
  ↓
Architecture Tests
  ↓
Security
  ↓
Static Analysis
  ↓
Code Review
  ↓
Documentation
  ↓
TASK = DONE
```

## 27. Definition of Done

Uma funcionalidade está concluída quando:

- código implementado;
- SOLID e arquitetura respeitados;
- validações implementadas;
- testes unitários criados;
- testes de integração criados quando necessários;
- build e testes executados;
- logs e tratamento de erros implementados;
- segurança revisada;
- documentação atualizada;
- Pull Request criado;
- Quality Gates aprovados.

## 28. Como aplicar no Kit IA Dev

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
    └── 01-estrutura-de-projeto.md
```

## 29. Regra para Agentes de IA

Antes de alterar qualquer projeto, a IA deve:

1. Ler `README.md`.
2. Ler `PROJECT.md`.
3. Ler `PROJECT_STRUCTURE.md`.
4. Ler `prompts.md`.
5. Identificar stack.
6. Identificar arquitetura.
7. Identificar padrões existentes.
8. Identificar infraestrutura.
9. Identificar testes.
10. Identificar documentação.
11. Identificar regras do Git.
12. Identificar Quality Gates.
13. Criar plano de execução.
14. Somente depois modificar código.

A IA não deve inventar arquitetura sem necessidade, ignorar padrões existentes, duplicar serviços ou abstrações, quebrar testes, misturar Domain com Infrastructure, colocar regra de negócio em Controllers/Endpoints ou ignorar segurança, observabilidade e Quality Gates.

## 30. Resultado Esperado

O objetivo é transformar:

```text
IA gerando código
```

em:

```text
IA trabalhando dentro de um processo de engenharia
```

Fluxo final:

```text
Requisito
   ↓
Planejamento
   ↓
Arquitetura
   ↓
Task
   ↓
Implementação
   ↓
Testes
   ↓
Review
   ↓
Quality Gate
   ↓
Documentação
   ↓
Pull Request
   ↓
Release
```

## 31. Checklist

### Estrutura
- [ ] Backend organizado
- [ ] Frontend organizado
- [ ] Domain separado
- [ ] Application separado
- [ ] Infrastructure separado
- [ ] APIs organizadas
- [ ] Testes separados

### Arquitetura
- [ ] SOLID
- [ ] Clean Code
- [ ] DDD
- [ ] CQRS
- [ ] Domain Events
- [ ] Vertical Slice quando aplicável

### Infraestrutura
- [ ] Docker
- [ ] Banco de dados
- [ ] Cache
- [ ] Mensageria
- [ ] Observabilidade
- [ ] Cloud preparada

### IA
- [ ] prompts.md
- [ ] Agents
- [ ] Skills
- [ ] Workflows
- [ ] Quality Gates

### Documentação
- [ ] README
- [ ] PROJECT
- [ ] REQUIREMENTS
- [ ] ARCHITECTURE
- [ ] Diagramas
- [ ] Plano de execução

### DevOps
- [ ] Git Flow
- [ ] CI/CD
- [ ] Build automatizado
- [ ] Testes automatizados
- [ ] Pull Request
- [ ] Release

## Relação com outros itens do Dicionário

Este conteúdo serve como base para:

- `01.1 - Estrutura de Projeto`
- `01.2 - Agentic Workflow`
- `02 - RAG`
- `03 - Plugins`
- `05 - Conectores e Funções`
- `09 - Skills`
- `11 - CI/CD`
- `13 - Microsserviços`
- `15 - RAG System`
- `16 - Arquitetura de Aplicações`
- `17 - Agentic AI`
- `18 - Kit IA Dev`

## Resumo

**Estrutura de Projeto** não significa apenas organizar pastas.

Ela define o padrão de engenharia utilizado por humanos e agentes de IA para transformar requisitos em software testado, documentado e implantável.

A estrutura conecta:

**Arquitetura + Código + Testes + Docker + Cloud + DevOps + Documentação + Agents + Skills + Quality Gates.**
