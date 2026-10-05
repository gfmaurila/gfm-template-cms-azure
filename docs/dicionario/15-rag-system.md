# 📘 Dicionário Técnico — 15 RAG System

> **Categoria:** Inteligência Artificial / RAG / Sistemas de Conhecimento  
> **Código:** 15  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** .NET / LLM / Vector Database / Agentic RAG / Multi-Agent / MCP  
> **Objetivo:** Documentar uma arquitetura completa de RAG System, desde ingestão e indexação até recuperação, geração, memória, agentes, ferramentas, segurança, observabilidade e avaliação.

---

# 1. O que é um RAG System

RAG significa:

```text
Retrieval-Augmented Generation
```

Um RAG System combina recuperação de conhecimento com geração por LLM.

```text
User Question
 ↓
Retrieval
 ↓
Relevant Knowledge
 ↓
LLM
 ↓
Grounded Answer
```

O objetivo é fornecer ao modelo contexto relevante no momento da resposta.

---

# 2. Problema que RAG resolve

Um LLM possui limitações:

```text
knowledge cutoff
no access to private data by default
hallucinations
limited context
no project-specific knowledge
```

RAG adiciona conhecimento externo.

---

# 3. Arquitetura clássica

```text
Query
 ↓
Embedding
 ↓
Vector Search
 ↓
Vector Database
 ↓
Retrieved Chunks
 ↓
Context Builder
 ↓
LLM
 ↓
Answer
```

---

# 4. Dois pipelines

Um sistema RAG possui dois grandes fluxos:

```text
INGESTION
```

e:

```text
RETRIEVAL / GENERATION
```

---

# 5. Pipeline de ingestão

```text
Documents
 ↓
Load
 ↓
Parse
 ↓
Clean
 ↓
Chunk
 ↓
Metadata
 ↓
Embedding
 ↓
Vector Store
```

---

# 6. Fontes de dados

Podem incluir:

```text
PDF
Markdown
TXT
DOCX
HTML
Web Pages
Database
Git Repository
APIs
Tickets
Knowledge Base
Cloud Storage
```

---

# 7. Document Loader

Responsável por carregar fontes.

Interface conceitual:

```csharp
public interface IDocumentLoader
{
    Task<IReadOnlyCollection<Document>> LoadAsync(
        CancellationToken cancellationToken);
}
```

---

# 8. Parsing

Transforma documento bruto em conteúdo utilizável.

```text
PDF
 ↓
Parser
 ↓
Text + Metadata
```

Preservar quando possível:

```text
title
section
page
source
author
date
```

---

# 9. Cleaning

Remove ruído.

Exemplos:

```text
duplicate headers
navigation
irrelevant footer
broken whitespace
duplicated text
```

Evitar remover informação semanticamente importante.

---

# 10. Chunking

Documento é dividido em partes menores.

```text
Document
 ↓
Chunk 1
Chunk 2
Chunk 3
```

O chunk precisa manter contexto suficiente.

---

# 11. Fixed-size Chunking

```text
500 tokens
+
overlap
```

Simples, mas pode cortar conceitos no meio.

---

# 12. Semantic Chunking

Divide por estrutura/significado.

```text
Heading
 ↓
Paragraphs
 ↓
Semantic Section
```

Pode produzir contexto mais coerente.

---

# 13. Recursive Chunking

Tenta dividir utilizando separadores hierárquicos.

```text
section
paragraph
sentence
token
```

---

# 14. Chunk Overlap

Exemplo:

```text
Chunk A
[1 ........ 500]

Chunk B
       [450 ........ 950]
```

Overlap pode preservar contexto entre fronteiras.

Muito overlap gera duplicação.

---

# 15. Metadata

Cada chunk deve carregar metadados.

Exemplo:

```json
{
  "documentId": "architecture",
  "section": "Caching",
  "source": "ARCHITECTURE.md",
  "version": "1.2",
  "environment": "prod"
}
```

---

# 16. Embeddings

Embedding converte texto em vetor.

```text
Text
 ↓
Embedding Model
 ↓
Vector
```

Textos semanticamente semelhantes tendem a ficar próximos no espaço vetorial.

---

# 17. Vector Database

Armazena e consulta vetores.

Possibilidades:

```text
Qdrant
Pinecone
Weaviate
Milvus
pgvector
Redis Vector Search
Azure AI Search
OpenSearch
```

A escolha depende de requisitos.

---

# 18. Index

Estrutura conceitual:

```text
Vector
+
Chunk
+
Metadata
```

