# 📘 Dicionário Técnico — 03 Plugins

> **Categoria:** Inteligência Artificial / Extensões / Integrações  
> **Código:** 03  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** Claude Code / Codex / Copilot / OpenCode / Agentes de IA / MCP  
> **Objetivo:** Documentar o papel de plugins no ambiente de desenvolvimento assistido por IA e como organizá-los dentro do Kit IA Dev.

---

# 1. O que são Plugins

Plugins são extensões que adicionam capacidades a uma ferramenta ou agente de IA.

Eles permitem que uma IA deixe de atuar apenas sobre texto e passe a interagir com ferramentas, serviços e fluxos especializados.

```text
IA
 │
 ├── Plugin Git
 ├── Plugin GitHub
 ├── Plugin Database
 ├── Plugin Docker
 ├── Plugin Cloud
 ├── Plugin Browser
 ├── Plugin Files
 └── Plugin Documentation
```

---

# 2. Objetivo

Plugins podem fornecer:

- novas ferramentas;
- comandos;
- automações;
- integração com APIs;
- acesso a repositórios;
- manipulação de arquivos;
- integração com bancos;
- execução de testes;
- análise de código;
- geração de documentação;
- integração com serviços Cloud.

---

# 3. Plugin x Skill x Agent x MCP

Esses conceitos não devem ser tratados como sinônimos.

```text
Plugin
→ adiciona uma capacidade/extensão à plataforma.

Skill
→ descreve conhecimento e procedimento reutilizável.

Agent
→ executa uma responsabilidade ou papel.

MCP
→ padroniza a exposição de ferramentas e recursos externos.
```

Eles podem trabalhar juntos:

```text
Agent
  ↓
Skill
  ↓
Tool / Plugin
  ↓
MCP
  ↓
External System
```

---

# 4. Estrutura conceitual

```text
User
  ↓
AI Assistant
  ↓
Agent
  ↓
Plugin / Tool
  ↓
External Service
```

Exemplo:

```text
Developer Agent
      ↓
GitHub Plugin
      ↓
Repository
      ↓
Pull Request
```

---

# 5. Plugins para desenvolvimento

Categorias úteis:

```text
Development
Git
GitHub
Testing
Database
Docker
Cloud
Security
Documentation
Browser
Search
Observability
Project Management
```

---

# 6. Git e GitHub

Plugins de Git/GitHub podem apoiar:

```text
status
diff
branch
commit
push
pull request
issues
code review
release
```

Fluxo:

```text
Task
 ↓
feature/task-xxx
 ↓
Implementation
 ↓
Tests
 ↓
Commit
 ↓
Push
 ↓
Pull Request
 ↓
Review
```

---

# 7. Plugins de Banco de Dados

Podem permitir:

- consulta de schema;
- execução de queries;
- análise de índices;
- validação de migrations;
- investigação de dados;
- geração de documentação.

Exemplos de alvos:

```text
MySQL
SQL Server
PostgreSQL
MongoDB
Redis
```

A IA deve respeitar permissões e evitar alterações destrutivas sem autorização.

---

# 8. Plugins Docker

Podem auxiliar em:

```text
docker compose
containers
images
logs
networks
volumes
health checks
```

Exemplo de uso:

```text
Agent
 ↓
Docker Tool
 ↓
docker compose up
 ↓
Health Check
 ↓
Integration Tests
```

---

# 9. Plugins Cloud

Categorias:

```text
AWS
Azure
GCP
Kubernetes
Terraform
```

Exemplos AWS:

```text
S3
SQS
SNS
Lambda
EC2
ECS
CloudWatch
```

Exemplos Azure:

```text
Blob Storage
Service Bus
Functions
App Service
Container Apps
AKS
Application Insights
```

---

# 10. Plugins de documentação

Podem ser utilizados para:

- gerar documentação;
- consultar documentação oficial;
- atualizar README;
- produzir diagramas;
- manter ADRs;
- documentar APIs.

Arquivos comuns:

```text
README.md
PROJECT.md
ARCHITECTURE.md
REQUIREMENTS.md
EXECUTION_PLAN.md
SECURITY.md
TEST_PLAN.md
```

