# 📘 Dicionário Técnico — 02 RAG

> **Categoria:** Inteligência Artificial / RAG  
> **Código:** 02  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** .NET / C# / LLM / RAG / Agentic AI  
> **Objetivo:** Padronizar a implementação de soluções de Retrieval-Augmented Generation no ecossistema do Kit IA Dev.

---

# 1. O que é RAG

**RAG — Retrieval-Augmented Generation** é uma arquitetura que combina um modelo de linguagem com fontes externas de conhecimento.

Em vez de depender somente do conhecimento interno do LLM, a aplicação pesquisa informações relevantes antes de gerar a resposta.

```text
Usuário
   ↓
Pergunta
   ↓
Retrieval
   ↓
Base de Conhecimento
   ↓
Contexto Recuperado
   ↓
LLM
   ↓
Resposta
```

O objetivo é produzir respostas baseadas em dados reais da aplicação.

---

# 2. Problema que o RAG resolve

Um LLM isolado possui limitações:

- não conhece necessariamente dados privados;
- pode possuir conhecimento desatualizado;
- não conhece documentos internos;
- pode gerar informações incorretas;
- não conhece regras específicas do projeto;
- não conhece documentação recém-criada.

O RAG adiciona uma camada de conhecimento externo.

```text
LLM
+
Documentos
+
Banco de Dados
+
Vector Database
+
APIs
+
Conhecimento Corporativo
```

---

# 3. Arquitetura Classic RAG

Fluxo tradicional:

```text
Query
   ↓
Embedding
   ↓
Vector Search
   ↓
Vector DB
   ↓
Retrieved Documents
   ↓
Query + Context + System Prompt
   ↓
LLM
   ↓
Output
```

Componentes principais:

```text
Document Loader
Chunking
Embedding Model
Vector Database
Retriever
Prompt Builder
LLM
Output Parser
```

---

# 4. Pipeline de Indexação

Antes das consultas, os documentos precisam ser processados.

```text
Documentos
    ↓
Loader
    ↓
Parser
    ↓
Cleaning
    ↓
Chunking
    ↓
Embeddings
    ↓
Vector Store
```

Fontes possíveis:

- PDF;
- Markdown;
- TXT;
- DOCX;
- páginas web;
- banco SQL;
- MongoDB;
- APIs;
- GitHub;
- documentação interna;
- arquivos de código.

---

# 5. Chunking

Chunking divide documentos grandes em partes menores.

```text
Documento
   ↓
Chunk 1
Chunk 2
Chunk 3
Chunk 4
```

Exemplo:

```text
Documento com 20.000 tokens
        ↓
Chunks de aproximadamente 500 tokens
        ↓
40 chunks
```

Estratégias:

- Fixed Size;
- Recursive;
- Semantic;
- Sentence-based;
- Paragraph-based;
- Markdown-aware;
- Code-aware.

A estratégia deve preservar contexto suficiente sem enviar informação desnecessária ao LLM.

---

# 6. Embeddings

Embedding transforma conteúdo em representação vetorial.

```text
"Como configurar Redis?"
        ↓
Embedding Model
        ↓
[0.128, -0.442, 0.731, ...]
```

Textos semanticamente semelhantes tendem a possuir vetores próximos.

Isso permite realizar busca semântica.

---

# 7. Vector Database

O Vector Database armazena embeddings e metadados.

Exemplos de tecnologias:

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

Estrutura conceitual:

```text
Vector
Content
DocumentId
ChunkId
Source
Metadata
Tags
CreatedAt
```

---

# 8. Retrieval

Retrieval é o processo de encontrar informações relevantes.

```text
Pergunta
   ↓
Embedding
   ↓
Similarity Search
   ↓
Top K resultados
```

Exemplo:

```text
Pergunta:
"Como funciona autenticação?"

Top K = 5

Resultado:
Chunk 12
Chunk 27
Chunk 44
Chunk 51
Chunk 62
```

---

# 9. Similaridade

Algoritmos comuns:

```text
Cosine Similarity
Dot Product
Euclidean Distance
```

O mecanismo compara o vetor da pergunta com os vetores armazenados.

---

# 10. Metadata Filtering

Além da similaridade, é possível filtrar documentos.

Exemplo:

```text
project = GFM.Template.CMS
documentType = architecture
environment = production
version = 2
```

Isso reduz resultados irrelevantes.

---

