# 📘 Dicionário Técnico — 10 LLM Local

> **Categoria:** Inteligência Artificial / LLM / Infraestrutura Local  
> **Código:** 10  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** .NET / RAG / Agentic AI / Desenvolvimento Local / Docker / Ollama  
> **Objetivo:** Explicar como executar e integrar Large Language Models localmente, quais são os cenários de uso, arquitetura recomendada, limitações, segurança e como incorporar essa capacidade ao Kit IA Dev.

---

# 1. O que é um LLM Local

LLM Local é um modelo de linguagem executado na própria máquina, servidor privado ou infraestrutura controlada pela organização.

```text
Application
    ↓
Local LLM Server
    ↓
Model
    ↓
CPU / GPU
```

Diferentemente de uma API externa, prompts e respostas podem permanecer dentro da infraestrutura controlada.

---

# 2. Arquitetura básica

```text
User
 ↓
.NET Application
 ↓
LLM Abstraction
 ↓
Local Provider
 ↓
Local Model
```

Exemplo:

```text
ASP.NET Core
 ↓
ILanguageModel
 ↓
OllamaProvider
 ↓
Ollama
 ↓
Local Model
```

---

# 3. Por que utilizar LLM local

Principais motivos:

- privacidade;
- desenvolvimento offline;
- experimentação;
- redução de dependência externa;
- testes;
- prototipação;
- controle de infraestrutura;
- modelos especializados;
- ambientes corporativos restritos.

---

# 4. Local não significa gratuito

Mesmo sem cobrança por token de um provider externo, existem custos:

```text
Hardware
Electricity
GPU
RAM
Storage
Maintenance
Operations
```

O custo precisa ser comparado com APIs externas conforme volume e necessidade.

---

# 5. Ollama

Ollama é uma opção popular para executar modelos localmente.

Arquitetura:

```text
Application
 ↓
HTTP API
 ↓
Ollama
 ↓
Model
```

Pode ser utilizado por:

```text
CLI
.NET
Python
Node.js
Docker
RAG applications
Agents
```

---

# 6. Outras opções

Dependendo do cenário:

```text
Ollama
llama.cpp
LM Studio
vLLM
LocalAI
Text Generation Inference
```

Cada ferramenta possui objetivos e características diferentes.

---

# 7. Modelos

Exemplos de famílias que podem possuir variantes executáveis localmente:

```text
Llama
Mistral
Qwen
Gemma
Phi
DeepSeek
Code-oriented models
Embedding models
```

A disponibilidade, licença e requisitos devem ser verificados para cada modelo.

---

# 8. Tamanho do modelo

Modelos maiores normalmente exigem mais recursos.

Conceitualmente:

```text
Small Model
→ menos RAM
→ menor latência
→ menor capacidade

Large Model
→ mais RAM/GPU
→ maior custo computacional
→ potencialmente maior capacidade
```

Não existe regra de que o maior modelo seja sempre o melhor para toda tarefa.

---

# 9. Quantização

Quantização reduz a precisão numérica dos pesos para diminuir consumo de memória e recursos.

Exemplo conceitual:

```text
Original Model
 ↓
Quantization
 ↓
Smaller Representation
 ↓
Lower Memory Requirement
```

Existe trade-off entre:

```text
size
speed
memory
quality
```

---

# 10. CPU x GPU

## CPU

Pode executar modelos menores, mas geralmente com desempenho inferior.

## GPU

Pode acelerar significativamente inferência.

Fatores:

```text
VRAM
Model Size
Quantization
Context Length
Batch Size
Architecture
```

---

# 11. RAM e VRAM

A escolha do modelo deve considerar recursos reais.

```text
Model
 ↓
Quantization
 ↓
Memory Requirement
 ↓
Available Hardware
```

Evitar selecionar modelo apenas por benchmark.

---

# 12. Context Window

Modelos locais também possuem limites de contexto.

Contexto inclui:

```text
System Prompt
Conversation
RAG Documents
Tool Results
User Prompt
Output
```

Quanto maior o contexto, maior pode ser o consumo de memória e processamento.

---

# 13. Local LLM no desenvolvimento

Excelente para:

```text
Proof of Concept
Prompt Tests
RAG Tests
Agent Experiments
Offline Development
CI Tests controlados
```

---

# 14. Local LLM em produção

Pode ser utilizado, mas exige engenharia operacional.

Avaliar:

```text
Availability
Scaling
GPU Capacity
Load Balancing
Monitoring
Security
Model Updates
Latency
Backup Strategy
```

---

# 15. Arquitetura .NET

```text
backend/
└── src/
    └── AI/
        ├── Abstractions/
        ├── Providers/
        │   ├── Ollama/
        │   └── Cloud/
        ├── Embeddings/
        ├── RAG/
        ├── Agents/
        ├── Tools/
        └── Observability/
```

---

# 16. Abstração

```csharp
public interface ILanguageModel
{
    Task<string> GenerateAsync(
        string prompt,
        CancellationToken cancellationToken = default);
}
```

A aplicação depende da interface, não do Ollama diretamente.

---

# 17. Provider Local

```text
ILanguageModel
      ↓
OllamaLanguageModel
      ↓
HTTP Client
      ↓
Ollama
```

---

# 18. Provider Cloud

A mesma aplicação pode possuir:

```text
OpenAIProvider
AnthropicProvider
AzureOpenAIProvider
GoogleProvider
```

A camada de negócio não precisa saber qual provider está sendo utilizado.

---

# 19. Provider Factory

```text
Configuration
 ↓
Provider Factory
 ├── Local
 └── Cloud
```

Exemplo:

```text
AI_PROVIDER=ollama
```

ou:

```text
AI_PROVIDER=cloud
```

---

# 20. Estratégia Local First

Para o Kit IA Dev:

```text
LOCAL FIRST
    ↓
CONTAINER FIRST
    ↓
CLOUD READY
    ↓
CLOUD TARGET
```

Isso permite desenvolver sem depender desde o primeiro momento de serviços externos.

---

# 21. Docker

Arquitetura:

```text
Docker Compose
├── api
├── ollama
├── redis
├── vector-db
├── mysql
└── observability
```

---

# 22. Exemplo docker-compose conceitual

```yaml
services:

  api:
    build: ./backend

  ollama:
    image: ollama/ollama

  redis:
    image: redis

  vector-db:
    image: qdrant/qdrant
```

Versões e configurações devem ser fixadas conforme o projeto.

---

# 23. RAG Local

```text
Documents
 ↓
Chunking
 ↓
Embedding Model
 ↓
Vector DB
 ↓
Retriever
 ↓
Local LLM
 ↓
Answer
```

Isso permite construir um pipeline RAG totalmente local.

---

# 24. Embeddings locais

O pipeline pode utilizar modelo de embedding local.

```text
Document
 ↓
Local Embedding Model
 ↓
Vector
 ↓
Vector DB
```

Benefícios:

- dados permanecem locais;
- independência de API externa;
- previsibilidade operacional.

---

# 25. Vector Database

Possíveis opções:

```text
Qdrant
Milvus
Weaviate
pgvector
Redis Vector Search
```

A escolha depende da arquitetura.

---

# 26. RAG híbrido

Não é necessário manter tudo local.

Exemplo:

```text
Local Documents
 ↓
Local Embeddings
 ↓
Local Vector DB
 ↓
Cloud LLM
```

ou:

```text
Cloud Search
 ↓
Retrieved Context
 ↓
Local LLM
```

---

# 27. Agentic AI Local

```text
User
 ↓
Agent
 ├── Local LLM
 ├── Memory
 ├── Tools
 └── RAG
```

O modelo local pode atuar como cérebro de um agente, desde que tenha capacidade suficiente para planejamento e tool calling do workflow adotado.

---

# 28. Tool Calling

