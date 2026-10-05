# Arquitetura Azure — GFM.Template.CMS

Este diretório recebe os artefatos de arquitetura gerados após a criação/inspeção da estrutura do projeto.

## Especificação oficial

- [PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md) — estrutura física oficial e regras arquiteturais.

## Artefatos esperados

- `azure-architecture.drawio` — diagrama principal editável;
- `structurizr/workspace.dsl` — modelo C4/Structurizr quando aplicável;
- diagramas UML e ER definidos pelo fluxo do `prompts.md`;
- ADRs referentes às decisões de arquitetura Azure.

## Artefatos presentes

| Arquivo | Tipo | Descrição |
|---|---|---|
| `Projeto.drawio` | editável | Diagrama principal de arquitetura Azure |
| `Arquitetura Azure Multi-Tenant e CI_CD.png` | imagem | Visão geral da arquitetura Azure multi-tenant e do CI/CD |
| `Fluxo Backend Azure Multi-Tenant.png` | imagem | Fluxo do backend Azure multi-tenant |
| `Fluxo Completo do Front-end em Azure.png` | imagem | Fluxo completo do front-end em Azure |
| `Infográfico GitFlow_ Fluxo Completo CI_CD no Azure.png` | imagem | Infográfico GitFlow + CI/CD no Azure |
| `diagrams/` | imagens | Diagramas genéricos da plataforma (`Arquitetura-GFM-Template-CMS.png`, `backend.png`, `frontend.png`, `gitflow.png`) |

Os arquivos `.drawio` e `.dsl` são os artefatos editáveis oficiais. Os `.png` são derivados.

## Princípio de implantação

`LOCAL FIRST → CONTAINER FIRST → CLOUD READY → AZURE TARGET`

O desenvolvimento local não deve depender de uma assinatura Azure real.

## Mapeamento Local → Azure

| Local / Docker | Azure Target |
|---|---|
| Containers | Azure Container Apps / AKS |
| MinIO | Azure Blob Storage |
| MySQL | Azure Database for MySQL - Flexible Server |
| Secrets locais | Azure Key Vault |
| Observabilidade | Azure Monitor / Application Insights |
| LLM Server Managed | Azure OpenAI / Azure AI Foundry |
| Speech-to-Text | Azure AI Speech |
| RabbitMQ | Azure Service Bus |
| Kafka | Azure Event Hubs |
| Redis | Azure Managed Redis |
| LocalStack | Azurite |
| API Gateway | Azure API Management |
| CDN | Azure Front Door |

Referência completa: [PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md) — seção `Fluxo LOCAL → AZURE`.