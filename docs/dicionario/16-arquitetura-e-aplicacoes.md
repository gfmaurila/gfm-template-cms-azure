# 📘 Dicionário Técnico — 16 Arquitetura e Aplicações

> **Categoria:** Arquitetura de Software / Engenharia de Aplicações  
> **Código:** 16  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** .NET / React / APIs / Cloud / Sistemas Distribuídos / IA  
> **Objetivo:** Consolidar os principais estilos arquiteturais, seus componentes, cenários de aplicação e critérios para escolha, evitando decisões arquiteturais baseadas apenas em tendência.

---

# 1. O que é Arquitetura de Software

Arquitetura de software define como as partes importantes de um sistema são organizadas e como se relacionam.

```text
Business Requirements
        ↓
Architecture
        ↓
Applications
        ↓
Infrastructure
```

Arquitetura deve responder:

```text
What?
Why?
Where?
How?
Who owns it?
How does it evolve?
```

---

# 2. Arquitetura não é apenas estrutura de pastas

Uma estrutura como:

```text
Domain/
Application/
Infrastructure/
Api/
```

é somente uma parte.

Arquitetura também envolve:

```text
boundaries
dependencies
data
communication
security
deployment
resilience
observability
scalability
```

---

# 3. Drivers arquiteturais

Antes de escolher arquitetura:

```text
Business Goals
Functional Requirements
Quality Attributes
Constraints
Risks
Team
Budget
Time
```

---

# 4. Quality Attributes

Exemplos:

```text
Performance
Scalability
Availability
Security
Maintainability
Testability
Observability
Resilience
Deployability
Cost
```

A arquitetura é um conjunto de trade-offs entre esses atributos.

---

# 5. Monólito

```text
Application
├── UI
├── Business
└── Data
```

Tudo é implantado como uma única unidade.

Não significa necessariamente código ruim.

---

# 6. Quando Monólito é adequado

```text
small system
small team
simple deployment
early product
limited operational complexity
```

Pode ser a melhor escolha.

---

# 7. Modular Monolith

Uma aplicação única com módulos bem delimitados.

```text
Application
├── Identity
├── Customers
├── Orders
├── Billing
└── Content
```

Deploy:

```text
one deployable
```

Domínio:

```text
multiple boundaries
```

---

# 8. Vantagem do Modular Monolith

Combina:

```text
simpler operations
+
clear boundaries
+
future extraction
```

É excelente ponto de partida para muitos sistemas.

---

# 9. Estrutura por módulo

```text
Modules/
└── Orders/
    ├── Domain/
    ├── Application/
    ├── Infrastructure/
    └── Endpoints/
```

---

# 10. Microsserviços

```text
Client
 ↓
Gateway
 ├── Identity Service
 ├── Order Service
 ├── Billing Service
 └── Notification Service
```

Cada serviço possui ciclo de vida mais independente.

---

# 11. Microsserviços não são evolução automática

Não pensar:

```text
Monolith
→ bad

Microservices
→ good
```

A pergunta correta:

```text
Which architecture fits the problem?
```

---

# 12. SOA

Service-Oriented Architecture organiza capacidades como serviços.

Microsserviços compartilham algumas ideias, mas normalmente enfatizam:

```text
independent deployment
bounded contexts
decentralized ownership
small autonomous services
```

---

# 13. Layered Architecture

```text
Presentation
 ↓
Application
 ↓
Domain
 ↓
Infrastructure
```

Simples e comum.

Risco:

```text
business logic leaking across layers
```

---

# 14. Clean Architecture

Princípio central:

```text
dependencies point inward
```

Exemplo:

```text
API
 ↓
Application
 ↓
Domain
 ↑
Infrastructure implements abstractions
```

O domínio não deve depender de detalhes externos.

---

# 15. Onion Architecture

Organização conceitual:

```text
Domain Model
    ↑
Domain Services
    ↑
Application
    ↑
Infrastructure / UI
```

Também enfatiza dependências para o núcleo.

---

