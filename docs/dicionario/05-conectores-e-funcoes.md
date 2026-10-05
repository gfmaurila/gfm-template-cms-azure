# 📘 Dicionário Técnico — 05 Conectores e Funções

> **Categoria:** Inteligência Artificial / Integrações / Tools / MCP  
> **Código:** 05  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** Claude Code / Codex / Copilot / OpenCode / Agentes de IA / MCP / APIs  
> **Objetivo:** Padronizar o conceito e o uso de conectores e funções para permitir que agentes de IA interajam com sistemas, dados e ferramentas externas.

---

# 1. O que são Conectores

Conectores são integrações que permitem que uma IA se comunique com sistemas externos.

```text
IA
 │
 ├── GitHub
 ├── Banco de Dados
 ├── Files
 ├── APIs
 ├── Docker
 ├── AWS
 ├── Azure
 ├── Gmail
 ├── Calendar
 └── Outros serviços
```

Sem conectores, o modelo normalmente trabalha apenas com o contexto fornecido.

Com conectores, o agente pode consultar informações e, quando autorizado, executar ações reais.

---

# 2. O que são Funções

Funções são operações específicas disponibilizadas para o agente.

Exemplo:

```text
GitHub Connector
│
├── get_repository()
├── create_branch()
├── create_issue()
├── create_pull_request()
└── review_pull_request()
```

O conector representa a integração.

A função representa uma capacidade executável dentro dessa integração.

---

# 3. Relação entre conceitos

```text
Agent
  ↓
Tool
  ↓
Connector
  ↓
Function
  ↓
External System
```

Exemplo:

```text
Developer Agent
      ↓
GitHub Connector
      ↓
create_pull_request()
      ↓
GitHub
```

---

# 4. Conector x Plugin x Skill x Agent

```text
Connector
→ conecta a IA a um sistema.

Function
→ executa uma operação.

Plugin
→ adiciona capacidades à plataforma.

Skill
→ ensina procedimento e conhecimento.

Agent
→ possui responsabilidade e toma decisões.
```

Eles podem atuar juntos:

```text
Agent
 ↓
Skill
 ↓
Connector
 ↓
Function
 ↓
External System
```

---

# 5. MCP

MCP — Model Context Protocol — pode padronizar como ferramentas e recursos são apresentados ao agente.

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

# 6. Categorias de Conectores

Um Kit IA Dev pode organizar conectores por domínio:

```text
Source Control
Files
Database
Cloud
Containers
CI/CD
Communication
Documentation
Project Management
Observability
Security
Search
AI Models
```

---

# 7. Conector GitHub

Capacidades comuns:

```text
repositories
branches
commits
issues
pull requests
reviews
releases
actions
```

Exemplo de fluxo:

```text
Task
 ↓
create_branch
 ↓
Implementation
 ↓
commit
 ↓
push
 ↓
create_pull_request
 ↓
review
 ↓
merge
```

---

# 8. Conector de Files

Permite trabalhar com arquivos e documentos.

Funções conceituais:

```text
search_files()
read_file()
find_text()
write_file()
move_file()
```

Aplicações:

- analisar documentação;
- localizar código;
- consultar requisitos;
- gerar relatórios;
- atualizar arquivos.

---

# 9. Conector de Banco de Dados

Pode expor funções como:

```text
get_schema()
execute_query()
list_tables()
describe_table()
validate_migration()
```

Bancos possíveis:

```text
MySQL
SQL Server
PostgreSQL
MongoDB
Redis
```

Acesso de escrita deve ser controlado.

---

# 10. Conector Docker

Possíveis funções:

```text
list_containers()
start_container()
stop_container()
get_logs()
run_compose()
inspect_health()
```

Fluxo:

```text
DevOps Agent
 ↓
Docker Connector
 ↓
docker compose
 ↓
Containers
 ↓
Health Check
```

---

# 11. Conector AWS

Pode disponibilizar capacidades para:

```text
S3
SQS
SNS
Lambda
EC2
ECS
CloudWatch
Secrets Manager
```

Exemplo:

```text
Cloud Agent
 ↓
AWS Connector
 ↓
SQS
 ↓
Inspect Queue
```

Operações em produção devem possuir controles adicionais.

---

# 12. Conector Azure

Pode integrar:

```text
Blob Storage
Service Bus
Functions
App Service
Container Apps
AKS
Key Vault
Application Insights
```

---

# 13. Conectores de comunicação

Exemplos:

```text
Gmail
Outlook
Slack
Teams
Discord
```

Podem permitir:

- buscar mensagens;
- resumir conversas;
- criar rascunhos;
- enviar mensagens quando autorizado;
- detectar pendências.

---

# 14. Conectores de calendário

Exemplos:

```text
Google Calendar
Outlook Calendar
```

Capacidades:

```text
search_events()
check_availability()
create_event()
update_event()
cancel_event()
```

---

# 15. Conectores de documentação

Podem integrar:

```text
Google Drive
Google Docs
Notion
Confluence
SharePoint
```

Uso:

```text
Requirements Agent
 ↓
Documentation Connector
 ↓
Requirements
 ↓
Analysis
```

---

# 16. Conectores de Project Management

Exemplos:

```text
Jira
Azure Boards
GitHub Issues
Trello
Linear
```

Funções possíveis:

```text
create_task()
update_task()
get_backlog()
assign_task()
change_status()
```

---

# 17. Conectores de Observabilidade

Exemplos:

```text
Grafana
Prometheus
Elastic
Datadog
Application Insights
CloudWatch
```

O agente pode consultar:

```text
logs
metrics
traces
alerts
health
```

---

# 18. Conectores de Segurança

Possíveis integrações:

```text
SonarQube
Snyk
Dependabot
Trivy
OWASP tools
Secret scanners
```

Fluxo:

```text
Security Agent
 ↓
Security Connector
 ↓
Scan
 ↓
Findings
 ↓
Remediation
```

---

# 19. Conectores de busca

Permitem consultar informações externas atualizadas.

Uso:

- documentação oficial;
- changelogs;
- versões;
- troubleshooting;
- pesquisa técnica.

A IA deve diferenciar conhecimento local do projeto de informação pública externa.

---

# 20. Conectores de LLM

Uma arquitetura pode permitir múltiplos providers:

```text
OpenAI
Anthropic
Azure OpenAI
Google
Ollama
Local Models
```

Abstração:

```text
Agent
 ↓
ILLMProvider
 ↓
Provider Adapter
 ↓
LLM
```

---

# 21. Function Calling

Modelos podem selecionar funções a partir de uma descrição estruturada.

Exemplo conceitual:

```json
{
  "name": "get_user",
  "description": "Busca usuário pelo identificador",
  "parameters": {
    "userId": "string"
  }
}
```

Fluxo:

```text
User Question
 ↓
LLM
 ↓
Function Selection
 ↓
Function Execution
 ↓
Result
 ↓
LLM
 ↓
Final Response
```

---

# 22. Tool Selection

Um agente deve selecionar a ferramenta correta.

```text
Criar PR
→ GitHub

Consultar documentação interna
→ Files / Drive

Consultar schema
→ Database

Subir ambiente
→ Docker

Consultar logs
→ Observability

Consultar infraestrutura
→ Cloud
```

---

# 23. Tool Router

Sistemas mais complexos podem possuir um roteador.

```text
Request
  ↓
Tool Router
  ├── GitHub
  ├── Files
  ├── Database
  ├── Docker
  ├── Cloud
  └── Search
```

O Router decide qual integração deve receber a tarefa.

---

# 24. Agentic Workflow

Conectores tornam workflows agentic possíveis.

```text
Goal
 ↓
Planning
 ↓
Tool Selection
 ↓
Function Call
 ↓
Observation
 ↓
Decision
 ↓
Next Tool
```

---

# 25. Exemplo completo

Solicitação:

```text
"Implemente a issue USER-105."
```

Fluxo:

```text
GitHub
 ↓
read_issue()

Files
 ↓
analisar projeto

Git
 ↓
create_branch()

Developer Agent
 ↓
implementar

Terminal
 ↓
dotnet build
dotnet test

Git
 ↓
commit
push

GitHub
 ↓
create_pull_request()
```

