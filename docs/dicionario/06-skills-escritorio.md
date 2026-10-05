# 📘 Dicionário Técnico — 06 Skills de Escritório

> **Categoria:** Inteligência Artificial / Produtividade / Office Automation  
> **Código:** 06  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** Agentes de IA, documentos, planilhas, apresentações, PDFs, comunicação e rotinas administrativas  
> **Objetivo:** Catalogar skills de escritório que podem ser reutilizadas por agentes para produzir, analisar, transformar e organizar artefatos profissionais.

---

# 1. O que são Skills de Escritório

Skills de escritório são capacidades especializadas para executar tarefas comuns de produtividade.

```text
AI Agent
   │
   ├── Documents
   ├── Spreadsheets
   ├── Presentations
   ├── PDF
   ├── Email
   ├── Calendar
   ├── Reports
   └── Data Analysis
```

No Kit IA Dev, essas skills podem ser utilizadas tanto por agentes administrativos quanto por agentes técnicos.

---

# 2. Objetivo

O objetivo é transformar tarefas como:

```text
"crie um relatório"
"analise esta planilha"
"gere uma apresentação"
"converta para PDF"
"resuma esta reunião"
```

em workflows padronizados e reutilizáveis.

---

# 3. Skill de Documentos

Responsável por:

- criar documentos;
- editar documentos;
- revisar texto;
- aplicar estrutura;
- criar relatórios;
- criar propostas;
- criar documentação técnica;
- gerar atas;
- criar memorandos.

Formatos comuns:

```text
DOCX
ODT
RTF
TXT
Markdown
```

---

# 4. Estrutura de documento

Um agente deve separar conteúdo de apresentação.

Exemplo:

```text
Title
Executive Summary
Context
Objectives
Analysis
Findings
Recommendations
Action Plan
Appendices
```

---

# 5. Skill de Planilhas

Responsável por:

- criar planilhas;
- editar células;
- aplicar fórmulas;
- organizar dados;
- criar tabelas;
- criar gráficos;
- validar dados;
- calcular indicadores;
- criar dashboards.

Formatos:

```text
XLSX
CSV
ODS
```

---

# 6. Casos de uso de Planilhas

```text
Budget
Project Tracker
Sales Pipeline
Operating Calendar
Analytics Dashboard
Inventory
Cost Analysis
Test Matrix
Backlog
```

---

# 7. Fórmulas

A skill deve saber trabalhar com:

```text
SUM
AVERAGE
COUNT
COUNTIF
SUMIF
IF
XLOOKUP
INDEX
MATCH
FILTER
SORT
```

Além de fórmulas específicas da ferramenta utilizada.

---

# 8. Gráficos

Possíveis gráficos:

```text
Bar
Column
Line
Pie
Scatter
Area
Histogram
```

A escolha deve depender do tipo de informação.

Exemplo:

```text
Evolução temporal
→ Line Chart

Comparação entre categorias
→ Bar Chart

Distribuição
→ Histogram
```

---

# 9. Skill de Apresentações

Responsável por criar apresentações profissionais.

Formatos:

```text
PPTX
ODP
Google Slides
```

Estrutura típica:

```text
Cover
Agenda
Context
Problem
Analysis
Architecture
Solution
Roadmap
Risks
Next Steps
```

---

# 10. Apresentação técnica

Exemplo:

```text
Slide 1  → Projeto
Slide 2  → Objetivo
Slide 3  → Problema
Slide 4  → Arquitetura atual
Slide 5  → Arquitetura proposta
Slide 6  → Stack
Slide 7  → Infraestrutura
Slide 8  → CI/CD
Slide 9  → Segurança
Slide 10 → Roadmap
```

---

# 11. Skill de PDF

Responsável por:

- gerar PDF;
- extrair informações;
- reorganizar conteúdo;
- criar relatórios;
- produzir documentação final;
- converter documentos quando suportado.

Casos de uso:

```text
Architecture Report
Project Proposal
Technical Documentation
Executive Report
Manual
Portfolio
```

---

# 12. Skill de Relatórios

Tipos:

```text
Technical Report
Executive Report
Architecture Report
Test Report
Security Report
Incident Report
Project Status Report
Cost Report
```