---

# 19. Similarity Search

```text
User Query
 ↓
Query Embedding
 ↓
Nearest Vectors
 ↓
Top-K Chunks
```

---

# 20. Top-K

Número de resultados recuperados.

```text
Top-K = 5
```

Mais documentos não significa necessariamente resposta melhor.

---

# 21. Metadata Filtering

Exemplo:

```text
environment = prod
documentType = architecture
version = current
```

Primeiro filtrar, depois recuperar candidatos relevantes.

---

# 22. Keyword Search

Busca lexical continua útil.

```text
BM25
```

é um exemplo conhecido.

Busca vetorial e lexical resolvem problemas diferentes.

---

# 23. Hybrid Search

Combina:

```text
Keyword Search
+
Vector Search
```

Pode melhorar recuperação.

---

# 24. Reranking

Primeira busca gera candidatos.

```text
Retriever
 ↓
20 Candidates
 ↓
Reranker
 ↓
Best 5
```

Os melhores chunks seguem para o LLM.

---

# 25. Context Builder

Organiza os resultados.

```text
Retrieved Chunks
 ↓
Deduplication
 ↓
Ranking
 ↓
Token Budget
 ↓
Prompt Context
```

---

# 26. Token Budget

Não enviar contexto ilimitado.

```text
System Prompt
+
History
+
Retrieved Context
+
User Query
+
Output Budget
```

Tudo deve caber no contexto do modelo.

---

# 27. Prompt Augmentation

```text
System Prompt
+
Retrieved Evidence
+
Question
 ↓
LLM
```

---

# 28. Grounding

Instrução importante:

```text
Use apenas as evidências fornecidas quando a pergunta
depender da base de conhecimento.
```

Quando não houver evidência suficiente, o sistema deve poder informar isso.

---

# 29. Citações

Resposta ideal:

```text
Answer
+
Source References
```

O sistema precisa preservar origem durante toda a pipeline.

---

# 30. Classic RAG

```text
Query
 ↓
Retriever
 ↓
Context
 ↓
LLM
 ↓
Answer
```

Simples e eficiente para muitos cenários.

---

# 31. Graph RAG

Utiliza relações entre entidades/conceitos.

```text
Entity
 ↓
Relationship
 ↓
Graph
 ↓
Context
```

Útil quando relações são importantes.

---

# 32. Knowledge Graph

Exemplo:

```text
Order Service
 ├── publishes → OrderCreated
 ├── uses → MySQL
 └── depends-on → Payment Service
```

Uma consulta pode navegar por essas relações.

---

# 33. Agentic RAG

Um agente decide como recuperar informação.

```text
Question
 ↓
Agent
 ├── Search Vector DB
 ├── Search SQL
 ├── Search Files
 ├── Search API
 └── Search Web
 ↓
Reason
 ↓
Answer
```

---

# 34. Diferença

Classic RAG:

```text
fixed retrieval pipeline
```

Agentic RAG:

```text
dynamic retrieval strategy
```

---

# 35. Query Planning

```text
Complex Question
 ↓
Planner
 ↓
Subquery 1
Subquery 2
Subquery 3
```

Cada subquery pode consultar fonte diferente.

---

# 36. Query Rewriting

Pergunta:

```text
"E o Redis?"
```

Histórico:

```text
"Como funciona o cache no projeto?"
```

Reescrita:

```text
"Como Redis é utilizado como cache no projeto?"
```

---

# 37. Multi-Query Retrieval

```text
Original Query
 ↓
Query A
Query B
Query C
 ↓
Retrieval
 ↓
Merge
```

Pode aumentar recall.

---

# 38. Retrieval Router

```text
Question
 ↓
Router
 ├── Vector DB
 ├── SQL
 ├── Graph
 ├── Search
 └── API
```

---

# 39. SQL Retrieval

Nem tudo precisa de vetor.

Pergunta:

```text
"Quantos usuários ativos existem?"
```

Melhor fonte:

```text
SQL
```

---

# 40. Vector Retrieval

Pergunta:

```text
"Qual é a estratégia de autenticação descrita nos documentos?"
```

Boa candidata:

```text
Vector Search
```

---

# 41. Graph Retrieval

Pergunta:

```text
"Quais serviços dependem de Payment?"
```

Pode ser adequada para grafo.

---

# 42. Tool Retrieval

```text
Agent
 ↓
Tool
 ↓
External API
 ↓
Data
```

---

# 43. MCP

MCP pode padronizar acesso a ferramentas/fontes.

