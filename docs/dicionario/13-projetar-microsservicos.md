# 📘 Dicionário Técnico — 13 Projetar Microsserviços

> **Categoria:** Arquitetura de Software / Sistemas Distribuídos  
> **Código:** 13  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** .NET / ASP.NET Core / AWS / Azure / Docker / Kubernetes / Mensageria  
> **Objetivo:** Definir um método prático para projetar microsserviços, delimitar responsabilidades, escolher comunicação, dados, resiliência, observabilidade, segurança, testes e implantação.

---

# 1. O que são Microsserviços

Microsserviços são uma abordagem arquitetural na qual um sistema é dividido em serviços independentes, cada um responsável por uma capacidade de negócio bem definida.

```text
Application
├── Identity Service
├── Customer Service
├── Order Service
├── Payment Service
├── Notification Service
└── Reporting Service
```

Cada serviço deve possuir responsabilidade clara e poder evoluir com baixo acoplamento.

---

# 2. Microsserviço não é apenas uma API pequena

Errado:

```text
Controller
+
Database
=
Microservice
```

Um microsserviço deve representar uma fronteira coerente de negócio e possuir autonomia operacional adequada.

---

# 3. Começar pelo domínio

Antes de criar serviços:

```text
Business Domain
 ↓
Capabilities
 ↓
Bounded Contexts
 ↓
Service Boundaries
```

Evitar começar dividindo o sistema por tabelas ou entidades CRUD.

---

# 4. Domain-Driven Design

DDD ajuda a identificar limites.

Conceitos importantes:

```text
Domain
Subdomain
Bounded Context
Aggregate
Entity
Value Object
Domain Event
Ubiquitous Language
```

---

# 5. Bounded Context

Um Bounded Context define um limite semântico.

Exemplo:

```text
Sales
Billing
Identity
Shipping
Support
```

A entidade `Customer` pode ter significados diferentes em contextos distintos.

---

# 6. Decomposição por capacidade

Exemplo de e-commerce:

```text
Identity
Catalog
Cart
Orders
Payments
Shipping
Notifications
```

Isso costuma ser melhor do que:

```text
UserTableService
ProductTableService
OrderTableService
```

---

# 7. Service Boundary

Perguntas:

1. Qual capacidade de negócio pertence ao serviço?
2. Quais dados ele controla?
3. Quem pode alterá-los?
4. Quais eventos ele publica?
5. Quais comandos recebe?
6. Pode ser implantado de forma independente?

---

# 8. Database per Service

Princípio comum:

```text
Service A → Database A
Service B → Database B
Service C → Database C
```

Outro serviço não deve manipular diretamente as tabelas internas de um serviço.

---

# 9. Polyglot Persistence

Cada serviço pode utilizar tecnologia adequada.

Exemplo:

```text
Orders        → MySQL
Documents     → MongoDB
Cache         → Redis
Search        → OpenSearch
```

Não utilizar tecnologias diferentes apenas por moda.

---

# 10. Comunicação síncrona

Exemplo:

```text
Service A
 ↓ HTTP/gRPC
Service B
```

Boa para situações em que A precisa de uma resposta imediata de B.

Trade-offs:

```text
latency
availability coupling
timeouts
cascading failures
```

---

# 11. Comunicação assíncrona

```text
Service A
 ↓
Broker
 ↓
Service B
```

Útil quando não é necessária resposta imediata.

Benefícios:

```text
decoupling
buffering
independent processing
event-driven workflows
```

---

# 12. Commands x Events

Command:

```text
"ProcessPayment"
```

Representa intenção direcionada.

Event:

```text
"OrderCreated"
```

Representa algo que já aconteceu.

Não tratar tudo como evento genérico.

---

# 13. Event-Driven Architecture

```text
Order Service
 ↓
OrderCreated
 ↓
Broker
 ├── Payment Service
 ├── Notification Service
 └── Analytics Service
```

Produtor não precisa conhecer todos os consumidores.

---

# 14. RabbitMQ

Adequado para muitos cenários de filas e processamento assíncrono.

```text
Producer
 ↓
Exchange
 ↓
Queue
 ↓
Consumer
```

---

# 15. Kafka

Adequado para event streaming e retenção/replay de eventos em cenários compatíveis.

```text
Producer
 ↓
Topic
 ↓
Partitions
 ↓
Consumer Groups
```

---

# 16. AWS SQS

Fila gerenciada.

```text
Service
 ↓
SQS
 ↓
Worker
```