---

# 11. Plugins de testes

Podem apoiar:

```text
Unit Tests
Integration Tests
Architecture Tests
Contract Tests
E2E
Coverage
Static Analysis
```

Fluxo recomendado:

```text
Implementation
 ↓
Build
 ↓
Unit Tests
 ↓
Integration Tests
 ↓
Static Analysis
 ↓
Quality Gate
```

---

# 12. Plugins de segurança

Possíveis capacidades:

```text
dependency scanning
secret scanning
SAST
container scanning
IaC scanning
vulnerability analysis
```

A segurança deve fazer parte do pipeline e não ser uma etapa opcional no final.

---

# 13. Plugins de Browser e Search

Úteis para:

- documentação atualizada;
- pesquisa técnica;
- comparação de versões;
- análise de bibliotecas;
- consulta de changelogs;
- investigação de erros.

A IA deve priorizar documentação oficial para decisões técnicas críticas.

---

# 14. Plugins e MCP

Um plugin pode utilizar MCP ou oferecer funcionalidade semelhante.

Arquitetura:

```text
AI Client
   ↓
MCP Client
   ↓
MCP Server
   ↓
Tools / Resources
   ↓
External System
```

Exemplo:

```text
Claude Code
   ↓
MCP
   ↓
GitHub
```

---

# 15. Plugins e Agents

Cada agente deve possuir apenas as ferramentas necessárias.

Exemplo:

```text
Developer Agent
├── Files
├── Git
├── Build
└── Tests

Database Agent
├── SQL
├── Schema
└── Migration

DevOps Agent
├── Docker
├── CI/CD
├── Terraform
└── Cloud
```

Isso reduz permissões desnecessárias.

---

# 16. Princípio de menor privilégio

Um agente não deve receber acesso ilimitado apenas porque a ferramenta permite.

```text
Agent
 ↓
Minimum Required Permissions
 ↓
Tool
```

Exemplo:

Um agente de documentação normalmente não precisa de permissão para excluir infraestrutura Cloud.

---

# 17. Plugins locais

Algumas extensões podem atuar somente no ambiente local.

Exemplos:

```text
filesystem
terminal
git
docker
local database
local LLM
```

São úteis durante desenvolvimento.

---

# 18. Plugins remotos

Integram serviços externos.

```text
GitHub
Cloud
Issue Tracker
Documentation Platform
External APIs
```

Devem considerar autenticação, autorização, auditoria e proteção de credenciais.

---

# 19. Credenciais

Nunca colocar secrets diretamente em:

```text
prompts.md
SKILL.md
README.md
source code
repository
```

Utilizar:

```text
Environment Variables
Secret Manager
AWS Secrets Manager
Azure Key Vault
GitHub Secrets
```

---

# 20. Organização no Kit IA Dev

Estrutura possível:

```text
Kit-IA-Dev/
├── 1-Prompts/
├── 2-Agents/
├── 3-Skills/
├── 4-Templates/
├── 5-Workflows/
├── 6-Quality-Gates/
├── 7-Documentation/
├── 8-Dictionary/
└── 9-Plugins/
```

---

# 21. Catálogo de Plugins

Criar um catálogo ajuda a IA a descobrir capacidades.

```text
9-Plugins/
├── README.md
├── development/
├── git/
├── github/
├── database/
├── docker/
├── cloud/
├── testing/
├── security/
├── documentation/
└── observability/
```

---

# 22. Manifesto conceitual

Cada plugin deve possuir documentação mínima:

```text
Name
Purpose
Category
Installation
Configuration
Permissions
Commands
Use Cases
Security
Limitations
Examples
```

---

# 23. Exemplo de definição

```yaml
name: github
category: source-control
purpose: Interagir com repositórios GitHub.

capabilities:
  - repository
  - issues
  - pull-requests
  - reviews

permissions:
  - read_repository
  - create_branch
  - create_pull_request
```

---

# 24. Plugin Registry

O Kit pode manter um registro:

```text
plugins-registry.md
```

Exemplo:

```text
| Plugin | Categoria | Status | Uso |
|---|---|---|---|
| GitHub | Git | Enabled | PR/Issues |
| Docker | Infra | Enabled | Containers |
| Database | Data | Optional | Queries |
| AWS | Cloud | Optional | Infra |
```

---

# 25. Descoberta automática

Antes de assumir que uma ferramenta não existe, o agente deve verificar quais integrações estão disponíveis.

```text
Task
 ↓
Discover Available Tools
 ↓
Find Required Capability
 ↓
Validate Permissions
 ↓
Execute
```

---

# 26. Seleção de ferramenta

A IA deve escolher a ferramenta de acordo com a tarefa.

```text
Criar PR
→ GitHub

Consultar banco
→ Database

Subir ambiente
→ Docker

Consultar documentação atual
→ Browser/Search

Criar infraestrutura
→ Terraform/Cloud
```

---

# 27. Fallback

Quando um plugin não estiver disponível:

```text
Plugin available?
 ├── Yes → Use plugin
 └── No
      ↓
   Alternative tool?
      ├── Yes → Use alternative
      └── No → Report limitation
```

A IA não deve inventar que executou uma ação.

---

# 28. Auditoria

Operações importantes devem ser rastreáveis.

Exemplos:

```text
quem executou
qual agente
qual ferramenta
qual comando
quando
resultado
```

Especialmente para:

- produção;
- banco;
- Cloud;
- Git;
- secrets;
- releases.

---

# 29. Observabilidade

Plugins críticos podem registrar:

```text
Execution Time
Success
Failure
Retries
Tool Name
Agent Name
Correlation ID
```

Isso ajuda a investigar automações de agentes.

---

# 30. Retry

Integrações remotas podem falhar temporariamente.

Estratégias:

```text
Retry
Exponential Backoff
Timeout
Circuit Breaker
```

Não aplicar retry cego em operações não idempotentes.

---

# 31. Idempotência

Operações automatizadas devem evitar duplicação.

Exemplo:

```text
Create Issue
 ↓
Already exists?
 ├── Yes → Reuse
 └── No → Create
```

O mesmo vale para:

- PRs;
- recursos Cloud;
- filas;
- arquivos;
- migrations.

---

# 32. Quality Gates para Plugins

Antes de adicionar um plugin ao Kit:

- [ ] possui objetivo claro;
- [ ] possui documentação;
- [ ] origem é confiável;
- [ ] permissões foram revisadas;
- [ ] secrets não ficam no código;
- [ ] existe estratégia de atualização;
- [ ] limitações estão documentadas;
- [ ] existe fallback;
- [ ] foi testado;
- [ ] não duplica outra ferramenta sem necessidade.

---

# 33. Plugins e prompts.md

O orquestrador pode orientar a IA:

```text
1. Identificar a tarefa.
2. Identificar o agente responsável.
3. Descobrir ferramentas disponíveis.
4. Selecionar plugin/tool apropriado.
5. Validar permissões.
6. Executar.
7. Validar resultado.
8. Registrar evidências.
```

---

# 34. Plugins e Skills

A Skill explica **como** executar uma tarefa.

O Plugin fornece a capacidade para executá-la.

Exemplo:

```text
Skill:
github-pull-request

ensina:
como validar uma task e abrir PR

Plugin:
GitHub

executa:
criação real do Pull Request
```

---

# 35. Plugins e Workflows

```text
Workflow
   ↓
Agent
   ↓
Skill
   ↓
Plugin
   ↓
External System
```

Exemplo:

```text
Feature Workflow
 ↓
Developer Agent
 ↓
Git Skill
 ↓
GitHub Plugin
 ↓
Pull Request
```

---

# 36. Plugins e Agentic AI

Plugins são importantes para transformar um LLM em um sistema capaz de agir.

```text
LLM
 ↓
Agent
 ↓
Planning
 ↓
Tool Selection
 ↓
Plugin
 ↓
Action
 ↓
Observation
 ↓
Next Decision
```

---

# 37. Plugins e RAG

Plugins também podem atuar como fontes de conhecimento.

