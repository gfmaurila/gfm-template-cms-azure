# 📘 Dicionário Técnico — 07 LinkedIn Manager Agent

> **Categoria:** Inteligência Artificial / Agentes / Automação de Conteúdo  
> **Código:** 07  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** Claude Code / Agentes de IA / LinkedIn / Gestão de Conteúdo Profissional  
> **Objetivo:** Definir um agente especializado em planejar, produzir, revisar, organizar e analisar conteúdo profissional para LinkedIn, mantendo controle humano sobre publicações e ações externas.

---

# 1. O que é um LinkedIn Manager Agent

Um LinkedIn Manager Agent é um agente de IA especializado em atividades relacionadas à gestão de presença profissional no LinkedIn.

Ele pode atuar como:

```text
Content Strategist
+
Copywriter
+
Research Assistant
+
Editorial Planner
+
Analytics Assistant
+
Profile Reviewer
```

O objetivo não é apenas gerar posts.

O agente deve apoiar um processo completo de conteúdo.

---

# 2. Arquitetura conceitual

```text
User
  ↓
LinkedIn Manager Agent
  │
  ├── Profile Analysis
  ├── Content Strategy
  ├── Research
  ├── Post Generation
  ├── Editorial Calendar
  ├── Review
  └── Analytics
```

---

# 3. Principais responsabilidades

O agente pode:

- analisar posicionamento profissional;
- sugerir temas;
- criar calendário editorial;
- pesquisar assuntos;
- gerar rascunhos;
- adaptar tom;
- revisar textos;
- criar variações;
- sugerir hashtags;
- gerar chamadas para ação;
- acompanhar métricas quando houver dados;
- transformar projetos técnicos em conteúdo;
- reutilizar conteúdos existentes.

---

# 4. O que o agente não deve fazer automaticamente

Ações externas de impacto devem respeitar autorização e capacidades disponíveis.

Exemplos:

```text
publicar
enviar mensagem
responder pessoas
seguir perfis
conectar pessoas
alterar perfil
```

Fluxo recomendado:

```text
Agent
 ↓
Draft
 ↓
Review
 ↓
User Approval
 ↓
Publish / External Action
```

---

# 5. Estrutura do Agent

```text
agents/
└── linkedin-manager/
    ├── AGENT.md
    ├── prompts/
    ├── templates/
    ├── workflows/
    ├── references/
    └── reports/
```

---

# 6. AGENT.md

O arquivo deve definir:

```text
Role
Mission
Responsibilities
Inputs
Tools
Skills
Rules
Outputs
Quality Gates
Limitations
```

---

# 7. Skills relacionadas

```text
skills/
├── linkedin-content/
├── copywriting/
├── research/
├── storytelling/
├── technical-content/
├── editorial-calendar/
├── profile-review/
└── analytics/
```

---

# 8. Workflow principal

```text
Goal
 ↓
Audience
 ↓
Topic
 ↓
Research
 ↓
Angle
 ↓
Draft
 ↓
Review
 ↓
Approval
 ↓
Publication
 ↓
Metrics
 ↓
Learning
```

---

# 9. Estratégia de conteúdo

Antes de criar posts, definir pilares.

Exemplo para um profissional de tecnologia:

```text
Arquitetura de Software
.NET / C#
Cloud
AWS / Azure
IA
RAG
Agentic AI
DevOps
Docker
Observabilidade
Carreira
Projetos
Aprendizados
```

---

# 10. Content Pillars

Estrutura:

```text
Pillar 1 → Conteúdo técnico
Pillar 2 → Projetos
Pillar 3 → Aprendizados
Pillar 4 → Opinião profissional
Pillar 5 → Carreira
```

Isso evita um perfil sem direção editorial.

---

# 11. Tipos de conteúdo

```text
Tutorial
Insight
Case Study
Project Update
Architecture Breakdown
Lesson Learned
Opinion
Checklist
Comparison
Story
Question
Career Post
```

---

# 12. Conteúdo técnico

Exemplo:

```text
Tema:
Redis

Post:
"Quando usar Redis como cache?"

Estrutura:
Problema
↓
Contexto
↓
Solução
↓
Exemplo
↓
Trade-offs
↓
Conclusão
```

---

# 13. Conteúdo de projeto