# 11. Hybrid Search

Hybrid Search combina:

```text
Semantic Search
+
Keyword Search
```

Exemplo:

```text
Vector Search
+
BM25
```

É útil quando nomes exatos, códigos, identificadores e termos técnicos precisam ser encontrados.

---

# 12. Reranking

O resultado inicial pode passar por uma segunda classificação.

```text
Query
   ↓
Retriever
   ↓
20 documentos
   ↓
Reranker
   ↓
5 melhores documentos
   ↓
LLM
```

Isso melhora a qualidade do contexto enviado ao modelo.

---

# 13. Prompt Augmentation

O contexto recuperado é inserido no prompt.

```text
System Prompt
+
User Question
+
Retrieved Context
=
Final Prompt
```

Exemplo conceitual:

```text
SYSTEM:
Responda utilizando somente as informações fornecidas.

CONTEXT:
[documentos recuperados]

QUESTION:
Como funciona o cache da aplicação?
```

---

# 14. Resposta com fontes

Uma implementação robusta deve manter referência da origem.

```text
Resposta
   ↓
Sources
   ├── ARCHITECTURE.md
   ├── REDIS.md
   └── PROJECT.md
```

Isso permite:

- auditoria;
- validação;
- transparência;
- rastreabilidade.

---

# 15. Graph RAG

Graph RAG adiciona relacionamentos explícitos entre informações.

```text
Documents
    ↓
Entities
    ↓
Relationships
    ↓
Knowledge Graph
```

Exemplo:

```text
User
 ├── belongsTo → Role
 ├── has → Permission
 └── creates → Document
```

A consulta pode navegar pelos relacionamentos antes de gerar uma resposta.

---

# 16. Quando usar Graph RAG

Graph RAG é útil quando existem relações complexas entre entidades.

Exemplos:

- sistemas jurídicos;
- fraude;
- compliance;
- PLD;
- conhecimento corporativo;
- dependências de software;
- arquitetura;
- relacionamentos empresariais.

---

# 17. Agentic RAG

Agentic RAG adiciona capacidade de decisão ao processo.

No RAG clássico:

```text
Pergunta
   ↓
Retrieve
   ↓
LLM
```

No Agentic RAG:

```text
Pergunta
   ↓
Agent
   ↓
Planejamento
   ↓
Escolha da ferramenta
   ↓
Busca
   ↓
Avaliação
   ↓
Nova busca se necessário
   ↓
Resposta
```

---

# 18. Componentes do Agentic RAG

```text
Agent
Memory
Planning
Tools
Retriever
Vector DB
APIs
Databases
LLM
```

O agente pode decidir qual fonte consultar.

---

# 19. Tools

Exemplos de ferramentas disponíveis para um agente:

```text
VectorSearchTool
SqlSearchTool
MongoSearchTool
WebSearchTool
GitHubTool
DocumentationTool
ApiTool
FileSearchTool
```

Fluxo:

```text
Agent
 ├── Vector DB
 ├── SQL
 ├── MongoDB
 ├── APIs
 ├── GitHub
 └── Files
```

---

# 20. Memory

Agentic RAG pode utilizar memória.

```text
Memory
├── Short-Term Memory
└── Long-Term Memory
```

Short-Term:

- contexto da conversa;
- passos atuais;
- resultados temporários.

Long-Term:

- conhecimento persistente;
- decisões;
- histórico;
- preferências;
- fatos relevantes.

---

# 21. Planning

O agente pode decompor perguntas complexas.

```text
Pergunta
   ↓
Planner
   ↓
Task 1
Task 2
Task 3
   ↓
Execution
```

Exemplo:

```text
"Analise a arquitetura e diga o que falta para AWS."

Planner:

1. Buscar arquitetura atual.
2. Buscar infraestrutura atual.
3. Buscar requisitos AWS.
4. Comparar estruturas.
5. Identificar gaps.
6. Gerar recomendação.
```

---

# 22. ReAct

Um padrão possível é ReAct:

```text
Reason
  ↓
Act
  ↓
Observe
  ↓
Reason
  ↓
Act
```

O agente raciocina, executa uma ferramenta, observa o resultado e decide o próximo passo.

---

# 23. Multi-Agent RAG

Problemas maiores podem ser divididos entre agentes especializados.

