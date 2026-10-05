# 📘 Dicionário Técnico — 04 Frameworks de Análise e Gestão

> **Categoria:** Estratégia / Análise / Gestão / Tomada de Decisão  
> **Código:** 04  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** Agentes de IA, análise de projetos, arquitetura, produto, planejamento e decisão técnica  
> **Objetivo:** Padronizar frameworks que ajudam agentes e equipes a estruturar problemas, analisar cenários, priorizar ações e transformar análise em execução.

---

# 1. Por que usar Frameworks

Frameworks de análise evitam que uma IA ou equipe responda de forma improvisada.

Eles fornecem uma sequência lógica:

```text
Problema
   ↓
Coleta de informações
   ↓
Análise estruturada
   ↓
Hipóteses
   ↓
Decisão
   ↓
Plano de ação
   ↓
Medição
```

No Kit IA Dev, podem ser utilizados por agentes de Requirements, Architect, Tech Lead, Product, Reviewer e Documentation.

---

# 2. SWOT

SWOT organiza uma análise em quatro dimensões:

```text
Strengths  → Forças
Weaknesses → Fraquezas
Opportunities → Oportunidades
Threats → Ameaças
```

Matriz:

```text
┌─────────────────────┬─────────────────────┐
│ FORÇAS              │ FRAQUEZAS           │
│ fatores internos    │ fatores internos    │
├─────────────────────┼─────────────────────┤
│ OPORTUNIDADES       │ AMEAÇAS             │
│ fatores externos    │ fatores externos    │
└─────────────────────┴─────────────────────┘
```

## Exemplo técnico

Analisando adoção de microsserviços:

**Forças**
- escalabilidade independente;
- isolamento de domínios;
- deploy independente.

**Fraquezas**
- maior complexidade operacional;
- observabilidade distribuída;
- consistência eventual.

**Oportunidades**
- crescimento do produto;
- equipes independentes;
- adoção de cloud.

**Ameaças**
- custos;
- falta de maturidade DevOps;
- excesso de serviços.

## Uso no Kit

```text
Requirements Agent
      ↓
SWOT
      ↓
Architect Agent
      ↓
Architecture Decision
```

---

# 3. PESTEL

PESTEL analisa fatores externos.

```text
P → Political
E → Economic
S → Social
T → Technological
E → Environmental
L → Legal
```

Pode ser utilizado para análise de produto, empresa, mercado ou adoção tecnológica.

## Exemplo

Para uma aplicação SaaS:

```text
Political     → regulamentação governamental
Economic      → custos de cloud
Social        → comportamento dos usuários
Technological → IA, cloud, mobile
Environmental → consumo de infraestrutura
Legal         → LGPD, contratos, compliance
```

---

# 4. 5W2H

Framework para transformar uma decisão em plano de execução.

```text
What
Why
Where
When
Who
How
How Much
```

Em português:

```text
O quê?
Por quê?
Onde?
Quando?
Quem?
Como?
Quanto custa?
```

## Exemplo

```text
What:
Implementar Redis.

Why:
Reduzir carga no banco.

Where:
Queries de leitura.

When:
Sprint 4.

Who:
Backend Agent.

How:
Cache-aside.

How Much:
Infra + desenvolvimento.
```

## Uso com agentes

```text
Requirement
    ↓
5W2H
    ↓
Execution Plan
    ↓
Tasks
```

---

# 5. PDCA

PDCA é utilizado para melhoria contínua.

```text
PLAN
 ↓
DO
 ↓
CHECK
 ↓
ACT
 └────→ PLAN
```

### Plan

Definir:

- problema;
- objetivo;
- métricas;
- solução;
- tarefas.

### Do

Executar.

### Check

Validar resultados.

### Act

Corrigir ou padronizar.

## Exemplo no desenvolvimento

```text
PLAN
Criar cache Redis.

DO
Implementar cache-aside.

CHECK
Executar testes e medir latência.

ACT
Ajustar TTL e estratégia de invalidação.
```

---

# 6. Frameworks trabalhando juntos

Eles não precisam ser usados isoladamente.

Exemplo:

```text
PESTEL
   ↓
entender ambiente externo
   ↓
SWOT
   ↓
entender posição atual
   ↓
5W2H
   ↓
transformar decisão em execução
   ↓
PDCA
   ↓
medir e melhorar
```

---

# 7. Aplicação em arquitetura

Pergunta:

```text
"Devemos migrar para AWS?"
```

Processo:

```text
PESTEL
 ↓
analisar contexto externo

SWOT
 ↓
analisar situação atual

5W2H
 ↓
planejar migração

PDCA
 ↓
executar e melhorar
```

---

# 8. Aplicação em refatoração

```text
Sistema legado
    ↓
SWOT
    ↓
Identificação dos problemas
    ↓
5W2H
    ↓
Plano de refatoração
    ↓
PDCA
    ↓
Execução incremental
```

---

# 9. Aplicação em escolha tecnológica

Exemplo:

```text
Kafka vs RabbitMQ
```

A análise pode considerar:

```text
problema
volume
latência
retenção
event streaming
filas
complexidade operacional
custo
experiência da equipe
```

Depois:

```text
Decision
 ↓
ADR
 ↓
Implementation Plan
```

---

# 10. Aplicação em IA

Pergunta:

```text
"Devemos utilizar Agentic RAG?"
```

SWOT pode avaliar a tecnologia.

5W2H transforma a decisão em implementação.

PDCA permite testar um MVP e medir resultados.

---

# 11. Uso pelo Requirements Agent

O agente pode utilizar frameworks para descobrir requisitos.

```text
Business Problem
     ↓
PESTEL
     ↓
SWOT
     ↓
Requirements
```

Saída:

```text
REQUIREMENTS.md
```

---

# 12. Uso pelo Architect Agent

```text
Requirements
     ↓
SWOT
     ↓
Architecture Options
     ↓
Decision
```

Saída:

```text
ARCHITECTURE_PLAN.md
ADR
```

---

# 13. Uso pelo Tech Lead Agent

O Tech Lead transforma decisões em execução.

```text
Architecture
     ↓
5W2H
     ↓
Tasks
     ↓
Dependencies
     ↓
Execution Plan
```

---

# 14. Uso pelo Developer Agent

O Developer pode utilizar PDCA durante implementação:

```text
Plan
 ↓
Implement
 ↓
Test
 ↓
Review
 ↓
Improve
```

---

# 15. Uso pelo Reviewer Agent

O Reviewer pode validar:

```text
Objetivo original
     ↓
Implementação
     ↓
Métricas
     ↓
Resultado
```

Pergunta principal:

```text
A implementação realmente resolveu o problema?
```

---

# 16. Uso em incidentes

Frameworks também ajudam em incidentes.

```text
Incident
   ↓
Análise
   ↓
Root Cause
   ↓
Action Plan
   ↓
PDCA
```

Pode ser combinado com:

```text
5 Whys
Fishbone
Postmortem
```

---

# 17. 5 Whys como complemento

Perguntar "por quê?" repetidamente ajuda a chegar à causa raiz.

Exemplo:

```text
API caiu.
↓ Por quê?
Banco ficou indisponível.
↓ Por quê?
Pool de conexões esgotou.
↓ Por quê?
Conexões não estavam sendo liberadas.
↓ Por quê?
Bug no repository.
↓ Por quê?
Faltavam testes de integração.
```

Resultado:

```text
Root Cause
+
Corrective Action
```

---

# 18. Matriz de decisão

Quando existem várias alternativas:

```text
Critério       Peso
Custo          20%
Performance    25%
Complexidade   20%
Escalabilidade 20%
Manutenção     15%
```

Alternativas recebem notas.

Isso ajuda a evitar decisões baseadas apenas em preferência pessoal.

---

# 19. Exemplo: banco de dados

Alternativas:

```text
MySQL
PostgreSQL
SQL Server
MongoDB
```

Critérios:

```text
custo
performance
conhecimento da equipe
cloud
manutenção
features
```

Resultado deve ser documentado em ADR.

---

# 20. RICE como complemento

Para priorização de funcionalidades:

```text
RICE =
Reach × Impact × Confidence
───────────────────────────
Effort
```

Onde:

```text
Reach      → alcance
Impact     → impacto
Confidence → confiança
Effort     → esforço
```

---

# 21. MoSCoW como complemento

Classificação de requisitos:

```text
Must Have
Should Have
Could Have
Won't Have Now
```

Útil para MVPs e planejamento de releases.

---

# 22. Eisenhower para priorização operacional

```text
              URGENTE       NÃO URGENTE
IMPORTANTE    Fazer         Planejar
NÃO IMPORT.   Delegar       Eliminar
```

Pode ser utilizado por agentes de planejamento para ordenar tarefas.

---

# 23. Framework Selection

A IA deve selecionar o framework pelo problema.

```text
Analisar cenário externo
→ PESTEL

Analisar posição/projeto
→ SWOT

Criar plano
→ 5W2H

Melhorar continuamente
→ PDCA

Descobrir causa
→ 5 Whys

Priorizar features
→ RICE / MoSCoW

Escolher tecnologia
→ Decision Matrix
```

---

# 24. Estrutura no Kit IA Dev

```text
Kit-IA-Dev/
└── 8-Dictionary/
    └── 04-frameworks-analise-gestao.md
```

Também pode existir uma Skill:

```text
3-Skills/
└── analysis-frameworks/
    └── SKILL.md
```

---

# 25. Workflow sugerido

```text
Problem
  ↓
Select Framework
  ↓
Collect Evidence
  ↓
Analyze
  ↓
Generate Options
  ↓
Decision
  ↓
Action Plan
  ↓
Execute
  ↓
Measure
```

---

# 26. Regra para agentes

Agentes não devem utilizar frameworks apenas para produzir texto bonito.

Cada framework deve resultar em uma decisão ou ação.

Exemplo ruim:

```text
SWOT
↓
documento
↓
fim
```

Exemplo correto:

```text
SWOT
↓
risco identificado
↓
ação criada
↓
owner
↓
prazo
↓
métrica
```

---

# 27. Evidências

Análises devem utilizar evidências disponíveis:

```text
requirements
code
logs
metrics
tests
costs
documentation
incidents
user feedback
```

Evitar decisões baseadas apenas em suposições.

---

# 28. Documentação da decisão

Decisões arquiteturais importantes devem gerar ADR.

```text
docs/
└── decisions/
    ├── ADR-001-use-redis.md
    ├── ADR-002-use-kafka.md
    └── ADR-003-cloud-strategy.md
```

Estrutura:

```text
Context
Decision
Alternatives
Consequences
Risks
Status
```

---

# 29. Integração com Quality Gates

```text
Analysis
   ↓
Decision
   ↓
Implementation
   ↓
Quality Gates
   ↓
Metrics
   ↓
PDCA
```

Assim, o framework participa do ciclo completo de engenharia.

---

# 30. Checklist

## Análise

- [ ] Problema definido
- [ ] Contexto conhecido
- [ ] Evidências coletadas
- [ ] Framework adequado selecionado
- [ ] Premissas registradas

## Decisão

- [ ] Alternativas comparadas
- [ ] Riscos avaliados
- [ ] Custos considerados
- [ ] Impactos considerados
- [ ] Decisão documentada

## Execução

- [ ] Plano criado
- [ ] Tasks criadas
- [ ] Owners definidos
- [ ] Dependências identificadas
- [ ] Critérios de aceite definidos

## Validação

- [ ] Métricas definidas
- [ ] Resultado medido
- [ ] Quality Gates executados
- [ ] Aprendizados registrados
- [ ] Próxima melhoria definida

---

# 31. Resumo

Os frameworks formam uma cadeia de raciocínio estruturado:

```text
PESTEL
   ↓
Contexto externo

SWOT
   ↓
Diagnóstico

Decision Matrix
   ↓
Escolha

5W2H
   ↓
Plano

PDCA
   ↓
Execução + melhoria
```

Dentro do Kit IA Dev, o objetivo é fazer os agentes saírem de:

```text
"gerar uma opinião"
```

para:

```text
analisar
→ justificar
→ decidir
→ planejar
→ executar
→ medir
→ melhorar
```

---

# 📁 Arquivo

```text
04-frameworks-analise-gestao.md
```
