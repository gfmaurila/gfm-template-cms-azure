# 📘 Dicionário Técnico — 14 LLM vs Jev

> **Categoria:** Inteligência Artificial / LLM / Motores de Decisão  
> **Código:** 14  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** .NET / Agentic AI / RAG / Decision Engines / Structured AI  
> **Objetivo:** Diferenciar modelos generativos baseados em linguagem de mecanismos de decisão probabilística tipada e mostrar como as duas abordagens podem trabalhar juntas.

---

# 1. Ideia central

A comparação apresentada pode ser resumida assim:

```text
LLM
→ gera conteúdo

Jev
→ decide entre possibilidades estruturadas
```

A ideia mais importante não é substituir um pelo outro.

É utilizar cada mecanismo para o tipo de problema em que ele é mais adequado.

```text
LLM + Decision Engine
```

---

# 2. O que é um LLM

LLM significa:

```text
Large Language Model
```

É um modelo treinado para trabalhar com sequências de tokens.

Pode executar tarefas como:

```text
gerar texto
resumir
explicar
traduzir
gerar código
classificar
extrair informação
responder perguntas
```

---

# 3. Pipeline simplificado de um LLM

```text
Prompt
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embeddings
 ↓
Transformer
 ↓
Logits
 ↓
Probabilities
 ↓
Next Token
 ↓
Repeat
```

A saída é construída progressivamente.

---

# 4. Prompt

Exemplo:

```text
"Explique CQRS em uma aplicação .NET."
```

O texto ainda não entra diretamente no Transformer.

Primeiro ele passa pelo tokenizer.

---

# 5. Tokenização

```text
Text
 ↓
Tokenizer
 ↓
Tokens
```

Exemplo conceitual:

```text
"software architecture"

software
architecture
```

A divisão real depende do tokenizer do modelo.

---

# 6. Token IDs

Cada token é representado internamente por identificadores.

```text
Token
 ↓
Token ID
```

Exemplo meramente ilustrativo:

```text
software     → 4821
architecture → 9182
```

---

# 7. Embeddings

Os IDs são convertidos em representações vetoriais.

```text
Token ID
 ↓
Embedding
 ↓
Vector
```

Esses vetores carregam representações aprendidas pelo modelo.

---

# 8. Transformer

O Transformer processa a sequência considerando relações entre tokens.

Conceitualmente:

```text
Embeddings
 ↓
Attention
 ↓
Transformer Layers
 ↓
Representation
```

---

# 9. Logits

Na saída, o modelo produz valores associados aos possíveis próximos tokens.

```text
Transformer
 ↓
Logits
```

Esses valores são transformados em uma distribuição de probabilidade.

---

# 10. Probabilidades

Exemplo conceitual:

```text
"Redis é um..."

cache       0.31
banco       0.25
sistema     0.18
serviço     0.10
...
```

O exemplo é apenas ilustrativo.

---

# 11. Geração token a token

O modelo escolhe o próximo token conforme sua estratégia de geração.

```text
Token 1
 ↓
Token 2
 ↓
Token 3
 ↓
...
```

Por isso um LLM é fundamentalmente generativo.

---

# 12. Temperature

Temperature pode alterar a distribuição usada na geração.

Conceitualmente:

```text
Lower Temperature
→ comportamento mais concentrado

Higher Temperature
→ maior diversidade
```

O comportamento exato depende do modelo/provider.

---

# 13. Problema das strings

LLMs normalmente se comunicam através de texto.

Exemplo:

```text
"Sim, eu aprovaria essa operação."
```

Mas sistemas de software preferem estruturas.

```text
bool approved
```

ou:

```text
DecisionResult
```

---

# 14. Texto x Tipo

```text
LLM Output
→ string
```

Aplicação:

```text
bool
enum
decimal
object
```

Isso cria uma fronteira de integração.

---

# 15. Exemplo

LLM:

```text
"Acredito que o risco seja aproximadamente 82%."
```

Aplicação deseja:

```json
{
  "riskScore": 0.82
}
```

---

# 16. Structured Output