---

# 26. Conectores e RAG

Conectores podem funcionar como fontes de conhecimento.

```text
RAG Agent
 ├── Files
 ├── GitHub
 ├── Database
 ├── Drive
 └── Search
```

Isso permite Retrieval sobre múltiplas fontes.

---

# 27. Conectores e Multi-Agent

Cada agente pode possuir ferramentas específicas.

```text
Architect Agent
├── Files
├── Documentation
└── Diagram Tools

Developer Agent
├── Files
├── Git
├── Terminal
└── GitHub

DevOps Agent
├── Docker
├── Cloud
└── CI/CD

Database Agent
├── SQL
└── Migration Tools
```

---

# 28. Princípio de menor privilégio

Um agente deve receber apenas as permissões necessárias.

```text
Agent
 ↓
Required Permission Only
 ↓
Connector
```

Isso reduz riscos.

---

# 29. Read x Write

Conectores devem diferenciar operações.

```text
READ
→ consultar dados

WRITE
→ modificar dados

DESTRUCTIVE
→ excluir ou substituir recursos
```

Quanto maior o impacto, maior deve ser o controle.

---

# 30. Confirmação para operações críticas

Exemplos de operações que podem exigir aprovação:

```text
delete production database
destroy cloud resource
merge into main
deploy production
delete repository
rotate credentials
```

O agente não deve tratar essas ações como equivalentes a uma consulta.

---

# 31. Credenciais

Nunca armazenar credenciais diretamente em:

```text
README.md
prompts.md
SKILL.md
source code
repository
```

Utilizar:

```text
Environment Variables
GitHub Secrets
AWS Secrets Manager
Azure Key Vault
Secret Manager
```

---

# 32. Auditoria

Registrar operações relevantes:

```text
Agent
Connector
Function
Environment
Timestamp
Input
Result
CorrelationId
```

Dados sensíveis devem ser mascarados.

---

# 33. Idempotência

Funções devem evitar duplicações.

Exemplo:

```text
create_pull_request()
 ↓
PR already exists?
 ├── Yes → reuse
 └── No → create
```

Também se aplica a:

- issues;
- recursos Cloud;
- migrations;
- filas;
- documentos;
- tarefas.

---

# 34. Retry e Timeout

Integrações externas podem falhar.

Padrões:

```text
Timeout
Retry
Exponential Backoff
Circuit Breaker
```

Retry deve respeitar idempotência.

---

# 35. Error Handling

Uma função deve retornar erros claros.

Evitar:

```text
"Something went wrong"
```

Preferir:

```text
Connector: GitHub
Function: create_pull_request
Error: branch not found
Retryable: false
```

---

# 36. Observabilidade

Métricas úteis:

```text
function calls
latency
success rate
failure rate
retry count
connector usage
cost
```

Fluxo:

```text
Agent
 ↓
Connector
 ↓
OpenTelemetry
 ↓
Logs + Metrics + Traces
```

---

# 37. Contratos de função

Funções devem possuir contratos claros.

```text
Name
Description
Input
Output
Errors
Permissions
Side Effects
Idempotency
Environment
```

Isso melhora a seleção correta pelo LLM.

---

# 38. Evitar funções ambíguas

Ruim:

```text
execute()
manage()
process()
```

Melhor:

```text
create_pull_request()
get_database_schema()
deploy_container()
search_documents()
```

Nomes específicos reduzem erros de tool selection.

---

# 39. Granularidade

Evitar funções gigantes como:

```text
build_test_deploy_commit_push_merge()
```

Preferir operações menores:

```text
build()
test()
commit()
push()
create_pull_request()
deploy()
```

O workflow orquestra as funções.

---

# 40. Estrutura no Kit IA Dev

```text
Kit-IA-Dev/
├── 2-Agents/
├── 3-Skills/
├── 5-Workflows/
├── 8-Dictionary/
└── 9-Connectors/
```

Este documento:

```text
8-Dictionary/
└── 05-conectores-e-funcoes.md
```

---

# 41. Catálogo de conectores

```text
9-Connectors/
├── README.md
├── github/
├── files/
├── database/
├── docker/
├── aws/
├── azure/
├── communication/
├── documentation/
├── observability/
└── security/
```

---

# 42. Registry

Criar:

```text
CONNECTORS_REGISTRY.md
```

Exemplo:

```text
| Connector | Category | Read | Write | Critical |
|---|---|---|---|---|
| GitHub | SCM | Yes | Yes | Some |
| Files | Storage | Yes | Yes | Some |
| Database | Data | Yes | Controlled | Yes |
| Docker | Infra | Yes | Yes | Some |
| AWS | Cloud | Yes | Controlled | Yes |
```

---

# 43. Skill de conectores

```text
3-Skills/
└── connectors/
    └── SKILL.md
```

Responsabilidades:

```text
discover connectors
validate permissions
select tool
execute function
validate result
handle errors
record evidence
```

---

# 44. Workflow recomendado

```text
Task
 ↓
Discover Available Connectors
 ↓
Select Agent
 ↓
Select Connector
 ↓
Select Function
 ↓
Validate Permissions
 ↓
Execute
 ↓
Validate Result
 ↓
Record Evidence
```

---

# 45. Quality Gates

Antes de considerar uma integração pronta:

- [ ] conector documentado;
- [ ] funções documentadas;
- [ ] inputs validados;
- [ ] outputs definidos;
- [ ] erros tratados;
- [ ] timeout configurado;
- [ ] retry avaliado;
- [ ] permissões mínimas;
- [ ] secrets protegidos;
- [ ] auditoria implementada quando necessária;
- [ ] testes existentes;
- [ ] observabilidade disponível.

---

# 46. Anti-patterns

Evitar:

```text
conector com acesso irrestrito
funções ambíguas
secret hardcoded
ações destrutivas sem controle
ausência de timeout
retry infinito
ausência de logs
função sem validação
IA afirmando execução que não ocorreu
```

---

# 47. Regra para agentes

Antes de executar uma função, o agente deve verificar:

1. Qual é o objetivo?
2. Qual conector atende à tarefa?
3. Qual função específica deve ser usada?
4. Possui permissão?
5. Qual ambiente será afetado?
6. A operação altera dados?
7. É destrutiva?
8. É idempotente?
9. Precisa de confirmação?
10. Como validar o resultado?

---

# 48. Arquitetura consolidada

```text
                         USER
                           │
                           ▼
                    AI ORCHESTRATOR
                           │
                           ▼
                         AGENT
                           │
                     TOOL ROUTER
                           │
       ┌───────────────────┼───────────────────┐
       ▼                   ▼                   ▼
    CONNECTOR           CONNECTOR           CONNECTOR
     GitHub             Database             Cloud
       │                   │                   │
       ▼                   ▼                   ▼
   Functions           Functions           Functions
       │                   │                   │
       └───────────────────┼───────────────────┘
                           ▼
                    EXTERNAL SYSTEMS
```

---

# 49. Relação com outros itens

Este conteúdo complementa:

```text
01 - Estrutura de Projeto
02 - RAG
03 - Plugins
06 - Skills
07 - LinkedIn Manager Agent
09 - Skills Claude Code
11 - CI/CD
16 - Arquitetura de Aplicações
17 - Agentic AI
18 - Kit IA Dev
```

---

# 50. Resumo

Conectores fornecem acesso.

Funções fornecem ações.

```text
Agent
 ↓
Skill
 ↓
Tool Router
 ↓
Connector
 ↓
Function
 ↓
External System
```

Um ambiente agentic robusto precisa de conectores:

```text
documentados
+
seguros
+
testáveis
+
observáveis
+
com permissões mínimas
+
com contratos claros
```

O objetivo do Kit IA Dev é permitir que agentes não apenas gerem respostas, mas utilizem ferramentas reais de engenharia de forma controlada e auditável.

---

# 📁 Arquivo

```text
05-conectores-e-funcoes.md
```