```text
User
  ↓
Orchestrator
  ↓
Aggregator Agent
  ├── Architecture Agent
  ├── Code Agent
  ├── Database Agent
  ├── Security Agent
  ├── Cloud Agent
  └── Documentation Agent
```

Cada agente pode utilizar seu próprio conjunto de ferramentas e fontes.

---

# 24. Aggregator Agent

O Aggregator recebe os resultados dos agentes especializados.

```text
Architecture Agent ─┐
Security Agent ─────┤
Database Agent ─────┼──→ Aggregator → Final Answer
Cloud Agent ────────┤
Code Agent ─────────┘
```

Sua responsabilidade é consolidar resultados, remover duplicações, resolver conflitos e produzir a resposta final.

---

# 25. MCP e RAG

MCP Servers podem fornecer ferramentas e fontes externas aos agentes.

```text
Agent
  ↓
MCP
  ├── GitHub
  ├── Database
  ├── Files
  ├── APIs
  ├── Cloud
  └── External Systems
```

Isso permite desacoplar integrações da lógica principal do agente.

---

# 26. Arquitetura .NET

A estrutura Python comum em projetos Generative AI deve ser reinterpretada para C#/.NET.

Não deve ser simplesmente copiada.

Estrutura sugerida:

```text
src/
├── Api/
├── Application/
├── Domain/
├── Infrastructure/
├── AI/
└── CrossCutting/
```

---

# 27. Camada AI

```text
AI/
├── Abstractions/
├── Providers/
├── Embeddings/
├── Retrieval/
├── RAG/
├── Agents/
├── Memory/
├── Tools/
├── Prompts/
├── Pipelines/
└── Orchestration/
```

---

# 28. Abstrações

Interfaces evitam dependência direta de um provedor.

```csharp
public interface ILanguageModel
{
    Task<string> GenerateAsync(
        string prompt,
        CancellationToken cancellationToken);
}
```

Embedding:

```csharp
public interface IEmbeddingService
{
    Task<float[]> GenerateAsync(
        string text,
        CancellationToken cancellationToken);
}
```

Retriever:

```csharp
public interface IRetriever
{
    Task<IReadOnlyCollection<RetrievedDocument>> SearchAsync(
        string query,
        CancellationToken cancellationToken);
}
```

---

# 29. Providers

Implementações podem ser substituídas.

```text
ILanguageModel
├── OpenAIProvider
├── AzureOpenAIProvider
├── AnthropicProvider
├── OllamaProvider
└── LocalModelProvider
```

A aplicação depende da abstração e não diretamente do SDK do fornecedor.

---

# 30. Factory e Dependency Injection

A seleção de modelos deve utilizar configuração e DI.

```text
Application
    ↓
ILanguageModel
    ↓
Dependency Injection
    ↓
Provider
```

Isso facilita testes e troca de modelos.

---

# 31. Pipeline RAG em .NET

```text
API
 ↓
Application
 ↓
RAG Orchestrator
 ↓
Query Processor
 ↓
Embedding Service
 ↓
Retriever
 ↓
Vector Store
 ↓
Context Builder
 ↓
Prompt Builder
 ↓
LLM
 ↓
Response
```

---

# 32. Estrutura de Pastas RAG

```text
AI/
└── RAG/
    ├── Abstractions/
    ├── Chunking/
    ├── Embeddings/
    ├── Indexing/
    ├── Retrieval/
    ├── Reranking/
    ├── Context/
    ├── Generation/
    └── Pipelines/
```

---

# 33. Pipeline de Ingestão

```text
Upload
  ↓
Document Loader
  ↓
Parser
  ↓
Normalizer
  ↓
Chunker
  ↓
Embedding
  ↓
Vector Store
```

Exemplo de arquivos:

```text
DocumentIngestionService.cs
DocumentParser.cs
TextNormalizer.cs
SemanticChunker.cs
EmbeddingService.cs
VectorStore.cs
```

---

# 34. Cache

Resultados podem utilizar cache.

```text
Query
 ↓
Redis
 ↓
Cache Hit?
 ├── Sim → Response
 └── Não
      ↓
      RAG Pipeline
      ↓
      Cache
```

Cuidados:

- TTL;
- invalidação;
- versão do documento;
- hash da pergunta;
- contexto do usuário.

---

# 35. Segurança

RAG não deve ignorar autorização.

```text
User
 ↓
Authentication
 ↓
Authorization
 ↓
Retriever
 ↓
Allowed Documents Only
```