Uma solução comum é pedir saída estruturada.

```text
LLM
 ↓
JSON
 ↓
Schema Validation
 ↓
Typed Object
```

---

# 17. JSON não elimina o problema

Mesmo pedindo JSON:

```text
Model
 ↓
Generated Text
 ↓
Parse
 ↓
Validate
```

A aplicação ainda precisa tratar a saída como não confiável.

---

# 18. Schema

Exemplo:

```json
{
  "approved": true,
  "score": 0.82,
  "reason": "..."
}
```

O schema define o contrato esperado.

---

# 19. Validação

Pipeline correto:

```text
LLM Output
 ↓
Deserialize
 ↓
Schema Validation
 ↓
Business Validation
 ↓
Use
```

Nunca:

```text
LLM Output
 ↓
Trust Automatically
```

---

# 20. O que Jev representa nesta comparação

No material de referência, **Jev** foi apresentado como um mecanismo/modelo de **decisão probabilística tipada**, em contraste com a geração aberta de linguagem de um LLM.

A ideia arquitetural é:

```text
Structured State
 ↓
Decision Mechanism
 ↓
Typed Decision
```

O Kit IA Dev não deve ficar arquiteturalmente preso a uma implementação específica chamada Jev. O conceito reutilizável é uma **Typed Probabilistic Decision Layer**.

---

# 21. Decisão estruturada

Em vez de:

```text
"Eu escolheria a opção B."
```

ter:

```text
Choice<B>
```

ou uma estrutura equivalente.

---

# 22. Noul

No material, `Noul` representa uma decisão binária.

Conceitualmente:

```text
Noul
├── Yes
└── No
```

Pode carregar probabilidade/confiança.

Exemplo:

```text
FraudDetected?
```

Saída:

```text
Yes
Confidence: 0.91
```

---

# 23. Exemplo Noul

Pergunta:

```text
O usuário possui permissão suficiente?
```

Possível representação:

```json
{
  "decision": true,
  "confidence": 0.97
}
```

O importante é o tipo binário, não texto livre.

---

# 24. Choice

`Choice` representa seleção entre alternativas conhecidas.

```text
Choice
├── Option A
├── Option B
└── Option C
```

---

# 25. Exemplo Choice

Roteamento de atendimento:

```text
Billing
TechnicalSupport
Sales
Cancellation
```

Saída conceitual:

```text
Choice<TicketRoute>
```

---

# 26. Score

`Score` representa um valor contínuo.

Exemplos:

```text
0.00 → 1.00
```

ou outro intervalo definido pelo domínio.

---

# 27. Exemplo Score

```text
Risk Score
 ↓
0.87
```

Aplicações:

```text
fraud risk
priority
relevance
similarity
quality
confidence
```

---

# 28. Noul + Choice + Score

Os três tipos cobrem várias decisões.

```text
Noul
→ sim/não

Choice
→ qual alternativa?

Score
→ quanto?
```

---

# 29. Exemplo completo

Sistema de atendimento:

```text
Noul
→ precisa de atendimento humano?

Choice
→ qual departamento?

Score
→ qual prioridade?
```

---

# 30. Estado estruturado

Em vez de prompt livre:

```text
"Analise tudo e diga o que acha."
```

uma camada decisória pode receber:

```json
{
  "customerType": "Premium",
  "daysOverdue": 18,
  "amount": 1200,
  "previousIncidents": 2
}
```

---

# 31. Saída estruturada

```json
{
  "escalate": true,
  "route": "Collections",
  "priority": 0.84
}
```

Isso é mais simples de integrar com regras e workflows.

---

# 32. LLM para tarefas abertas

LLM é forte quando não existe uma pequena lista fixa de respostas.

Exemplos:

```text
escrever documentação
explicar arquitetura
resumir contrato
gerar código
responder pergunta
criar conteúdo
```

---

# 33. Decision Engine para tarefas fechadas

Mecanismo decisório é interessante quando a saída pertence a um espaço conhecido.

Exemplos:

```text
Approve / Reject
Low / Medium / High
Route A / B / C
Score 0..1
```

