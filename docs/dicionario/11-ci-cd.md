# 📘 Dicionário Técnico — 11 CI/CD

> **Categoria:** Engenharia de Software / DevOps / Automação  
> **Código:** 11  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** .NET / React / Docker / GitFlow / GitHub Actions / GitLab CI / Cloud  
> **Objetivo:** Definir CI/CD, seus componentes, cenários de uso e um pipeline reutilizável para projetos do Kit IA Dev.

---

# 1. O que é CI/CD

CI/CD representa práticas para automatizar integração, validação, empacotamento e entrega de software.

```text
Developer
 ↓
Git
 ↓
CI
 ↓
Build
 ↓
Tests
 ↓
Quality Gates
 ↓
Artifact
 ↓
CD
 ↓
Environment
```

---

# 2. CI — Continuous Integration

Integração Contínua significa integrar mudanças frequentemente e validá-las automaticamente.

Fluxo:

```text
Commit / Pull Request
 ↓
Restore
 ↓
Build
 ↓
Tests
 ↓
Static Analysis
 ↓
Security Checks
 ↓
Result
```

Objetivo:

```text
detectar problemas cedo
```

---

# 3. CD — Continuous Delivery

Continuous Delivery mantém uma versão validada pronta para implantação.

```text
CI
 ↓
Artifact
 ↓
DEV
 ↓
HML
 ↓
Approval
 ↓
PROD
```

Produção pode exigir aprovação.

---

# 4. Continuous Deployment

Continuous Deployment vai além:

```text
CI
 ↓
Quality Gates
 ↓
Automatic Deployment
 ↓
Production
```

Toda mudança aprovada pelos gates pode chegar automaticamente à produção.

Não é obrigatório utilizar esse modelo.

---

# 5. Pipeline

Pipeline é a sequência automatizada de etapas.

```text
Source
 ↓
Build
 ↓
Test
 ↓
Analyze
 ↓
Package
 ↓
Deploy
 ↓
Validate
```

---

# 6. Stage

Um pipeline é dividido em stages.

Exemplo:

```text
1. Validate
2. Build
3. Test
4. Security
5. Package
6. Deploy
7. Verify
```

---

# 7. Job

Um stage pode conter vários jobs.

```text
TEST
├── Unit Tests
├── Integration Tests
├── Architecture Tests
└── Coverage
```

---

# 8. Artifact

Artifact é um resultado versionado do build.

Exemplos:

```text
Docker Image
NuGet Package
ZIP
Frontend Build
Helm Chart
```

Princípio importante:

```text
Build Once
Deploy Many
```

O mesmo artifact deve avançar entre ambientes quando possível.

---

# 9. Ambientes

Padrão recomendado:

```text
TEST
DEV
HML
PROD
```

Responsabilidades:

```text
TEST → testes automatizados
DEV  → desenvolvimento/integrado
HML  → homologação
PROD → produção
```

---

# 10. GitFlow

Fluxo alinhado ao modelo do Kit:

```text
feature/task-*
      ↓
   develop
      ↓
     hml
      ↓
release/x.y.z
      ↓
     main
```

---

# 11. Branch main

```text
main
```

Representa código de produção.

Proteções recomendadas:

- sem push direto;
- Pull Request obrigatório;
- testes obrigatórios;
- review obrigatório;
- quality gates;
- release versionada.

---

# 12. Branch develop

```text
develop
```

Base para desenvolvimento integrado.

Features devem nascer dela:

```text
develop
 ↓
feature/task-user-auth
```

---

# 13. Branch hml

```text
hml
```

Representa homologação.

Fluxo:

```text
develop
 ↓
hml
 ↓
validation
```

---

# 14. Feature Branch

Padrão:

```text
feature/task-123-description
```

Fluxo:

```text
develop
 ↓
feature/task-123
 ↓
implementation
 ↓
tests
 ↓
PR
 ↓
develop
```

---

# 15. Release Branch

Exemplo:

```text
release/1.0.0
```

ou conforme padrão definido pelo projeto:

```text
release/1.0.0.0
```