```text
Agent
 ↓
MCP Client
 ↓
MCP Servers
 ├── GitHub
 ├── Files
 ├── Database
 └── External Systems
```

---

# 44. Multi-Agent RAG

```text
User
 ↓
Orchestrator
 ├── Documentation Agent
 ├── Code Agent
 ├── Database Agent
 └── Research Agent
 ↓
Aggregator
 ↓
Answer
```

---

# 45. Specialized Agents

Exemplo:

```text
Code Agent
→ repository

Database Agent
→ SQL

Docs Agent
→ vector store

Cloud Agent
→ infrastructure docs
```

---

# 46. Aggregator Agent

Responsável por:

```text
merge findings
remove duplicates
detect conflicts
rank evidence
compose final context
```

---

# 47. Memory

RAG e memória são conceitos diferentes.

```text
RAG
→ external knowledge

Memory
→ interaction/state/history
```

Podem trabalhar juntos.

---

# 48. Short-Term Memory

```text
current conversation
current task
recent tool results
```

---

# 49. Long-Term Memory

Pode guardar conhecimento autorizado e persistente.

Precisa de:

```text
retention policy
privacy
ownership
update strategy
```

---

# 50. Conversation Summary

Em vez de enviar histórico inteiro:

```text
Conversation
 ↓
Summarization
 ↓
Compact Memory
```

---

# 51. Cache

RAG pode usar cache em várias camadas.

```text
Document Cache
Embedding Cache
Retrieval Cache
Response Cache
Semantic Cache
```

---

# 52. Redis

Pode ser usado para:

```text
cache
session
semantic cache
rate limiting
temporary state
```

---

# 53. Semantic Cache

```text
Question
 ↓
Embedding
 ↓
Similar Cached Question?
 ├── Yes → Cached Result
 └── No → RAG
```

---

# 54. MongoDB

Pode armazenar:

```text
documents
conversation history
projections
metadata
AI execution history
```

quando adequado.

---

# 55. MySQL

Pode armazenar:

```text
users
permissions
business data
document registry
ingestion status
```

---

# 56. Event-Driven Ingestion

```text
Document Uploaded
 ↓
Event
 ↓
Ingestion Worker
 ↓
Chunk
 ↓
Embedding
 ↓
Index
```

---

# 57. RabbitMQ

Pode processar filas como:

```text
document-ingestion
embedding-generation
reindexing
```

---

# 58. Kafka

Pode distribuir eventos:

```text
DocumentUpdated
KnowledgeChanged
IndexUpdated
```

em arquiteturas que precisam de streaming.

---

# 59. AWS S3

Fluxo:

```text
Upload
 ↓
S3
 ↓
Event
 ↓
SQS / Lambda
 ↓
Ingestion
 ↓
Vector Store
```

---

# 60. AWS Lambda

Pode executar partes leves/event-driven da ingestão.

Para processamento pesado, avaliar limites e arquitetura apropriada.

---

# 61. SQS

```text
S3 Event
 ↓
SQS
 ↓
AI Worker
```

Ajuda a desacoplar ingestão.

---

# 62. SNS

```text
KnowledgeUpdated
 ↓
SNS
 ├── Reindex Queue
 ├── Audit Queue
 └── Notification Queue
```

---

# 63. Local RAG

```text
Documents
 ↓
Local Embeddings
 ↓
Qdrant
 ↓
Local LLM
```

Pode funcionar sem provider externo.

---

# 64. Hybrid RAG

```text
Local Vector DB
+
Cloud LLM
```

ou:

```text
Cloud Search
+
Local LLM
```

Arquitetura deve abstrair providers.

---

# 65. Estrutura .NET

```text
AI/
├── Abstractions/
├── Providers/
├── Embeddings/
├── Ingestion/
├── Chunking/
├── Retrieval/
├── Reranking/
├── RAG/
├── Agents/
├── Memory/
├── Tools/
├── Prompts/
├── Evaluation/
└── Observability/
```

---

# 66. Abstrações

```text
ILanguageModel
IEmbeddingService
IDocumentLoader
IDocumentParser
IChunker
IVectorStore
IRetriever
IReranker
IContextBuilder
IRagPipeline
```

---

# 67. IEmbeddingService

```csharp
public interface IEmbeddingService
{
    Task<float[]> CreateAsync(
        string text,
        CancellationToken cancellationToken);
}
```

---

# 68. IRetriever

```csharp
public interface IRetriever
{
    Task<IReadOnlyCollection<SearchResult>> RetrieveAsync(
        string query,
        CancellationToken cancellationToken);
}
```

