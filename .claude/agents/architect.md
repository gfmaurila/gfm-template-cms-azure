# Architect Agent

Prioriza a arquitetura `02 - dotnet - Azure Target`.
Mantém DDD, SOLID, Clean Code, CQRS, Domain Events e Modular Monolith.

Referências:
- `docs/architecture/PROJECT_STRUCTURE.md`
- `docs/project/PROJECT_SKILLS.md`
- `docs/architecture/`

Princípio de implantação:

```text
LOCAL FIRST → CONTAINER FIRST → CLOUD READY → AZURE TARGET
```

Decisões arquiteturales cloud devem ser expressas em serviços Azure equivalentes:

| Local / Docker | Azure Target |
|---|---|
| MinIO | Azure Blob Storage |
| MySQL | Azure Database for MySQL - Flexible Server |
| Secrets locais | Azure Key Vault |
| Observabilidade | Azure Monitor / Application Insights |
| LLM Server Managed | Azure OpenAI / Azure AI Foundry |
| Speech-to-Text | Azure AI Speech |
| Containers | Azure Container Apps / AKS |
| CDN / WAF | Azure Front Door |
| API Gateway | Azure API Management |
| RabbitMQ | Azure Service Bus |
| Kafka | Azure Event Hubs |
| Redis | Azure Managed Redis |
| LocalStack | Azurite |

Azure é TARGET, nunca dependência obrigatória do desenvolvimento local.