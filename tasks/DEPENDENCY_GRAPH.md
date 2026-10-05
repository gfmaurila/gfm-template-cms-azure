# DEPENDENCY GRAPH - GFM.Template.CMS

## Visão Geral
Grafo de dependências planejado para execução sequencial/paralela por Tasks.

Plataforma alvo: **Azure** (`LOCAL FIRST -> CONTAINER FIRST -> CLOUD READY -> AZURE TARGET`).

## Estrutura EPICs
EPIC-00 Bootstrap & Governance (DONE)
EPIC-01 Repository Foundation
EPIC-02 Solution & Architecture
EPIC-03 Domain Foundation
EPIC-04 Application/CQRS
EPIC-05 Infrastructure
EPIC-06 AuthN/AuthZ
EPIC-07 Persistence
EPIC-08 Cache (Redis / Azure Managed Redis)
EPIC-09 Messaging (Azure Service Bus / Event Hubs)
EPIC-10 Transactional Outbox
EPIC-11 Site API
EPIC-12 Admin API
EPIC-13 Auth API
EPIC-14 React Site
EPIC-15 React Admin
EPIC-16 Docker (+ Azurite)
EPIC-17 Observability (Azure Monitor / Application Insights)
EPIC-18 Testing & QA
EPIC-19 Architecture Docs (C4/Structurizr/ADRs)
EPIC-20 Azure Target (Blob Storage, Key Vault, Container Apps, Entra ID, OpenTofu)
EPIC-21 CI/CD
EPIC-22 Security
EPIC-23 AI Content Intelligence
EPIC-24 Audio Intelligence
EPIC-25 Release & Deployment

## Dependency Graph (alto nível)
```text
TASK-001 (EPIC-01: Repo Foundation)
    |
    v
TASK-002 (EPIC-02: Solution & Architecture)
    |
    v
TASK-003 (EPIC-03: Domain Core)
    |
    v
TASK-004 (EPIC-04: Application Base)
    |
    +-- TASK-005 (EPIC-05: Infra Core)
    +-- TASK-006 (EPIC-07: Persistence Base)
    +-- TASK-007 (EPIC-08: Redis / Azure Managed Redis)
    +-- TASK-008 (EPIC-09: Messaging)
    +-- TASK-009 (EPIC-10: Outbox)
         |
         v
    (APIs/Frontend/Docker/Obs/Azure/CI-CD/AI seguem após base)
```

## Mapeamento Azure por EPIC

| EPIC | Local First | Azure Target |
|---|---|---|
| 07 Persistence | MySQL | Azure Database for MySQL - Flexible Server |
| 08 Cache | Redis | Azure Managed Redis |
| 09 Messaging | RabbitMQ / Kafka | Azure Service Bus / Azure Event Hubs |
| 16 Docker | LocalStack | Azurite |
| 17 Observability | Prometheus / Grafana / Loki / OpenTelemetry | Azure Monitor + Application Insights |
| 20 Azure | IaC genérica | Bicep / OpenTofu (provider Azure) |
| 21 CI/CD | GitHub Actions | GitHub Actions + azure/login-action (OIDC) + ACR |
| 22 Security | Secrets locais | Azure Key Vault + Managed Identities + Azure RBAC |
| 23 AI Content | Azure OpenAI / AI Foundry / AI Speech | Azure OpenAI / Azure AI Foundry / Azure AI Speech |

## Notas
- Paralelização permitida quando branches não compartilham dependências.
- Status inicial: maioria BACKLOG. READY apenas com dependências DONE.
- Nenhuma implementação iniciada nesta execução.