# 16. Hexagonal Architecture

Também conhecida como:

```text
Ports and Adapters
```

```text
          REST
           ↓
       [Adapter]
           ↓
        [Port]
           ↓
        DOMAIN
           ↑
        [Port]
           ↑
       [Adapter]
           ↑
        Database
```

---

# 17. Port

Contrato utilizado pelo núcleo.

Exemplo:

```csharp
public interface IOrderRepository
{
    Task<Order?> GetAsync(Guid id);
}
```

---

# 18. Adapter

Implementação de um port.

```text
IOrderRepository
 ↓
MySqlOrderRepository
```

---

# 19. Vertical Slice Architecture

Organiza por funcionalidade.

```text
Features/
├── CreateUser/
│   ├── Command.cs
│   ├── Validator.cs
│   ├── Handler.cs
│   └── Endpoint.cs
└── GetUser/
```

---

# 20. Horizontal x Vertical

Horizontal:

```text
Controllers
Services
Repositories
Models
```

Vertical:

```text
CreateOrder
CancelOrder
GetOrder
```

Vertical Slice reduz dispersão de uma feature por muitas pastas genéricas.

---

# 21. CQRS

```text
Commands
→ write

Queries
→ read
```

Pode ser usado em:

```text
monolith
modular monolith
microservices
```

Não depende de microsserviços.

---

# 22. Command

```text
CreateOrderCommand
CancelOrderCommand
```

Altera estado.

---

# 23. Query

```text
GetOrderByIdQuery
SearchOrdersQuery
```

Consulta estado.

---

# 24. Domain-Driven Design

DDD ajuda em domínios complexos.

Conceitos:

```text
Entity
Value Object
Aggregate
Repository
Domain Service
Domain Event
Bounded Context
Ubiquitous Language
```

---

# 25. Domain Model

Domínio deve representar comportamento, não apenas tabelas.

Ruim:

```text
Order.Data
```

Melhor:

```text
Order.Cancel()
Order.AddItem()
Order.Confirm()
```

---

# 26. Aggregate

Define fronteira de consistência.

```text
Order
├── OrderItem
├── Address
└── PaymentReference
```

Alterações passam pelo Aggregate Root quando essa é a modelagem escolhida.

---

# 27. Domain Events

```text
Order
 ↓
OrderCreatedDomainEvent
 ↓
Handler
```

Desacoplam reações internas.

---

# 28. Event-Driven Architecture

```text
Producer
 ↓
Event
 ↓
Broker
 ↓
Consumers
```

Útil para desacoplamento e processamento assíncrono.

---

# 29. Event Streaming

```text
Producer
 ↓
Kafka Topic
 ↓
Consumer Groups
```

Adequado a cenários de fluxo contínuo de eventos.

---

# 30. Message Queue

```text
Producer
 ↓
Queue
 ↓
Consumer
```

Adequada para processamento assíncrono de trabalho.

---

# 31. Serverless

```text
Event
 ↓
Function
 ↓
Service
```

Exemplos:

```text
AWS Lambda
Azure Functions
```

Bom para workloads compatíveis com execução orientada a eventos e escala sob demanda.

---

# 32. Event-Driven Serverless

```text
S3 Upload
 ↓
Event
 ↓
Lambda
 ↓
Processing
 ↓
Database
```

---

# 33. Client-Server

```text
Client
 ↓
Server
 ↓
Database
```

Modelo fundamental usado por muitas aplicações web.

---

# 34. SPA

```text
Browser
 ↓
React SPA
 ↓
REST API
```

Boa experiência interativa, mas exige atenção a:

```text
SEO
initial load
routing
security
```

---

# 35. SSR

```text
Request
 ↓
Server Rendering
 ↓
HTML
 ↓
Browser
```

Pode beneficiar conteúdo público e tempo de primeira renderização em cenários adequados.

---

# 36. BFF

Backend for Frontend:

```text
Web
 ↓
Web BFF

Mobile
 ↓
Mobile BFF
```

