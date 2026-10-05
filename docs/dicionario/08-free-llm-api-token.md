# 📘 Dicionário Técnico — 08 FreeLLMAPI / Token

> **Categoria:** Inteligência Artificial / LLM / APIs / Tokens  
> **Código:** 08  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** Claude Code / Codex / OpenCode / Aplicações .NET / Agentes / RAG  
> **Objetivo:** Explicar o conceito de serviços de acesso a LLMs via API, gerenciamento de tokens, chaves, limites, custos, providers e como abstrair essas integrações dentro do Kit IA Dev.

---

# 1. O que é uma LLM API

Uma LLM API permite que uma aplicação envie solicitações para um Large Language Model.

```text
Application
    ↓
LLM API
    ↓
Model
    ↓
Response
```

Exemplo:

```text
.NET API
 ↓
AI Provider
 ↓
LLM
 ↓
Generated Response
```

---

# 2. O que significa Free LLM API

O termo pode representar serviços que disponibilizam:

- camada gratuita;
- créditos gratuitos;
- modelos open source hospedados;
- endpoints compatíveis com APIs conhecidas;
- gateways para vários modelos;
- limites gratuitos de requisições.

"Free" não significa necessariamente uso ilimitado.

É necessário verificar:

```text
Rate Limit
Token Limit
Daily Limit
Monthly Limit
Available Models
Privacy
Terms of Use
```

---

# 3. O que é um Token

Tokens são unidades utilizadas pelos modelos para processar texto.

Uma frase é dividida em partes.

Exemplo conceitual:

```text
"Arquitetura de software"
        ↓
Tokenizer
        ↓
Token 1
Token 2
Token 3
...
```

Tokens não são equivalentes exatamente a palavras.

---

# 4. Input Tokens

São os tokens enviados ao modelo.

Incluem:

```text
System Prompt
User Prompt
Conversation History
Retrieved Context
Tool Results
Documents
```

Exemplo:

```text
System Prompt      500
User Prompt        100
RAG Context       3000
History           1500
----------------------
Input Tokens      5100
```

---

# 5. Output Tokens

São os tokens gerados pelo modelo.

```text
Input
 ↓
LLM
 ↓
Output Tokens
```

Quanto maior a resposta, maior o consumo de output.

---

# 6. Context Window

Context Window representa quanto conteúdo o modelo consegue considerar em uma solicitação.

```text
System Prompt
+
History
+
Documents
+
User Query
+
Tool Results
+
Expected Output
```

Tudo precisa caber dentro da janela suportada pelo modelo.

---

# 7. Por que tokens importam

Tokens afetam:

```text
Cost
Latency
Context Limit
Throughput
Rate Limits
```

Em aplicações RAG e Agentic AI, controlar tokens é essencial.

---

# 8. Token Budget

Uma aplicação pode definir orçamento.

Exemplo:

```text
Total Context Budget = 32K

System Prompt = 2K
History       = 4K
RAG Context   = 16K
Tools         = 4K
Output        = 6K
```

Isso evita crescimento descontrolado do contexto.

---

# 9. Tokenizer

Tokenizer é o componente que converte texto em tokens.

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Model
```

Cada família de modelos pode utilizar tokenização diferente.

---

# 10. API Key

Uma API Key autentica a aplicação junto ao provider.

Exemplo conceitual:

```text
Application
 ↓
API Key
 ↓
Provider
 ↓
Model
```

A chave deve ser tratada como secret.

---

# 11. Nunca armazenar API Key no código

Errado:

```csharp
var apiKey = "sk-xxxxxxxx";
```

Correto:

```text
Environment Variable
Secret Manager
User Secrets
AWS Secrets Manager
Azure Key Vault
```

---

# 12. Variáveis de ambiente

Exemplo:

```text
LLM_PROVIDER=openai
LLM_MODEL=model-name
LLM_API_KEY=secret
```

No repositório:

```text
.env.example
```

deve conter apenas placeholders.

---

# 13. Configuração .NET

Exemplo:

```json
{
  "AI": {
    "Provider": "OpenAI",
    "Model": "model-name",
    "BaseUrl": ""
  }
}
```

A API Key deve vir de secret/environment.

---

# 14. Abstração de Provider

A aplicação não deve depender diretamente de um único fornecedor.

```csharp
public interface ILanguageModel
{
    Task<string> GenerateAsync(
        string prompt,
        CancellationToken cancellationToken);
}
```

Implementações:

```text
OpenAIProvider
AnthropicProvider
AzureOpenAIProvider
GoogleProvider
OllamaProvider
CustomProvider
```

---

# 15. Arquitetura Multi-Provider

```text
Application
     ↓
