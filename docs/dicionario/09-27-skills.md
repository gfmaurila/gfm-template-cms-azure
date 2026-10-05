# 📘 Dicionário Técnico — 09 As 27 Skills

> **Categoria:** Inteligência Artificial / Agent Skills / Claude Code  
> **Código:** 09  
> **Uso:** Kit IA Dev  
> **Objetivo:** Registrar as 27 skills catalogadas no material de referência e mostrar como podem ser incorporadas a workflows de desenvolvimento, pesquisa, conteúdo, design e produtividade.

---

# 1. Conceito

Uma **Skill** encapsula instruções e conhecimento reutilizável para uma atividade especializada.

```text
Prompt
  ↓
Orchestrator
  ↓
Agent
  ↓
Skill
  ↓
Tools / Connectors
  ↓
Resultado
```

Uma skill não precisa representar um agente independente. Um agente pode carregar várias skills conforme a tarefa.

---

# 2. As 27 Skills

| # | Skill | Uso principal |
|---:|---|---|
| 1 | `reddit-automation` | Automação e apoio a fluxos de conteúdo/pesquisa no Reddit, com uso responsável das integrações disponíveis. |
| 2 | `seo-audit` | Auditoria de SEO técnico e de conteúdo: estrutura, metadados, rastreabilidade, problemas e recomendações. |
| 3 | `copywriting` | Criação e revisão de textos persuasivos para páginas, campanhas, produtos e comunicação. |
| 4 | `find-skills` | Descoberta de skills existentes antes de criar uma nova capacidade do zero. |
| 5 | `grill-me` | Revisão crítica por perguntas: desafia premissas, requisitos, decisões e lacunas de uma proposta. |
| 6 | `caveman` | Transformação de explicações complexas em linguagem extremamente simples, direta e fácil de compreender. |
| 7 | `faceless-explainer` | Planejamento de conteúdo explicativo em vídeo sem exigir apresentador visível, incluindo roteiro e estrutura narrativa. |
| 8 | `twitter-automation` | Apoio a workflows de conteúdo para X/Twitter: ideias, drafts, calendário e reaproveitamento de conteúdo. |
| 9 | `talking-head-recut` | Planejamento de recortes e reaproveitamento de vídeos de fala/apresentação em peças menores. |
| 10 | `hyperframes-cli` | Skill relacionada a workflows de mídia/vídeo via CLI, automatizando etapas suportadas pela ferramenta associada. |
| 11 | `ai-video-generation` | Planejamento e geração assistida por IA de assets e workflows de vídeo. |
| 12 | `remotion-best-practices` | Boas práticas para projetos de vídeo programático com Remotion/React: composição, organização, performance e manutenção. |
| 13 | `skill-creator` | Criação padronizada de novas skills reutilizáveis, com instruções, gatilhos, exemplos, referências e validações. |
| 14 | `brainstorming` | Exploração estruturada de ideias, alternativas, riscos e possibilidades antes da implementação. |
| 15 | `pptx` | Criação, edição e estruturação de apresentações PowerPoint profissionais. |
| 16 | `frontend-design` | Projeto e implementação de interfaces frontend com atenção a layout, componentes, responsividade e qualidade visual. |
| 17 | `design-taste-frontend` | Revisão de qualidade estética de frontend: hierarquia, espaçamento, tipografia, consistência e refinamento visual. |
| 18 | `ui-ux-pro-max` | Apoio avançado a UI/UX, design systems, componentes, experiência, acessibilidade e consistência de interfaces. |
| 19 | `teach` | Explicação didática de assuntos com exemplos, progressão de dificuldade e foco em aprendizado. |
| 20 | `research` | Pesquisa estruturada, comparação de fontes, síntese de evidências e produção de conclusões. |
| 21 | `just-scrape` | Extração estruturada de informações públicas de páginas/fontes quando o workflow e as permissões aplicáveis permitirem. |
| 22 | `vercel-react-best-practices` | Boas práticas para aplicações React no ecossistema Vercel, com foco em arquitetura, performance e padrões modernos. |
| 23 | `web-design-guidelines` | Revisão de interfaces web segundo princípios de design, usabilidade, responsividade e acessibilidade. |
| 24 | `supabase-postgres` | Desenvolvimento e boas práticas com Supabase/PostgreSQL: modelagem, queries, segurança e integração. |
| 25 | `grill-with-docs` | Revisão crítica baseada em documentação fornecida, confrontando decisões e implementação com as fontes do projeto. |
| 26 | `improve-codebase-architecture` | Análise e melhoria arquitetural de codebases: acoplamento, modularização, dependências, responsabilidades e evolução. |
| 27 | `tdd` | Desenvolvimento orientado a testes: Red → Green → Refactor, testes pequenos e evolução incremental. |