Um usuário não deve recuperar chunks de documentos aos quais não possui acesso.

Metadados podem conter:

```text
TenantId
UserId
Role
Permission
DocumentClassification
```

---

# 36. Multi-Tenant RAG

Em SaaS:

```text
Tenant A → Knowledge Base A
Tenant B → Knowledge Base B
Tenant C → Knowledge Base C
```

Nunca permitir retrieval cruzado entre tenants.

---

# 37. Observabilidade

Registrar:

```text
Query
Retrieval Time
Documents Retrieved
Similarity Score
Reranking Time
LLM Provider
Model
Token Usage
Latency
Errors
Cost
```

OpenTelemetry pode acompanhar todo o pipeline.

---

# 38. Avaliação

Um sistema RAG precisa ser avaliado.

Métricas possíveis:

```text
Retrieval Precision
Retrieval Recall
Context Relevance
Answer Relevance
Faithfulness
Latency
Token Usage
Cost
```

---

# 39. Anti-Hallucination

Estratégias:

- exigir contexto;
- retornar "não encontrado" quando necessário;
- citar fontes;
- limitar escopo;
- usar score mínimo;
- reranking;
- validar resposta;
- utilizar guardrails.

Fluxo:

```text
Retrieved Context
      ↓
Enough Evidence?
 ├── Não → Informar ausência de dados
 └── Sim → Gerar resposta
```

---

# 40. RAG + Banco Relacional

Nem toda informação deve ir para Vector DB.

Exemplo:

```text
"Qual é o saldo do cliente?"
```

Melhor fonte:

```text
SQL
```

Enquanto:

```text
"Explique a política de cancelamento."
```

pode utilizar:

```text
Vector DB
```

Agentic RAG pode decidir qual ferramenta utilizar.

---

# 41. RAG + MongoDB

MongoDB pode armazenar:

- documentos;
- histórico;
- projeções;
- conversas;
- resultados processados;
- metadados;
- conteúdo semiestruturado.

---

# 42. RAG + Redis

Redis pode ser utilizado para:

- cache;
- memória curta;
- session state;
- semantic cache;
- rate limiting;
- eventualmente busca vetorial.

---

# 43. RAG + Mensageria

Indexação pode ser assíncrona.

```text
Upload
 ↓
API
 ↓
Queue
 ↓
Document Processor
 ↓
Chunking
 ↓
Embedding
 ↓
Vector DB
```

Tecnologias:

```text
RabbitMQ
Kafka
AWS SQS
Azure Service Bus
```

---

# 44. RAG + Cloud

Exemplo AWS:

```text
S3
 ↓
SQS
 ↓
Worker / Lambda
 ↓
Document Processing
 ↓
Embedding
 ↓
Vector Store
```

Exemplo Azure:

```text
Blob Storage
 ↓
Service Bus
 ↓
Function
 ↓
Document Processing
 ↓
Azure AI Search
```

---

# 45. RAG Local

Para desenvolvimento local:

```text
.NET API
Ollama
Qdrant
Redis
MongoDB
Docker Compose
```

Permite testar boa parte da arquitetura sem depender da cloud.

---

# 46. Docker

Exemplo conceitual:

```text
docker-compose
├── api
├── ollama
├── qdrant
├── redis
├── mongodb
└── observability
```

Objetivo:

```text
docker compose up -d
```

e todo o ambiente de desenvolvimento RAG estar disponível.

---

# 47. Testes

Estrutura:

```text
tests/
├── Unit/
├── Integration/
├── RAG/
├── Agents/
└── Evaluation/
```

Testar:

- chunking;
- parsing;
- filtros;
- retrieval;
- autorização;
- ranking;
- fallback;
- providers;
- tools;
- pipelines.

---

# 48. Testes determinísticos

Não depender exclusivamente de um LLM real.

Criar mocks:

```text
FakeLanguageModel
FakeEmbeddingService
FakeRetriever
FakeVectorStore
```

Isso permite testes rápidos e previsíveis.

---

# 49. Quality Gates

```text
Build
 ↓
Unit Tests
 ↓
Integration Tests
 ↓
RAG Tests
 ↓
Security Tests
 ↓
Evaluation
 ↓
Observability Check
 ↓
Documentation
```

---

# 50. Estrutura no Kit IA Dev

```text
Kit-IA-Dev/
└── 8-Dictionary/
    └── 02-rag.md
```