Serve para preparar a versão destinada à produção.

---

# 16. Pull Request

PR deve executar validações automaticamente.

```text
Pull Request
 ↓
Build
 ↓
Tests
 ↓
Coverage
 ↓
Security
 ↓
Architecture Rules
 ↓
AI / Human Review
 ↓
Approval
```

---

# 17. CI para .NET

Pipeline:

```text
dotnet restore
 ↓
dotnet build
 ↓
dotnet test
 ↓
coverage
 ↓
static analysis
```

---

# 18. CI para React

```text
npm ci
 ↓
lint
 ↓
typecheck
 ↓
tests
 ↓
build
```

---

# 19. Backend + Frontend

```text
Pull Request
      │
      ├── Backend Pipeline
      │    ├── restore
      │    ├── build
      │    └── tests
      │
      └── Frontend Pipeline
           ├── install
           ├── lint
           ├── test
           └── build
```

---

# 20. Unit Tests

Devem ser:

```text
fast
isolated
repeatable
deterministic
```

Executados em praticamente todo PR.

---

# 21. Integration Tests

Validam integrações reais ou controladas.

Exemplo:

```text
API
 ↓
MySQL
Redis
MongoDB
RabbitMQ
```

Podem utilizar containers de teste.

---

# 22. Architecture Tests

Validam regras arquiteturais.

Exemplos:

```text
Domain não depende de Infrastructure
Application não depende de API
Modules não criam dependências proibidas
```

---

# 23. Contract Tests

Importantes em integrações e microsserviços.

```text
Consumer
 ↓
Contract
 ↓
Provider
```

Reduzem quebra de APIs.

---

# 24. E2E

```text
Browser / Client
 ↓
Frontend
 ↓
API
 ↓
Database
```

São mais caros e lentos; usar estrategicamente.

---

# 25. Code Coverage

Coverage mede código exercitado pelos testes.

Não deve ser interpretado como garantia de qualidade.

```text
High Coverage
≠
Good Tests
```

---

# 26. Static Analysis

Ferramentas podem verificar:

```text
bugs
code smells
complexity
duplication
security issues
style
```

Exemplo conhecido:

```text
SonarQube
```

---

# 27. Security Pipeline

Adicionar:

```text
SAST
Dependency Scan
Secret Scan
Container Scan
IaC Scan
```

---

# 28. Secret Scanning

Detecta:

```text
API keys
tokens
passwords
private keys
credentials
```

Secrets não devem chegar ao repositório.

---

# 29. Dependency Scanning

Verifica vulnerabilidades em dependências.

```text
NuGet
npm
Docker Images
```

---

# 30. Container Scanning

```text
Docker Image
 ↓
Vulnerability Scan
 ↓
Pass / Fail
```

Imagens vulneráveis podem bloquear release conforme política.

---

# 31. IaC Scanning

Infraestrutura como código também precisa ser analisada.

```text
Terraform
CloudFormation
Bicep
Kubernetes manifests
```

---

# 32. Quality Gate

Um Quality Gate decide se o pipeline pode continuar.

```text
Build
 ✓

Tests
 ✓

Security
 ✓

Coverage
 ✓

Architecture
 ✓
     ↓
Deploy
```

---

# 33. Falha no Gate

```text
Quality Gate
 ↓
FAIL
 ↓
Stop Pipeline
```

Não promover artifact inválido.

---

# 34. Docker Build

```text
Source
 ↓
Docker Build
 ↓
Image
 ↓
Scan
 ↓
Registry
```

---

# 35. Registry

Exemplos:

```text
GitHub Container Registry
GitLab Container Registry
Amazon ECR
Azure Container Registry
```

---

# 36. Versionamento da imagem

Evitar depender apenas de:

```text
latest
```

Preferir:

```text
app:1.0.0
app:commit-sha
```

Isso melhora rastreabilidade.

---

# 37. Immutable Artifact

Depois de aprovado:

```text
Artifact
 ↓
DEV
 ↓
HML
 ↓
PROD
```

Não recompilar um código diferente para cada ambiente sem necessidade.

