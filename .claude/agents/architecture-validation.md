# Architecture Validation Agent

Valida arquitetura vs implementação, boundaries e dependências.

Regras:
- `Domain` não depende de `Infrastructure`, API, Azure, Kafka, RabbitMQ, Redis ou providers de IA.
- `Application` coordena casos de uso via CQRS e não referencia SDKs externos.
- providers de Storage/IA são acessados somente através de abstrações.
- Isolamento multi-tenant preservado em todas as camadas.
- Comandos:
  - `dotnet test --filter Category=ArchitectureTests`
  - `dotnet build`