Cada frontend recebe API adaptada às suas necessidades.

---

# 37. API Gateway

```text
Clients
 ↓
Gateway
 ├── API A
 ├── API B
 └── API C
```

Pode cuidar de:

```text
routing
authentication
rate limiting
TLS
observability
```

---

# 38. REST

```text
GET /orders
POST /orders
GET /orders/{id}
```

Simples e amplamente suportado.

---

# 39. gRPC

```text
Service A
 ↓
gRPC
 ↓
Service B
```

Útil em integrações internas com contratos fortes e baixa sobrecarga em cenários compatíveis.

---

# 40. GraphQL

```text
Client
 ↓
GraphQL
 ↓
Schema
 ↓
Resolvers
```

Permite que cliente solicite campos necessários.

Precisa de governança de complexidade.

---

# 41. WebSocket

```text
Client
 ↕
Persistent Connection
 ↕
Server
```

Adequado a comunicação bidirecional em tempo real.

---

# 42. SignalR

Em .NET:

```text
ASP.NET Core
 ↓
SignalR Hub
 ↓
Clients
```

Facilita cenários realtime.

---

# 43. Database Architecture

Escolha depende dos dados.

```text
Relational
Document
Key-Value
Graph
Vector
Search
Time-Series
```

---

# 44. Relational Database

Exemplos:

```text
MySQL
PostgreSQL
SQL Server
```

Boa escolha para dados relacionais e transações.

---

# 45. Document Database

Exemplo:

```text
MongoDB
```

Útil para documentos e estruturas flexíveis quando o domínio justificar.

---

# 46. Key-Value / Cache

Exemplo:

```text
Redis
```

Usos:

```text
cache
sessions
rate limiting
temporary state
```

---

# 47. Vector Database

Usada em aplicações de IA/RAG.

```text
Text
 ↓
Embedding
 ↓
Vector Store
 ↓
Similarity Search
```

---

# 48. Graph Database

Útil quando relações são centrais.

```text
Person
 ↓ knows
Person
 ↓ works-at
Company
```

---

# 49. Polyglot Persistence

```text
Transactions → MySQL
Documents    → MongoDB
Cache        → Redis
Vectors      → Qdrant
Search       → OpenSearch
```

Usar múltiplos bancos somente quando a complexidade se justifica.

---

# 50. Cache-Aside

```text
Application
 ↓
Redis
 ├── HIT
 └── MISS
      ↓
      DB
      ↓
     Cache
```

---

# 51. API + Cache + DB

```text
React
 ↓
ASP.NET API
 ↓
Application
 ↓
Redis
 ↓ miss
MySQL
```

---

# 52. Infrastructure Abstraction

Domínio não deve depender diretamente de:

```text
Redis
Kafka
AWS
Azure
MongoDB
```

Preferir interfaces/adapters.

---

# 53. Cloud-Agnostic Core

```text
Domain
 ↓
Application Ports
 ↓
Infrastructure Adapters
 ├── AWS
 ├── Azure
 └── Local
```

Facilita evolução.

---

# 54. AWS Architecture

```text
Internet
 ↓
CloudFront / ALB / API Gateway
 ↓
ECS / Lambda
 ↓
RDS / DynamoDB / S3
 ↓
SQS / SNS
 ↓
Observability
```

Selecionar apenas serviços necessários.

---

# 55. Azure Architecture

```text
Internet
 ↓
Front Door / Application Gateway
 ↓
Container Apps / AKS / Functions
 ↓
Azure SQL / Storage
 ↓
Service Bus / Event Grid
 ↓
Monitor
```

---

# 56. Local First

Estratégia recomendada para templates:

```text
LOCAL FIRST
 ↓
CONTAINER FIRST
 ↓
CLOUD READY
 ↓
CLOUD TARGET
```

---

# 57. Docker

```text
Docker Compose
├── frontend
├── api
├── mysql
├── mongodb
├── redis
├── broker
└── observability
```

---

# 58. Kubernetes