---

# 38. Configuração por ambiente

Artifact permanece o mesmo.

Configuração muda:

```text
Environment Variables
Secrets
Configuration Store
```

---

# 39. Secrets no CI/CD

Utilizar:

```text
GitHub Secrets
GitLab Variables
AWS Secrets Manager
Azure Key Vault
```

Nunca:

```text
appsettings.json com senha real
.env commitado
secret no YAML
```

---

# 40. DEV Deployment

```text
develop
 ↓
CI
 ↓
Artifact
 ↓
DEV
 ↓
Smoke Test
```

---

# 41. HML Deployment

```text
hml
 ↓
Artifact
 ↓
HML
 ↓
Integration / Acceptance Tests
```

---

# 42. PROD Deployment

```text
release
 ↓
Approval
 ↓
main
 ↓
Production Deployment
 ↓
Health Check
```

---

# 43. Smoke Test

Após deploy:

```text
Application Started?
Database Reachable?
Critical Endpoint Works?
Dependencies Healthy?
```

---

# 44. Health Checks

```text
/health
/live
/ready
```

Separar:

```text
Liveness
Readiness
Dependency Health
```

---

# 45. Deployment Strategies

Principais estratégias:

```text
Rolling
Blue/Green
Canary
Recreate
```

---

# 46. Rolling Deployment

Atualiza instâncias progressivamente.

```text
v1 v1 v1
 ↓
v2 v1 v1
 ↓
v2 v2 v1
 ↓
v2 v2 v2
```

---

# 47. Blue/Green

```text
BLUE  → current
GREEN → new
```

Depois da validação:

```text
Traffic
 ↓
GREEN
```

Rollback pode redirecionar para BLUE.

---

# 48. Canary

```text
New Version
 ↓
5% traffic
 ↓
Metrics OK?
 ↓
25%
 ↓
50%
 ↓
100%
```

Reduz impacto de falhas.

---

# 49. Rollback

Todo deploy precisa considerar rollback.

```text
Deploy
 ↓
Health Failure
 ↓
Rollback
 ↓
Previous Stable Version
```

---

# 50. Database Migration

Migração exige cuidado especial.

```text
Application
 ↓
Migration
 ↓
Database
```

Evitar mudanças incompatíveis difíceis de reverter.

---

# 51. Expand and Contract

Estratégia para schema:

```text
Expand
 ↓
Deploy Compatible Code
 ↓
Migrate Data
 ↓
Contract
```

Ajuda em deploys sem downtime.

---

# 52. Feature Flags

```text
Code Deployed
 ↓
Feature Flag OFF
 ↓
Validation
 ↓
Feature Flag ON
```

Deploy e release de funcionalidade deixam de ser a mesma coisa.

---

# 53. Observabilidade no Deployment

Após deploy monitorar:

```text
Errors
Latency
CPU
Memory
Requests
Database
Queue
Business Metrics
```

---

# 54. OpenTelemetry

Pode instrumentar:

```text
HTTP
Database
Redis
Messaging
External APIs
```

Pipeline não termina no deploy; ele deve validar o comportamento.

---

# 55. Logs estruturados

```text
Timestamp
Level
Service
Environment
CorrelationId
Message
```

Facilitam troubleshooting.

---

# 56. Métricas do pipeline

Medir:

```text
Build Duration
Test Duration
Failure Rate
Deployment Frequency
Lead Time
Rollback Rate
```

---

# 57. DORA Metrics

Métricas conhecidas:

```text
Deployment Frequency
Lead Time for Changes
Change Failure Rate
Time to Restore Service
```

Ajudam a avaliar entrega de software.

---

# 58. GitHub Actions

Estrutura típica:

```text
.github/
└── workflows/
    ├── ci.yml
    ├── deploy-dev.yml
    ├── deploy-hml.yml
    └── deploy-prod.yml
```

---

# 59. GitLab CI

Estrutura:

```text
.gitlab-ci.yml
```

Stages:

```text
validate
build
test
security
package
deploy
```

---

# 60. Pipeline conceitual