Estrutura:

```text
Summary
Evidence
Findings
Impact
Recommendations
Actions
```

---

# 13. Skill de E-mail

Responsável por:

```text
draft
reply
summarize
classify
follow-up
```

Exemplo de fluxo:

```text
Incoming Email
 ↓
Analyze
 ↓
Classify
 ↓
Generate Draft
 ↓
Human Review
 ↓
Send
```

---

# 14. Skill de Calendário

Pode apoiar:

- consultar agenda;
- localizar horários;
- preparar reuniões;
- criar eventos;
- reagendar;
- cancelar;
- acompanhar compromissos.

---

# 15. Skill de Reuniões

Pode transformar uma reunião em:

```text
Transcript
   ↓
Summary
   ↓
Decisions
   ↓
Action Items
   ↓
Owners
   ↓
Deadlines
```

Saída sugerida:

```text
MEETING_NOTES.md
```

---

# 16. Skill de Ata

Estrutura:

```text
Meeting
Date
Participants
Agenda
Discussion
Decisions
Action Items
Owners
Deadlines
```

---

# 17. Skill de Resumo

Tipos de resumo:

```text
Executive Summary
Technical Summary
Meeting Summary
Document Summary
Email Thread Summary
Project Summary
```

O nível de detalhe deve acompanhar o público-alvo.

---

# 18. Skill de Pesquisa

Responsável por:

```text
collect
compare
validate
summarize
cite
```

Pode apoiar relatórios, decisões técnicas e documentação.

---

# 19. Skill de Comparação

Exemplo:

```text
AWS vs Azure
Kafka vs RabbitMQ
SQL Server vs MySQL
Monolith vs Microservices
```

Estrutura recomendada:

```text
Criteria
Option A
Option B
Trade-offs
Recommendation
```

---

# 20. Skill de Checklist

Checklists ajudam agentes a não esquecer etapas.

Exemplo:

```text
Release Checklist
Security Checklist
Deployment Checklist
Architecture Checklist
Documentation Checklist
```

---

# 21. Skill de Templates

Templates permitem padronizar documentos recorrentes.

Exemplos:

```text
Project Kickoff
Business Review
Operating Review
Strategy Memorandum
Legal Memorandum
Experiment Analysis
Design Report
Market Trends Report
```

---

# 22. Skill de Markdown

Markdown é importante no Kit IA Dev.

Arquivos comuns:

```text
README.md
PROJECT.md
REQUIREMENTS.md
ARCHITECTURE.md
EXECUTION_PLAN.md
SKILL.md
AGENT.md
REPORT.md
```

---

# 23. Skill de Conversão

Pode converter conteúdo entre formatos quando tecnicamente suportado.

Exemplo:

```text
Markdown
 ↓
DOCX
 ↓
PDF
```

ou:

```text
CSV
 ↓
XLSX
```

---

# 24. Skill de Dados

Fluxo:

```text
Raw Data
 ↓
Cleaning
 ↓
Validation
 ↓
Analysis
 ↓
Visualization
 ↓
Report
```

---

# 25. Limpeza de dados

Operações:

```text
remove duplicates
normalize dates
handle nulls
standardize categories
validate types
detect outliers
```

---

# 26. Skill de Dashboard

Pode transformar dados em indicadores.

```text
Data
 ↓
KPIs
 ↓
Charts
 ↓
Dashboard
 ↓
Insights
```

Exemplos:

```text
Revenue
Conversion
Retention
Cost
Errors
Latency
Coverage
Tasks Completed
```

---

# 27. Aplicação em Engenharia de Software

Skills de escritório também são úteis para desenvolvimento.

```text
Code
 ↓
Test Results
 ↓
Spreadsheet
 ↓
Metrics
 ↓
Report
 ↓
Presentation
```

Exemplo:

```text
SonarQube
 ↓
Quality Metrics
 ↓
XLSX
 ↓
Technical Report
 ↓
Architecture Review
```

---

# 28. Aplicação no Kit IA Dev

Estrutura possível:

```text
Kit-IA-Dev/
└── 3-Skills/
    └── office/
        ├── documents/
        ├── spreadsheets/
        ├── presentations/
        ├── pdf/
        ├── email/
        ├── meetings/
        ├── reports/
        └── research/
```

---

# 29. Estrutura de uma Skill

```text
skill-name/
├── SKILL.md
├── templates/
├── examples/
└── references/
```

O `SKILL.md` deve explicar:

```text
Purpose
When to Use
Inputs
Process
Outputs
Quality Rules
Examples
Limitations
```

---

# 30. Skill Documents

```text
3-Skills/
└── office/
    └── documents/
        └── SKILL.md
```

Responsabilidades:

```text
create
edit
format
review
export
```

---

# 31. Skill Spreadsheets

```text
3-Skills/
└── office/
    └── spreadsheets/
        └── SKILL.md
```

Responsabilidades:

```text
tables
formulas
charts
validation
analysis
dashboard
```

---

# 32. Skill Presentations

```text
3-Skills/
└── office/
    └── presentations/
        └── SKILL.md
```

Responsabilidades:

```text
storyline
slide structure
visual hierarchy
charts
architecture diagrams
speaker notes
```

---

# 33. Skill PDF

```text
3-Skills/
└── office/
    └── pdf/
        └── SKILL.md
```

Responsabilidades:

```text
generate
read
extract
organize
publish
```

---

# 34. Skill Reports

```text
3-Skills/
└── office/
    └── reports/
        └── SKILL.md
```

Pode produzir:

```text
TEST_REPORT.md
SECURITY_REPORT.md
ARCHITECTURE_REPORT.md
PROJECT_STATUS.md
```

---

# 35. Office Agent

Pode existir um agente especializado:

```text
Office Agent
   │
   ├── Documents Skill
   ├── Spreadsheet Skill
   ├── Presentation Skill
   ├── PDF Skill
   └── Report Skill
```

---

# 36. Documentation Agent

Para projetos técnicos:

```text
Documentation Agent
      ↓
Markdown Skill
      ↓
Documents Skill
      ↓
PDF Skill
      ↓
Presentation Skill
```

Assim, a mesma informação pode gerar diferentes artefatos.

---

# 37. Workflow de documentação

```text
Project Data
    ↓
Documentation Agent
    ↓
README
    ↓
Technical Report
    ↓
Presentation
    ↓
PDF
```

---

# 38. Workflow de reunião

```text
Meeting
 ↓
Transcript
 ↓
Summary
 ↓
Decisions
 ↓
Action Items
 ↓
Project Tracker
 ↓
Follow-up
```

---

# 39. Workflow de relatório executivo

```text
Raw Data
 ↓
Spreadsheet Analysis
 ↓
KPIs
 ↓
Charts
 ↓
Executive Summary
 ↓
Presentation
 ↓
PDF
```

---

# 40. Quality Gates de Documentos

- [ ] estrutura correta;
- [ ] ortografia revisada;
- [ ] títulos consistentes;
- [ ] conteúdo completo;
- [ ] dados validados;
- [ ] referências preservadas;
- [ ] formato final verificado;
- [ ] arquivo abre corretamente.

---

# 41. Quality Gates de Planilhas

- [ ] fórmulas válidas;
- [ ] células sem erros;
- [ ] datas normalizadas;
- [ ] números formatados;
- [ ] filtros corretos;
- [ ] gráficos legíveis;
- [ ] dados de origem preservados;
- [ ] abas nomeadas corretamente.

---

# 42. Quality Gates de Apresentações

- [ ] narrativa coerente;
- [ ] uma ideia principal por slide;
- [ ] títulos claros;
- [ ] texto legível;
- [ ] gráficos compreensíveis;
- [ ] arquitetura consistente;
- [ ] alinhamento visual;
- [ ] conclusão e próximos passos.

---

# 43. Quality Gates de PDF

- [ ] nenhuma página cortada;
- [ ] fontes renderizadas;
- [ ] tabelas legíveis;
- [ ] links válidos quando aplicável;
- [ ] cabeçalhos consistentes;
- [ ] paginação correta;
- [ ] conteúdo final revisado.

---

# 44. Naming Convention

