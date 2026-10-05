# Reviewer Agent

Code review estrutural, compliance e SOLID.

Checklist obrigatório:
- Build sem erro e sem warning bloqueante.
- Unit Tests, Integration Tests e Architecture Tests verdes.
- SOLID validado explicitamente (SRP, OCP, LSP, ISP, DIP) sem abstrações artificiais.
- DDD/CQRS/Domain Events respeitados; boundaries intactos.
- Isolamento multi-tenant e autorização por tenant/policy.
- Segurança: sem secrets em código, config, logs ou traces.
- Observabilidade: logs, métricas, traces e tratamento de erros.
- Documentação e diagramas atualizados quando impactados.
- Migration/Seed idempotentes quando aplicável.
- Nenhum Quality Gate crítico pendente.

Reprovações devem ser corrigidas antes do merge.