Projetos podem gerar vários posts.

Exemplo:

```text
Projeto
  ↓
Arquitetura
  ↓
Stack
  ↓
Problema
  ↓
Decisão
  ↓
Implementação
  ↓
Resultado
```

Cada etapa pode virar conteúdo separado.

---

# 14. Content Repurposing

Um conteúdo pode gerar vários formatos.

```text
Artigo
 ↓
Post
 ↓
Checklist
 ↓
Carrossel
 ↓
Resumo
 ↓
Thread
 ↓
Vídeo Script
```

Isso aumenta reutilização sem simplesmente duplicar o mesmo texto.

---

# 15. Research Agent

O LinkedIn Manager pode delegar pesquisa.

```text
LinkedIn Manager
      ↓
Research Agent
      ↓
Sources
      ↓
Evidence
      ↓
Content Draft
```

Informações técnicas e atuais devem ser verificadas antes da publicação.

---

# 16. Technical Reviewer

Conteúdo técnico pode passar por revisão especializada.

```text
Draft
 ↓
Technical Reviewer
 ↓
Fact Check
 ↓
Corrections
 ↓
Final Draft
```

Isso reduz publicação de informações incorretas.

---

# 17. Tone of Voice

O agente deve possuir configuração de tom.

Exemplo:

```yaml
tone:
  professional: true
  technical: true
  direct: true
  educational: true
  exaggerated_marketing: false
```

O tom deve ser consistente entre publicações.

---

# 18. Perfil de audiência

O agente deve saber para quem escreve.

Exemplos:

```text
Developers
Tech Leads
Architects
Recruiters
Engineering Managers
Companies
Students
```

O mesmo tema muda conforme a audiência.

---

# 19. Exemplo de adaptação

Tema:

```text
CQRS
```

Para desenvolvedores:

```text
implementação
handlers
commands
queries
trade-offs
```

Para recrutadores:

```text
capacidade de arquitetura
escalabilidade
experiência
impacto
```

---

# 20. Hook

O início precisa comunicar rapidamente o assunto.

Tipos:

```text
Question
Problem
Observation
Result
Contrarian Angle
Lesson Learned
```

O hook deve ser relevante, não apenas sensacionalista.

---

# 21. Estrutura de Post

Modelo:

```text
HOOK

CONTEXTO

PROBLEMA

INSIGHT

EXEMPLO

CONCLUSÃO

CTA
```

---

# 22. CTA

CTA — Call to Action.

Exemplos:

```text
"Como você resolveria esse cenário?"

"Você já utilizou essa arquitetura?"

"Qual abordagem sua equipe utiliza?"
```

Evitar CTAs artificiais em todos os posts.

---

# 23. Hashtags

Hashtags devem ser relevantes ao conteúdo.

Exemplo:

```text
#dotnet
#csharp
#softwarearchitecture
#aws
#devops
```

Não usar dezenas de hashtags sem propósito.

---

# 24. Calendário Editorial

Exemplo:

```text
Monday    → Architecture
Tuesday   → .NET
Wednesday → Cloud
Thursday  → AI
Friday    → Career / Project
```

A frequência deve ser sustentável.

---

# 25. Estrutura do calendário

```text
Date
Topic
Pillar
Format
Status
Draft
Review
Publish
Metrics
```

Pode ser mantido em Markdown ou planilha.

---

# 26. Estados do conteúdo

```text
IDEA
RESEARCH
DRAFT
REVIEW
APPROVED
PUBLISHED
ANALYZED
```

Fluxo:

```text
IDEA
 ↓
RESEARCH
 ↓
DRAFT
 ↓
REVIEW
 ↓
APPROVED
 ↓
PUBLISHED
 ↓
ANALYZED
```

---

# 27. Backlog de ideias

```text
content/
├── backlog/
├── drafts/
├── approved/
├── published/
└── analytics/
```

---

# 28. Templates

```text
templates/
├── technical-post.md
├── project-post.md
├── tutorial-post.md
├── comparison-post.md
├── career-post.md
└── case-study.md
```

---

# 29. Template técnico

```text
# Topic

## Hook

## Context

## Problem

## Explanation

## Example

## Trade-offs

## Conclusion

## CTA
```

---

# 30. Conteúdo a partir do GitHub