Sugestão:

```text
PROJECT_REPORT.md
PROJECT_REPORT.docx
PROJECT_REPORT.pdf
PROJECT_PRESENTATION.pptx
PROJECT_DATA.xlsx
```

Para versões:

```text
architecture-report-v1.md
architecture-report-v2.md
```

---

# 45. Templates reutilizáveis

```text
templates/
├── technical-report/
├── executive-report/
├── architecture-review/
├── project-kickoff/
├── project-status/
└── presentation/
```

Isso reduz retrabalho.

---

# 46. Automação

Skills podem ser combinadas.

Exemplo:

```text
Analyze Repository
 ↓
Generate Metrics
 ↓
Create Spreadsheet
 ↓
Generate Report
 ↓
Create Presentation
 ↓
Export PDF
```

---

# 47. Integração com Agents

```text
Requirements Agent
→ documentos

Architect Agent
→ diagramas + relatório

Tech Lead Agent
→ plano + tracker

Tester Agent
→ test report

Reviewer Agent
→ review report

Documentation Agent
→ README + PDF + apresentação
```

---

# 48. Integração com Conectores

```text
Office Skill
 ↓
Connector
 ↓
Drive / Docs / Sheets / Slides
```

ou:

```text
Office Skill
 ↓
Local File Tool
 ↓
DOCX / XLSX / PPTX / PDF
```

---

# 49. Segurança

Documentos podem conter informações sensíveis.

Antes de gerar ou compartilhar:

```text
Classify Data
 ↓
Check Permissions
 ↓
Mask Secrets
 ↓
Generate Artifact
```

Nunca incluir:

```text
passwords
API keys
tokens
private keys
production secrets
```

---

# 50. Versionamento

Artefatos importantes devem ser versionados quando fizer sentido.

```text
docs/
reports/
presentations/
```

Arquivos temporários ou gerados automaticamente podem ser tratados separadamente.

---

# 51. Regra para Agentes

Antes de criar um artefato, o agente deve identificar:

1. Qual é o objetivo?
2. Quem é o público?
3. Qual formato é adequado?
4. Qual template deve ser usado?
5. Quais fontes devem ser consideradas?
6. Existem dados sensíveis?
7. Quais validações são necessárias?
8. Qual deve ser o nome do arquivo?

---

# 52. Checklist Geral

## Documentos

- [ ] objetivo definido
- [ ] público definido
- [ ] template selecionado
- [ ] conteúdo revisado

## Planilhas

- [ ] dados validados
- [ ] fórmulas testadas
- [ ] gráficos adequados
- [ ] formato consistente

## Apresentações

- [ ] storyline
- [ ] hierarquia visual
- [ ] dados corretos
- [ ] próximos passos

## PDF

- [ ] renderização validada
- [ ] páginas verificadas
- [ ] conteúdo completo

## Segurança

- [ ] sem secrets
- [ ] permissões verificadas
- [ ] dados sensíveis tratados

---

# 53. Estrutura no Dicionário

Este documento deve ficar em:

```text
Kit-IA-Dev/
└── 8-Dictionary/
    └── 06-skills-escritorio.md
```

---

# 54. Relação com outros itens

Complementa:

```text
01 - Estrutura de Projeto
03 - Plugins
05 - Conectores e Funções
09 - Skills Claude Code
11 - CI/CD
16 - Arquitetura de Aplicações
17 - Agentic AI
18 - Kit IA Dev
```

---

# 55. Resumo

Skills de escritório transformam tarefas administrativas e documentais em capacidades reutilizáveis por agentes.

```text
Data
 ↓
Analysis
 ↓
Document
 ↓
Spreadsheet
 ↓
Presentation
 ↓
PDF
```

Dentro do Kit IA Dev, elas também fazem parte do processo de engenharia:

```text
Projeto
 ↓
Métricas
 ↓
Relatório
 ↓
Documentação
 ↓
Apresentação
 ↓
Entrega
```

O objetivo é possuir um conjunto de skills padronizadas, reutilizáveis e verificáveis para gerar artefatos profissionais com consistência.

---

# 📁 Arquivo

```text
06-skills-escritorio.md
```
