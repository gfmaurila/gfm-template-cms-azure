# 📘 Dicionário Técnico --- 23 AI Development Roadmap

> **Categoria:** Inteligência Artificial / Engenharia de Software /
> Roadmap de Estudos\
> **Código:** 23\
> **Uso:** Kit IA Dev\
> **Aplicação:** .NET, C#, LLM, RAG, Agents, MCP, Cloud e Agentic
> Engineering

## 1. Visão geral

O roadmap organiza a evolução de um desenvolvedor de software para
desenvolvimento profissional de aplicações com IA:

``` text
Software Engineering
→ AI Fundamentals
→ LLM APIs
→ Prompt Engineering
→ Structured Outputs
→ Embeddings
→ Vector Search
→ RAG
→ Advanced RAG
→ Tool Calling
→ Agents
→ MCP
→ Agentic RAG
→ Multi-Agent
→ Evaluation
→ Security
→ Observability
→ Production AI
```

O objetivo não é abandonar engenharia de software. É acrescentar IA a
uma base sólida de arquitetura, testes, segurança, dados, DevOps e
cloud.

## 2. Fundamentos de engenharia

Antes de avançar em Agentic AI, dominar:

-   C# e .NET;
-   Git e GitFlow;
-   HTTP, REST e JSON;
-   SQL e NoSQL;
-   testes automatizados;
-   Docker;
-   CI/CD;
-   segurança;
-   observabilidade;
-   cloud.

Python pode ser complementar para notebooks, experimentação, dados e
bibliotecas específicas de IA, mas não é obrigatório abandonar .NET.

## 3. Fundamentos de IA

Entender as diferenças entre:

``` text
Artificial Intelligence
Machine Learning
Deep Learning
Generative AI
Large Language Models
```

Conhecer conceitos como treinamento, inferência, classificação,
validação, redes neurais, Transformers, tokens, embeddings, attention e
context window.

## 4. Tokens e contexto

Fluxo conceitual:

``` text
Text → Tokenizer → Tokens → Model → Output
```

Tokens influenciam custo, latência e capacidade de contexto.

O context window inclui instruções, histórico, documentos, resultados de
ferramentas e espaço reservado para a resposta.

## 5. LLM APIs

Aprender a integrar aplicações .NET com modelos:

``` text
ASP.NET Core
→ ILanguageModel
→ Provider Adapter
→ LLM
```

Exemplo de abstração:

``` csharp
public interface ILanguageModel
{
    Task<string> GenerateAsync(
        string prompt,
        CancellationToken cancellationToken);
}
```

Providers podem incluir serviços cloud ou modelos locais.

## 6. Prompt Engineering

Estrutura recomendada:

``` text
Role
Context
Task
Constraints
Output Format
Examples
```

Evitar prompts vagos. Preferir instruções com objetivo, limites e
formato de saída.

## 7. Structured Outputs

Para integração de software:

``` text
LLM
→ JSON
→ Schema Validation
→ Application
```

Nunca confiar cegamente na saída do modelo.

Aplicar parse, validação, tratamento de erro e retry controlado.

## 8. Embeddings

``` text
Text
→ Embedding Model
→ Vector
```

Embeddings permitem busca por similaridade semântica e são fundamentais
para RAG.

## 9. Vector Search

Aprender:

-   similaridade;
-   Top-K;
-   metadata filtering;
-   thresholds;
-   indexação;
-   busca híbrida.

Possíveis tecnologias incluem Qdrant, Pinecone, Weaviate, Milvus,
pgvector, Redis Vector Search, Azure AI Search e OpenSearch.

## 10. RAG

Arquitetura:

``` text
Question
→ Embedding
→ Retrieval
→ Vector DB
→ Relevant Chunks
→ Context
→ LLM
→ Answer + Sources
```

Pipeline de ingestão:

``` text
Documents
→ Parse
→ Clean
→ Chunk
→ Embed
→ Index
```

## 11. Chunking

Estudar:

-   fixed-size;
-   recursive;
-   semantic;
-   structure-aware;
-   overlap.

A estratégia deve ser avaliada com dados reais.

## 12. Advanced RAG

Evoluir para:

``` text
Metadata Filtering
→ Hybrid Search
→ Query Rewriting
→ Multi-Query
→ Reranking
→ Evaluation
→ Graph RAG
```

## 13. RAG Evaluation

Métricas de retrieval podem incluir:

``` text
Precision@K
Recall@K
MRR
Hit Rate
```

Avaliar também correctness, groundedness, relevance e qualidade das
citações.

## 14. Local LLM

Conhecer ferramentas como Ollama, llama.cpp, LM Studio, LocalAI e vLLM.

Cenários:

-   privacidade;
-   desenvolvimento offline;
-   testes;
-   experimentação;
-   infraestrutura controlada.

Arquitetura híbrida:

``` text
AI Router
├── Local Model
└── Cloud Model
```

## 15. Tool Calling

``` text
User
→ LLM
→ Tool Selection
→ Policy
→ Tool
→ Result
→ LLM
```

Regra arquitetural:

``` text
LLM decide intenção
Policy autoriza
Tool executa
```

## 16. Tools

Exemplos:

``` text
search_documents
read_file
run_tests
create_issue
query_database
get_repository_status
```

Cada tool precisa de contrato, schema, permissões e tratamento de erros.

## 17. AI Agents

Um agente combina:

``` text
Goal
+
Model
+
Planning
+
State
+
Memory
+
Tools
+
Policies
```

Loop:

``` text
Goal
→ Plan
→ Action
→ Observation
→ Decision
→ Continue / Stop
```

## 18. Memory

Separar:

``` text
Working Memory
Short-Term Memory
Long-Term Memory
```

RAG não é a mesma coisa que memória:

``` text
RAG → conhecimento externo
Memory → estado/contexto retido
```

## 19. Agentic RAG

O agente escolhe como recuperar informação:

``` text
Question
→ Agent
├── Vector Search
├── SQL
├── Files
├── Git
├── APIs
└── Web
→ Evidence
→ Answer
```

## 20. MCP

Model Context Protocol permite integração padronizada com ferramentas e
fontes:

``` text
Agent
→ MCP Client
→ MCP Server
→ External System
```

Exemplos de integrações: GitHub, arquivos, bancos, documentação, cloud e
ferramentas corporativas.

## 21. Multi-Agent Systems

``` text
Orchestrator
├── Requirements Agent
├── Architect Agent
├── Tech Lead Agent
├── Developer Agent
├── Tester Agent
├── Reviewer Agent
└── Documentation Agent
```

Evitar um mega-agent com todas as responsabilidades.

## 22. Artifact-Driven AI

Handoffs devem utilizar artifacts claros:

``` text
REQUIREMENTS.md
ARCHITECTURE_PLAN.md
EXECUTION_PLAN.md
TEST_REPORT.md
REVIEW_REPORT.md
```

## 23. Guardrails

Implementar:

-   permissões;
-   least privilege;
-   max steps;
-   timeout;
-   budgets;
-   schemas;
-   tool policies;
-   approval gates;
-   audit trail.

## 24. Human in the Loop

Ações críticas podem exigir aprovação explícita:

``` text
merge to main
production deployment
destructive migration
delete cloud resource
external communication
```

## 25. AI Security

Estudar:

``` text
Prompt Injection
Tool Injection
Data Leakage
Secret Exposure
Authorization
PII Handling
Model Abuse
```

Conteúdo recuperado deve ser tratado como dado, não como autoridade
sobre as políticas do sistema.

## 26. Evaluation

``` text
Input
→ AI System
→ Output
→ Evaluator
```

Criar Golden Datasets com input, comportamento esperado, fatos esperados
e comportamentos proibidos.

Executar regressão ao alterar modelo, prompt, retrieval, chunking, agent
ou tools.

## 27. Observabilidade

Monitorar:

``` text
latency
tokens
cost
model
retrieval
tool calls
agent steps
errors
```

Utilizar traces para correlacionar API, agent, retriever, LLM e tools.

## 28. OpenTelemetry

Pode instrumentar:

``` text
ASP.NET Core
HTTP
Database
Redis
Messaging
AI Calls
```

## 29. Context Engineering

Competência central:

``` text
Available Information
→ Search
→ Filter
→ Rank
→ Compress
→ Model Context
```

Prompt é instrução; contexto é a informação fornecida para resolver a
tarefa.

## 30. Token e custo

Otimizar com:

-   contexto relevante;
-   RAG;
-   cache;
-   semantic cache;
-   model routing;
-   compressão de outputs;
-   respostas estruturadas;
-   limites de passos.

## 31. Arquitetura .NET para IA

``` text
AI/
├── Abstractions/
├── Providers/
├── Prompts/
├── Embeddings/
├── Ingestion/
├── Retrieval/
├── RAG/
├── Agents/
├── Memory/
├── Tools/
├── Orchestration/
├── Evaluation/
└── Observability/
```

O Domain não deve depender diretamente de SDK de provider de IA.

## 32. Async AI

Tarefas demoradas:

``` text
API
→ Queue
→ AI Worker
→ Result
```

Pode usar RabbitMQ, Kafka, SQS ou Service Bus conforme arquitetura.

## 33. AWS para IA

Competências úteis:

``` text
S3
SQS
SNS
Lambda
EC2
ECS
```

Exemplo:

``` text
Document
→ S3
→ SQS
→ AI Worker on ECS
→ Embeddings
→ Vector Store
```

## 34. Docker

Ambiente local possível:

``` text
docker-compose
├── API
├── frontend
├── database
├── redis
├── vector-db
├── local-llm
└── observability
```

## 35. AI Testing

Camadas:

``` text
Unit Tests
Integration Tests
Prompt Tests
RAG Evaluation
Agent Evaluation
Security Tests
```

Usar Fake LLM, Fake Embeddings e Fake Tools para testes determinísticos
quando adequado.

## 36. AI CI/CD

``` text
Build
→ Unit Tests
→ Integration Tests
→ AI Evaluations
→ Security
→ Docker
→ Deploy
```

## 37. Prompt Versioning

Versionar prompts importantes e registrar:

``` text
provider
model
prompt version
configuration
evaluation result
```

## 38. LLMOps

LLMOps enfatiza:

``` text
models
prompts
RAG
evaluations
tokens
cost
guardrails
observability
```

## 39. Production Readiness

Antes de produção:

-   segurança;
-   avaliação;
-   fallback;
-   rate limiting;
-   cost controls;
-   observabilidade;
-   privacidade;
-   incident response;
-   retry e timeout;
-   data governance.

## 40. Roadmap --- Fase 1: Engenharia

Aprender:

``` text
C#
.NET
Git
HTTP
REST
SQL
Testing
Docker
```

Projeto: **REST API .NET bem testada**.

## 41. Fase 2: Fundamentos LLM

Aprender:

``` text
tokens
context
embeddings
transformers
inference
```

Projeto: **chat console em .NET**.

## 42. Fase 3: LLM APIs

Aprender:

``` text
provider abstraction
DI
timeouts
retry
streaming
structured output
```

Projeto: **AI API com ASP.NET Core**.

## 43. Fase 4: Prompt Engineering

Aprender:

``` text
system prompts
few-shot
schemas
validation
```

Projeto: **Requirements Analyzer**.

## 44. Fase 5: Embeddings

Aprender:

``` text
embedding models
similarity
vector search
metadata
```

Projeto: **Semantic Search**.

## 45. Fase 6: RAG

Aprender:

``` text
ingestion
chunking
embeddings
vector DB
retrieval
sources
```

Projeto: **Documentation Assistant**.

## 46. Fase 7: Advanced RAG

Aprender:

``` text
hybrid search
reranking
query rewriting
evaluation
Graph RAG concepts
```

Projeto: **Enterprise Knowledge Assistant**.

## 47. Fase 8: Tool Calling

Aprender:

``` text
schemas
function calling
authorization
errors
```

Projeto: **Assistant com GitHub e Files tools**.

## 48. Fase 9: Agents

Aprender:

``` text
planning
state
memory
tools
loops
stop conditions
guardrails
```

Projeto: **Developer Agent**.

## 49. Fase 10: MCP

Aprender:

``` text
MCP clients
MCP servers
tool discovery
resources
permissions
```

Projeto: **Agent conectado a ferramentas de desenvolvimento**.

## 50. Fase 11: Multi-Agent

Aprender:

``` text
orchestration
handoffs
specialized agents
quality gates
parallel execution
```

Projeto:

``` text
Requirements
→ Architect
→ Developer
→ Tester
→ Reviewer
```

## 51. Fase 12: Production AI

Aprender:

``` text
evaluation
observability
security
cost
CI/CD
cloud
resilience
```

Projeto: **Production-ready AI Platform**.

## 52. Projetos progressivos

``` text
01. Chat Console
02. AI REST API
03. Structured Extractor
04. Semantic Search
05. RAG Assistant
06. Advanced RAG
07. Tool-Calling Assistant
08. Developer Agent
09. MCP Agent
10. Multi-Agent System
11. Kit IA Dev
12. Production AI Platform
```

## 53. Skills para o Kit IA Dev

``` text
3-Skills/
├── llm-api/
├── prompt-engineering/
├── structured-output/
├── embeddings/
├── vector-search/
├── rag/
├── advanced-rag/
├── tool-calling/
├── mcp/
├── agent-development/
├── multi-agent/
├── ai-evaluation/
├── ai-security/
└── ai-observability/
```

## 54. Agents sugeridos

``` text
2-Agents/
├── ai-architect/
├── rag-engineer/
├── agent-engineer/
├── ai-security/
└── ai-evaluator/
```

## 55. Templates sugeridos

``` text
4-Templates/
├── dotnet-ai-api/
├── dotnet-rag/
├── dotnet-agent/
├── dotnet-mcp/
└── dotnet-multi-agent/
```