ILanguageModel
     ↓
Provider Factory
     │
     ├── Provider A
     ├── Provider B
     ├── Provider C
     └── Local LLM
```

Isso reduz vendor lock-in.

---

# 16. Provider Factory

A seleção pode ocorrer por configuração.

```text
AI_PROVIDER=ollama
```

ou:

```text
AI_PROVIDER=cloud-provider
```

Fluxo:

```text
Configuration
 ↓
Provider Factory
 ↓
ILanguageModel
```

---

# 17. Base URL

Alguns serviços expõem endpoints compatíveis com APIs existentes.

Configuração:

```text
BaseUrl
ApiKey
Model
```

Isso permite trocar backend sem alterar toda a aplicação.

---

# 18. Gateway de LLM

Um gateway pode centralizar acesso a vários modelos.

```text
Application
    ↓
LLM Gateway
    │
    ├── Model A
    ├── Model B
    ├── Model C
    └── Local Model
```

Responsabilidades possíveis:

```text
Routing
Authentication
Rate Limiting
Logging
Cost Tracking
Fallback
```

---

# 19. Model Router

Um router pode escolher modelos conforme a tarefa.

```text
Simple Task
→ Fast/Cheap Model

Complex Reasoning
→ Stronger Model

Embeddings
→ Embedding Model

Local Sensitive Data
→ Local Model
```

---

# 20. Fallback

Caso um provider falhe:

```text
Primary Provider
 ↓
Failure
 ↓
Fallback Provider
 ↓
Response
```

Fallback precisa considerar compatibilidade, custo, privacidade e qualidade.

---

# 21. Rate Limit

Providers podem limitar:

```text
Requests per minute
Tokens per minute
Requests per day
Tokens per day
Concurrent requests
```

A aplicação deve tratar limites explicitamente.

---

# 22. Retry

Para erros transitórios:

```text
Request
 ↓
429 / Temporary Failure
 ↓
Backoff
 ↓
Retry
```

Utilizar:

```text
Exponential Backoff
Jitter
Maximum Retry Count
```

---

# 23. Timeout

Toda chamada remota deve possuir timeout.

```text
Application
 ↓
LLM Request
 ↓
Timeout
```

Nunca permitir espera infinita.

---

# 24. Circuit Breaker

Quando um provider está instável:

```text
Failures
 ↓
Circuit Open
 ↓
Stop Requests Temporarily
 ↓
Recovery Test
 ↓
Circuit Closed
```

---

# 25. Custos

Custo normalmente depende de fatores como:

```text
Input Tokens
Output Tokens
Model
Cached Tokens
Requests
Provider
```

Os valores variam entre providers e modelos.

Nunca fixar preços no código.

---

# 26. Cost Tracking

Registrar:

```text
RequestId
Model
Provider
InputTokens
OutputTokens
Latency
EstimatedCost
Timestamp
```

---

# 27. Observabilidade

Fluxo:

```text
Application
 ↓
LLM Client
 ↓
OpenTelemetry
 ↓
Logs
Metrics
Traces
```

Métricas úteis:

```text
request_count
latency
input_tokens
output_tokens
errors
rate_limits
provider
model
```

---

# 28. Correlation ID

Cada operação pode possuir um identificador.

```text
HTTP Request
 ↓
CorrelationId
 ↓
RAG
 ↓
LLM
 ↓
Tool
 ↓
Logs
```

Isso facilita rastrear uma execução completa.

---

# 29. Prompt Logging

Prompts podem conter dados sensíveis.

Não registrar indiscriminadamente:

```text
PII
Secrets
Private Documents
Credentials
Sensitive Business Data
```

Aplicar masking/redaction quando necessário.

---

# 30. Local LLM

Uma alternativa a APIs externas é executar modelos localmente.

Exemplo:

```text
Application
 ↓
Ollama
 ↓
Local Model
```

Benefícios possíveis:

- desenvolvimento local;
- privacidade;
- ausência de custo por token externo;
- funcionamento offline em alguns cenários.

Trade-offs:

- hardware;
- performance;
- manutenção;
- qualidade variável.

---

# 31. Arquitetura Local First

```text
.NET Application
      ↓
ILanguageModel
      ↓
OllamaProvider
      ↓
Local LLM
```

Depois:

```text
ILanguageModel
 ↓
