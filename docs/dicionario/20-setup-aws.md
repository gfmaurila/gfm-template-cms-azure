# 📘 Dicionário Técnico — 20 Setup AWS

> **Categoria:** Cloud / AWS / DevOps / Arquitetura  
> **Código:** 20  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** .NET / Docker / LocalStack / AWS / CI/CD / Observabilidade  
> **Objetivo:** Padronizar o setup AWS dos projetos do Kit IA Dev, mantendo desenvolvimento local reproduzível, infraestrutura desacoplada do domínio e evolução progressiva até produção em AWS.

---

# 1. Objetivo do Setup AWS

O setup AWS deve permitir a evolução:

```text
LOCAL FIRST
    ↓
CONTAINER FIRST
    ↓
CLOUD READY
    ↓
AWS TARGET
```

A aplicação deve funcionar localmente antes de depender da nuvem.

---

# 2. Princípio principal

Não acoplar o domínio diretamente à AWS.

Evitar:

```text
Domain
 ↓
AWS SDK
```

Preferir:

```text
Domain
 ↓
Application Ports
 ↓
Infrastructure Adapters
 ↓
AWS SDK
```

---

# 3. Arquitetura base

```text
Frontend
   ↓
API / Gateway
   ↓
Application
   ↓
Domain
   ↓
Infrastructure
   ├── MySQL
   ├── MongoDB
   ├── Redis
   ├── Messaging
   ├── Storage
   └── AWS Adapters
```

---

# 4. Estrutura .NET recomendada

```text
src/
├── Domain/
├── Application/
├── Infrastructure/
├── Api/
└── CrossCutting/
```

Com módulos quando necessário:

```text
Modules/
├── Identity/
├── Users/
├── Content/
└── Notifications/
```

---

# 5. Domain

Responsável por:

```text
Entities
Value Objects
Aggregates
Domain Services
Domain Events
Business Rules
```

Não deve conhecer:

```text
SQS
SNS
S3
Lambda
ECS
Redis
Kafka
RabbitMQ
```

---

# 6. Application

Contém:

```text
Commands
Queries
Handlers
Validators
Interfaces
Use Cases
Policies
```

---

# 7. Infrastructure

Implementa integrações:

```text
Persistence
Caching
Messaging
Storage
Cloud
Observability
External APIs
```

---

# 8. CrossCutting

Pode concentrar:

```text
Dependency Injection
Logging
Tracing
Configuration
Security helpers
Resilience
```

Sem virar depósito genérico de código.

---

# 9. SOLID

O setup deve preservar:

```text
S — Single Responsibility
O — Open/Closed
L — Liskov Substitution
I — Interface Segregation
D — Dependency Inversion
```

Especialmente:

```text
Application
 ↓
Interface
 ↓
AWS Adapter
```

---

# 10. CQRS

```text
Commands
→ alteração de estado

Queries
→ leitura
```

Exemplo:

```text
CreateUserCommand
GetUserByIdQuery
```

---

# 11. Domain Events

```text
Aggregate
 ↓
Domain Event
 ↓
Application Handler
```

Domain Event não deve ser equivalente diretamente a mensagem SQS/SNS/Kafka.

---

# 12. Integration Events

Depois da decisão interna:

```text
Domain Event
 ↓
Application
 ↓
Integration Event
 ↓
Broker
```

---

# 13. Transactional Outbox

Para reduzir inconsistência:

```text
Business Transaction
      +
Outbox Record
      ↓
Commit
      ↓
Outbox Publisher
      ↓
Broker
```

---

# 14. Local First

Todo desenvolvedor deve conseguir executar o projeto sem precisar de uma conta AWS para o fluxo básico.

```text
Git Clone
 ↓
Environment Setup
 ↓
Docker Compose
 ↓
Application Running
```

---

# 15. Container First

Dependências locais devem preferencialmente estar containerizadas.

```text
docker-compose
├── APIs
├── frontend
├── mysql
├── mongodb
├── redis
├── rabbitmq
├── kafka
├── localstack
└── observability
```

Adicionar somente componentes necessários ao projeto.

---

# 16. LocalStack

LocalStack pode simular serviços AWS localmente.

Exemplos:

```text
SQS
SNS
S3
Lambda
```

A cobertura real depende da edição/versão utilizada.

---

# 17. Fluxo LocalStack

```text
.NET API
 ↓
AWS SDK
 ↓
LocalStack
 ↓
SQS / SNS / S3
```

Configuração troca endpoint, não regra de negócio.

---

# 18. Cloud Ready

A aplicação deve estar preparada para:

```text
configuration by environment
external secrets
stateless containers
health checks
structured logs
distributed tracing
horizontal scaling
```

---

# 19. AWS Target

Arquitetura alvo pode utilizar:

```text
SQS
SNS
Lambda
S3
EC2
ECS
```

de acordo com o cenário.

---

# 20. Amazon SQS

SQS é serviço de filas.

```text
Producer
 ↓
SQS Queue
 ↓
Consumer
```

Usos:

```text
background processing
integration
retries
decoupling
work queues
```

---

# 21. Standard Queue

Adequada quando:

```text
high throughput
at-least-once delivery
strict global ordering not required
```

Consumidores precisam ser idempotentes.

---

# 22. FIFO Queue

Usar quando requisitos exigirem ordenação/deduplicação compatíveis com FIFO.

```text
MessageGroupId
DeduplicationId
```

Não selecionar FIFO automaticamente.

---

# 23. Visibility Timeout

Quando consumidor recebe mensagem:

```text
Message
 ↓
Invisible temporarily
 ↓
Processed?
 ├── Yes → Delete
 └── No  → Visible again
```

Configurar conforme duração do processamento.

---

# 24. Dead Letter Queue

```text
Main Queue
 ↓
Repeated Failure
 ↓
DLQ
```

A DLQ precisa de monitoramento e processo de reprocessamento.

---

# 25. Idempotência

Como SQS pode entregar mais de uma vez:

```text
Message
 ↓
Idempotency Check
 ↓
Already Processed?
 ├── Yes → Ignore safely
 └── No → Process
```

---

# 26. Amazon SNS

SNS implementa publicação/assinatura.

```text
Publisher
 ↓
SNS Topic
 ├── SQS A
 ├── SQS B
 └── Other Subscriber
```

---

# 27. Fan-Out

Exemplo:

```text
UserCreated
 ↓
SNS
 ├── Email Queue
 ├── Audit Queue
 └── Analytics Queue
```

---

# 28. SNS + SQS

Padrão importante:

```text
Producer
 ↓
SNS
 ↓
Multiple SQS Queues
 ↓
Independent Consumers
```

Combina fan-out com isolamento de processamento.

---

# 29. AWS Lambda

Lambda executa funções serverless.

```text
Event
 ↓
Lambda
 ↓
Action
```

---

# 30. Bons cenários Lambda

```text
S3 event processing
small integrations
scheduled functions
lightweight asynchronous processing
webhooks
automation
```

Avaliar duração, cold start, memória, concorrência e limites.

---

# 31. Lambda não é obrigatória

Workloads longos ou serviços persistentes podem ser melhores em:

```text
ECS
EC2
other compute
```

---

# 32. Amazon S3

Object Storage.

```text
Application
 ↓
S3 Bucket
 ↓
Objects
```

Usos:

```text
documents
images
exports
backups
AI ingestion files
static assets
```

---

# 33. Upload Architecture

```text
Frontend
 ↓
API
 ↓
Presigned URL
 ↓
S3
```

Pode evitar que arquivos grandes atravessem a API.

---

# 34. S3 Events

```text
Object Created
 ↓
S3 Event
 ↓
SQS / SNS / Lambda
 ↓
Processing
```

---

# 35. Versioning

Para buckets importantes:

```text
S3 Versioning
```

pode auxiliar recuperação e auditoria.

---

# 36. Lifecycle

Políticas podem mover/remover objetos conforme idade e requisito.

```text
Current
 ↓
Archive
 ↓
Expiration
```

Sempre considerar requisitos legais e retenção.

---

# 37. Amazon EC2

Máquina virtual AWS.

```text
EC2
├── OS
├── Runtime
├── Application
└── Agent/Monitoring
```

Oferece controle, mas aumenta responsabilidade operacional.

---

# 38. Quando usar EC2

Possíveis cenários:

```text
legacy workloads
special OS requirements
custom networking
software requiring full host control
```

---

# 39. Amazon ECS

Orquestra containers.

```text
ECS Cluster
 ↓
Service
 ↓
Task
 ↓
Container
```

---

# 40. ECS Service

Mantém quantidade desejada de tasks.

```text
Desired Count = N
```

Pode integrar com Load Balancer e Auto Scaling.

---

# 41. ECS Task Definition

Define:

```text
container image
CPU
memory
ports
environment
secrets
logging
health
IAM role
```

---

# 42. ECS Fargate

Permite executar containers sem administrar instâncias EC2 diretamente.

```text
Container
 ↓
Fargate
```

---

# 43. ECS EC2 Launch Type

```text
ECS
 ↓
EC2 Capacity
```

Pode ser adequado quando há necessidade de controle/custo/capacidade específicos.

---

# 44. ECR

Registry de imagens:

```text
CI
 ↓
Docker Build
 ↓
ECR
 ↓
ECS
```

Mesmo que ECR não seja requisito inicial, é integração natural com ECS.

---

# 45. API Deployment

Exemplo:

```text
Internet
 ↓
Load Balancer
 ↓
ECS Service
 ↓
ASP.NET Core Containers
```

---

# 46. Stateless API

Para escalar:

```text
ALB
 ├── API Task 1
 ├── API Task 2
 └── API Task 3
```

Não guardar sessão crítica apenas em memória local.

---

# 47. Redis

Pode ser utilizado para:

```text
cache
distributed state
rate limiting
temporary data
```

Em AWS, um target comum é ElastiCache/serviço compatível conforme arquitetura.

---

# 48. Cache-Aside

```text
Query
 ↓
Redis
 ├── HIT → Response
 └── MISS
      ↓
      Database
      ↓
      Redis
```

---

# 49. Cache Invalidation

Planejar:

```text
TTL
explicit invalidation
event-driven invalidation
```

Cache sem estratégia de invalidação produz dados obsoletos.

---

# 50. MySQL

Banco transacional principal em muitos templates.

```text
Commands
 ↓
MySQL
```

Em AWS, pode ser hospedado em serviço gerenciado compatível, conforme decisão arquitetural.

---

# 51. MongoDB

Pode ser usado para:

```text
documents
projections
history
read models
AI data
```

quando o modelo documental fizer sentido.

---

# 52. Polyglot Persistence

```text
MySQL
→ transactions

MongoDB
→ documents/read models

Redis
→ cache

S3
→ objects
```

Usar somente quando benefícios justificarem complexidade.

---

# 53. Kafka

No ambiente local/arquitetura genérica:

```text
Producer
 ↓
Kafka
 ↓
Consumer Groups
```

Bom para event streaming.

---

# 54. RabbitMQ

```text
Producer
 ↓
Queue
 ↓
Consumer
```

Bom para filas/work distribution.

---

# 55. Migração conceitual para AWS

Exemplo de adaptação:

```text
RabbitMQ use case
→ evaluate SQS

Pub/Sub use case
→ evaluate SNS + SQS

Object Storage
→ S3

Container runtime
→ ECS
```

Não realizar equivalência cega; comparar semântica.

---

# 56. Broker Abstraction

```csharp
public interface IMessagePublisher
{
    Task PublishAsync<T>(
        T message,
        CancellationToken cancellationToken);
}
```

Implementações:

```text
RabbitMQPublisher
KafkaPublisher
SnsPublisher
SqsPublisher
```

conforme contrato necessário.

---

# 57. Storage Abstraction

```csharp
public interface IObjectStorage
{
    Task<string> UploadAsync(
        Stream content,
        string key,
        CancellationToken cancellationToken);
}
```

Implementações:

```text
LocalStorage
S3Storage
```

---

# 58. Credentials

Nunca:

```text
AWS_ACCESS_KEY_ID=real-key
```

dentro do Git.

---

# 59. Local Credentials

Em desenvolvimento, utilizar mecanismos apropriados ao ambiente e SDK.

Para LocalStack:

```text
fake/local credentials
+
local endpoint
```

quando suportado.

---

# 60. Produção

Preferir credenciais temporárias por identidade/role.

```text
ECS Task
 ↓
IAM Role
 ↓
AWS Service
```

Evitar chaves estáticas sempre que possível.

---

# 61. IAM

Princípio:

```text
Least Privilege
```

Exemplo:

```text
Notification Worker
→ SendMessage only to required queue
```

Não:

```text
Action: *
Resource: *
```

sem justificativa excepcional.

---

# 62. Task Role

ECS Task Role fornece permissões à aplicação.

```text
Application Container
 ↓
Task Role
 ↓
S3/SQS/SNS
```

---

# 63. Execution Role

Separar permissões usadas pelo ECS para executar task das permissões da aplicação.

---

# 64. Secrets

Possíveis mecanismos AWS:

```text
Secrets Manager
SSM Parameter Store
IAM
```

Escolher conforme necessidade.

---

# 65. Configuration

```text
appsettings.json
+
environment variables
+
external secrets
```

---

# 66. Environments

```text
TEST
DEV
HML
PROD
```

Cada ambiente deve ter recursos/configuração isolados quando necessário.

---

# 67. Naming

Exemplo:

```text
gfm-app-dev-users-queue
gfm-app-hml-users-queue
gfm-app-prod-users-queue
```

Definir convenção consistente.

---

# 68. Tags

Recursos devem possuir tags úteis.

```text
Project
Environment
Owner
CostCenter
ManagedBy
```

---

# 69. Infrastructure as Code

Evitar criação manual como fonte de verdade.

```text
IaC
 ↓
AWS
```

---

# 70. Terraform

Estrutura possível:

```text
infrastructure/
└── terraform/
    ├── modules/
    └── environments/
        ├── dev/
        ├── hml/
        └── prod/
```