---

# 69. IRagPipeline

```csharp
public interface IRagPipeline
{
    Task<RagResponse> AskAsync(
        string question,
        CancellationToken cancellationToken);
}
```

---

# 70. Dependency Injection

```text
Application
 ↓
Interfaces
 ↓
DI
 ↓
Providers
```

Trocar:

```text
OpenAI
Azure OpenAI
Anthropic
Ollama
Qdrant
Redis
```

sem alterar regras centrais.

---

# 71. API

Exemplo:

```text
POST /api/rag/query
```

Entrada:

```json
{
  "question": "Como funciona a autenticação?"
}
```

---

# 72. Resposta

```json
{
  "answer": "...",
  "sources": [],
  "traceId": "..."
}
```

---

# 73. Streaming

Respostas podem ser transmitidas progressivamente.

```text
LLM
 ↓
Token Stream
 ↓
API
 ↓
Frontend
```

---

# 74. Security Trimming

Usuário só pode recuperar documentos autorizados.

```text
User
 ↓
Permissions
 ↓
Retriever Filter
 ↓
Authorized Chunks
```

Crítico em bases multiusuário.

---

# 75. Multi-Tenancy

Cada chunk deve carregar tenant quando aplicável.

```text
tenantId
documentId
permissions
```

Consulta:

```text
WHERE tenantId = currentTenant
```

ou filtro equivalente no vector store.

---

# 76. Prompt Injection

Documento pode conter:

```text
"Ignore todas as instruções anteriores..."
```

Conteúdo recuperado deve ser tratado como dados não confiáveis.

---

# 77. Tool Injection

Um documento não deve conseguir autorizar ferramentas.

```text
Retrieved Content
 ≠
Permission
```

---

# 78. Data Leakage

Evitar:

```text
Tenant A
 ↓
Retriever
 ↓
Tenant B Document
```

Testar isolamento explicitamente.

---

# 79. Secrets

Não indexar:

```text
passwords
API keys
private keys
tokens
connection strings
```

---

# 80. PII

Definir política para:

```text
ingestion
masking
storage
retrieval
logging
retention
```

---

# 81. Observabilidade

Pipeline:

```text
Query
 ↓
Trace
 ├── Rewrite
 ├── Embedding
 ├── Retrieval
 ├── Reranking
 ├── LLM
 └── Response
```

---

# 82. Métricas

Registrar:

```text
retrieval latency
LLM latency
total latency
tokens
cache hit
documents retrieved
rerank latency
errors
```

---

# 83. OpenTelemetry

Instrumentar:

```text
HTTP
Database
Redis
Vector DB
Messaging
LLM Calls
Tools
```

---

# 84. Correlation ID

```text
Request
 ↓
CorrelationId
 ↓
Retriever
 ↓
LLM
 ↓
Tools
 ↓
Logs
```

---

# 85. Evaluation

RAG precisa ser avaliado.

Separar:

```text
Retrieval Evaluation
Generation Evaluation
End-to-End Evaluation
```

---

# 86. Retrieval Metrics

Exemplos:

```text
Precision@K
Recall@K
MRR
Hit Rate
```

---

# 87. Generation Metrics

Avaliar:

```text
correctness
relevance
groundedness
citation correctness
completeness
```

---

# 88. Golden Dataset

Criar:

```text
Question
Expected Sources
Expected Facts
```

Isso permite regressão automatizada.

---

# 89. RAG Regression Tests

```text
Change Chunking
 ↓
Run Evaluation
 ↓
Compare Metrics
 ↓
Accept / Reject
```

---

# 90. Hallucination Control

Estratégias:

```text
strong grounding
source citations
confidence threshold
answer refusal
retrieval validation
human review
```

---

# 91. No Evidence

Comportamento recomendado:

```text
No Relevant Evidence
 ↓
"I don't have enough information"
```

em vez de inventar.

---

# 92. Retrieval Threshold

```text
Similarity < threshold
 ↓
Do not use result
```

Threshold deve ser calibrado com dados reais.

---

# 93. Reranker Evaluation

Comparar:

```text
Retriever only
vs
Retriever + Reranker
```

Medir qualidade e latência.

---

# 94. Chunk Evaluation

Testar diferentes:

```text
chunk size
overlap
semantic boundaries
metadata
```

Não existe tamanho universal.

---

# 95. Embedding Evaluation

Modelos diferentes podem funcionar melhor em:

```text
Portuguese
code
legal documents
multilingual
short text
long text
```