Pode substituir infraestrutura de filas autogerenciada em arquiteturas AWS quando adequado.

---

# 17. AWS SNS

Pub/Sub:

```text
Service
 ↓
SNS Topic
 ├── SQS A
 ├── SQS B
 └── Lambda
```

---

# 18. API Gateway

Ponto de entrada:

```text
Client
 ↓
API Gateway
 ├── Identity
 ├── Orders
 ├── Catalog
 └── Payments
```

Responsabilidades possíveis:

```text
routing
authentication
rate limiting
TLS
observability
```

Evitar colocar regras de domínio no gateway.

---

# 19. YARP

Em .NET, YARP pode ser utilizado como reverse proxy/gateway em determinados cenários.

```text
Client
 ↓
YARP
 ↓
ASP.NET Core Services
```

---

# 20. Service Discovery

Em ambientes dinâmicos, serviços precisam localizar outros serviços.

Plataformas como Kubernetes e orquestradores cloud oferecem mecanismos próprios.

---

# 21. Resiliência

Sistemas distribuídos falham parcialmente.

Projetar para:

```text
timeout
retry
circuit breaker
bulkhead
fallback
rate limiting
```

---

# 22. Timeout

Toda chamada remota deve possuir limite.

```text
Service A
 ↓
Service B
```

Nunca depender de espera infinita.

---

# 23. Retry

Aplicar apenas a falhas transitórias e operações seguras/idempotentes.

```text
Failure
 ↓
Backoff
 ↓
Retry
```

Evitar retry infinito.

---

# 24. Exponential Backoff

```text
1s
2s
4s
8s
```

Adicionar jitter ajuda a evitar múltiplos clientes repetindo ao mesmo tempo.

---

# 25. Circuit Breaker

```text
Failures
 ↓
Circuit Open
 ↓
Stop Calls
 ↓
Recovery Probe
 ↓
Close
```

Protege contra dependência continuamente indisponível.

---

# 26. Bulkhead

Isola recursos.

```text
Service
├── Pool A
├── Pool B
└── Pool C
```

Uma integração problemática não deve consumir todos os recursos.

---

# 27. Idempotência

Processar a mesma mensagem mais de uma vez não deve causar efeitos duplicados indevidos.

```text
MessageId
 ↓
Already Processed?
 ├── Yes → Ignore / Return Result
 └── No  → Process
```

Essencial em mensageria.

---

# 28. At-least-once delivery

Muitos brokers podem entregar novamente.

Portanto:

```text
Consumer
=
Idempotent
```

deve ser uma premissa frequente.

---

# 29. Dead Letter Queue

Mensagens que não conseguem ser processadas após política de retry:

```text
Queue
 ↓
Retries
 ↓
DLQ
```

DLQ precisa ser monitorada.

---

# 30. Transactional Outbox

Problema:

```text
Save Database
 ↓
Publish Event
```

Se a aplicação cair entre as operações, banco e broker podem divergir.

Solução:

```text
Transaction
├── Business Data
└── Outbox Message

Outbox Worker
 ↓
Broker
```

---

# 31. Inbox Pattern

Consumidor registra mensagens processadas.

```text
Message
 ↓
Inbox
 ↓
Duplicate?
 ├── Yes → Skip
 └── No → Process
```

Ajuda na idempotência.

---

# 32. Saga

Coordena processo distribuído de longa duração.

Exemplo:

```text
Create Order
 ↓
Reserve Inventory
 ↓
Charge Payment
 ↓
Create Shipment
```

Se algo falhar, podem existir ações compensatórias.

---

# 33. Saga Orchestration

```text
Saga Orchestrator
 ├── Order
 ├── Inventory
 ├── Payment
 └── Shipping
```

Existe um coordenador explícito.

---

# 34. Saga Choreography

```text
OrderCreated
 ↓
InventoryReserved
 ↓
PaymentApproved
 ↓
ShipmentCreated
```

Serviços reagem a eventos.

Trade-off: fluxos podem ficar difíceis de visualizar sem boa observabilidade.

---

# 35. Distributed Transaction

Evitar depender de transação ACID única entre serviços.

Em sistemas distribuídos, frequentemente utilizamos:

```text
local transactions
+
events
+
eventual consistency
+
compensation
```

---

# 36. Eventual Consistency

Nem todos os dados ficam atualizados instantaneamente.

```text
Write
 ↓
Event
 ↓
Projection
 ↓
Eventually Updated
```