---

# 71. CloudFormation

Alternativa nativa AWS.

```text
Templates
 ↓
CloudFormation
 ↓
Stacks
```

---

# 72. IaC Modules

```text
modules/
├── network/
├── ecs/
├── sqs/
├── sns/
├── s3/
└── observability/
```

---

# 73. Network

Arquitetura típica pode conter:

```text
VPC
├── Public Subnets
└── Private Subnets
```

Não existe topologia universal; definir conforme exposição e dependências.

---

# 74. Private Workloads

APIs internas, workers e bancos geralmente devem ter exposição mínima necessária.

---

# 75. Load Balancer

```text
Internet
 ↓
ALB
 ↓
ECS Service
```

Pode realizar health checks e distribuição.

---

# 76. Security Groups

Funcionam como controle de tráfego de recursos.

Regra:

```text
allow only required communication
```

---

# 77. TLS

Comunicação pública deve utilizar HTTPS.

Certificados podem ser gerenciados com serviços apropriados da AWS.

---

# 78. Observabilidade

O padrão deve incluir:

```text
Structured Logging
Metrics
Distributed Tracing
Correlation ID
Health Checks
```

---

# 79. Structured Logging

Exemplo:

```json
{
  "level": "Information",
  "event": "OrderCreated",
  "orderId": "...",
  "correlationId": "..."
}
```

Não registrar secrets.

---

# 80. Correlation ID

```text
HTTP Request
 ↓
API
 ↓
SQS
 ↓
Worker
 ↓
External API
```

Propagar identificador de correlação.

---

# 81. Distributed Tracing

```text
API Span
 ↓
Database Span
 ↓
Queue Span
 ↓
Worker Span
```

---

# 82. OpenTelemetry

Instrumentar:

```text
ASP.NET Core
HTTP Client
Database
Redis
Messaging
External APIs
```

---

# 83. Metrics

Exemplos:

```text
request rate
latency
error rate
queue depth
processing duration
cache hit rate
```

---

# 84. Health Checks

```text
/health
/live
/ready
```

---

# 85. Liveness

Responde:

```text
process alive?
```

---

# 86. Readiness

Responde:

```text
instance ready to receive traffic?
```

---

# 87. SQS Metrics

Monitorar:

```text
queue depth
oldest message age
DLQ messages
processing errors
```

---

# 88. ECS Metrics

Monitorar:

```text
CPU
memory
task count
restarts
deployment failures
```

---

# 89. Alerts

Exemplos:

```text
DLQ > 0
high error rate
queue age above threshold
service unavailable
```

Thresholds devem refletir SLOs.

---

# 90. Resilience

Padrões:

```text
Timeout
Retry
Backoff
Jitter
Circuit Breaker
Bulkhead
```

---

# 91. Retry

Retry somente para falhas transitórias.

Evitar:

```text
infinite retry
```

---

# 92. Timeout

Toda integração externa deve possuir timeout definido.

---

# 93. Circuit Breaker

```text
Failures
 ↓
Circuit Opens
 ↓
Temporary Block
 ↓
Recovery Probe
```

---

# 94. DLQ Strategy

Definir:

```text
why message failed
how to inspect
how to correct
how to replay
```

---

# 95. CI/CD

```text
Git
 ↓
Build
 ↓
Tests
 ↓
Security
 ↓
Docker Image
 ↓
Registry
 ↓
Deploy
```

---

# 96. GitFlow

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

# 97. Feature Branch

Base:

```text
develop
```

Formato:

```text
feature/task-<id>-<description>
```

---

# 98. AI Git Workflow

```text
AI
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
Validate PR
```

---

# 99. PR Quality Gate

```text
dotnet restore
dotnet build
dotnet test
architecture tests
security scan
Docker build
```

Adicionar frontend checks quando houver React.

---

# 100. Release

```text
develop
 ↓
hml
 ↓
release/1.0.0
 ↓
main
 ↓
production
```

---

# 101. Build Once, Deploy Many

Ideal:

```text
Commit
 ↓
Docker Image
 ↓
DEV
 ↓
HML
 ↓
PROD
```

A mesma imagem deve ser promovida quando possível.

---

# 102. Docker Image

```text
Source
 ↓
Docker Build
 ↓
Immutable Image
```

Configuração varia por ambiente; imagem não.

---

# 103. Database Migration

Pipeline:

```text
Deploy
 ↓
Migration Strategy
 ↓
Application
```

Mudanças destrutivas exigem cuidado.

---

# 104. Expand / Contract

Estratégia:

```text
Add compatible schema
 ↓
Deploy compatible app
 ↓
Migrate data
 ↓
Remove obsolete schema later
```

---

# 105. Rollback

Definir antes do deploy:

```text
application rollback
configuration rollback
database compatibility
infrastructure rollback
```

---

# 106. Testing

Camadas:

```text
Unit
Integration
Architecture
Contract
E2E
```

---

# 107. Unit Tests

Não devem depender de AWS real.

```text
Domain
Application
Policies
Validators
```

---

# 108. Integration Tests

Podem usar:

```text
Docker
LocalStack
Testcontainers
temporary databases
```

---

# 109. LocalStack Tests

Exemplo:

```text
Test
 ↓
AWS SDK
 ↓
LocalStack SQS
 ↓
Assert Message
```

---

# 110. Contract Tests

Validam contratos entre:

```text
producer
consumer
```

Importante para eventos.

---

# 111. Architecture Tests

Exemplos:

```text
Domain must not reference AWS SDK
Application must not reference Infrastructure
```

---

# 112. Test Environment

```text
docker compose
 ↓
test dependencies
 ↓
dotnet test
```

---

# 113. Um comando

Objetivo:

```text
one command
→ run all tests
```

---

# 114. Fake AWS

Testes unitários podem utilizar:

```text
FakeQueue
FakeStorage
FakePublisher
```

Não simular AWS em testes que deveriam testar apenas regras de negócio.

---

# 115. AWS Integration Layer

Estrutura:

```text
Infrastructure/
└── AWS/
    ├── SQS/
    ├── SNS/
    ├── S3/
    ├── Lambda/
    └── Configuration/
```

---

# 116. Messaging Abstractions

```text
Application/
└── Abstractions/
    └── Messaging/
        ├── IMessagePublisher.cs
        └── IMessageConsumer.cs
```

---

# 117. Storage Abstractions

```text
Application/
└── Abstractions/
    └── Storage/
        └── IObjectStorage.cs
```

---

# 118. AWS Options

Exemplo:

```csharp
public sealed class AwsOptions
{
    public string Region { get; init; } = string.Empty;
    public string? ServiceUrl { get; init; }
}
```

`ServiceUrl` pode apontar para LocalStack localmente.

---

# 119. Environment Configuration

```text
Development
→ LocalStack

HML
→ AWS HML

Production
→ AWS PROD
```

---

# 120. Endpoint Abstraction

Código de domínio não precisa saber se:

```text
localhost:4566
```

ou endpoint AWS real está sendo utilizado.

---

# 121. Example Local Configuration

```text
AWS_REGION=us-east-1
AWS_SERVICE_URL=http://localstack:4566
```

Credenciais locais devem ser fictícias quando usadas apenas pelo simulador.

---

# 122. Production Configuration

Não configurar:

```text
AWS_SERVICE_URL
```

para substituir endpoints AWS padrão sem necessidade.

Credenciais devem vir de role/identidade.

---

# 123. Docker Compose AWS Local

Exemplo conceitual:

```text
services:
  api
  worker
  localstack
  mysql
  redis
```

---

# 124. Bootstrap AWS Local

Script pode criar:

```text
queues
topics
buckets
subscriptions
```

---

# 125. Idempotent Bootstrap

Executar duas vezes deve resultar no mesmo ambiente.

```text
create-if-not-exists
```

---

# 126. Resource Registry

Documentar:

```text
Resource
Environment
Purpose
Owner
Producer
Consumer
```

---

# 127. Queue Registry

Exemplo:

```text
users-created
email-dispatch
document-processing
```

---

# 128. Event Catalog

```text
UserCreated
PasswordResetRequested
DocumentUploaded
ContentPublished
```

Cada evento precisa de contrato.

---

# 129. Event Contract

Exemplo:

```json
{
  "eventId": "...",
  "eventType": "UserCreated",
  "version": 1,
  "occurredAt": "...",
  "correlationId": "...",
  "data": {}
}
```

---

# 130. Event Versioning

Evitar quebrar consumidores.

```text
v1
 ↓
compatible evolution
```

Mudança incompatível pode exigir nova versão.

---

# 131. Message Envelope

Campos úteis:

```text
MessageId
CorrelationId
CausationId
Timestamp
Type
Version
Payload
```

---

# 132. Idempotency Key

```text
MessageId
```

ou chave de negócio apropriada.

---

# 133. Consumer Flow

```text
Receive
 ↓
Validate
 ↓
Idempotency
 ↓
Process
 ↓
Persist
 ↓
Delete/Ack
```

---

# 134. Failure Flow

```text
Receive
 ↓
Process
 ↓ FAIL
Retry
 ↓
DLQ
```

---

# 135. Security Flow

```text
User
 ↓
Authentication
 ↓
Authorization
 ↓
API
 ↓
IAM Role
 ↓
AWS Resource
```

São camadas diferentes de segurança.

---

# 136. JWT

Pode autenticar usuários da aplicação.