---

# 3. Agrupamento por finalidade

```text
Marketing / Conteúdo
├── reddit-automation
├── seo-audit
└── copywriting

Produtividade / Raciocínio
├── find-skills
├── grill-me
├── caveman
├── brainstorming
├── teach
├── research
└── grill-with-docs

Social / Vídeo
├── faceless-explainer
├── twitter-automation
├── talking-head-recut
├── hyperframes-cli
├── ai-video-generation
└── remotion-best-practices

Criação / Escritório
├── skill-creator
└── pptx

Frontend / UI / UX
├── frontend-design
├── design-taste-frontend
├── ui-ux-pro-max
├── vercel-react-best-practices
└── web-design-guidelines

Web / Dados
├── just-scrape
└── supabase-postgres

Engenharia de Software
├── improve-codebase-architecture
└── tdd
```

---

# 4. Catálogo detalhado

## 1. `reddit-automation`

**Finalidade:** Automação e apoio a fluxos de conteúdo/pesquisa no Reddit, com uso responsável das integrações disponíveis.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
reddit-automation
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 2. `seo-audit`

**Finalidade:** Auditoria de SEO técnico e de conteúdo: estrutura, metadados, rastreabilidade, problemas e recomendações.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
seo-audit
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 3. `copywriting`

**Finalidade:** Criação e revisão de textos persuasivos para páginas, campanhas, produtos e comunicação.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
copywriting
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 4. `find-skills`

**Finalidade:** Descoberta de skills existentes antes de criar uma nova capacidade do zero.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
find-skills
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 5. `grill-me`

**Finalidade:** Revisão crítica por perguntas: desafia premissas, requisitos, decisões e lacunas de uma proposta.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
grill-me
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 6. `caveman`

**Finalidade:** Transformação de explicações complexas em linguagem extremamente simples, direta e fácil de compreender.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
caveman
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 7. `faceless-explainer`

**Finalidade:** Planejamento de conteúdo explicativo em vídeo sem exigir apresentador visível, incluindo roteiro e estrutura narrativa.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
faceless-explainer
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 8. `twitter-automation`

**Finalidade:** Apoio a workflows de conteúdo para X/Twitter: ideias, drafts, calendário e reaproveitamento de conteúdo.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
twitter-automation
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 9. `talking-head-recut`

**Finalidade:** Planejamento de recortes e reaproveitamento de vídeos de fala/apresentação em peças menores.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
talking-head-recut
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 10. `hyperframes-cli`

**Finalidade:** Skill relacionada a workflows de mídia/vídeo via CLI, automatizando etapas suportadas pela ferramenta associada.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
hyperframes-cli
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 11. `ai-video-generation`

**Finalidade:** Planejamento e geração assistida por IA de assets e workflows de vídeo.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
ai-video-generation
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 12. `remotion-best-practices`

**Finalidade:** Boas práticas para projetos de vídeo programático com Remotion/React: composição, organização, performance e manutenção.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
remotion-best-practices
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 13. `skill-creator`

**Finalidade:** Criação padronizada de novas skills reutilizáveis, com instruções, gatilhos, exemplos, referências e validações.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
skill-creator
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 14. `brainstorming`

**Finalidade:** Exploração estruturada de ideias, alternativas, riscos e possibilidades antes da implementação.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
brainstorming
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 15. `pptx`

**Finalidade:** Criação, edição e estruturação de apresentações PowerPoint profissionais.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
pptx
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 16. `frontend-design`

**Finalidade:** Projeto e implementação de interfaces frontend com atenção a layout, componentes, responsividade e qualidade visual.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
frontend-design
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 17. `design-taste-frontend`

**Finalidade:** Revisão de qualidade estética de frontend: hierarquia, espaçamento, tipografia, consistência e refinamento visual.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
design-taste-frontend
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 18. `ui-ux-pro-max`

**Finalidade:** Apoio avançado a UI/UX, design systems, componentes, experiência, acessibilidade e consistência de interfaces.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
ui-ux-pro-max
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 19. `teach`