O negócio precisa aceitar essa característica quando adotada.

---

# 37. CQRS

Separar escrita e leitura:

```text
Commands
 ↓
Write Model

Queries
 ↓
Read Model
```

Não é obrigatório em todo microsserviço.

---

# 38. Read Models

Podem utilizar:

```text
MongoDB
Redis
SQL
Search Engine
```

conforme necessidade.

---

# 39. Cache

Padrão:

```text
Query
 ↓
Redis
 ├── HIT → Return
 └── MISS
       ↓
      DB
       ↓
     Cache
```

---

# 40. Cache Invalidation

Ao alterar dados:

```text
Command
 ↓
Database
 ↓
Domain Event
 ↓
Invalidate Cache
```

Cache sem estratégia de invalidação gera dados obsoletos.

---

# 41. Domain Events

Evento interno ao domínio:

```text
Order
 ↓
OrderCreatedDomainEvent
 ↓
Application Handler
```

Não acoplar diretamente domínio ao Kafka, RabbitMQ ou SQS.

---

# 42. Integration Events

Evento publicado para outros serviços:

```text
Domain Event
 ↓
Application / Outbox
 ↓
Integration Event
 ↓
Broker
```

Separar evento de domínio de contrato externo.

---

# 43. Contratos

Contratos entre serviços precisam de versionamento.

Exemplo:

```text
OrderCreatedV1
```

Mudanças incompatíveis exigem estratégia de evolução.

---

# 44. Backward Compatibility

Preferir mudanças aditivas.

Exemplo:

```text
Add optional field
```

é normalmente menos arriscado que remover/renomear campo consumido.

---

# 45. API Versioning

Exemplo:

```text
/api/v1/orders
/api/v2/orders
```

Usar apenas quando houver necessidade real de manter contratos incompatíveis.

---

# 46. Segurança

Cada serviço deve considerar:

```text
Authentication
Authorization
Secrets
TLS
Input Validation
Rate Limiting
Audit
```

---

# 47. JWT

Fluxo possível:

```text
Client
 ↓
Identity
 ↓
JWT
 ↓
Gateway / Services
```

Serviços devem validar token conforme arquitetura definida.

---

# 48. Authorization

Não basta autenticar.

```text
User
 ↓
Role / Permission / Policy
 ↓
Resource
```

---

# 49. Service-to-Service Authentication

Comunicação interna também precisa de confiança explícita.

Possibilidades:

```text
mTLS
workload identity
managed identity
IAM roles
service tokens
```

---

# 50. Secrets

Nunca armazenar:

```text
password
API key
connection string
private key
```

diretamente no repositório.

---

# 51. Observabilidade

Três pilares tradicionais:

```text
Logs
Metrics
Traces
```

Complementados por:

```text
Health Checks
Correlation IDs
Business Metrics
```

---

# 52. Structured Logging

```text
Timestamp
Service
Level
TraceId
CorrelationId
Message
```

---

# 53. Distributed Tracing

```text
Client
 ↓ TraceId
Gateway
 ↓
Order Service
 ↓
Payment Service
 ↓
Database
```

Permite seguir uma requisição entre componentes.

---

# 54. OpenTelemetry

Instrumentação comum para:

```text
HTTP
Database
Redis
Messaging
External APIs
```

---

# 55. Metrics

Exemplos:

```text
requests/sec
latency
error rate
queue depth
consumer lag
CPU
memory
```

---

# 56. Health Checks

```text
/live
/ready
/health
```

Separar:

```text
Liveness
Readiness
Dependencies
```

---

# 57. Correlation ID

```text
Request
 ↓
CorrelationId
 ↓
Gateway
 ↓
Services
 ↓
Events
```

Propagar também em mensagens quando apropriado.

---

# 58. Docker

Cada serviço pode possuir imagem própria.

```text
services/
├── identity/
│   └── Dockerfile
├── orders/
│   └── Dockerfile
└── payments/
    └── Dockerfile
```

---

# 59. Docker Compose

Ambiente local:

```text
docker-compose
├── gateway
├── identity
├── orders
├── payments
├── mysql
├── redis
├── rabbitmq
└── observability
```

---

# 60. Kubernetes

Quando a complexidade operacional justificar:

```text
Kubernetes
├── Deployments
├── Services
├── ConfigMaps
├── Secrets
├── Ingress
└── Autoscaling
```

Não adotar Kubernetes apenas porque existem microsserviços.

---

# 61. AWS ECS

Arquitetura possível:

```text
ALB
 ↓
ECS Services
 ├── Identity
 ├── Orders
 └── Payments
```

---

# 62. AWS Lambda

Boa opção para workloads event-driven/serverless adequados.

```text
SQS
 ↓
Lambda
 ↓
Database
```

---

# 63. S3

Pode armazenar:

```text
documents
images
exports
attachments
```

Não usar banco relacional para blobs grandes sem necessidade.

---

# 64. SNS + SQS

```text
Service
 ↓
SNS
 ├── SQS Notification
 ├── SQS Analytics
 └── SQS Audit
```

Permite fan-out gerenciado.

---

# 65. Azure equivalente

Arquitetura pode utilizar serviços equivalentes:

```text
Service Bus
Event Grid
Functions
Blob Storage
Container Apps / AKS
Key Vault
```

A arquitetura de domínio não deve depender diretamente do fornecedor.

---

# 66. Clean Architecture por serviço

```text
Service/
├── Domain/
├── Application/
├── Infrastructure/
└── Api/
```

---

# 67. Vertical Slice

Dentro de Application/API:

```text
Features/
├── CreateOrder/
├── CancelOrder/
└── GetOrder/
```

Cada slice concentra o fluxo da funcionalidade.

---

# 68. Estrutura exemplo

```text
services/
└── orders/
    ├── src/
    │   ├── Orders.Domain/
    │   ├── Orders.Application/
    │   ├── Orders.Infrastructure/
    │   └── Orders.Api/
    └── tests/
        ├── Orders.UnitTests/
        └── Orders.IntegrationTests/
```

---

# 69. SOLID

Microsserviços não substituem SOLID.

Aplicar:

```text
SRP
OCP
LSP
ISP
DIP
```

principalmente dentro dos serviços.

---

# 70. Testes

Estratégia:

```text
Unit
Integration
Contract
Architecture
E2E
```

---

# 71. Unit Tests

Testam domínio e regras isoladamente.

```text
Order
 ↓
Business Rule
 ↓
Expected Result
```

---

# 72. Integration Tests

Testam:

```text
API
Database
Cache
Broker
External adapters
```

Utilizar infraestrutura efêmera quando possível.

---

# 73. Contract Tests

Muito importantes para evitar quebra entre serviços.

```text
Consumer Expectation
 ↓
Provider Verification
```

---

# 74. E2E

Reservar para jornadas críticas.

```text
Create Account
 ↓
Create Order
 ↓
Payment
 ↓
Notification
```

---

# 75. CI/CD

Cada serviço pode possuir pipeline independente.

```text
Change Orders
 ↓
Orders Pipeline
 ↓
Orders Image
 ↓
Orders Deployment
```

Evitar obrigar redeploy de todos os serviços para qualquer mudança.

---

# 76. Monorepo

Estrutura:

```text
repo/
├── services/
│   ├── identity/
│   ├── orders/
│   └── payments/
└── shared/
```

Pipeline deve detectar componentes alterados quando possível.

---

# 77. Polyrepo

```text
identity-repo
orders-repo
payments-repo
```

Maior independência, mas também maior custo de governança.

---

# 78. Shared Library

Cuidado com bibliotecas compartilhadas.

Bom para:

```text
technical primitives
observability
common infrastructure abstractions
```

Perigoso para:

```text
shared domain model
```

Isso pode reacoplar serviços.

---

# 79. Shared Kernel

Se necessário, deve ser pequeno e explicitamente governado.

---

# 80. Anti-Corruption Layer

Ao integrar sistemas externos:

```text
External Model
 ↓
Adapter / ACL
 ↓
Internal Domain Model
```

Evita contaminar o domínio.

---

# 81. Strangler Pattern

Para migrar monólito gradualmente:

```text
Monolith
 ↓
Extract Capability
 ↓
Route Traffic
 ↓
New Service
```

Repetir progressivamente.

---

# 82. Modular Monolith First

Nem todo sistema precisa começar com microsserviços.

Estratégia muito útil:

```text
Modular Monolith
 ↓
Clear Boundaries
 ↓
Measure Need
 ↓
Extract Service
```

Isso reduz complexidade prematura.

---

# 83. Quando usar microsserviços

Bons sinais:

```text
independent scaling
independent deployment
clear bounded contexts
different team ownership
different reliability needs
large evolving platform
```

---

# 84. Quando evitar

Evitar se:

```text
small team
simple domain
low scale
unclear boundaries
immature DevOps
no observability
```