Não substitui IAM para autorização de workloads AWS.

---

# 137. Policies

Aplicação:

```text
admin
editor
reader
visitor
```

Cloud:

```text
IAM Policies
```

Não misturar responsabilidades.

---

# 138. Audit

Registrar ações relevantes:

```text
who
what
when
resource
result
correlationId
```

---

# 139. Cost Awareness

Arquitetura AWS precisa considerar:

```text
compute
storage
requests
network
logs
managed services
idle resources
```

---

# 140. Cost Tags

Tags facilitam análise de custos por:

```text
project
environment
team
```

---

# 141. DEV Cost Strategy

Evitar manter recursos caros ligados sem necessidade.

Possíveis estratégias dependem do serviço:

```text
scale down
scheduled shutdown
shared non-prod resources
local development
```

---

# 142. HML

Deve ser suficientemente semelhante à produção para validar:

```text
deploy
configuration
permissions
network
integrations
```

sem necessariamente possuir a mesma escala.

---

# 143. PROD

Priorizar:

```text
availability
security
backup
monitoring
rollback
capacity
cost control
```

---

# 144. Backup

Definir por datastore:

```text
frequency
retention
restore procedure
RPO
RTO
```

---

# 145. Disaster Recovery

Perguntas:

```text
What if region fails?
What data can be lost?
How long can system stay offline?
How to restore?
```

---

# 146. RPO

```text
Recovery Point Objective
```

Quanto de dados pode ser perdido.

---

# 147. RTO

```text
Recovery Time Objective
```

Quanto tempo o serviço pode ficar indisponível.

---

# 148. SLO

```text
Service Level Objective
```

Exemplo:

```text
99.9% availability
```

Deve ser definido conforme negócio, não arbitrariamente.

---

# 149. Infrastructure Diagram

```text
                           INTERNET
                              │
                              ▼
                     ┌────────────────┐
                     │ LOAD BALANCER  │
                     └───────┬────────┘
                             │
                             ▼
                     ┌────────────────┐
                     │   ECS / API    │
                     └───────┬────────┘
                             │
          ┌──────────────────┼──────────────────┐
          │                  │                  │
          ▼                  ▼                  ▼
       DATABASE            REDIS               S3
          │
          │
          ▼
       OUTBOX
          │
          ▼
       SNS/SQS
          │
          ▼
       WORKERS
```

---

# 150. Local Diagram

```text
                       DEVELOPER
                           │
                           ▼
                    DOCKER COMPOSE
                           │
       ┌───────────────────┼────────────────────┐
       │                   │                    │
       ▼                   ▼                    ▼
     API                DATABASE             REDIS
       │
       ▼
   LOCALSTACK
    ├── SQS
    ├── SNS
    └── S3
```

---

# 151. Evolution Diagram

```text
LOCAL
Docker Compose
    ↓
LOCAL AWS
LocalStack
    ↓
CONTAINER READY
Docker Images
    ↓
CLOUD READY
IaC + External Config
    ↓
AWS
ECS + SQS + SNS + S3 + Lambda
```

---

# 152. Observability Diagram

```text
API
 │
 ├── Logs ─────┐
 ├── Metrics ──┼──► Observability Backend
 └── Traces ───┘
       │
       ▼
     Alerts
```

---

# 153. GitFlow Diagram

```text
feature/task-*
      │
      ▼
   develop
      │
      ▼
     hml
      │
      ▼
 release/x.y.z
      │
      ▼
     main
      │
      ▼
 production
```

---

# 154. AWS Skill

No Kit:

```text
3-Skills/
└── aws-architecture/
    ├── SKILL.md
    ├── references/
    ├── examples/
    └── templates/
```

---

# 155. SKILL.md AWS

Deve orientar:

```text
analyze requirements
select AWS services
define abstractions
define local equivalents
define IAM
define IaC
define observability
define testing
define cost controls
```

---

# 156. AWS Architect Agent

Responsabilidades:

```text
service selection
network
security
IAM
compute
messaging
storage
resilience
observability
cost
```

---

# 157. DevOps Agent

Responsabilidades:

```text
Docker
LocalStack
IaC
CI/CD
ECR
ECS
environment configuration
deployment
```

---

# 158. Security Agent

Verifica:

```text
IAM
secrets
network exposure
encryption
dependencies
container image
```

---

# 159. Tester Agent

Deve validar:

```text
unit
integration
LocalStack
message contracts
failure scenarios
idempotency
```

---

# 160. Documentation Agent

Atualiza:

```text
README
AWS architecture
resource catalog
runbook
environment setup
deployment guide
```

---

# 161. AWS Workflow

```text
Requirements
 ↓
AWS Architecture
 ↓
Local Mapping
 ↓
Docker / LocalStack
 ↓
IaC
 ↓
Security Review
 ↓
Tests
 ↓
HML
 ↓
Production
```