Nem todos os modelos possuem o mesmo desempenho em chamadas de ferramentas.

Avaliar:

```text
Structured Output
JSON Reliability
Tool Selection
Argument Generation
Instruction Following
```

Testes são obrigatórios.

---

# 29. Structured Output

Para integração com aplicações:

```text
LLM
 ↓
JSON
 ↓
Validation
 ↓
Application
```

Nunca confiar em JSON sem validação.

---

# 30. FluentValidation / Schema Validation

Em .NET:

```text
LLM Output
 ↓
Deserialize
 ↓
Validate
 ↓
Accept / Reject
```

O resultado do modelo é entrada não confiável.

---

# 31. Local Coding Assistant

Um LLM local pode apoiar:

```text
Code Explanation
Refactoring Suggestions
Test Generation
Documentation
Code Review
SQL Explanation
```

A qualidade varia conforme modelo e contexto.

---

# 32. Knowledge Assistant

```text
Project Docs
 ↓
RAG
 ↓
Local Model
 ↓
Project Assistant
```

Perguntas:

```text
"Como funciona autenticação?"
"Qual é a arquitetura?"
"Onde está implementado Redis?"
```

---

# 33. Document Assistant

```text
PDF / Markdown / Docs
 ↓
Ingestion
 ↓
Vector DB
 ↓
Local LLM
 ↓
Q&A
```

---

# 34. Uso corporativo

Cenários:

```text
Internal Documentation
Source Code
Policies
Contracts
Knowledge Base
Support
```

Privacidade local pode ser vantagem, mas ainda exige controles de segurança.

---

# 35. Segurança

Executar localmente não elimina riscos.

Avaliar:

```text
Authentication
Network Exposure
Model API
File Access
Tool Permissions
Prompt Injection
Secrets
Logs
```

---

# 36. Network Binding

Evitar expor o servidor local desnecessariamente.

```text
localhost
```

é diferente de:

```text
0.0.0.0
```

A exposição de rede deve ser deliberada e protegida.

---

# 37. Autenticação

Se o servidor de inferência for compartilhado:

```text
Client
 ↓
API Gateway
 ↓
Authentication
 ↓
Local LLM Server
```

Não assumir que o servidor do modelo fornece todos os controles necessários.

---

# 38. API Gateway

Arquitetura corporativa:

```text
Applications
 ↓
Internal AI Gateway
 ↓
Authentication
 ↓
Rate Limit
 ↓
Model Router
 ↓
Local LLM Cluster
```

---

# 39. Model Router

```text
Task
 ↓
Router
 ├── Small Local Model
 ├── Large Local Model
 └── Cloud Model
```

A escolha pode considerar:

```text
Privacy
Complexity
Latency
Cost
Availability
```

---

# 40. Hybrid Model Strategy

Estratégia recomendada:

```text
Sensitive / Simple
→ Local

Complex / Non-sensitive
→ Cloud

Offline
→ Local

Fallback
→ Alternate Provider
```

As regras devem ser explícitas.

---

# 41. Observabilidade

Registrar:

```text
model
latency
tokens
memory
GPU utilization
errors
requests
queue time
```

Ferramentas possíveis:

```text
OpenTelemetry
Prometheus
Grafana
Structured Logging
```

---

# 42. Health Checks

```text
/health
/ready
/live
```

Separar:

```text
Liveness
Readiness
Dependency Health
```

---

# 43. Métricas de qualidade

Não medir apenas velocidade.

Avaliar:

```text
Accuracy
Groundedness
Tool Calling Success
JSON Validity
Hallucination Rate
Latency
Resource Usage
```

---

# 44. Benchmark interno

Criar dataset de perguntas reais.

```text
evaluation/
├── questions.json
├── expected-results.json
└── reports/
```

Comparar modelos usando os mesmos cenários.

---

# 45. Model Evaluation

```text
Model A
Model B
Model C
   ↓
Same Dataset
   ↓
Evaluation
   ↓
Decision
```