**Finalidade:** Explicação didática de assuntos com exemplos, progressão de dificuldade e foco em aprendizado.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
teach
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 20. `research`

**Finalidade:** Pesquisa estruturada, comparação de fontes, síntese de evidências e produção de conclusões.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
research
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 21. `just-scrape`

**Finalidade:** Extração estruturada de informações públicas de páginas/fontes quando o workflow e as permissões aplicáveis permitirem.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
just-scrape
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 22. `vercel-react-best-practices`

**Finalidade:** Boas práticas para aplicações React no ecossistema Vercel, com foco em arquitetura, performance e padrões modernos.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
vercel-react-best-practices
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 23. `web-design-guidelines`

**Finalidade:** Revisão de interfaces web segundo princípios de design, usabilidade, responsividade e acessibilidade.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
web-design-guidelines
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 24. `supabase-postgres`

**Finalidade:** Desenvolvimento e boas práticas com Supabase/PostgreSQL: modelagem, queries, segurança e integração.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
supabase-postgres
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 25. `grill-with-docs`

**Finalidade:** Revisão crítica baseada em documentação fornecida, confrontando decisões e implementação com as fontes do projeto.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
grill-with-docs
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 26. `improve-codebase-architecture`

**Finalidade:** Análise e melhoria arquitetural de codebases: acoplamento, modularização, dependências, responsabilidades e evolução.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
improve-codebase-architecture
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

## 27. `tdd`

**Finalidade:** Desenvolvimento orientado a testes: Red → Green → Refactor, testes pequenos e evolução incremental.

**Aplicação no Kit IA Dev:**

```text
Task
 ↓
tdd
 ↓
Resultado especializado
 ↓
Quality Gate / revisão
```

A skill deve ser acionada somente quando sua especialização realmente contribuir para a tarefa. Ela pode ser combinada com agentes, conectores, plugins e outras skills.

---

# 5. Combinação de Skills

O maior ganho aparece quando skills são encadeadas.

## Desenvolvimento de feature

```text
brainstorming
 ↓
grill-with-docs
 ↓
improve-codebase-architecture
 ↓
tdd
 ↓
review
```

## Criação de frontend

```text
brainstorming
 ↓
frontend-design
 ↓
ui-ux-pro-max
 ↓
design-taste-frontend
 ↓
web-design-guidelines
```

## Pesquisa técnica

```text
research
 ↓
grill-with-docs
 ↓
teach
 ↓
pptx
```

## Conteúdo técnico

```text
research
 ↓
copywriting
 ↓
seo-audit
 ↓
faceless-explainer / twitter-automation
```

---

# 6. Aplicação no Kit IA Dev

Estrutura recomendada:

```text
Kit-IA-Dev/
├── 2-Agents/
├── 3-Skills/
│   ├── reddit-automation/
│   ├── seo-audit/
│   ├── copywriting/
│   ├── find-skills/
│   ├── grill-me/
│   ├── caveman/
│   ├── faceless-explainer/
│   ├── twitter-automation/
│   ├── talking-head-recut/
│   ├── hyperframes-cli/
│   ├── ai-video-generation/
│   ├── remotion-best-practices/
│   ├── skill-creator/
│   ├── brainstorming/
│   ├── pptx/
│   ├── frontend-design/
│   ├── design-taste-frontend/
│   ├── ui-ux-pro-max/
│   ├── teach/
│   ├── research/
│   ├── just-scrape/
│   ├── vercel-react-best-practices/
│   ├── web-design-guidelines/
│   ├── supabase-postgres/
│   ├── grill-with-docs/
│   ├── improve-codebase-architecture/
│   └── tdd/
└── 8-Dictionary/
    └── 09-27-skills.md
```

---

# 7. Estrutura padrão de uma Skill

```text
skill-name/
├── SKILL.md
├── references/
├── examples/
├── templates/
└── scripts/
```

Nem toda skill precisa de todas as pastas, mas `SKILL.md` deve ser o contrato principal.

---

# 8. Conteúdo recomendado para SKILL.md

```text
Name
Purpose
When to Use
When Not to Use
Inputs
Workflow
Tools
Rules
Outputs
Examples
Quality Gates
Limitations
```

---

# 9. Descoberta antes da criação

A skill `find-skills` deve ser usada como princípio de reutilização:

```text
Nova necessidade
 ↓
Existe skill?
 ├── Sim → reutilizar/adaptar
 └── Não → skill-creator
```

Isso evita duplicação de capacidades.

---

# 10. Skill Creator

Quando realmente faltar uma capacidade:

```text
Requirement
 ↓
find-skills
 ↓
No Match
 ↓
skill-creator
 ↓
SKILL.md
 ↓
Examples
 ↓
Validation
 ↓
Registry
```

---

# 11. Registry de Skills

Criar um catálogo central:

```text
PROJECT_SKILLS.md
```

ou:

```text
SKILLS_REGISTRY.md
```

Campos recomendados:

```text
Name
Category
Purpose
Agent
Status
Dependencies
Tools
```

---

# 12. Skills por Agente

Exemplo:

```text
Architect Agent
├── brainstorming
├── grill-with-docs
└── improve-codebase-architecture

Developer Agent
├── tdd
├── improve-codebase-architecture
└── research

Frontend Agent
├── frontend-design
├── ui-ux-pro-max
├── design-taste-frontend
└── web-design-guidelines

Documentation / Content Agent
├── research
├── teach
├── copywriting
└── pptx
```

---

# 13. Skill Routing

O orquestrador deve selecionar apenas as skills relevantes.

```text
Task
 ↓
Intent Analysis
 ↓
Agent Selection
 ↓
Skill Selection
 ↓
Execution
```

Evitar carregar todas as skills em toda tarefa.

---

# 14. Quality Gates

Antes de incorporar uma skill:

- [ ] finalidade clara;
- [ ] gatilhos de uso definidos;
- [ ] entradas documentadas;
- [ ] saída esperada definida;
- [ ] exemplos disponíveis;
- [ ] ferramentas necessárias documentadas;
- [ ] limitações registradas;
- [ ] não duplica outra skill;
- [ ] testada em cenário real;
- [ ] registrada no catálogo.

---

# 15. Segurança

Skills não devem conceder permissões automaticamente.

```text
Skill
 ↓
Required Tool
 ↓
Permission Check
 ↓
Execution
```

Ações externas, destrutivas ou sensíveis devem respeitar autorização, ambiente e política do projeto.

---

# 16. Anti-patterns

Evitar:

```text
skill genérica demais
skill duplicada
skill sem gatilho
skill sem exemplos
skill sem output definido
skill misturando muitas responsabilidades
skill com segredo hardcoded
skill assumindo ferramenta inexistente
```

---

# 17. Estratégia para o Kit

As 27 skills não precisam ser executadas em todo projeto.

O Kit deve tratá-las como catálogo:

```text
Available Skills
      ↓
Project Requirements
      ↓
Select Relevant Skills
      ↓
Install / Configure
      ↓
Agents
      ↓
Workflows
```

---

# 18. Exemplo para projeto .NET

```text
Requirement
 ↓
brainstorming
 ↓
grill-with-docs
 ↓
Architect Agent
 ↓
improve-codebase-architecture
 ↓
Developer Agent
 ↓
tdd
 ↓
Documentation
 ↓
teach / pptx
```

---

# 19. Exemplo para React

```text
Requirement
 ↓
frontend-design
 ↓
ui-ux-pro-max
 ↓
Implementation
 ↓
design-taste-frontend
 ↓
web-design-guidelines
 ↓
Quality Gate
```

---

# 20. Exemplo para conteúdo

```text
Topic
 ↓
research
 ↓
copywriting
 ↓
seo-audit
 ↓
faceless-explainer
 ↓
Distribution Workflow
```

---

# 21. Relação com outros itens

```text
01 - Estrutura de Projeto
01.2 - Agentic Workflow
03 - Plugins
05 - Conectores e Funções
06 - Skills de Escritório
07 - LinkedIn Manager Agent
17 - Agentic AI
18 - Kit IA Dev
```

---

# 22. Resumo

As 27 skills formam um catálogo de capacidades especializadas.

```text
Orchestrator
     ↓
Agent
     ↓
Relevant Skills
     ↓
Tools
     ↓
Quality Gates
     ↓
Result
```

O princípio central para o Kit IA Dev é:

```text
Descobrir
→ Selecionar
→ Reutilizar
→ Combinar
→ Validar
```

em vez de criar uma nova skill para cada tarefa.

---

# 📁 Arquivo

```text
09-27-skills.md
```