O conteúdo pode ser utilizado por agentes especializados.

```text
agents/
├── rag-architect/
├── rag-developer/
├── ai-security/
└── ai-tester/
```

---

# 51. Skill RAG

Uma skill pode ser criada:

```text
skills/
└── rag/
    └── SKILL.md
```

Responsabilidades:

```text
analisar requisitos
definir estratégia RAG
definir chunking
definir embeddings
definir Vector DB
implementar retrieval
implementar reranking
configurar observabilidade
criar testes
avaliar qualidade
```

---

# 52. Evolução recomendada

Não começar diretamente com Multi-Agent RAG se o problema não exigir.

Evolução:

```text
Classic RAG
    ↓
Hybrid RAG
    ↓
Reranking
    ↓
Graph RAG
    ↓
Agentic RAG
    ↓
Multi-Agent RAG
```

A complexidade deve ser adicionada somente quando trouxer benefício mensurável.

---

# 53. Arquitetura Consolidada

```text
                         USER
                           │
                           ▼
                     ASP.NET API
                           │
                           ▼
                    AI ORCHESTRATOR
                           │
              ┌────────────┼─────────────┐
              ▼            ▼             ▼
           MEMORY       PLANNER        ROUTER
              │            │             │
              └────────────┼─────────────┘
                           ▼
                         AGENT
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
      RETRIEVER           TOOLS          MCP SERVERS
          │                │                │
          ▼                ▼                ▼
      VECTOR DB       SQL / Mongo       External APIs
          │
          ▼
      DOCUMENTS
          │
          ▼
       CONTEXT
          │
          ▼
          LLM
          │
          ▼
       RESPONSE
```

---

# 54. Checklist

## Dados

- [ ] Fontes identificadas
- [ ] Loader implementado
- [ ] Parser implementado
- [ ] Normalização definida
- [ ] Chunking definido
- [ ] Metadados definidos

## Embeddings

- [ ] Modelo escolhido
- [ ] Dimensão documentada
- [ ] Versionamento definido
- [ ] Reindexação prevista

## Retrieval

- [ ] Vector Search
- [ ] Metadata Filtering
- [ ] Top K definido
- [ ] Score mínimo
- [ ] Hybrid Search quando necessário
- [ ] Reranking quando necessário

## Segurança

- [ ] Autenticação
- [ ] Autorização
- [ ] Tenant isolation
- [ ] Filtros por permissão
- [ ] Dados sensíveis protegidos

## IA

- [ ] Abstração de LLM
- [ ] Provider desacoplado
- [ ] Prompt versionado
- [ ] Context Builder
- [ ] Guardrails
- [ ] Fallback

## Agentic

- [ ] Tools
- [ ] Memory
- [ ] Planner
- [ ] Router
- [ ] MCP quando necessário
- [ ] Multi-Agent somente quando justificado

## Qualidade

- [ ] Unit Tests
- [ ] Integration Tests
- [ ] RAG Evaluation
- [ ] Observabilidade
- [ ] Métricas
- [ ] Custos monitorados

---

# 55. Regra para Agentes de IA

Antes de implementar RAG, o agente deve responder:

1. Qual problema será resolvido?
2. Quais são as fontes?
3. Os dados são estruturados ou não estruturados?
4. É realmente necessário Vector DB?
5. Qual estratégia de chunking será utilizada?
6. Qual embedding será utilizado?
7. Como será feita autorização?
8. Existe multi-tenancy?
9. Como serão citadas as fontes?
10. Como será medida a qualidade?
11. Qual será o custo?
12. Classic RAG é suficiente?
13. Agentic RAG realmente é necessário?

Somente depois deve definir a arquitetura.

---

# 56. Resumo

RAG não é apenas:

```text
PDF → Vector DB → ChatGPT
```

Uma arquitetura de produção envolve:

```text
Ingestion
+
Parsing
+
Chunking
+
Embeddings
+
Vector Store
+
Retrieval
+
Filtering
+
Reranking
+
Prompt Engineering
+
LLM
+
Security
+
Observability
+
Evaluation
```

Quando necessário, pode evoluir para:

```text
RAG
  ↓
Graph RAG
  ↓
Agentic RAG
  ↓
Multi-Agent RAG
```

No Kit IA Dev, a implementação deve ser desacoplada, testável, observável, segura e preparada para diferentes providers e ambientes.