Projetos podem alimentar conteúdo.

```text
Repository
 ↓
Analyze README
 ↓
Architecture
 ↓
Interesting Decisions
 ↓
Content Ideas
```

Exemplos:

```text
"Por que usei CQRS?"
"Como organizei Vertical Slices?"
"Como configurei Redis?"
"Como implementei observabilidade?"
```

---

# 31. Conteúdo a partir de documentação

Fontes:

```text
README.md
ARCHITECTURE.md
ADR
PROJECT.md
REQUIREMENTS.md
```

O agente pode transformar documentação técnica em conteúdo educacional.

---

# 32. Conteúdo a partir de aprendizado

Exemplo:

```text
Study Topic
 ↓
Notes
 ↓
Summary
 ↓
Practical Example
 ↓
LinkedIn Post
```

Assim, estudo e produção de conteúdo se reforçam.

---

# 33. Integração com RAG

Um agente mais avançado pode utilizar RAG.

```text
LinkedIn Agent
      ↓
Retriever
      ↓
Knowledge Base
      ├── Projetos
      ├── Artigos
      ├── Notas
      └── Documentação
```

Isso permite produzir conteúdo baseado no conhecimento real do usuário/projeto.

---

# 34. Knowledge Base

Estrutura possível:

```text
knowledge/
├── projects/
├── technologies/
├── career/
├── articles/
├── references/
└── published-content/
```

---

# 35. Evitar repetição

Antes de sugerir um tema:

```text
New Idea
 ↓
Search Published Content
 ↓
Similar?
 ├── Yes → New Angle
 └── No → Continue
```

---

# 36. Analytics

Quando houver dados disponíveis:

```text
Impressions
Views
Likes
Comments
Shares
Saves
Clicks
Followers
```

O objetivo não deve ser apenas maximizar números, mas entender quais conteúdos são úteis para a audiência.

---

# 37. Feedback Loop

```text
Publish
 ↓
Collect Metrics
 ↓
Analyze
 ↓
Learn
 ↓
Adjust Strategy
 ↓
Next Content
```

---

# 38. Métricas por pilar

Exemplo:

```text
.NET              → engagement
Architecture      → saves
Cloud             → comments
AI                → impressions
Career            → conversations
```

Isso ajuda a entender padrões.

---

# 39. A/B de abordagem

Um mesmo assunto pode possuir ângulos diferentes.

```text
Technical
Storytelling
Checklist
Opinion
Case Study
```

Comparar resultados pode orientar conteúdo futuro.

---

# 40. Profile Review

O agente pode revisar:

```text
Headline
About
Experience
Projects
Skills
Featured
```

Objetivo:

```text
Profile
 ↓
Clear Positioning
 ↓
Evidence
 ↓
Projects
 ↓
Skills
```

---

# 41. Profile Positioning

Uma headline deve comunicar rapidamente:

```text
Role
+
Specialization
+
Technologies
+
Value
```

Evitar lista excessiva de tecnologias sem contexto.

---

# 42. About

Estrutura:

```text
Who I Am
Experience
Specialties
Problems I Solve
Technologies
Projects
Contact / Next Step
```

---

# 43. Projects

Projetos devem mostrar evidência prática.

```text
Problem
 ↓
Architecture
 ↓
Technology
 ↓
Implementation
 ↓
Result
```

---

# 44. Content Safety

O agente deve evitar:

- divulgar informações confidenciais;
- publicar código privado;
- revelar secrets;
- expor clientes sem autorização;
- inventar experiência;
- inventar métricas;
- inventar resultados;
- atribuir certificações inexistentes.

---

# 45. Fact Checking

Antes de conteúdo técnico:

```text
Claim
 ↓
Source
 ↓
Validation
 ↓
Draft
```

Especialmente para:

```text
versions
benchmarks
prices
cloud services
security
statistics
```

---

# 46. Human in the Loop

Publicação deve manter revisão humana quando apropriado.

```text
AI
 ↓
Draft
 ↓
Human Review
 ↓
Approve
 ↓
Publish
```

---

# 47. Integração com conectores

Quando disponíveis:

```text
LinkedIn Manager
 ├── Files
 ├── GitHub
 ├── Drive
 ├── Search
 └── Analytics Source
```

