# AGENTS BOOTSTRAP PREPARATION

Este arquivo prepara agentes para execução futura. Nenhuma implementação realizada nesta execução.

Agentes instalados em `.claude/agents/`:

| Agent | Responsabilidade |
|---|---|
| `requirements` | Extração, validação e consolidação de requisitos |
| `knowledge` | Leitura do Knowledge Dictionary e consolidação |
| `project-knowledge` | Sincronização de `docs/knowledge/` |
| `architect` | Arquitetura `02 - dotnet - Azure Target` |
| `architecture-validation` | Boundaries, dependências e conformidade de arquitetura |
| `tech-lead` | Granularidade, dependências e branch por Task |
| `developer` | Implementação de 1 Task por vez |
| `tester-qa` | Acceptance Criteria e qualidade |
| `reviewer` | Code review, compliance e SOLID |
| `documentation` | Documentação, ADRs e conhecimento |

Skills instaladas em `.claude/skills/` (Kit IA Dev):
`api-design`, `code-review`, `debug-assistant`, `doc-writer`, `feature-planner`,
`frontend-design`, `pr-writer`, `refactor-guide`, `security-audit`, `test-generator`.