Cloud Provider
```

sem alterar regras de negócio.

---

# 32. Docker

Ambiente local:

```text
docker-compose
├── api
├── ollama
├── qdrant
├── redis
└── observability
```

Isso é útil para RAG e testes locais.

---

# 33. LLM em RAG

```text
User
 ↓
Retriever
 ↓
Documents
 ↓
Context Builder
 ↓
LLM API
 ↓
Response
```

RAG pode consumir muitos tokens se o contexto não for controlado.

---

# 34. Redução de tokens no RAG

Estratégias:

```text
Chunking adequado
Top-K controlado
Metadata Filtering
Reranking
Context Compression
Deduplication
Summarization
```

---

# 35. Semantic Cache

Perguntas semanticamente semelhantes podem reutilizar respostas.

```text
Query
 ↓
Semantic Cache
 ├── Hit → Response
 └── Miss → LLM
```

Isso pode reduzir latência e custo.

---

# 36. Prompt Cache

Alguns providers podem oferecer mecanismos de cache de contexto/prompt.

A implementação deve ser abstraída, pois o comportamento varia por fornecedor.

---

# 37. Conversation History

Enviar todo o histórico indefinidamente é um anti-pattern.

```text
Conversation
 ↓
History Manager
 ↓
Relevant Messages
+
Summary
 ↓
LLM
```

---

# 38. Context Compression

```text
Large Context
 ↓
Compression
 ↓
Relevant Context
 ↓
LLM
```

Pode utilizar:

- summarization;
- extraction;
- ranking;
- deduplication.

---

# 39. Agentes e tokens

Agentic AI pode consumir mais tokens devido a múltiplos passos.

```text
Plan
 ↓
Tool
 ↓
Observation
 ↓
Reason
 ↓
Tool
 ↓
Observation
 ↓
Answer
```

Cada etapa possui custo computacional e potencial consumo de tokens.

---

# 40. Limite de passos

Um agente deve possuir limites.

Exemplo:

```text
MaxSteps
MaxToolCalls
MaxTokens
Timeout
```

Isso evita loops.

---

# 41. Budget por agente

Exemplo conceitual:

```text
Requirements Agent → Medium Budget
Architect Agent    → High Budget
Developer Agent    → High Budget
Reviewer Agent     → Medium Budget
Documentation      → Low/Medium Budget
```

O orçamento real depende da tarefa.

---

# 42. Model Selection

Não utilizar o modelo mais caro/forte para tudo.

```text
Classification
→ Small/Fast Model

Summarization
→ Efficient Model

Architecture
→ Strong Reasoning Model

Code Review
→ Strong Coding Model
```

---

# 43. Embeddings

Embeddings também podem ter custos e limites.

```text
Documents
 ↓
Embedding Model
 ↓
Vectors
 ↓
Vector DB
```

Evitar recalcular embeddings de documentos inalterados.

---

# 44. Hash de conteúdo

```text
Document
 ↓
Hash
 ↓
Changed?
 ├── No → Reuse Embedding
 └── Yes → Reindex
```

Isso reduz processamento.

---

# 45. Segurança

Riscos principais:

```text
API Key leakage
Prompt injection
Sensitive data exposure
Unauthorized tools
Provider logging
Data retention
```

Todos devem ser avaliados.

---

# 46. Prompt Injection

Conteúdo recuperado pode tentar manipular o agente.

```text
Document
 ↓
Malicious Instruction
 ↓
RAG Context
```

A aplicação deve tratar conteúdo recuperado como dados, não como instruções confiáveis.

---

# 47. Secrets

Nunca enviar secrets para o LLM sem necessidade.

Exemplos:

```text
API keys
passwords
private keys
connection strings
access tokens
```

---

# 48. Privacidade

Antes de utilizar um serviço gratuito ou externo, avaliar:

```text
Data Retention
Training Policy
Region
Compliance
Terms
Privacy Policy
```

Especialmente para dados corporativos.

---

# 49. Free Tier para desenvolvimento

Camadas gratuitas podem ser úteis para:

```text
POC
Study
Prototype
Local Development
Small Tests
```

Não assumir que são adequadas para produção.

---

# 50. Produção

Antes de produção, avaliar:

```text
SLA
Rate Limits
Support
Security
Compliance
Cost
Latency
Availability
Model Stability
Versioning
```

---

# 51. Testes

Não depender de API real em todos os testes.

Criar:

```text
FakeLanguageModel
MockLLMProvider
StubEmbeddingService
```

Exemplo:

```csharp
public sealed class FakeLanguageModel : ILanguageModel
{
    public Task<string> GenerateAsync(
        string prompt,
        CancellationToken cancellationToken)
        => Task.FromResult("Fake response");
}
```

---

# 52. Integration Tests

Testes reais podem ficar separados:

```text
Unit Tests
→ Fake Provider