Um monólito modular pode ser melhor.

---

# 85. Distributed Monolith

Pior cenário:

```text
many services
+
shared database
+
synchronous dependency everywhere
+
single deployment
```

Você recebe complexidade distribuída sem autonomia.

---

# 86. Chatty Services

Anti-pattern:

```text
Service A
 ↓
B
 ↓
C
 ↓
D
 ↓
E
```

para completar uma operação simples.

Reavaliar boundaries e dados.

---

# 87. N+1 entre serviços

Evitar:

```text
GET Orders
 ↓
for each Order
    GET Customer
```

Pode gerar centenas de chamadas.

Usar contratos adequados, projeções ou agregação conforme o caso.

---

# 88. API Composition

```text
Aggregator
 ├── Service A
 ├── Service B
 └── Service C
```

Pode ser útil para algumas telas, mas precisa de controle de latência e falhas.

---

# 89. BFF

Backend for Frontend:

```text
Web
 ↓
Web BFF

Mobile
 ↓
Mobile BFF
```

Útil quando clientes possuem necessidades muito diferentes.

---

# 90. Data Ownership

Regra:

```text
Orders Service
owns
Orders Data
```

Outro serviço pergunta via contrato ou consome evento/projeção.

---

# 91. Reporting

Relatórios que precisam de vários domínios podem utilizar:

```text
Events
 ↓
Reporting Projection
 ↓
Read Database
```

em vez de joins diretos entre bancos de serviços.

---

# 92. Audit

Eventos e logs de auditoria devem permitir responder:

```text
who
what
when
where
correlation
```

Sem registrar secrets.

---

# 93. Compliance

Em domínios regulados:

```text
audit trail
data retention
access control
encryption
PII handling
```

devem entrar no desenho desde o início.

---

# 94. Diagrama de Contexto

```text
Users
 ↓
Platform
 ↓
External Systems
```

Primeiro nível de visão.

---

# 95. Diagrama de Containers

```text
Frontend
 ↓
Gateway
 ├── Identity
 ├── Orders
 └── Payments
```

Pode ser documentado usando C4/draw.io.

---

# 96. Diagrama por Serviço

Documentar:

```text
API
Application
Domain
Infrastructure
Database
Broker
External Dependencies
```

---

# 97. Sequence Diagram

Exemplo:

```text
Client → Gateway
Gateway → Order
Order → DB
Order → Outbox
Outbox → Broker
Broker → Payment
```

Muito útil para fluxos distribuídos.

---

# 98. ADR

Decisões importantes devem ser registradas.

Exemplo:

```text
ADR-001 - Use RabbitMQ for Commands
ADR-002 - Use Kafka for Event Streaming
ADR-003 - Database per Service
```

---

# 99. Service Catalog

Manter catálogo:

```text
Service
Owner
Domain
Repository
API
Database
Events
Dependencies
SLO
Dashboard
```

---

# 100. SLI / SLO

Definir expectativas operacionais.

Exemplo:

```text
Availability
Latency
Error Rate
```

Evitar exigir o mesmo nível de disponibilidade para todo serviço sem necessidade.

---

# 101. Dependency Map

```text
Gateway
├── Identity
├── Orders
│   └── Payment
└── Catalog
```

Quanto mais dependências síncronas, maior o risco de cascata.

---

# 102. Local Development

Desenvolvedor deve conseguir iniciar o necessário facilmente.

```text
docker compose up
```

Pode subir:

```text
databases
cache
broker
observability
local cloud emulator
```

---

# 103. Test Environment

Separar:

```text
test
dev
hml
prod
```

Dados e credenciais nunca devem ser compartilhados indevidamente.

---

# 104. LocalStack

Para AWS local:

```text
Application
 ↓
LocalStack
 ├── SQS
 ├── SNS
 ├── S3
 └── other supported services
```

Bom para desenvolvimento/testes, respeitando diferenças em relação à AWS real.

---

# 105. Evolução arquitetural

Estratégia recomendada:

```text
LOCAL FIRST
 ↓
CONTAINER FIRST
 ↓
CLOUD READY
 ↓
AWS / AZURE TARGET
```

---

# 106. Agentes no Kit IA Dev

```text
Requirements Agent
 ↓
Domain Analysis
 ↓
Architect Agent
 ↓
Service Boundaries
 ↓
Developer Agents
 ↓
Tester
 ↓
Reviewer
 ↓
DevOps
```

---

# 107. Architect Agent