Adotar quando existir necessidade operacional.

```text
Cluster
├── Deployments
├── Services
├── Ingress
├── ConfigMaps
├── Secrets
└── Autoscaling
```

---

# 59. Scalability

Escala vertical:

```text
bigger machine
```

Escala horizontal:

```text
more instances
```

Arquitetura deve considerar estado e dependências.

---

# 60. Stateless API

Ideal para escalar horizontalmente:

```text
Load Balancer
 ├── API 1
 ├── API 2
 └── API 3
```

Estado compartilhado fica em serviços apropriados.

---

# 61. Availability

```text
Multiple Instances
+
Health Checks
+
Load Balancer
+
Redundancy
```

---

# 62. Resilience

```text
Timeout
Retry
Circuit Breaker
Bulkhead
Fallback
Rate Limit
```

---

# 63. Security Architecture

```text
User
 ↓
Authentication
 ↓
Authorization
 ↓
Application
 ↓
Protected Resources
```

---

# 64. Authentication

Exemplos:

```text
JWT
OAuth 2.0
OpenID Connect
```

---

# 65. Authorization

```text
Role
Permission
Policy
Resource-based authorization
```

---

# 66. Zero Trust

Princípio:

```text
Never trust solely because traffic is internal.
```

Validar identidade e autorização conforme contexto.

---

# 67. Secrets Management

```text
Environment Variables
Secret Manager
Key Vault
IAM
Managed Identity
```

Nunca armazenar secrets reais no Git.

---

# 68. Observability Architecture

```text
Application
 ├── Logs
 ├── Metrics
 └── Traces
      ↓
Observability Platform
```

---

# 69. OpenTelemetry

Instrumentar:

```text
HTTP
Database
Redis
Messaging
External APIs
AI Calls
```

---

# 70. Correlation ID

```text
Request
 ↓
Gateway
 ↓
API
 ↓
Broker
 ↓
Worker
```

O mesmo identificador ajuda a correlacionar a operação.

---

# 71. Health Checks

```text
/live
/ready
/health
```

---

# 72. CI/CD Architecture

```text
Git
 ↓
Build
 ↓
Tests
 ↓
Security
 ↓
Artifact
 ↓
DEV
 ↓
HML
 ↓
PROD
```

---

# 73. Infrastructure as Code

```text
Terraform
CloudFormation
Bicep
```

Infraestrutura deve ser reproduzível.

---

# 74. GitFlow

```text
feature/task-*
 ↓
develop
 ↓
hml
 ↓
release/*
 ↓
main
```

---

# 75. Testing Architecture

```text
Unit
Integration
Architecture
Contract
E2E
```

Cada nível cobre risco diferente.

---

# 76. Architecture Tests

Exemplo:

```text
Domain must not reference Infrastructure
```

Transforma regras arquiteturais em testes.

---

# 77. Architecture Decision Record

```text
docs/adr/
├── ADR-001-modular-monolith.md
├── ADR-002-redis.md
└── ADR-003-messaging.md
```

Documenta decisões e trade-offs.

---

# 78. C4 Model

Diagramas:

```text
Level 1 → Context
Level 2 → Container
Level 3 → Component
Level 4 → Code
```

Nem todo projeto precisa desenhar todos os níveis.

---

# 79. Draw.io

No Kit IA Dev, diagramas podem ser mantidos em:

```text
docs/architecture/
├── context.drawio
├── containers.drawio
├── backend.drawio
├── frontend.drawio
└── infrastructure.drawio
```

---

# 80. Sequence Diagram

Mostra fluxo temporal.

```text
User → Frontend
Frontend → API
API → Redis
Redis → API
API → DB
API → Frontend
```

---

# 81. ER Diagram

Mostra modelo relacional.

```text
User
 ↓
Role
 ↓
Permission
```

---

# 82. Deployment Diagram

```text
Internet
 ↓
Load Balancer
 ↓
Containers
 ↓
Databases
```

---

# 83. AI Architecture