Avaliar com dataset do domínio.

---

# 96. Cost

Custos possíveis:

```text
embedding
vector storage
LLM tokens
reranking
compute
network
observability
```

---

# 97. Token Optimization

```text
retrieve less
rerank
compress
deduplicate
summarize
cache
```

---

# 98. Context Compression

```text
Large Retrieved Context
 ↓
Compression
 ↓
Relevant Evidence
 ↓
LLM
```

---

# 99. Deduplication

Evitar enviar o mesmo conteúdo várias vezes.

```text
Chunks
 ↓
Hash / Similarity
 ↓
Unique Context
```

---

# 100. Incremental Indexing

Não reprocessar tudo.

```text
Document
 ↓
Hash
 ↓
Changed?
 ├── No → Skip
 └── Yes → Reindex
```

---

# 101. Delete Handling

Quando documento é removido:

```text
Delete Event
 ↓
Remove Chunks
 ↓
Remove Vectors
 ↓
Invalidate Cache
```

---

# 102. Versioning

Guardar:

```text
document version
embedding model
chunking strategy
index version
prompt version
LLM model
```

---

# 103. Reindexing

Mudança de embedding model pode exigir:

```text
New Index
 ↓
Re-embed
 ↓
Validation
 ↓
Switch Alias
```

---

# 104. Blue/Green Index

```text
Index V1 → production

Build Index V2
 ↓
Evaluate
 ↓
Switch
```

Permite rollback.

---

# 105. CI/CD para RAG

```text
Code Change
 ↓
Unit Tests
 ↓
Integration Tests
 ↓
Golden Dataset
 ↓
RAG Evaluation
 ↓
Quality Gate
 ↓
Deploy
```

---

# 106. Unit Tests

Testar:

```text
chunker
metadata
filters
context builder
prompt builder
permissions
```

---

# 107. Integration Tests

Testar:

```text
vector store
embedding provider
database
cache
queue
```

---

# 108. Fake LLM

Não usar modelo real em todos os testes.

```text
FakeLanguageModel
```

permite respostas previsíveis.

---

# 109. Fake Embeddings

Para testes determinísticos:

```text
FakeEmbeddingService
```

---

# 110. Docker

Ambiente:

```text
docker-compose
├── api
├── worker
├── mysql
├── mongodb
├── redis
├── qdrant
├── rabbitmq
├── kafka
├── ollama
└── observability
```

Nem todo projeto precisa de todos os componentes.

---

# 111. Health Checks

```text
LLM
Embedding Provider
Vector DB
Redis
Database
Broker
```

Separar dependências críticas das opcionais.

---

# 112. Failure Modes

Planejar:

```text
LLM unavailable
vector DB unavailable
embedding failure
broker unavailable
timeout
rate limit
corrupt document
```

---

# 113. Retry

Somente para falhas transitórias.

```text
Retry
+
Backoff
+
Jitter
```

---

# 114. DLQ

Documentos que falham repetidamente:

```text
Ingestion Queue
 ↓
Retries
 ↓
DLQ
```

Devem ser investigados.

---

# 115. Idempotência

```text
DocumentId
+
Version
```

pode compor chave de processamento.

Evitar embeddings duplicados.

---

# 116. Content Hash

```text
Content
 ↓
Hash
 ↓
Index Key
```

Útil para detectar alteração.

---

# 117. Architecture Diagram

```text
                         ┌───────────────────┐
                         │       USER        │
                         └─────────┬─────────┘
                                   │
                                   ▼
                         ┌───────────────────┐
                         │   ASP.NET API     │
                         └─────────┬─────────┘
                                   │
                                   ▼
                         ┌───────────────────┐
                         │ RAG ORCHESTRATOR  │
                         └─────────┬─────────┘
                                   │
                 ┌─────────────────┼─────────────────┐
                 ▼                 ▼                 ▼
             MEMORY            RETRIEVER           TOOLS
                                   │
                         ┌─────────┼─────────┐
                         ▼         ▼         ▼
                      VECTOR      SQL      GRAPH/API
                         │
                         ▼
                     RERANKER
                         │
                         ▼
                   CONTEXT BUILDER
                         │
                         ▼
                         LLM
                         │
                         ▼
                  GROUNDED ANSWER
```

---

# 118. Ingestion Diagram

```text
SOURCE
 ↓
LOADER
 ↓
PARSER
 ↓
CLEANER
 ↓
CHUNKER
 ↓
METADATA
 ↓
EMBEDDING
 ↓
VECTOR STORE
```

