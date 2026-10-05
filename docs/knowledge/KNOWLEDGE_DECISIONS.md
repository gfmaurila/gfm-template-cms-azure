# KNOWLEDGE DECISIONS

| Documento | Classificação | Justificativa |
|---|---|---|
| 01-estrutura-de-projeto.md | ADOPT | Baseline de estrutura do projeto (DDD, CQRS, Modular Monolith). |
| 02-rag.md | REFERENCE | Conceitos RAG/Agentic RAG úteis para AI Content Intelligence. |
| 03-plugins.md | REFERENCE | Padrões de extensibilidade e Plugins/MCP para evolução futura. |
| 04-frameworks-analise-gestao.md | REFERENCE | Frameworks analíticos para decisões estratégicas. |
| 05-conectores-e-funcoes.md | REFERENCE | Conectores/Tools para integrações futuras. |
| 06-skills-escritorio.md | FUTURE | Automação de escritório não essencial agora. |
| 07-linkedin-manager-agent.md | FUTURE | Caso de uso específico fora do escopo atual. |
| 08-free-llm-api-token.md | REFERENCE | Opções de LLM free para BYOAI/local. |
| 09-27-skills.md | ADAPT | Catálogo de skills aplicável ao Kit IA Dev no projeto. |
| 10-llm-local.md | REFERENCE | Suporte a LLM local no modelo BYOAI. |
| 11-ci-cd.md | ADOPT | Base para CI/CD GitHub Actions e Quality Gates. |
| 12-seo-aeo.md | REFERENCE | SEO/AEO aplicável ao React Site no futuro. |
| 13-projetar-microsservicos.md | REFERENCE | Evolução futura para microsserviços (modular monolith first). |
| 14-llm-vs-jev.md | REFERENCE | Comparação conceitual para decisões de arquitetura IA. |
| 15-rag-system.md | ADAPT | RAG System para indexação/vector store no AI Content Intelligence. |
| 16-arquitetura-e-aplicacoes.md | ADOPT | Princípios arquiteturais alinhados com .NET/Azure. |
| 17-agentic-ai.md | ADAPT | Agentic AI para agentes/workflows (n8n/tools). |
| 18-kit-ia-dev.md | ADOPT | Filosofia Kit IA Dev (Agents/Skills/Orquestração). |
| 20-setup-aws.md | ADAPT | Baseline de setup cloud. Somente a parte de IaC/operação é adaptada para Azure (OpenTofu + Azure); a estrutura de setup local permanece ADOPT. |
| 23-ai-development-roadmap.md | ADAPT | Roadmap de engenharia de IA. Adotada como trilha de evolução técnica e como critério de maturidade para as camadas de AI Content Intelligence, RAG, Agents e Observability. |

## Adaptação AWS → Azure

Nenhum documento do dicionário é copiado literalmente quando contém decisões de cloud.
As seguintes equivalências foram aplicadas:

| AWS (dicionário 20-setup-aws.md) | Azure (projeto) |
|---|---|
| Amazon S3 / S3 | Azure Blob Storage |
| Amazon RDS / Aurora MySQL | Azure Database for MySQL - Flexible Server |
| ElastiCache | Azure Managed Redis |
| Amazon MQ (RabbitMQ) | Azure Service Bus |
| MSK (Kafka) | Azure Event Hubs |
| Secrets Manager / KMS | Azure Key Vault |
| Cognito | Microsoft Entra ID |
| IAM Roles / Policies | Azure RBAC + Managed Identities |
| ECS / EKS | Azure Container Apps / AKS |
| Lambda | Azure Functions (quando serverless for justificável) |
| SQS / SNS | Azure Service Bus Queues / Topics |
| CloudFront | Azure Front Door (CDN + WAF) |
| Route 53 | Azure DNS |
| CloudWatch | Azure Monitor + Application Insights |
| Step Functions | Azure Durable Functions (ou Logic Apps) |
| LocalStack | Azurite |
| AWS Transcribe | Azure AI Speech |
| Amazon Bedrock | Azure OpenAI / Azure AI Foundry |
| CloudFormation | Bicep / OpenTofu com provider Azure |
| OIDC com GitHub Actions | OIDC com GitHub Actions (`azure/login-action`) |

Fonte do dicionário (EXTERNAL, read-only):
`D:\Empresa\GFMaurila\projetos\Kit-IA-Dev\dicionario`
Espelho local: `docs/dicionario/`