```text
RAG Agent
 ├── Files Plugin
 ├── GitHub Plugin
 ├── Database Plugin
 └── Search Plugin
```

O agente pode consultar várias fontes antes de produzir uma resposta.

---

# 38. Cenário .NET

Exemplo:

```text
Developer solicita:
"Implemente a task USER-101."
```

Fluxo:

```text
AI Orchestrator
 ↓
GitHub → lê issue
 ↓
Files → analisa projeto
 ↓
Developer Agent
 ↓
dotnet build
 ↓
dotnet test
 ↓
Git
 ↓
GitHub → cria PR
```

---

# 39. Cenário Docker

```text
DevOps Agent
 ↓
Docker Plugin
 ↓
docker compose up
 ↓
Health Checks
 ↓
Integration Tests
 ↓
Logs
 ↓
Report
```

---

# 40. Cenário AWS

```text
Cloud Agent
 ↓
AWS / IaC Tools
 ↓
Validate Infrastructure
 ↓
Plan
 ↓
Approval
 ↓
Apply
 ↓
Health Check
```

Operações destrutivas ou de produção devem exigir controle adicional.

---

# 41. Cenário Banco

```text
Database Agent
 ↓
Read Schema
 ↓
Analyze Migration
 ↓
Validate Query
 ↓
Test Environment
 ↓
Report
```

Nunca iniciar por produção quando a validação puder ocorrer em TEST/DEV.

---

# 42. Anti-patterns

Evitar:

```text
plugin sem documentação
plugin com acesso total
secret hardcoded
ferramentas duplicadas
execução sem validação
produção como ambiente de teste
ações destrutivas automáticas
dependência excessiva de um fornecedor
```

---

# 43. Estratégia recomendada

Começar com um conjunto pequeno e controlado.

```text
Core Plugins
├── Files
├── Git
├── GitHub
├── Terminal
├── Docker
└── Documentation
```

Depois adicionar conforme necessidade:

```text
Database
Cloud
Security
Observability
Project Management
Browser
Specialized APIs
```

---

# 44. Checklist de instalação

Para cada plugin:

- [ ] identificar necessidade;
- [ ] validar origem;
- [ ] verificar compatibilidade;
- [ ] revisar permissões;
- [ ] instalar;
- [ ] configurar credenciais;
- [ ] executar teste básico;
- [ ] documentar comandos;
- [ ] documentar casos de uso;
- [ ] registrar no catálogo.

---

# 45. Checklist operacional

Antes de um agente usar plugin:

- [ ] plugin disponível;
- [ ] conexão funcionando;
- [ ] permissões suficientes;
- [ ] ambiente correto;
- [ ] operação é segura;
- [ ] impacto conhecido;
- [ ] rollback previsto quando necessário;
- [ ] resultado será validado.

---

# 46. Regra para Agentes de IA

A IA deve:

1. descobrir ferramentas disponíveis;
2. selecionar a menor capacidade suficiente;
3. respeitar permissões;
4. proteger secrets;
5. validar ambiente;
6. evitar ações destrutivas desnecessárias;
7. validar o resultado;
8. registrar evidências;
9. usar fallback quando possível;
10. nunca afirmar que uma ação foi executada sem evidência.

---

# 47. Relação com o restante do Kit

Plugins se relacionam diretamente com:

```text
01 - Estrutura de Projeto
02 - RAG
05 - Conectores e Funções
06 - Skills
07 - LinkedIn Manager Agent
09 - Skills Claude Code
11 - CI/CD
16 - Arquitetura de Aplicações
17 - Agentic AI
18 - Kit IA Dev
```

---

# 48. Resumo

Plugin é uma extensão de capacidade.

Dentro de uma arquitetura de IA:

```text
Prompt
  ↓
Orchestrator
  ↓
Agent
  ↓
Skill
  ↓
Plugin / Tool
  ↓
MCP
  ↓
External System
```

O objetivo não é instalar o maior número possível de plugins.

O objetivo é possuir um conjunto controlado, seguro, documentado e reutilizável de capacidades que permita aos agentes executar tarefas reais de engenharia.

---

# 📁 Arquivo

```text
03-plugins.md
```