---

# 46. Testes automatizados

Aplicações não devem depender do LLM real em todos os testes.

```text
Unit Tests
→ Fake Model

Integration Tests
→ Local Model opcional

Evaluation Tests
→ Real Models
```

---

# 47. Fake Provider

```csharp
public sealed class FakeLanguageModel : ILanguageModel
{
    public Task<string> GenerateAsync(
        string prompt,
        CancellationToken cancellationToken = default)
        => Task.FromResult("Fake response");
}
```

---

# 48. CI/CD

Rodar um modelo grande em toda pipeline pode ser caro e lento.

Estratégia:

```text
CI
├── Unit Tests → Fake
├── Integration → Fake/Stub
└── AI Evaluation → pipeline específica
```

---

# 49. Model Versioning

Registrar:

```text
model name
model version
quantization
configuration
prompt version
embedding model
```

Sem isso, resultados ficam difíceis de reproduzir.

---

# 50. Prompt Versioning

```text
prompts/
├── v1/
├── v2/
└── current/
```

ou utilizar Git normalmente.

Mudanças de prompt podem alterar comportamento tanto quanto mudanças de código.

---

# 51. Model Configuration

Parâmetros possíveis:

```text
temperature
top_p
max_tokens
context
seed
stop
```

A disponibilidade depende do runtime/modelo.

---

# 52. Determinismo

Para testes:

```text
lower temperature
fixed dataset
controlled prompt
fixed model version
```

Mesmo assim, não assumir determinismo absoluto sem verificar o runtime.

---

# 53. Cache

```text
Prompt
 ↓
Cache
 ├── Hit → Response
 └── Miss → Local LLM
```

Pode reduzir processamento repetitivo.

---

# 54. Semantic Cache

```text
Query
 ↓
Embedding
 ↓
Similar Query?
 ├── Yes → Cached Answer
 └── No → LLM
```

Útil em sistemas de perguntas frequentes.

---

# 55. Queue

Inferência pode ser limitada pelo hardware.

```text
Requests
 ↓
Queue
 ↓
Worker
 ↓
GPU
```

Isso evita sobrecarga.

---

# 56. Mensageria

Para tarefas assíncronas:

```text
API
 ↓
RabbitMQ / SQS
 ↓
AI Worker
 ↓
Local Model
 ↓
Result
```

Exemplo:

```text
document summarization
batch embeddings
classification
content processing
```

---

# 57. Escalabilidade

```text
Load Balancer
     ↓
Inference Nodes
├── GPU Node 1
├── GPU Node 2
└── GPU Node 3
```

Produção local/on-premises exige capacidade operacional.

---

# 58. Persistência

Separar:

```text
Model Files
Vector Data
Conversation Data
Application Data
Logs
```

Cada tipo possui requisitos diferentes.

---

# 59. Privacidade

Definir explicitamente:

```text
What data enters the model?
What is logged?
Where is it stored?
Who can access it?
How long is it retained?
```

---

# 60. Prompt Injection em RAG

Mesmo localmente:

```text
Malicious Document
 ↓
Retriever
 ↓
Context
 ↓
Model
```

Pode manipular comportamento.

Conteúdo recuperado deve ser tratado como dados não confiáveis.

---

# 61. Guardrails

Possíveis controles:

```text
Input Validation
Output Validation
Tool Permissions
Content Policies
Schema Validation
Human Approval
```

---

# 62. Local LLM + MCP

```text
Local LLM
 ↓
Agent
 ↓
MCP Client
 ↓
MCP Servers
 ↓
GitHub / DB / Files / Tools
```

O modelo local pode participar de ecossistemas de ferramentas desde que a camada de agente suporte o protocolo/workflow.

---

# 63. Local LLM + Kit IA Dev

Estrutura:

```text
Kit-IA-Dev/
├── 3-Skills/
│   └── local-llm/
├── 4-Templates/
│   └── local-ai/
├── 5-Workflows/
│   └── model-evaluation/
└── 8-Dictionary/
    └── 10-llm-local.md
```

