# STANDARDIZATION REPORT — AWS → AZURE

Repositório alvo: `D:\Empresa\GFMaurila\projetos\gfm-template-cms-azure`
Referência de engenharia: `D:\Empresa\GFMaurila\projetos\gfm-template-cms-aws`
Fonte oficial de conhecimento: `D:\Empresa\GFMaurila\projetos\Kit-IA-Dev`

## Objetivo

Padronizar o projeto Azure com o mesmo modelo de engenharia do projeto AWS
(estrutura, organização, documentação, Agents, Skills, Quality Gates, GitFlow,
testes, Docker, observabilidade e governança), **sem** transformar o projeto Azure
em um projeto AWS.

## Princípio aplicado

```text
READ → UNDERSTAND → COMPARE → IDENTIFY GAPS → ADAPT AWS → AZURE → MERGE → UPDATE → VALIDATE
```

- O AWS foi usado **apenas** como referência de padrão de engenharia.
- Toda decisão de cloud do AWS foi mapeada para o serviço Azure equivalente.
- Toda regra de negócio, arquitetura específica e decisão Azure do projeto foram preservadas.

## Matriz de gaps e resolução

| # | Gap identificado (Azure) | Padrão AWS | Resolução aplicada no Azure |
|---|---|---|---|
| 01 | `.claude/agents/` ausente | 9 agents | 10 agents criados, com `architect` e `architecture-validation` parametrizados para Azure; `project-knowledge` adicionado |
| 02 | `.claude/skills/` ausente | 10 skills | 10 skills do Kit IA Dev instaladas verbatim (agnósticas de cloud) |
| 03 | `docs/dicionario/` ausente | 19 arquivos | 20 arquivos copiados do Kit IA Dev (inclui `23-ai-development-roadmap.md`, ausente no projeto AWS) |
| 04 | `docs/governance/` ausente | 6 arquivos | 7 arquivos criados (GITFLOW_SOLID movido + GITFLOW_AI_DELIVERY com tabela de ambientes Azure) |
| 05 | `docs/knowledge/` ausente | 3 arquivos | 3 arquivos criados, incluindo tabela de adaptação AWS → Azure |
| 06 | `docs/README.md` ausente | índice | Índice completo criado |
| 07 | `docs/reports/` e `docs/archive/` ausentes | 2 + 1 arquivos | BOOTSTRAP_REPORT, DOCUMENTATION_REORGANIZATION_REPORT, STANDARDIZATION_AWS_TO_AZURE + backup |
| 08 | Documentos na raiz | `docs/ai`, `docs/architecture`, `docs/project` | Movidos para a árvore oficial `docs/` |
| 09 | `tasks/` ausente | DEPENDENCY_GRAPH + 26 tasks | Criados com EPIC-20 = Azure Target e demais EPICs Azure |
| 10 | Workflows stub (`workflow_dispatch` apenas) | ci/deploy reais | `ci.yml`, `deploy.yml`, `docker.yml`, `security.yml` reescritos com Azure (OIDC, ACR, Container Apps) |
| 11 | `prompts.md` sem Knowledge-Driven Execution | seção 28 | Seção 11 `KNOWLEDGE-DRIVEN EXECUTION` + regra de adaptação AWS → Azure |
| 12 | `prompts.md` com caminhos obsoletos | caminhos `docs/*` | Todos os caminhos normalizados |
| 13 | GitFlow/SOLID duplicado em 3 lugares | fonte única | Consolidado em `docs/governance/GITFLOW_SOLID.md` |
| 14 | `docs/prompts.md` divergente de `prompts.md` | espelho | `docs/prompts.md` virou espelho exato |
| 15 | `README.md` com estrutura desatualizada e `AzureOpenAI` duplicado | — | Estrutura oficial real + providers Azure AI Foundry/Azure OpenAI |
| 16 | Sem `.gitkeep` em diretórios de task | — | `.gitkeep` adicionado para versionamento |
| 17 | `.gitignore` sem regras para Azure/Azurite e diagramas | seção `AWS / LOCALSTACK` | Seção adaptada para `AZURE / AZURITE / SERVERLESS` (`.azure/`, `.azurite/`, `.azure-env/`, `ARM_TEMPLATE_OUTPUT.json`, `.arm/`); adicionadas regras de temporários de Draw.io (`*.drawio.bkp`, `*.drawio.tmp`) mantendo `.drawio` oficiais versionados |
| 18 | `docs/architecture/.$Projeto.drawio.bkp` versionado (~7 MB de backup) | — | Removido do versionamento e adicionado ao `.gitignore`; arquivo preservado em disco |

## Adaptação AWS → Azure (nenhuma configuração AWS copiada)

| Domínio | AWS (referência) | Azure (implementado) |
|---|---|---|
| Object Storage | Amazon S3 | Azure Blob Storage |
| Relacional | Amazon RDS / Aurora MySQL | Azure Database for MySQL - Flexible Server |
| Cache | ElastiCache | Azure Managed Redis |
| Mensageria | SQS / SNS / Amazon MQ / MSK | Azure Service Bus Queues / Topics / Event Hubs |
| Secrets | Secrets Manager / KMS | Azure Key Vault |
| Identidade | Cognito / IAM | Microsoft Entra ID / Azure RBAC + Managed Identities |
| Orquestração | ECS / EKS / Lambda | Azure Container Apps / AKS / Azure Functions |
| CDN/WAF | CloudFront | Azure Front Door |
| DNS | Route 53 | Azure DNS |
| Observabilidade | CloudWatch | Azure Monitor + Application Insights |
| STT | AWS Transcribe | Azure AI Speech |
| LLM gerenciado | Amazon Bedrock | Azure OpenAI / Azure AI Foundry |
| Orquestração de workflow | Step Functions | Azure Durable Functions / Logic Apps |
| Emulador local | LocalStack | Azurite |
| IaC | CloudFormation | Bicep / OpenTofu (provider Azure) |
| CI/CD auth | OIDC | OIDC (`azure/login@v2`, `id-token: write`) |

## Regras de negócio preservadas

- Multi-tenant com isolamento de dados e configurações.
- BYOAI com modos `ServerManaged`, `CustomerManaged` e `Hybrid`.
- AI Content Intelligence (documentos, áudio, vídeo → LLM/RAG/Agents).
- Storage Orchestration com providers por tenant.
- n8n como camada de automação, sem substituir regras de negócio.
- Modular Monolith com DDD, CQRS, Domain Events e SOLID.
- Estratégia `LOCAL FIRST → CONTAINER FIRST → CLOUD READY → AZURE TARGET`.

## Validação

- Paridade de estrutura com o padrão AWS: **OK**
- Ausência de dependência AWS introduzida: **OK** (AWS aparece apenas como origem histórica em `docs/dicionario/` e na tabela de adaptação em `docs/knowledge/`)
- Referências de caminho quebradas: **OK** (0)
- Workflows YAML válidos: **OK**
- `docs/prompts.md` == `prompts.md`: **OK**
- Implementação de código de aplicação: **NÃO INICIADA** (somente governança/documentação)