Deve avaliar:

```text
bounded contexts
service boundaries
data ownership
communication
consistency
resilience
security
observability
deployment
```

---

# 108. Developer Agent

Não deve criar integração direta sem contrato.

Fluxo:

```text
Requirement
 ↓
Contract
 ↓
Implementation
 ↓
Tests
 ↓
Observability
```

---

# 109. Reviewer Agent

Verificar:

- acoplamento;
- dependências síncronas;
- shared database;
- idempotência;
- timeout;
- retry;
- DLQ;
- outbox;
- segurança;
- testes;
- observabilidade.

---

# 110. Quality Gates

Antes de aprovar um novo microsserviço:

- [ ] bounded context identificado;
- [ ] responsabilidade clara;
- [ ] dados possuem owner;
- [ ] contratos definidos;
- [ ] eventos versionados;
- [ ] timeouts configurados;
- [ ] retries controlados;
- [ ] idempotência tratada;
- [ ] DLQ definida quando necessária;
- [ ] outbox avaliado;
- [ ] autenticação/autorização definidas;
- [ ] observabilidade configurada;
- [ ] testes automatizados;
- [ ] Docker;
- [ ] pipeline CI/CD;
- [ ] documentação e diagramas;
- [ ] estratégia de rollback.

---

# 111. Anti-patterns

Evitar:

```text
service per table
shared database
distributed monolith
chatty APIs
retry infinito
eventos sem versionamento
mensagens sem idempotência
broker dentro do Domain
deploy acoplado
sem tracing
sem ownership
microservices before domain boundaries
```

---

# 112. Estrutura no Kit IA Dev

```text
Kit-IA-Dev/
├── 2-Agents/
│   └── architect/
├── 3-Skills/
│   └── microservices-design/
├── 4-Templates/
│   └── dotnet-microservice/
├── 5-Workflows/
│   └── service-design/
├── 6-Quality-Gates/
│   └── microservices/
└── 8-Dictionary/
    └── 13-projetar-microsservicos.md
```

---

# 113. Skill microservices-design

Responsabilidades:

```text
analyze domain
identify boundaries
define contracts
define data ownership
choose sync/async
define resilience
define observability
define security
define deployment
generate diagrams
```

---

# 114. Fluxo completo

```text
BUSINESS DOMAIN
      ↓
DOMAIN ANALYSIS
      ↓
BOUNDED CONTEXTS
      ↓
SERVICE BOUNDARIES
      ↓
DATA OWNERSHIP
      ↓
CONTRACTS
      ↓
SYNC / ASYNC COMMUNICATION
      ↓
RESILIENCE
      ↓
SECURITY
      ↓
OBSERVABILITY
      ↓
TESTING
      ↓
CI/CD
      ↓
DEPLOYMENT
      ↓
OPERATIONS
```

---

# 115. Regra principal

Antes de criar um microsserviço, responder:

1. Qual problema de negócio ele resolve?
2. Qual bounded context representa?
3. Quais dados possui?
4. Quem altera esses dados?
5. Quais comandos recebe?
6. Quais eventos publica?
7. Quais eventos consome?
8. Quais dependências síncronas possui?
9. Como trata indisponibilidade?
10. Como garante idempotência?
11. Como será observado?
12. Como será testado?
13. Como será implantado?
14. Como será versionado?
15. Ele realmente precisa ser um serviço separado?

---

# 116. Relação com outros itens

```text
01 - Estrutura de Projeto
01.2 - Agentic Workflow
03 - Plugins
05 - Conectores e Funções
11 - CI/CD
16 - Arquitetura de Aplicações
17 - Agentic AI
18 - Kit IA Dev
```

---

# 117. Resumo

Projetar microsserviços corretamente não significa dividir uma aplicação em muitas APIs.

A sequência correta é:

```text
DOMAIN
 ↓
BOUNDARIES
 ↓
OWNERSHIP
 ↓
CONTRACTS
 ↓
COMMUNICATION
 ↓
CONSISTENCY
 ↓
RESILIENCE
 ↓
SECURITY
 ↓
OBSERVABILITY
 ↓
DELIVERY
```

Para o Kit IA Dev, a IA deve primeiro questionar se microsserviços são realmente necessários. Quando forem, deve preservar autonomia, baixo acoplamento, ownership de dados, contratos explícitos, mensageria resiliente, observabilidade distribuída e pipelines independentes.

---

# 📁 Arquivo

```text
13-projetar-microsservicos.md
```