---

# 64. Skill local-llm

Responsabilidades:

```text
detect hardware
select runtime
select model
configure provider
configure Docker
test inference
benchmark
configure observability
document limitations
```

---

# 65. Workflow de instalação

```text
Hardware Check
 ↓
Runtime Selection
 ↓
Model Selection
 ↓
Installation
 ↓
Inference Test
 ↓
.NET Integration
 ↓
Observability
 ↓
Evaluation
```

---

# 66. Workflow RAG local

```text
Documents
 ↓
Parser
 ↓
Chunker
 ↓
Local Embeddings
 ↓
Vector DB
 ↓
Retriever
 ↓
Local LLM
 ↓
Grounded Answer
```

---

# 67. Workflow Agentic local

```text
Goal
 ↓
Local LLM
 ↓
Plan
 ↓
Tool
 ↓
Observation
 ↓
Local LLM
 ↓
Final Result
```

Definir:

```text
MaxSteps
Timeout
Tool Permissions
Token Budget
```

---

# 68. Quality Gates

- [ ] runtime documentado;
- [ ] modelo documentado;
- [ ] licença verificada;
- [ ] requisitos de hardware conhecidos;
- [ ] API não exposta indevidamente;
- [ ] timeout configurado;
- [ ] logs configurados;
- [ ] dados sensíveis protegidos;
- [ ] benchmark executado;
- [ ] testes existentes;
- [ ] fallback definido quando necessário;
- [ ] versão do modelo registrada.

---

# 69. Anti-patterns

Evitar:

```text
baixar o maior modelo sem avaliar hardware
expor endpoint sem autenticação
usar LLM real em todos os unit tests
não versionar modelo
não medir qualidade
não monitorar memória/GPU
assumir que local = seguro
acoplar aplicação ao runtime
```

---

# 70. Quando usar

Bom candidato:

```text
privacy
offline development
RAG interno
experimentation
high repetitive volume
controlled infrastructure
```

---

# 71. Quando API Cloud pode ser melhor

Possíveis cenários:

```text
no suitable hardware
need high-end model
low operational maturity
variable workload
need managed scalability
```

A decisão deve considerar custo total e requisitos, não apenas preço por token.

---

# 72. Estratégia recomendada

Para templates reutilizáveis:

```text
Application
     ↓
AI Abstraction
     ↓
Model Router
     │
     ├── Local Provider
     └── Cloud Provider
```

Isso mantém flexibilidade.

---

# 73. Regra para agentes

Antes de escolher um modelo local:

1. Qual é a tarefa?
2. Quais dados serão processados?
3. Existe requisito de privacidade?
4. Qual hardware está disponível?
5. Qual tamanho de modelo é viável?
6. O modelo suporta o workflow necessário?
7. Precisa de tool calling?
8. Precisa de structured output?
9. Qual latência é aceitável?
10. Como será monitorado?
11. Como será atualizado?
12. Existe fallback?

---

# 74. Relação com outros itens

```text
02 - RAG
02.1 - RAG
02.2 - RAG .NET
05 - Conectores e Funções
08 - FreeLLMAPI / Token
14 - LLM
15 - RAG System
17 - Agentic AI
18 - Kit IA Dev
```

---

# 75. Resumo

LLM local não é simplesmente:

```text
baixar modelo
+
executar prompt
```

Uma arquitetura profissional considera:

```text
Runtime
+
Model Selection
+
Hardware
+
Abstraction
+
Security
+
RAG
+
Tools
+
Observability
+
Evaluation
+
Versioning
+
Fallback
```

No Kit IA Dev, a estratégia recomendada é permitir:

```text
LOCAL
  ↕
CLOUD
```

através de abstrações, para que aplicações .NET, agentes e pipelines RAG possam trocar de provider sem alterar o domínio da aplicação.

---

# 📁 Arquivo

```text
10-llm-local.md
```