```text
Frontend
 ↓
ASP.NET Core
 ↓
AI Orchestrator
 ├── LLM
 ├── RAG
 ├── Memory
 ├── Tools
 └── Agents
```

---

# 84. RAG Architecture

```text
Documents
 ↓
Chunking
 ↓
Embeddings
 ↓
Vector DB
 ↓
Retriever
 ↓
LLM
```

---

# 85. Agentic Architecture

```text
Goal
 ↓
Planner
 ↓
Agent
 ├── Memory
 ├── Tools
 ├── RAG
 └── Policies
 ↓
Action
```

---

# 86. Multi-Agent Architecture

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

# 87. MCP Architecture

```text
Agent
 ↓
MCP Client
 ↓
MCP Servers
 ├── GitHub
 ├── Files
 ├── Database
 └── External Tools
```

---

# 88. Hybrid AI Architecture

```text
Application
 ↓
AI Router
 ├── Local LLM
 └── Cloud LLM
```

Pode escolher provider por:

```text
privacy
cost
complexity
latency
availability
```

---

# 89. Architecture for CMS

Exemplo:

```text
React Site
React Admin
      ↓
API Gateway
 ├── Auth API
 ├── Admin API
 └── Site API
      ↓
Application / Domain
      ↓
MySQL + Redis + MongoDB
      ↓
Messaging
```

---

# 90. Read Architecture

```text
Query
 ↓
Cache
 ├── HIT → Response
 └── MISS
      ↓
      Database
      ↓
      Cache
```

---

# 91. Write Architecture

```text
Command
 ↓
Domain
 ↓
Database
 ↓
Domain Event
 ↓
Outbox
 ↓
Broker
```

---

# 92. Async Processing

```text
API
 ↓
Queue
 ↓
Worker
 ↓
External Integration
```

Bom para tarefas demoradas.

---

# 93. Background Jobs

Exemplos:

```text
email
reports
document processing
cleanup
reindexing
AI processing
```

---

# 94. Scheduled Jobs

```text
Scheduler
 ↓
Job
 ↓
Application Service
```

Exemplo:

```text
daily report
cache cleanup
data synchronization
```

---

# 95. Batch Architecture

```text
Source
 ↓
Reader
 ↓
Processor
 ↓
Writer
```

Pode ser adequada para grandes volumes offline.

---

# 96. Streaming Architecture

```text
Events
 ↓
Stream
 ↓
Processors
 ↓
Real-time Projections
```

---

# 97. Architecture Selection Matrix

| Cenário | Candidato |
|---|---|
| Sistema pequeno | Monólito |
| Domínio crescente | Modular Monolith |
| Times/domínios independentes | Microsserviços |
| Integração desacoplada | Event-Driven |
| Processamento sob evento | Serverless |
| Frontend complexo | SPA/BFF |
| Conteúdo público | SSR/SSG |
| IA com conhecimento privado | RAG |
| Automação inteligente | Agentic AI |

Isso é ponto de partida, não regra absoluta.

---

# 98. Trade-offs

Toda decisão possui custo.

Exemplo:

```text
Microservices
+
Independent Deployment

but

-
Operational Complexity
Distributed Failures
Observability Cost
```

---

# 99. Architecture Fitness Functions

Criar validações automatizadas.

Exemplos:

```text
dependency rules
latency limits
coverage
security
container size
API compatibility
```

---

# 100. Evolutionary Architecture

Arquitetura deve permitir evolução.

```text
Simple
 ↓
Measure
 ↓
Identify Pressure
 ↓
Evolve
```

Não antecipar toda complexidade futura.

---

# 101. YAGNI

```text
You Aren't Gonna Need It
```

Não adicionar tecnologia sem necessidade comprovada.

---

# 102. KISS

```text
Keep It Simple
```

Arquitetura simples que atende requisitos costuma ser melhor que arquitetura sofisticada sem necessidade.

---

# 103. SOLID

```text
SRP
OCP
LSP
ISP
DIP
```

Ajuda a organizar componentes internos.