## 56. Workflows sugeridos

``` text
5-Workflows/
├── ai-feature/
├── rag-development/
├── agent-development/
├── ai-evaluation/
└── ai-production-release/
```

## 57. Quality Gates

``` text
6-Quality-Gates/
└── ai/
    ├── prompt/
    ├── rag/
    ├── agents/
    ├── security/
    ├── evaluation/
    └── production/
```

### Prompt Gate

-   [ ] instrução clara;
-   [ ] formato definido;
-   [ ] output validado;
-   [ ] prompt versionado.

### RAG Gate

-   [ ] chunking testado;
-   [ ] metadata;
-   [ ] retrieval avaliado;
-   [ ] fontes;
-   [ ] no-evidence behavior;
-   [ ] autorização.

### Agent Gate

-   [ ] objetivo;
-   [ ] tools;
-   [ ] max steps;
-   [ ] timeout;
-   [ ] stop condition;
-   [ ] approval boundary;
-   [ ] audit.

### Production Gate

-   [ ] evaluation;
-   [ ] security;
-   [ ] observability;
-   [ ] fallback;
-   [ ] rate limits;
-   [ ] cost controls;
-   [ ] runbook.

## 58. Estratégia de estudo

Preferir:

``` text
Learn
→ Build
→ Test
→ Document
→ Publish
→ Improve
```

Cada etapa deve produzir algo utilizável.

Exemplo:

``` text
Learn Embeddings
→ Build Semantic Search
→ Add Tests
→ Create README
→ Draw Architecture
```

## 59. Portfólio esperado

Ao completar a trilha, o portfólio pode demonstrar:

``` text
AI API
Structured Output
Semantic Search
RAG
Advanced RAG
Tool Calling
Agent
MCP
Multi-Agent
Cloud Deployment
Evaluation
Observability
```

Isso demonstra engenharia de IA, não apenas uso de prompts.

## 60. Prioridade para desenvolvedor .NET

``` text
1. LLM API
2. Prompt Engineering
3. Structured Output
4. Embeddings
5. Vector DB
6. RAG
7. Evaluation
8. Tool Calling
9. Agents
10. MCP
11. Agentic RAG
12. Multi-Agent
13. AI Security
14. AI Observability
15. Cloud Production
```

## 61. O que não precisa ser prioridade inicial

Se o objetivo é construir aplicações empresariais com IA, não é
necessário começar por:

``` text
training LLM from scratch
CUDA kernels
advanced neural network mathematics
distributed model training
```

Esses assuntos tornam-se importantes em especializações diferentes.

## 62. Anti-patterns

Evitar:

``` text
pular diretamente para multi-agent
usar LLM sem validação
RAG sem avaliação
agent com permissões ilimitadas
ignorar testes
ignorar segurança
ignorar custo
ignorar observabilidade
acoplar domínio ao provider
seguir frameworks por hype
```

## 63. Roadmap consolidado

``` text
FOUNDATION
   ↓
LLM
   ↓
PROMPTS
   ↓
STRUCTURED OUTPUT
   ↓
EMBEDDINGS
   ↓
VECTOR SEARCH
   ↓
RAG
   ↓
ADVANCED RAG
   ↓
EVALUATION
   ↓
TOOLS
   ↓
AGENTS
   ↓
MCP
   ↓
AGENTIC RAG
   ↓
MULTI-AGENT
   ↓
SECURITY
   ↓
OBSERVABILITY
   ↓
PRODUCTION AI
```

## 64. Relação com outros itens

``` text
01.2 - Agentic Workflow
02   - RAG
02.2 - RAG .NET
03   - Plugins
05   - Conectores e Funções
08   - Free LLM API / Token
09   - Skills
10   - LLM Local
11   - CI/CD
14   - LLM vs Jev
15   - RAG System
16   - Arquitetura e Aplicações
17   - Agentic AI
18   - Kit IA Dev
20   - Setup AWS
23   - AI Development Roadmap
```

## 65. Resumo final

O objetivo final não é apenas aprender a chamar um modelo.

É construir sistemas de IA:

``` text
TESTÁVEIS
+
SEGUROS
+
OBSERVÁVEIS
+
DESACOPLADOS
+
AVALIÁVEIS
+
ESCALÁVEIS
+
PRONTOS PARA PRODUÇÃO
```

Para um desenvolvedor .NET, a evolução natural é manter **C#/.NET e
engenharia de software como base**, acrescentando progressivamente LLMs,
embeddings, RAG, tools, agents, MCP, avaliação, segurança,
observabilidade e cloud.

# 📁 Arquivo

``` text
23-ai-development-roadmap.md
```