---

# 162. Quality Gate — Architecture

- [ ] domínio desacoplado da AWS;
- [ ] serviços AWS justificados;
- [ ] boundaries definidos;
- [ ] comunicação síncrona/assíncrona definida;
- [ ] persistência definida;
- [ ] failure modes documentados.

---

# 163. Quality Gate — Security

- [ ] sem secrets no Git;
- [ ] IAM least privilege;
- [ ] workloads usam roles;
- [ ] rede com exposição mínima;
- [ ] TLS;
- [ ] dados sensíveis protegidos;
- [ ] logs sem secrets.

---

# 164. Quality Gate — Messaging

- [ ] idempotência;
- [ ] retry;
- [ ] timeout;
- [ ] DLQ;
- [ ] correlation ID;
- [ ] event versioning;
- [ ] observabilidade.

---

# 165. Quality Gate — Containers

- [ ] image builds;
- [ ] health checks;
- [ ] non-root quando aplicável;
- [ ] configuração externa;
- [ ] sem secrets na image;
- [ ] image scan.

---

# 166. Quality Gate — Tests

- [ ] unit tests;
- [ ] integration tests;
- [ ] architecture tests;
- [ ] LocalStack tests quando necessário;
- [ ] contract tests;
- [ ] failure scenarios.

---

# 167. Quality Gate — Observability

- [ ] structured logs;
- [ ] correlation ID;
- [ ] traces;
- [ ] metrics;
- [ ] readiness;
- [ ] liveness;
- [ ] alerts.

---

# 168. Quality Gate — Deployment

- [ ] immutable artifact;
- [ ] IaC;
- [ ] environment config;
- [ ] migration strategy;
- [ ] rollback;
- [ ] release notes.

---

# 169. Anti-patterns

Evitar:

```text
AWS SDK inside Domain
hardcoded credentials
Action: *
Resource: *
shared production credentials
manual infrastructure without documentation
no DLQ
no idempotency
infinite retries
no timeout
logs without correlation
deploy directly from developer machine
different source builds per environment
```

---

# 170. Estrutura no Kit IA Dev

```text
Kit-IA-Dev/
├── 2-Agents/
│   ├── aws-architect/
│   ├── devops/
│   └── security/
├── 3-Skills/
│   ├── aws-architecture/
│   ├── localstack/
│   ├── aws-messaging/
│   └── aws-observability/
├── 4-Templates/
│   └── dotnet-aws/
├── 5-Workflows/
│   └── aws-setup/
├── 6-Quality-Gates/
│   └── aws/
└── 8-Dictionary/
    └── 20-setup-aws.md
```

---

# 171. Estrutura no projeto

```text
project/
├── backend/
├── frontend/
├── tests/
├── docker/
├── infrastructure/
│   ├── terraform/
│   └── aws/
├── docs/
│   └── architecture/
├── scripts/
│   └── localstack/
├── agents/
├── skills/
└── prompts.md
```

---

# 172. Documentação AWS

```text
docs/
└── architecture/
    ├── aws-context.drawio
    ├── aws-infrastructure.drawio
    ├── aws-messaging.drawio
    ├── aws-deployment.drawio
    └── aws-security.md
```

---

# 173. Scripts

```text
scripts/
└── localstack/
    ├── create-sqs.ps1
    ├── create-sns.ps1
    ├── create-s3.ps1
    └── bootstrap.ps1
```

Como o ambiente principal pode ser Windows/PowerShell, scripts `.ps1` são úteis; opcionalmente fornecer `.sh` para CI/Linux.

---

# 174. README

Deve explicar:

```text
requirements
local setup
Docker
LocalStack
tests
AWS authentication
IaC
deployment
troubleshooting
```

---

# 175. Runbook

Exemplos:

```text
SQS backlog
DLQ processing
ECS task failing
S3 permission denied
deployment rollback
```

---

# 176. prompts.md AWS

O orquestrador deve instruir a IA a:

```text
1. ler PROJECT.md;
2. ler arquitetura existente;
3. identificar serviços AWS necessários;
4. preservar abstrações;
5. configurar ambiente local;
6. configurar LocalStack;
7. gerar/ajustar IaC;
8. implementar testes;
9. configurar observabilidade;
10. gerar diagramas;
11. executar quality gates;
12. atualizar documentação.
```

---

# 177. Regra de seleção AWS

Nunca adicionar serviço apenas porque está disponível.

Perguntar:

```text
What problem does this AWS service solve?
```

---

# 178. Exemplo — Upload de documento

```text
Frontend
 ↓
API
 ↓
S3
 ↓
SQS
 ↓
Worker
 ↓
Process Document
```

---

# 179. Exemplo — Notificação