---

# 104. Clean Code

Arquitetura não compensa código ruim.

Aplicar:

```text
clear naming
small responsibilities
explicit dependencies
testability
low accidental complexity
```

---

# 105. Architecture Governance

Definir:

```text
standards
ADRs
templates
quality gates
reviews
architecture tests
```

---

# 106. Architecture Review

Perguntas:

1. Qual problema resolve?
2. Quais são os boundaries?
3. Onde estão os dados?
4. Quem é owner?
5. Quais dependências?
6. Como falha?
7. Como escala?
8. Como protege?
9. Como observa?
10. Como testa?
11. Como implanta?
12. Como evolui?

---

# 107. Kit IA Dev

Estrutura:

```text
Kit-IA-Dev/
├── 2-Agents/
│   └── architect/
├── 3-Skills/
│   ├── architecture-design/
│   └── architecture-review/
├── 4-Templates/
│   ├── modular-monolith/
│   ├── microservices/
│   └── cloud/
├── 5-Workflows/
│   └── architecture/
├── 6-Quality-Gates/
│   └── architecture/
└── 8-Dictionary/
    └── 16-arquitetura-e-aplicacoes.md
```

---

# 108. Architect Agent

Responsabilidades:

```text
read requirements
identify drivers
identify constraints
propose options
compare trade-offs
select architecture
generate ADRs
generate diagrams
define quality gates
```

---

# 109. Architecture Workflow

```text
Requirements
 ↓
Architecture Drivers
 ↓
Options
 ↓
Trade-off Analysis
 ↓
Decision
 ↓
ADR
 ↓
Diagrams
 ↓
Implementation Plan
 ↓
Quality Gates
```

---

# 110. Quality Gates

- [ ] arquitetura atende requisitos;
- [ ] boundaries definidos;
- [ ] dependências permitidas documentadas;
- [ ] dados e ownership definidos;
- [ ] segurança definida;
- [ ] observabilidade definida;
- [ ] testes definidos;
- [ ] deployment definido;
- [ ] rollback considerado;
- [ ] custos considerados;
- [ ] ADR criado para decisão relevante;
- [ ] diagramas atualizados;
- [ ] complexidade justificada.

---

# 111. Anti-patterns

Evitar:

```text
architecture by hype
microservices by default
shared database without ownership
domain coupled to cloud provider
business logic in controller
business logic in gateway
no observability
no architecture tests
no ADR
diagram disconnected from implementation
too many technologies
```

---

# 112. Regra para Agentes

Antes de alterar arquitetura:

1. Ler requisitos.
2. Identificar drivers.
3. Identificar restrições.
4. Mapear arquitetura atual.
5. Identificar impacto.
6. Criar opções.
7. Comparar trade-offs.
8. Selecionar solução mínima suficiente.
9. Registrar ADR.
10. Atualizar diagramas.
11. Criar/atualizar testes arquiteturais.
12. Executar Quality Gates.

---

# 113. Relação com outros itens

```text
01 - Estrutura de Projeto
01.1 - Estrutura de Projeto
01.2 - Agentic Workflow
02 - RAG
05 - Conectores e Funções
11 - CI/CD
13 - Projetar Microsserviços
15 - RAG System
17 - Agentic AI
18 - Kit IA Dev
```

---

# 114. Resumo

Arquitetura não começa escolhendo:

```text
Kafka
Kubernetes
Microservices
Redis
AWS
Azure
```

Começa com:

```text
PROBLEM
 ↓
REQUIREMENTS
 ↓
QUALITY ATTRIBUTES
 ↓
CONSTRAINTS
 ↓
TRADE-OFFS
 ↓
ARCHITECTURE
```

Para o Kit IA Dev, a arquitetura recomendada deve ser **evolutiva, testável, observável, segura e justificável**, privilegiando a solução mais simples capaz de atender os requisitos atuais sem impedir evolução futura.

---

# 📁 Arquivo

```text
16-arquitetura-e-aplicacoes.md
```