Integration Tests
→ Test Provider

E2E
→ Controlled Real Provider
```

---

# 53. Configuration

Estrutura:

```text
AI/
├── Provider
├── Model
├── BaseUrl
├── Timeout
├── MaxRetries
├── MaxTokens
└── Temperature
```

Secrets permanecem fora do arquivo versionado.

---

# 54. Estrutura .NET

```text
AI/
├── Abstractions/
├── Providers/
├── Configuration/
├── Routing/
├── Resilience/
├── Observability/
├── Tokenization/
└── Cost/
```

---

# 55. Interfaces

Exemplos:

```text
ILanguageModel
IEmbeddingService
ITokenCounter
IModelRouter
ICostTracker
```

---

# 56. Resilience

```text
AI/
└── Resilience/
    ├── RetryPolicy.cs
    ├── TimeoutPolicy.cs
    └── CircuitBreakerPolicy.cs
```

---

# 57. Token Counter

Uma abstração pode estimar tokens antes do envio.

```text
Prompt
 ↓
Token Counter
 ↓
Within Budget?
 ├── Yes → Send
 └── No → Compress
```

---

# 58. LLM Gateway interno

Projetos maiores podem centralizar integrações.

```text
Applications
    ↓
Internal AI Gateway
    │
    ├── Authentication
    ├── Routing
    ├── Rate Limit
    ├── Cost
    ├── Logging
    └── Providers
```

---

# 59. Kit IA Dev

Estrutura possível:

```text
Kit-IA-Dev/
├── 3-Skills/
│   └── llm-integration/
├── 4-Templates/
│   └── ai-provider/
└── 8-Dictionary/
    └── 08-free-llm-api-token.md
```

---

# 60. Skill de integração LLM

```text
3-Skills/
└── llm-integration/
    └── SKILL.md
```

Responsabilidades:

```text
select provider
configure secrets
implement abstraction
configure resilience
track tokens
track cost
add observability
create tests
```

---

# 61. Workflow

```text
Requirement
 ↓
Select Model
 ↓
Select Provider
 ↓
Configure Abstraction
 ↓
Configure Secrets
 ↓
Configure Resilience
 ↓
Configure Observability
 ↓
Test
 ↓
Measure Cost
```

---

# 62. Quality Gates

- [ ] API Key fora do código;
- [ ] provider abstraído;
- [ ] timeout configurado;
- [ ] retry controlado;
- [ ] rate limit tratado;
- [ ] token usage monitorado;
- [ ] logs sem secrets;
- [ ] testes com fake provider;
- [ ] custos observáveis;
- [ ] fallback avaliado;
- [ ] política de privacidade avaliada.

---

# 63. Anti-patterns

Evitar:

```text
API key hardcoded
provider acoplado ao domínio
sem timeout
retry infinito
todo histórico enviado sempre
contexto RAG gigantesco
modelo mais caro para toda tarefa
logs contendo prompts sensíveis
free tier tratado como produção garantida
```

---

# 64. Regra para Agentes

Antes de integrar um LLM API:

1. Qual tarefa o modelo executará?
2. Precisa realmente de um modelo remoto?
3. Existe alternativa local?
4. Qual provider atende melhor?
5. Qual modelo é suficiente?
6. Qual o limite de contexto?
7. Qual orçamento de tokens?
8. Quais dados serão enviados?
9. Existem dados sensíveis?
10. Como secrets serão armazenados?
11. Como rate limit será tratado?
12. Como custo será medido?
13. Como a integração será testada?
14. Existe fallback?

---

# 65. Relação com outros itens

Complementa:

```text
02 - RAG
03 - Plugins
05 - Conectores e Funções
10 - LLM Local
14 - LLM
15 - RAG System
17 - Agentic AI
18 - Kit IA Dev
```

---

# 66. Resumo

Uma integração LLM robusta não deve ser:

```text
API Key
+
HTTP Request
+
Prompt
```

Ela deve considerar:

```text
Abstraction
+
Provider
+
Model Selection
+
Secrets
+
Token Budget
+
Rate Limits
+
Timeout
+
Retry
+
Fallback
+
Security
+
Observability
+
Cost Tracking
+
Tests
```

O objetivo do Kit IA Dev é permitir trocar providers e modelos sem reescrever a aplicação e controlar custo, segurança e consumo de tokens desde o início.

---

# 📁 Arquivo

```text
08-free-llm-api-token.md
```