```yaml
stages:
  - validate
  - build
  - test
  - security
  - package
  - deploy
```

A sintaxe real deve seguir a plataforma utilizada.

---

# 61. AWS

Possível fluxo:

```text
Git
 ↓
CI
 ↓
Docker Image
 ↓
ECR
 ↓
ECS
 ↓
Health Check
 ↓
CloudWatch
```

---

# 62. AWS Serverless

```text
Git
 ↓
CI
 ↓
Tests
 ↓
Package
 ↓
Lambda
 ↓
Validation
```

---

# 63. Azure

Exemplo:

```text
Git
 ↓
CI
 ↓
Docker Image
 ↓
ACR
 ↓
Container Apps / AKS
 ↓
Application Insights
```

---

# 64. Kubernetes

```text
CI
 ↓
Container Registry
 ↓
Helm / Manifest
 ↓
Kubernetes
 ↓
Readiness
 ↓
Traffic
```

---

# 65. Infrastructure as Code

```text
Infrastructure Repository
 ↓
Validate
 ↓
Plan
 ↓
Review
 ↓
Apply
```

Aplicação automática em produção deve seguir política de aprovação.

---

# 66. Terraform Pipeline

```text
fmt
 ↓
validate
 ↓
security scan
 ↓
plan
 ↓
approval
 ↓
apply
```

---

# 67. AI no CI/CD

Agentes podem ajudar em:

```text
PR Review
Test Analysis
Failure Explanation
Security Finding Summary
Release Notes
Documentation
```

---

# 68. AI não substitui gates determinísticos

Exemplo:

```text
AI Review
+
Compiler
+
Tests
+
Security Scanner
+
Architecture Tests
```

A revisão por IA é complementar.

---

# 69. AI Developer Workflow

```text
Task
 ↓
AI creates feature branch
 ↓
Implementation
 ↓
Tests
 ↓
Commit
 ↓
Push
 ↓
PR
 ↓
CI
 ↓
AI Review
 ↓
Human / Policy Approval
```

---

# 70. Release Notes

Podem ser geradas a partir de:

```text
Commits
PRs
Issues
Changes
```

Saída:

```text
RELEASE_NOTES.md
```

---

# 71. Semantic Versioning

Modelo comum:

```text
MAJOR.MINOR.PATCH
```

Exemplo:

```text
1.4.2
```

O projeto pode adotar quatro segmentos se isso fizer parte da convenção definida.

---

# 72. Pipeline para o Kit IA Dev

```text
Feature
 ↓
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
Code Quality
 ↓
Docker Build
 ↓
Container Scan
 ↓
Artifact
 ↓
DEV
 ↓
HML
 ↓
Release
 ↓
PROD
```

---

# 73. Docker Compose para TEST

O projeto deve permitir:

```text
docker compose
 ↓
Test Infrastructure
 ↓
dotnet test
```

Idealmente com um comando documentado.

---

# 74. Bancos separados

```text
TEST DB
DEV DB
HML DB
PROD DB
```

Nunca executar testes destrutivos contra produção.

---

# 75. Seed Data

Para TEST/DEV:

```text
Migration
 ↓
Seed
 ↓
Test Data
```

Seeds de teste não devem inserir credenciais reais.

---

# 76. Pipeline rápido x completo

## PR

```text
fast build
unit tests
lint
static analysis
```

## Merge / Release

```text
integration tests
security scans
container build
E2E
deployment validation
```

A divisão depende do tempo e risco do projeto.

---

# 77. Cache de dependências

CI pode utilizar cache para:

```text
NuGet
npm
Docker layers
```

Mas o cache nunca deve comprometer reprodutibilidade.

---

# 78. Paralelização

Jobs independentes podem rodar em paralelo.

```text
          ┌─ Unit Tests
Build ────┼─ Static Analysis
          └─ Security Scan
```

Isso reduz tempo de pipeline.

---

# 79. Pipeline as Code

Pipeline deve estar versionado.

```text
Repository
 ↓
Pipeline Definition
 ↓
Version History
```

Mudanças no CI/CD também passam por review.