```text
Application
 ↓
Outbox
 ↓
SNS
 ↓
SQS
 ↓
Notification Worker
```

---

# 180. Exemplo — Processamento assíncrono

```text
POST /reports
 ↓
API
 ↓
SQS
 ↓
Worker
 ↓
S3
 ↓
Report Ready
```

---

# 181. Exemplo — Lambda

```text
S3 Object Created
 ↓
Lambda
 ↓
Metadata Extraction
 ↓
Database
```

---

# 182. Exemplo — ECS

```text
ALB
 ↓
ECS Service
 ↓
ASP.NET Core
 ↓
MySQL / Redis / SQS
```

---

# 183. Exemplo — RAG AWS

```text
Document
 ↓
S3
 ↓
SQS
 ↓
AI Worker
 ↓
Chunking
 ↓
Embeddings
 ↓
Vector Store
```

---

# 184. Exemplo — Agentic AI AWS

```text
Task
 ↓
SQS
 ↓
Agent Worker on ECS
 ↓
LLM + Tools + RAG
 ↓
Result
 ↓
SNS/Event
```

---

# 185. Exemplo — Local equivalente

```text
AWS PROD
S3 + SQS + SNS + ECS

LOCAL
LocalStack + Docker Containers
```

A regra de negócio permanece a mesma.

---

# 186. Definition of Ready

Antes da implementação AWS:

- [ ] requisito definido;
- [ ] serviço AWS justificado;
- [ ] contrato definido;
- [ ] segurança analisada;
- [ ] estratégia local definida;
- [ ] custo considerado;
- [ ] failure modes definidos.

---

# 187. Definition of Done

- [ ] código;
- [ ] testes;
- [ ] Docker;
- [ ] LocalStack quando aplicável;
- [ ] IaC;
- [ ] IAM;
- [ ] observabilidade;
- [ ] diagramas;
- [ ] documentação;
- [ ] CI/CD;
- [ ] rollback;
- [ ] quality gates.

---

# 188. Arquitetura consolidada

```text
                         CLIENTS
                            │
                            ▼
                    LOAD BALANCER/API
                            │
                            ▼
                      ECS SERVICES
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
        ▼                   ▼                   ▼
      MYSQL               REDIS                 S3
        │                                       │
        ▼                                       ▼
      OUTBOX                                  EVENTS
        │                                       │
        ▼                                       ▼
       SNS ───────────────► SQS ◄──────────── LAMBDA
                              │
                              ▼
                           WORKERS
                              │
                              ▼
                     EXTERNAL SERVICES
```

---

# 189. Evolução consolidada

```text
PHASE 1
Local Application

        ↓

PHASE 2
Docker Compose

        ↓

PHASE 3
LocalStack

        ↓

PHASE 4
IaC + Cloud Ready

        ↓

PHASE 5
AWS HML

        ↓

PHASE 6
AWS Production
```

---

# 190. Princípio final

O objetivo não é transformar o projeto em:

```text
AWS everywhere
```

O objetivo é:

```text
CLEAN CORE
+
AWS ADAPTERS
+
LOCAL DEVELOPMENT
+
AUTOMATED TESTS
+
INFRASTRUCTURE AS CODE
+
SECURITY
+
OBSERVABILITY
+
CONTROLLED DEPLOYMENT
```

---

# 191. Relação com outros itens

```text
01 - Estrutura de Projeto
01.2 - Agentic Workflow
03 - Plugins
05 - Conectores e Funções
10 - LLM Local
11 - CI/CD
13 - Projetar Microsserviços
15 - RAG System
16 - Arquitetura e Aplicações
17 - Agentic AI
18 - Kit IA Dev
20 - Setup AWS
```

---

# 192. Resumo

O **Setup AWS** do Kit IA Dev deve manter uma arquitetura portátil e evolutiva:

```text
LOCAL FIRST
→ CONTAINER FIRST
→ LOCALSTACK
→ CLOUD READY
→ AWS TARGET
```

A aplicação deve preservar:

```text
DDD
CQRS
Domain Events
SOLID
Clean Architecture
Vertical Slices quando aplicável
Transactional Outbox
Idempotência
Retry
Timeout
DLQ
Correlation ID
OpenTelemetry
Automated Tests
CI/CD
IaC
```

E utilizar AWS de forma orientada a requisitos:

```text
SQS
→ filas

SNS
→ pub/sub e fan-out

Lambda
→ processamento serverless/event-driven

S3
→ object storage

EC2
→ compute com controle de host

ECS
→ containers
```

O domínio permanece independente dos serviços AWS. Isso permite desenvolvimento local, testes confiáveis, substituição de infraestrutura e evolução segura para cloud.

---

# 📁 Arquivo

```text
20-setup-aws.md
```
