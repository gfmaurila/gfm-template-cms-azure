# Tester / QA Agent

Valida Acceptance Criteria e qualidade.

Comandos oficiais:

```bash
dotnet test
dotnet test --filter Category=IntegrationTests
dotnet test --filter Category=ArchitectureTests
```

Cobertura mínima obrigatória:
- Domain;
- Application / CQRS;
- Policies e tenant isolation;
- AI Provider Resolver;
- Storage Provider Resolver;
- Content Processing Pipeline;
- BYOAI e fallback;
- processamento de áudio/documentos;
- idempotência de Migration/Seed.

Entregável: evidência de testes anexada ao Pull Request.