---

# 34. Comparação

| Aspecto | LLM | Decisão tipada |
|---|---|---|
| Entrada | texto/contexto | estado estruturado |
| Saída | geralmente generativa | tipos conhecidos |
| Melhor para | tarefas abertas | decisões fechadas |
| Integração | exige parsing/validação | contrato explícito |
| Criatividade | alta | não é o objetivo |
| Controle de saída | variável | elevado |
| Explicação textual | excelente | pode precisar de LLM |

---

# 35. Exemplo — classificação

LLM:

```text
"Esse ticket parece ser um problema de cobrança."
```

Decisão tipada:

```text
Choice<TicketCategory>
=
Billing
```

---

# 36. Exemplo — aprovação

LLM:

```text
"Com base nos dados apresentados, eu aprovaria."
```

Decisão:

```text
Noul
=
Yes
```

---

# 37. Exemplo — score

LLM:

```text
"O risco parece alto."
```

Decisão:

```text
Score
=
0.91
```

---

# 38. LLM + Jev

A arquitetura combinada é mais interessante.

```text
Structured Data
      ↓
Decision Layer
      ↓
Typed Decision
      ↓
LLM
      ↓
Human-Friendly Explanation
```

---

# 39. Outra combinação

```text
User Text
 ↓
LLM
 ↓
Structured Extraction
 ↓
Decision Engine
 ↓
Decision
```

O LLM interpreta linguagem; o motor toma decisão sobre dados estruturados.

---

# 40. Exemplo antifraude

```text
Transaction
 ↓
Features
 ↓
Decision Engine
 ↓
Risk Score
 ↓
Policy
```

Se necessário:

```text
Risk Result
 ↓
LLM
 ↓
Analyst Explanation
```

---

# 41. Exemplo suporte

```text
Customer Message
 ↓
LLM
 ↓
Extract Intent
 ↓
Choice<Route>
 ↓
Queue
```

---

# 42. Exemplo documentos

```text
Document
 ↓
LLM
 ↓
Structured Extraction
 ↓
Decision Rules
 ↓
Approval / Review
```

---

# 43. Exemplo RAG

```text
Question
 ↓
RAG
 ↓
Retrieved Evidence
 ↓
LLM
 ↓
Answer
```

Se houver decisão:

```text
Evidence
 ↓
Decision Layer
 ↓
Noul / Choice / Score
```

---

# 44. Agentic AI

```text
Agent
 ├── LLM
 ├── Decision Layer
 ├── Tools
 ├── Memory
 └── Policies
```

Cada componente possui responsabilidade diferente.

---

# 45. Planning

LLM pode gerar plano:

```text
Goal
 ↓
LLM Planner
 ↓
Steps
```

Uma camada decisória pode escolher:

```text
Which Tool?
Which Route?
Continue?
Stop?
```

---

# 46. Stop Decision

Exemplo:

```text
Noul<ContinueExecution>
```

Evita depender apenas de texto como:

```text
"acho que já terminei"
```

---

# 47. Tool Routing

```text
Available Tools
 ↓
Decision
 ↓
Choice<Tool>
```

Depois:

```text
Selected Tool
 ↓
Execution
```

---

# 48. Paralelismo

Decisões independentes podem ser avaliadas em paralelo.

Exemplo:

```text
State
 ├── Fraud Score
 ├── Priority Score
 ├── Route Choice
 └── Human Review?
```

Se forem independentes:

```text
Task.WhenAll(...)
```

pode ser utilizado na implementação .NET.

---

# 49. Arquitetura .NET

```text
AI/
├── Language/
│   ├── ILanguageModel.cs
│   └── Providers/
├── Decisioning/
│   ├── IDecisionEngine.cs
│   ├── Decisions/
│   ├── Models/
│   └── Policies/
├── RAG/
├── Agents/
└── Tools/
```

---

# 50. ILanguageModel

```csharp
public interface ILanguageModel
{
    Task<string> GenerateAsync(
        string prompt,
        CancellationToken cancellationToken);
}
```