---

# 80. Evidências

O pipeline deve produzir evidências:

```text
Test Results
Coverage
Security Report
Build Artifact
Image Digest
Deployment Result
```

---

# 81. Quality Gates do Kit

Antes do merge:

- [ ] build passou;
- [ ] unit tests passaram;
- [ ] integration tests passaram quando exigidos;
- [ ] architecture tests passaram;
- [ ] lint passou;
- [ ] análise estática passou;
- [ ] security checks passaram;
- [ ] secrets scan passou;
- [ ] documentação relevante atualizada;
- [ ] PR revisado.

---

# 82. Definition of Done

Uma task não está concluída apenas porque o código foi escrito.

```text
Code
+
Tests
+
Review
+
Documentation
+
CI
+
Quality Gates
```

---

# 83. Anti-patterns

Evitar:

```text
push direto na main
testes manuais como único gate
secrets no pipeline
usar latest sem rastreabilidade
rebuild diferente por ambiente
deploy sem health check
produção sem rollback
pipeline ignorado por agentes
merge com testes falhando
```

---

# 84. Estrutura no Kit IA Dev

```text
Kit-IA-Dev/
├── 3-Skills/
│   └── cicd/
├── 4-Templates/
│   ├── github-actions/
│   └── gitlab-ci/
├── 5-Workflows/
│   └── release/
├── 6-Quality-Gates/
│   └── cicd/
└── 8-Dictionary/
    └── 11-ci-cd.md
```

---

# 85. Skill CI/CD

Responsabilidades:

```text
detect stack
build
test
scan
package
deploy
verify
rollback
report
```

---

# 86. Cenário 1 — Pull Request

```text
Developer
 ↓
feature/task-123
 ↓
Push
 ↓
PR
 ↓
Build
 ↓
Tests
 ↓
Security
 ↓
Review
```

---

# 87. Cenário 2 — Homologação

```text
develop
 ↓
hml
 ↓
Deploy HML
 ↓
Acceptance Tests
 ↓
Approval
```

---

# 88. Cenário 3 — Produção

```text
release/1.0.0
 ↓
Final Gates
 ↓
main
 ↓
Tag
 ↓
Production
 ↓
Health Check
 ↓
Monitoring
```

---

# 89. Cenário 4 — Hotfix

```text
Production Incident
 ↓
hotfix/*
 ↓
Fix
 ↓
Tests
 ↓
PR
 ↓
Release
 ↓
Production
 ↓
Back-merge
```

---

# 90. Cenário 5 — Infraestrutura

```text
Terraform Change
 ↓
Validate
 ↓
Security Scan
 ↓
Plan
 ↓
Review
 ↓
Approval
 ↓
Apply
```

---

# 91. Regra para Agentes

Antes de alterar ou executar pipeline:

1. identificar ambiente;
2. identificar branch;
3. validar testes;
4. verificar secrets;
5. validar artifact;
6. verificar impacto;
7. verificar necessidade de aprovação;
8. garantir rollback;
9. validar health checks;
10. registrar resultado.

---

# 92. Relação com outros itens

```text
01 - Estrutura de Projeto
03 - Plugins
05 - Conectores e Funções
09 - Skills
10 - LLM Local
13 - Microsserviços
16 - Arquitetura de Aplicações
17 - Agentic AI
18 - Kit IA Dev
```

---

# 93. Resumo

CI/CD não é apenas:

```text
"rodar deploy"
```

É um sistema de garantia contínua:

```text
CODE
 ↓
BUILD
 ↓
TEST
 ↓
SECURITY
 ↓
QUALITY
 ↓
PACKAGE
 ↓
DEPLOY
 ↓
VERIFY
 ↓
OBSERVE
```

No Kit IA Dev, o pipeline deve trabalhar junto com GitFlow, testes automatizados, Docker, observabilidade, segurança e agentes de IA, mantendo rastreabilidade e Quality Gates entre `feature`, `develop`, `hml`, `release` e `main`.

---

# 📁 Arquivo

```text
11-ci-cd.md
```
