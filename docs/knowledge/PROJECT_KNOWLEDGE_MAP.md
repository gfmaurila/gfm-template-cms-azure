# PROJECT KNOWLEDGE MAP

## Dicionário → Conceitos → Requisitos → Decisões → Tasks

Mapeamento inicial baseado no dicionário carregado em `docs/dicionario/`.

| # | Documento | Conceito extraído | Requisito gerado | Decisão | Tasks |
|---|---|---|---|---|---|
| 01 | 01-estrutura-de-projeto.md | DDD, CQRS, Domain Events, Modular Monolith | Estrutura de solução em `backend/`, `frontend/`, `tests/` conforme `docs/architecture/PROJECT_STRUCTURE.md` | ADOPT | TASK-002, TASK-003, TASK-004 |
| 02 | 02-rag.md | RAG / Agentic RAG | Pipeline de indexação e recuperação por tenant | ADAPT | TASK-005, TASK-023 |
| 03 | 03-plugins.md | Extensibilidade, Plugins/MCP | Ports para providers externos | REFERENCE | TASK-005 |
| 04 | 04-frameworks-analise-gestao.md | Frameworks analíticos | Não aplicável ao runtime | REFERENCE | — |
| 05 | 05-conectores-e-funcoes.md | Conectores/Tools | Catálogo de tools para agentes | REFERENCE | TASK-023 |
| 06 | 06-skills-escritorio.md | Automação de escritório | Fora do escopo atual | FUTURE | — |
| 07 | 07-linkedin-manager-agent.md | Agent de LinkedIn | Caso de uso específico | FUTURE | — |
| 08 | 08-free-llm-api-token.md | LLM gratuitas | Providers free/low-cost para BYOAI | REFERENCE | TASK-023 |
| 09 | 09-27-skills.md | Catálogo de skills | Skills do Kit IA Dev instaladas | ADAPT | TASK-000 |
| 10 | 10-llm-local.md | LLM local | Provider `Ollama`/`vLLM` no BYOAI | REFERENCE | TASK-023 |
| 11 | 11-ci-cd.md | CI/CD, Quality Gates | GitHub Actions + gates obrigatórios | ADOPT | TASK-021 |
| 12 | 12-seo-aeo.md | SEO/AEO | Metadados e conteúdo do React Site | REFERENCE | TASK-014 |
| 13 | 13-projetar-microsservicos.md | Evolução a microsserviços | Modular monolith first | REFERENCE | TASK-002 |
| 14 | 14-llm-vs-jev.md | LLM vs job engine | Definição de IAs por tenant | REFERENCE | TASK-023 |
| 15 | 15-rag-system.md | RAG System | Vector Store + indexação por tenant | ADAPT | TASK-023 |
| 16 | 16-arquitetura-e-aplicacoes.md | Princípios arquiteturais | Boundaries e.Dependency Inversion | ADOPT | TASK-002, TASK-005 |
| 17 | 17-agentic-ai.md | Agentic AI | Agents/Tools + integração n8n por webhook | ADAPT | TASK-023 |
| 18 | 18-kit-ia-dev.md | Filosofia Kit IA Dev | Agents, Skills e orquestração | ADOPT | TASK-000, TASK-001 |
| 19 | 20-setup-aws.md | Setup de cloud (AWS) | Setup de cloud **adaptado para Azure** | ADAPT | TASK-020 |
| 20 | 23-ai-development-roadmap.md | Roadmap de engenharia de IA | Trilha de evolução técnica e maturidade das camadas de IA | ADAPT | TASK-023, TASK-017 |

## Conceitos → Onde vivem no projeto

| Conceito | Artefato |
|---|---|
| Estrutura física oficial | `docs/architecture/PROJECT_STRUCTURE.md` |
| Catálogo de Skills do projeto | `docs/project/PROJECT_SKILLS.md` |
| Orquestração principal | `prompts.md` |
| GitFlow / SOLID / entrega | `docs/governance/GITFLOW_AI_DELIVERY.md`, `docs/governance/GITFLOW_SOLID.md` |
| Quality Gates | `docs/governance/QUALITY_GATES.md` |
| Knowledge Gate | `docs/governance/KNOWLEDGE_QUALITY_GATE.md` |
| AI Content Intelligence | `docs/ai/AI_CONTENT_INTELLIGENCE.md` |
| Audio Intelligence | `docs/ai/AUDIO_INTELLIGENCE.md` |
| Seed de dados fake | `docs/project/SEED_FAKE_DATA.md` |
| Grafo de dependências | `tasks/DEPENDENCY_GRAPH.md` |