---

# 51. IDecisionEngine

Exemplo conceitual:

```csharp
public interface IDecisionEngine<TState, TResult>
{
    Task<TResult> DecideAsync(
        TState state,
        CancellationToken cancellationToken);
}
```

---

# 52. Noul em C#

Uma representação possível:

```csharp
public sealed record BinaryDecision(
    bool Value,
    double Confidence);
```

O nome concreto não precisa ser `Noul`.

---

# 53. Choice em C#

```csharp
public sealed record ChoiceDecision<T>(
    T Value,
    double Confidence);
```

---

# 54. Score em C#

```csharp
public sealed record ScoreDecision(
    double Value);
```

---

# 55. Domain Types

É preferível usar tipos de domínio.

Exemplo:

```csharp
public enum TicketRoute
{
    Billing,
    TechnicalSupport,
    Sales
}
```

Saída:

```text
ChoiceDecision<TicketRoute>
```

---

# 56. Business Rules

A decisão do modelo não precisa ser a decisão final.

```text
AI Decision
 ↓
Business Policy
 ↓
Final Action
```

Exemplo:

```text
RiskScore > threshold
AND
Amount > limit
→ Human Review
```

---

# 57. Determinismo

Uma camada tipada melhora previsibilidade da interface, mas isso não significa automaticamente que o modelo subjacente seja matematicamente determinístico.

Separar:

```text
Typed Output
≠
Guaranteed Correctness
```

---

# 58. Confidence

Confidence também não deve ser tratada automaticamente como probabilidade calibrada.

É necessário avaliar/calibrar conforme a tecnologia utilizada.

---

# 59. Validation

Toda decisão precisa ser validada.

```text
Decision
 ↓
Schema Validation
 ↓
Range Validation
 ↓
Business Validation
```

---

# 60. Human in the Loop

Decisões críticas:

```text
AI
 ↓
Recommendation
 ↓
Human
 ↓
Final Decision
```

Exemplos:

```text
financial approval
legal decision
high-risk security action
production destructive operation
```

---

# 61. Audit

Registrar:

```text
DecisionId
Input Version
Model
Decision
Confidence
Timestamp
Policy Version
Final Action
```

Sem registrar dados sensíveis desnecessariamente.

---

# 62. Explainability

Uma estratégia:

```text
Typed Decision
 ↓
Evidence
 ↓
LLM
 ↓
Explanation
```

O LLM explica, mas não altera silenciosamente a decisão.

---

# 63. Separation of Concerns

```text
LLM
→ Language

Decision Engine
→ Decision

Policy
→ Business Rule

Tool
→ Action
```

Essa separação é poderosa para sistemas agentic.

---

# 64. Policy Engine

```text
Decision
 ↓
Policy Engine
 ↓
Allowed Action
```

Exemplo:

```text
Choice = DeleteFile
```

não significa:

```text
Delete Automatically
```

A policy pode exigir aprovação.

---

# 65. Security

Nunca permitir:

```text
Model Output
 ↓
Direct Destructive Action
```

Preferir:

```text
Model
 ↓
Typed Decision
 ↓
Policy
 ↓
Permission
 ↓
Approval
 ↓
Tool
```

---

# 66. Observabilidade

Registrar métricas:

```text
decision_count
decision_latency
choice_distribution
score_distribution
validation_failures
human_overrides
```

---

# 67. Evaluation

Criar dataset:

```text
Input
Expected Decision
Actual Decision
```

Métricas:

```text
accuracy
precision
recall
F1
calibration
false positives
false negatives
```

conforme o problema.

---

# 68. LLM Evaluation

Para tarefas generativas, métricas são diferentes:

```text
groundedness
relevance
correctness
format validity
human rating
```

Isso reforça que os dois tipos de sistema exigem avaliações distintas.

---

# 69. Escolha de tecnologia

Não escolher:

```text
LLM para tudo
```

nem:

```text
Decision Engine para tudo
```

Perguntar:

```text
A resposta é aberta?
ou
A resposta pertence a um conjunto conhecido?
```

---