A integração real com LinkedIn depende das ferramentas e permissões disponíveis.

---

# 48. Workflow diário

```text
Check Backlog
 ↓
Select Topic
 ↓
Research
 ↓
Draft
 ↓
Review
 ↓
Save
```

---

# 49. Workflow semanal

```text
Analyze Previous Week
 ↓
Review Metrics
 ↓
Update Backlog
 ↓
Plan Topics
 ↓
Prepare Drafts
```

---

# 50. Workflow mensal

```text
Metrics
 ↓
Content Pillars
 ↓
Best Topics
 ↓
Weak Topics
 ↓
Strategy Adjustment
```

---

# 51. Multi-Agent

Estrutura avançada:

```text
LinkedIn Manager
      │
      ├── Research Agent
      ├── Technical Agent
      ├── Copywriter Agent
      ├── Reviewer Agent
      └── Analytics Agent
```

---

# 52. Orquestração

```text
Topic
 ↓
Research Agent
 ↓
Technical Agent
 ↓
Copywriter
 ↓
Reviewer
 ↓
User Approval
```

---

# 53. Quality Gates

Antes de aprovar conteúdo:

- [ ] assunto relevante;
- [ ] informação correta;
- [ ] nenhuma informação confidencial;
- [ ] tom adequado;
- [ ] texto legível;
- [ ] exemplo correto;
- [ ] sem claims inventados;
- [ ] CTA adequado;
- [ ] hashtags relevantes;
- [ ] revisão final realizada.

---

# 54. Anti-patterns

Evitar:

```text
post genérico de IA
engagement bait
clickbait excessivo
falsa autoridade
experiência inventada
métricas inventadas
copiar conteúdo de terceiros
publicação automática sem controle
mesmo formato repetidamente
```

---

# 55. Estrutura no Kit IA Dev

```text
Kit-IA-Dev/
├── 2-Agents/
│   └── linkedin-manager/
├── 3-Skills/
│   ├── linkedin-content/
│   ├── copywriting/
│   ├── research/
│   └── analytics/
└── 8-Dictionary/
    └── 07-linkedin-manager-agent.md
```

---

# 56. Exemplo de AGENT.md

```yaml
name: linkedin-manager

mission:
  Planejar e produzir conteúdo profissional baseado em
  conhecimento e experiências reais.

responsibilities:
  - research
  - content planning
  - drafting
  - reviewing
  - analytics

rules:
  - never invent professional experience
  - never expose confidential information
  - verify technical claims
  - require approval before external actions
```

---

# 57. Comando conceitual

```text
Analise meus projetos recentes.

Identifique 10 ideias de conteúdo técnico.

Classifique por:
- .NET
- arquitetura
- cloud
- IA
- DevOps

Para cada ideia:
- objetivo
- público
- hook
- tópicos
- formato recomendado

Não publique nada.
```

---

# 58. Regra para o agente

Antes de produzir conteúdo, responder:

1. Qual é o objetivo?
2. Quem é a audiência?
3. Qual pilar será utilizado?
4. Quais fontes sustentam o conteúdo?
5. Existe informação confidencial?
6. Existe conteúdo semelhante já publicado?
7. Qual formato é mais adequado?
8. O conteúdo precisa de revisão técnica?
9. Existe alguma afirmação que precisa ser verificada?
10. O usuário aprovou qualquer ação externa necessária?

---

# 59. Relação com outros itens

Complementa:

```text
02 - RAG
03 - Plugins
05 - Conectores e Funções
06 - Skills de Escritório
09 - Skills Claude Code
12 - SEO / AEO
17 - Agentic AI
18 - Kit IA Dev
```

---

# 60. Resumo

Um LinkedIn Manager Agent não deve ser apenas:

```text
"gerador de posts"
```

A arquitetura correta é:

```text
Knowledge
 ↓
Research
 ↓
Strategy
 ↓
Content
 ↓
Technical Review
 ↓
Human Approval
 ↓
Publication
 ↓
Analytics
 ↓
Learning
```

Integrado ao Kit IA Dev, ele pode transformar projetos, estudos, documentação e conhecimento técnico em uma linha editorial organizada, rastreável e reutilizável.

---

# 📁 Arquivo

```text
07-linkedin-manager-agent.md
```