---

# 119. Agentic RAG Diagram

```text
User
 ↓
Planner
 ↓
Agent
 ├── Vector Search
 ├── SQL
 ├── Files
 ├── GitHub
 ├── MCP
 └── Web/API
 ↓
Aggregator
 ↓
LLM
 ↓
Answer
```

---

# 120. Multi-Agent RAG Diagram

```text
                  ORCHESTRATOR
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
    CODE AGENT      DOC AGENT      DATA AGENT
        │              │              │
      Git            Vector          SQL
        │              │              │
        └──────────────┼──────────────┘
                       ▼
                   AGGREGATOR
                       ↓
                      LLM
                       ↓
                    ANSWER
```

---

# 121. Kit IA Dev

Estrutura:

```text
Kit-IA-Dev/
├── 2-Agents/
│   ├── rag-orchestrator/
│   ├── retrieval-agent/
│   └── evaluator-agent/
├── 3-Skills/
│   ├── rag/
│   ├── embeddings/
│   ├── vector-search/
│   └── rag-evaluation/
├── 4-Templates/
│   └── dotnet-rag/
├── 5-Workflows/
│   ├── ingestion/
│   └── rag-query/
├── 6-Quality-Gates/
│   └── rag/
└── 8-Dictionary/
    └── 15-rag-system.md
```

---

# 122. RAG Skill

Responsabilidades:

```text
analyze sources
select chunking
configure embeddings
configure vector store
implement retrieval
implement reranking
build context
generate grounded answer
return sources
```

---

# 123. RAG Evaluation Skill

```text
create dataset
run retrieval tests
run generation tests
compare versions
generate report
```

---

# 124. Quality Gates

- [ ] fontes identificadas;
- [ ] chunking definido;
- [ ] metadata definida;
- [ ] embeddings versionados;
- [ ] retrieval testado;
- [ ] filtros de autorização;
- [ ] reranking avaliado;
- [ ] citações preservadas;
- [ ] token budget;
- [ ] prompt injection tratado;
- [ ] tenant isolation;
- [ ] observabilidade;
- [ ] golden dataset;
- [ ] regression tests;
- [ ] no-evidence behavior;
- [ ] cache strategy;
- [ ] ingestion idempotente.

---

# 125. Anti-patterns

Evitar:

```text
vector DB para toda consulta
chunking arbitrário
Top-K enorme
contexto gigante
sem metadata
sem autorização
sem fontes
LLM inventando quando retrieval falha
reindex completo desnecessário
prompt injection ignorado
RAG sem avaliação
```

---

# 126. Evolução recomendada

```text
Classic RAG
 ↓
Metadata Filtering
 ↓
Hybrid Search
 ↓
Reranking
 ↓
Evaluation
 ↓
Graph RAG
 ↓
Agentic RAG
 ↓
Multi-Agent RAG
```

Não começar pela arquitetura mais complexa sem necessidade.

---

# 127. Regra para agentes

Antes de criar um RAG:

1. Qual problema será resolvido?
2. Quais são as fontes?
3. Os dados podem ser indexados?
4. Quem pode acessar cada documento?
5. Qual estratégia de chunking?
6. Qual embedding model?
7. Qual vector store?
8. Precisa de hybrid search?
9. Precisa de reranking?
10. Qual token budget?
11. Como fontes serão citadas?
12. Como tratar ausência de evidência?
13. Como medir qualidade?
14. Como atualizar/remover documentos?
15. Precisa realmente de Agentic RAG?

---

# 128. Relação com outros itens

```text
02 - RAG
02.1 - RAG
02.2 - RAG .NET
05 - Conectores e Funções
08 - FreeLLMAPI / Token
10 - LLM Local
14 - LLM vs Jev
17 - Agentic AI
18 - Kit IA Dev
```

---

# 129. Resumo

Um RAG System profissional não é apenas:

```text
PDF
 ↓
Vector DB
 ↓
LLM
```

É:

```text
DATA GOVERNANCE
+
INGESTION
+
CHUNKING
+
METADATA
+
EMBEDDINGS
+
RETRIEVAL
+
RERANKING
+
CONTEXT MANAGEMENT
+
LLM
+
SECURITY
+
SOURCES
+
OBSERVABILITY
+
EVALUATION
```

A evolução para Graph RAG, Agentic RAG e Multi-Agent RAG deve ocorrer somente quando a complexidade do problema justificar.

---

# 📁 Arquivo

```text
15-rag-system.md
```