# 70. Decision Matrix

```text
Open-ended generation
→ LLM

Summarization
→ LLM

Explanation
→ LLM

Binary decision
→ Typed Decision

Routing
→ Choice

Risk/Relevance
→ Score

Natural language extraction
→ LLM + validation

Critical action
→ Decision + Policy + Human Approval
```

---

# 71. Kit IA Dev

Estrutura recomendada:

```text
Kit-IA-Dev/
├── 3-Skills/
│   ├── llm-integration/
│   └── decision-engine/
├── 4-Templates/
│   └── ai-decision-layer/
├── 5-Workflows/
│   └── structured-decision/
├── 6-Quality-Gates/
│   └── ai-decision/
└── 8-Dictionary/
    └── 14-llm-vs-jev.md
```

---

# 72. Skill decision-engine

Responsabilidades:

```text
identify decision type
define state
define output type
define validation
define confidence handling
define policies
define audit
define evaluation
```

---

# 73. Workflow

```text
Requirement
 ↓
Open or Closed Task?
 ↓
┌─────────────────┬─────────────────┐
│ Open            │ Closed          │
│                 │                 │
│ LLM             │ Decision Engine │
└─────────────────┴─────────────────┘
         ↓
Combined when necessary
         ↓
Validation
         ↓
Policy
         ↓
Action
```

---

# 74. Quality Gates

- [ ] problema classificado como aberto/fechado;
- [ ] estado de entrada definido;
- [ ] tipo de saída definido;
- [ ] schema validado;
- [ ] ranges validados;
- [ ] confidence tratada corretamente;
- [ ] policy separada do modelo;
- [ ] ações críticas protegidas;
- [ ] auditoria configurada;
- [ ] testes/evaluation dataset;
- [ ] observabilidade;
- [ ] fallback definido quando necessário.

---

# 75. Anti-patterns

Evitar:

```text
LLM decidindo tudo em texto livre
parse de "sim"/"não" sem contrato
confidence tratada como verdade absoluta
ação destrutiva direta
modelo contendo regra de negócio crítica
ausência de auditoria
ausência de validação
arquitetura acoplada a uma tecnologia específica
```

---

# 76. Regra arquitetural do Kit

Não criar dependência central:

```text
Domain
 ↓
Jev
```

Preferir:

```text
Domain/Application
 ↓
IDecisionEngine
 ↓
Adapter
 ↓
Concrete Decision Technology
```

Assim, a implementação pode ser substituída.

---

# 77. Arquitetura final

```text
                    USER / SYSTEM
                          ↓
                  ORCHESTRATION
                          ↓
        ┌─────────────────┴──────────────────┐
        │                                    │
        ▼                                    ▼
   LANGUAGE LAYER                      DECISION LAYER
       LLM                            Typed Decisions
        │                             Noul/Choice/Score
        │                                    │
        └─────────────────┬──────────────────┘
                          ↓
                       POLICY
                          ↓
                      VALIDATION
                          ↓
                        TOOLS
                          ↓
                       ACTION
```

---

# 78. Princípio principal

```text
LLM gera.
O mecanismo de decisão decide.
A política autoriza.
A ferramenta executa.
```

Esse princípio mantém responsabilidades claras.

---

# 79. Relação com outros itens

```text
02 - RAG
05 - Conectores e Funções
08 - FreeLLMAPI / Token
10 - LLM Local
13 - Microsserviços
15 - RAG System
17 - Agentic AI
18 - Kit IA Dev
```

---

# 80. Resumo

O ponto principal da comparação LLM vs Jev é distinguir **geração aberta de linguagem** de **decisão probabilística estruturada**.

```text
LLM
→ Language / Generation

Typed Decision Layer
→ Noul / Choice / Score

Policy
→ Business Constraints

Tools
→ Execution
```

No Kit IA Dev, o conceito deve ser abstraído por interfaces próprias. Assim, a arquitetura aproveita decisões tipadas sem ficar dependente de uma tecnologia específica.

---

# 📁 Arquivo

```text
14-llm-vs-jev.md
```
