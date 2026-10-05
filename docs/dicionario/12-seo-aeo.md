# 📘 Dicionário Técnico — 12 SEO / AEO

> **Categoria:** Web / Conteúdo / Marketing Técnico / IA  
> **Código:** 12  
> **Uso:** Kit IA Dev  
> **Aplicação principal:** Sites, CMS, React, conteúdo técnico, documentação pública e mecanismos de busca tradicionais e baseados em IA  
> **Objetivo:** Explicar SEO e AEO, suas diferenças e como incorporá-los ao desenvolvimento, conteúdo e automações do Kit IA Dev.

---

# 1. SEO

SEO significa **Search Engine Optimization**.

É o conjunto de práticas utilizadas para melhorar descoberta, compreensão, indexação e posicionamento de páginas em mecanismos de busca.

```text
Website
 ↓
Crawler
 ↓
Index
 ↓
Ranking
 ↓
Search Results
```

SEO não é apenas utilização de palavras-chave.

Inclui:

```text
Technical SEO
Content
Architecture
Performance
Accessibility
Structured Data
Authority
User Experience
```

---

# 2. AEO

AEO significa **Answer Engine Optimization**.

Seu foco é estruturar conteúdo para que sistemas de resposta consigam identificar e utilizar uma resposta clara.

```text
Question
 ↓
Answer Engine
 ↓
Information Retrieval
 ↓
Relevant Answer
```

Pode ser relevante para:

- mecanismos de busca com respostas diretas;
- assistentes;
- sistemas generativos;
- experiências de busca baseadas em IA.

---

# 3. SEO x AEO

```text
SEO
→ otimizar páginas para descoberta e ranking.

AEO
→ otimizar conteúdo para responder perguntas de forma clara.
```

Eles são complementares.

```text
SEO + AEO
     ↓
Discoverable
+
Understandable
+
Answerable
```

---

# 4. Exemplo

Busca:

```text
"O que é CQRS?"
```

Uma página bem estruturada pode conter:

```text
H1: O que é CQRS?

Resposta curta:
CQRS é um padrão que separa operações de escrita
(commands) das operações de leitura (queries).

Depois:
- como funciona;
- arquitetura;
- exemplo .NET;
- vantagens;
- desvantagens;
- quando usar;
- FAQ.
```

Essa organização beneficia tanto leitores quanto mecanismos automáticos.

---

# 5. SEO Técnico

SEO técnico envolve infraestrutura e implementação.

```text
Crawlability
Indexability
URLs
Canonical
Sitemap
Robots
Performance
Mobile
HTTPS
Structured Data
```

---

# 6. Crawlability

Crawler precisa conseguir navegar pelo site.

Evitar:

```text
links quebrados
rotas inacessíveis
navegação exclusivamente dependente de mecanismos obscuros
bloqueios incorretos
```

---

# 7. Indexability

Nem toda página deve necessariamente ser indexada.

Exemplos geralmente privados:

```text
/admin
/login
/account
/internal
```

Conteúdo público relevante pode ser indexável conforme estratégia.

---

# 8. robots.txt

Pode orientar crawlers.

Exemplo conceitual:

```text
User-agent: *
Disallow: /admin/
```

Não utilizar `robots.txt` como mecanismo de segurança.

---

# 9. Sitemap

Sitemap ajuda mecanismos a descobrir URLs.

```text
/sitemap.xml
```

Um CMS pode gerá-lo automaticamente.

---

# 10. Canonical

Canonical ajuda a indicar URL preferencial quando existem páginas equivalentes ou duplicadas.

```html
<link rel="canonical" href="https://example.com/article" />
```

---

# 11. URLs

Preferir URLs compreensíveis.

Melhor:

```text
/articles/cqrs-dotnet
```

Pior:

```text
/page?id=48291
```

---

# 12. Title

Cada página deve possuir título descritivo.

Exemplo:

```text
CQRS com .NET: arquitetura, exemplos e boas práticas
```

---

# 13. Meta Description

Resumo da página.

Exemplo:

```text
Aprenda como aplicar CQRS em aplicações .NET,
com Commands, Queries, handlers e exemplos práticos.
```

Não tratar meta description como garantia de snippet específico.

---

# 14. Headings

Hierarquia:

```text
H1
 ├── H2
 │    ├── H3
 │    └── H3
 └── H2
```

Evitar estrutura sem hierarquia lógica.

---

# 15. Conteúdo

Conteúdo útil deve responder intenção real.

```text
Question
 ↓
Direct Answer
 ↓
Explanation
 ↓
Example
 ↓
Evidence
 ↓
Related Questions
```

---

# 16. Search Intent

Tipos comuns:

```text
Informational
Navigational
Commercial
Transactional
```

Exemplo:

```text
"o que é Redis"
→ informational

"Redis vs Memcached"
→ comparison/commercial investigation

"Redis documentation"
→ navigational
```

---

# 17. Keyword

Keyword continua útil como representação da intenção.

Evitar:

```text
keyword stuffing
```

O conteúdo deve ser escrito para pessoas e estruturado para máquinas.

---

# 18. Topic Cluster

Organizar conhecimento em tópicos relacionados.

```text
.NET
├── ASP.NET Core
├── CQRS
├── DDD
├── Entity Framework
├── Minimal APIs
└── Testing
```

---

# 19. Pillar Page

Uma página principal pode conectar conteúdos relacionados.

```text
Software Architecture
 ↓
DDD
CQRS
Clean Architecture
Microservices
Event-Driven Architecture
```

Isso cria arquitetura de informação coerente.

---

# 20. Internal Linking

```text
Article A
 ↓
Article B
 ↓
Article C
```

Links internos ajudam navegação e descoberta de conteúdo relacionado.

---

# 21. External References

Conteúdo técnico deve utilizar fontes confiáveis quando necessário.

Preferência:

```text
Official Documentation
Standards
Primary Sources
Vendor Documentation
Research
```

---

# 22. Structured Data

Dados estruturados ajudam sistemas a interpretar entidades e conteúdo.

Tecnologia comum:

```text
JSON-LD
```

---

# 23. Schema.org

Tipos podem incluir:

```text
Article
Organization
Person
Product
FAQPage
BreadcrumbList
SoftwareApplication
```

Usar apenas marcação compatível com o conteúdo real da página.

---

# 24. Exemplo JSON-LD

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "CQRS com .NET"
}
</script>
```

A implementação real deve seguir as propriedades recomendadas para o tipo escolhido.

---

# 25. Breadcrumbs

```text
Home
 >
Architecture
 >
CQRS
```

Podem melhorar navegação e compreensão da estrutura.

---

# 26. AEO e perguntas

Conteúdo orientado a perguntas funciona bem para respostas diretas.

```text
O que é?
Como funciona?
Quando usar?
Quais vantagens?
Quais riscos?
Como implementar?
```

---

# 27. Resposta direta

Exemplo:

```text
## O que é Redis?

Redis é um armazenamento de dados em memória frequentemente
utilizado para cache, sessões, filas e outros cenários de baixa latência.
```

Depois, aprofundar.

---

# 28. FAQ

FAQ pode organizar dúvidas reais.

```text
FAQ
├── O que é?
├── Quando usar?
├── Quanto custa?
├── Como configurar?
└── Quais alternativas?
```

Evitar perguntas artificiais criadas apenas para SEO.

---

# 29. Conteúdo citável

Conteúdo tende a ser mais reutilizável quando possui:

```text
clear definitions
tables
examples
steps
evidence
sources
dates
author information
```

---

# 30. Entidades

Sistemas modernos tentam compreender entidades e relações.

Exemplo:

```text
ASP.NET Core
  ↓
Framework
  ↓
Microsoft
```

Conteúdo claro reduz ambiguidades.

---

# 31. Autoridade

Demonstre experiência através de evidências reais:

```text
Projects
Code
Examples
Benchmarks
Case Studies
References
```

Evitar afirmações inventadas de autoridade.

---

# 32. Atualização

Conteúdo técnico envelhece.

Registrar quando útil:

```text
Published
Updated
Technology Version
```

Exemplo:

```text
.NET 10
```

se o conteúdo for realmente específico dessa versão.

---

# 33. Performance

Performance afeta experiência e pode impactar descoberta/ranking.

Avaliar:

```text
HTML
CSS
JavaScript
Images
Fonts
Caching
CDN
Server Response
```

---

# 34. Core Web Vitals

Indicadores de experiência devem ser acompanhados com ferramentas atuais.

Não otimizar apenas para uma pontuação; investigar o impacto real no usuário.

---

# 35. Imagens

Boas práticas:

```text
correct dimensions
compression
modern formats
lazy loading when appropriate
alt text
```

---

# 36. Alt Text

Alt deve descrever o conteúdo relevante da imagem.

Ruim:

```text
image123
```

Melhor:

```text
Diagrama da arquitetura CQRS com Commands e Queries
```

---

# 37. Mobile

O site deve funcionar corretamente em diferentes tamanhos.

```text
Desktop
Tablet
Mobile
```

---

# 38. HTTPS

Conteúdo público deve utilizar conexão segura.

```text
HTTP
 ↓
HTTPS
```

---

# 39. React e SEO

Aplicações React precisam considerar como o conteúdo público será entregue e descoberto.

Possíveis estratégias:

```text
SSR
SSG
Pre-rendering
Server Components / framework-specific rendering
```

A escolha depende da stack.

---

# 40. SPA

Uma SPA pode exigir cuidados adicionais:

```text
metadata
routing
rendering
crawlability
performance
```

Para um CMS público, avaliar renderização adequada para páginas de conteúdo.

---

# 41. CMS

Um CMS pode possuir campos SEO próprios.

Exemplo:

```text
Page
├── Title
├── Slug
├── Meta Title
├── Meta Description
├── Canonical
├── Indexable
├── Open Graph
├── Structured Data
└── Sitemap Priority
```

---

# 42. Modelo de domínio SEO

Exemplo .NET:

```csharp
public sealed class SeoMetadata
{
    public string? MetaTitle { get; init; }
    public string? MetaDescription { get; init; }
    public string? CanonicalUrl { get; init; }
    public bool Indexable { get; init; }
}
```

---

# 43. Slug

Gerado a partir do título ou definido manualmente.

```text
CQRS com .NET
 ↓
cqrs-com-dotnet
```

Deve possuir regras de unicidade.

---

# 44. Redirect

Ao alterar URL publicada:

```text
Old URL
 ↓
301
 ↓
New URL
```

Isso ajuda usuários e mecanismos a encontrar o novo endereço.

---

# 45. Broken Links

Criar validação periódica:

```text
Site
 ↓
Crawler
 ↓
Broken Links
 ↓
Report
```

---

# 46. Open Graph

Metadados sociais ajudam no compartilhamento.

```text
og:title
og:description
og:image
og:url
```

---

# 47. Social Preview

CMS pode mostrar preview:

```text
Title
Description
Image
URL
```

antes da publicação.

---

# 48. SEO Audit

Workflow:

```text
Crawl
 ↓
Collect
 ↓
Analyze
 ↓
Prioritize
 ↓
Fix
 ↓
Measure
```

---

# 49. Categorias de auditoria

```text
Technical
Content
Performance
Links
Metadata
Structured Data
Accessibility
```

---

# 50. Severity

Classificar problemas:

```text
Critical
High
Medium
Low
Info
```

---

# 51. Exemplo

```text
Issue:
Missing title

Severity:
High

Impact:
Página possui sinal descritivo insuficiente.

Action:
Adicionar title único e relevante.
```

---

# 52. SEO Skill

No Kit:

```text
3-Skills/
└── seo-audit/
    └── SKILL.md
```

Responsabilidades:

```text
crawl
inspect
analyze
prioritize
recommend
validate
```

---

# 53. AEO Skill

Pode existir:

```text
3-Skills/
└── aeo/
    └── SKILL.md
```

Responsabilidades:

```text
question discovery
answer formatting
entity clarity
structured content
source validation
FAQ analysis
```

---

# 54. Content Agent

```text
Content Agent
├── research
├── copywriting
├── seo-audit
└── aeo
```

---

# 55. Workflow de artigo

```text
Topic
 ↓
Search Intent
 ↓
Research
 ↓
Outline
 ↓
Direct Answers
 ↓
Detailed Content
 ↓
Internal Links
 ↓
Metadata
 ↓
Structured Data
 ↓
Review
```

---

# 56. Workflow de conteúdo técnico

```text
Technical Topic
 ↓
Official Sources
 ↓
Definition
 ↓
Architecture
 ↓
Code Example
 ↓
Trade-offs
 ↓
FAQ
 ↓
SEO/AEO Review
```

---

# 57. Aplicação no dia a dia do desenvolvedor

Ao criar página:

```text
Route
 ↓
Semantic HTML
 ↓
Metadata
 ↓
Performance
 ↓
Accessibility
 ↓
Structured Data
 ↓
Sitemap
```

---

# 58. Aplicação no README / documentação pública

Mesmo sem ser SEO tradicional, princípios de clareza ajudam descoberta.

```text
Clear Title
Description
Keywords naturally in context
Examples
Architecture
FAQ
Links
```

---

# 59. Aplicação no LinkedIn

SEO/AEO não deve ser aplicado mecanicamente ao LinkedIn, mas conceitos úteis permanecem:

```text
clear topic
clear answer
entities
keywords
structured explanation
```

---

# 60. IA para conteúdo

IA pode apoiar:

```text
topic research
outline
FAQ discovery
metadata suggestions
content review
internal linking suggestions
```

Mas conteúdo precisa de validação.

---

# 61. IA não deve inventar dados

Especialmente:

```text
statistics
benchmarks
market share
quotes
research
customer results
```

Informações factuais devem possuir fonte adequada.

---

# 62. AEO + RAG

Uma base RAG pode ajudar a produzir conteúdo fundamentado.

```text
Knowledge Base
 ↓
Retriever
 ↓
Evidence
 ↓
Content Agent
 ↓
SEO/AEO
```

---

# 63. Search Analytics

Dados úteis:

```text
Queries
Impressions
Clicks
CTR
Position
Landing Pages
Conversions
```

Analisar tendência ao longo do tempo.

---

# 64. Content Performance

Não medir apenas tráfego.

```text
Traffic
+
Engagement
+
Conversion
+
Business Outcome
```

---

# 65. Content Decay

Conteúdo pode perder relevância.

Workflow:

```text
Old Content
 ↓
Performance Drop
 ↓
Review
 ↓
Update
 ↓
Republish / Maintain
```

---

# 66. Programmatic SEO

Geração automatizada de páginas pode funcionar em cenários legítimos, mas exige qualidade.

Evitar:

```text
milhares de páginas vazias
conteúdo duplicado
conteúdo sem utilidade
```

---

# 67. SEO em arquitetura

SEO precisa aparecer no design da aplicação.

```text
Architecture
├── Rendering
├── Routing
├── Metadata
├── Sitemap
├── Cache
├── CDN
└── Performance
```

Não deixar SEO apenas para o final.

---

# 68. Observabilidade SEO

Automatizar verificações:

```text
Build
 ↓
SEO Checks
 ↓
Broken Links
 ↓
Metadata
 ↓
Performance
 ↓
Report
```

---

# 69. CI/CD

Pipeline pode validar:

```text
broken links
missing metadata
invalid HTML
accessibility
bundle size
performance budget
```

---

# 70. Performance Budget

Exemplo conceitual:

```text
JS Size
Image Size
Page Weight
Response Time
```

Se exceder limite:

```text
Quality Gate → FAIL/WARN
```

---

# 71. Sitemap automático

CMS:

```text
Published Pages
 ↓
Filter Indexable
 ↓
Generate Sitemap
 ↓
Cache
```

---

# 72. robots.txt por ambiente

Exemplo:

```text
DEV → no indexing
HML → no indexing
PROD → according to policy
```

Evita homologação aparecendo em busca.

---

# 73. Canonical por ambiente

URLs canônicas devem apontar para o domínio correto de produção quando aplicável.

Evitar indexação acidental de ambientes temporários.

---

# 74. Multi-language

Para conteúdo multilíngue:

```text
language routes
hreflang
localized metadata
localized content
```

Não utilizar tradução automática sem revisão quando qualidade for importante.

---

# 75. Accessibility

SEO e acessibilidade não são iguais, mas boas práticas frequentemente se complementam.

Exemplos:

```text
semantic HTML
headings
alt text
clear navigation
```

---

# 76. Anti-patterns SEO

Evitar:

```text
keyword stuffing
hidden text
duplicate pages
fake backlinks
doorway pages
copied content
misleading titles
```

---

# 77. Anti-patterns AEO

Evitar:

```text
respostas vagas
FAQ artificial
afirmações sem fonte
conteúdo gerado em massa sem revisão
definições contraditórias
entidades ambíguas
```

---

# 78. Quality Gates

Antes de publicar:

- [ ] title definido;
- [ ] meta description revisada;
- [ ] slug correto;
- [ ] H1 único e coerente;
- [ ] headings estruturados;
- [ ] intenção atendida;
- [ ] resposta principal clara;
- [ ] links internos úteis;
- [ ] imagens otimizadas;
- [ ] alt text adequado;
- [ ] structured data validado quando aplicável;
- [ ] canonical correto;
- [ ] indexação configurada;
- [ ] performance verificada;
- [ ] conteúdo factual validado.

---

# 79. Estrutura no Kit IA Dev

```text
Kit-IA-Dev/
├── 3-Skills/
│   ├── seo-audit/
│   └── aeo/
├── 4-Templates/
│   └── seo-content/
├── 5-Workflows/
│   └── content-publishing/
├── 6-Quality-Gates/
│   └── web-content/
└── 8-Dictionary/
    └── 12-seo-aeo.md
```

---

# 80. Exemplo para um CMS .NET + React

```text
Admin
 ↓
Create Article
 ↓
Content
+
SEO Metadata
+
Structured Data
 ↓
Publish
 ↓
Site
 ↓
Sitemap
 ↓
Search / Answer Engines
```

---

# 81. Campos recomendados no CMS

```text
Title
Slug
Summary
Content
Author
PublishedAt
UpdatedAt
MetaTitle
MetaDescription
CanonicalUrl
Indexable
OpenGraphTitle
OpenGraphDescription
OpenGraphImage
StructuredData
```

---

# 82. API

Exemplo:

```text
GET /api/site/articles/{slug}
```

Resposta pode fornecer:

```text
content
seo metadata
author
dates
structured information
```

---

# 83. Cache

Conteúdo público pode utilizar:

```text
Redis
CDN
HTTP Cache
```

Invalidar cache quando conteúdo publicado for atualizado.

---

# 84. Agente SEO/AEO

Arquitetura:

```text
Article
 ↓
SEO/AEO Agent
 ↓
Technical Checks
 ↓
Content Checks
 ↓
Metadata
 ↓
Recommendations
 ↓
Quality Gate
```

---

# 85. Regra para agentes

Antes de otimizar conteúdo:

1. Qual é o público?
2. Qual é a intenção?
3. Qual pergunta principal será respondida?
4. Qual entidade é central?
5. Existem fontes confiáveis?
6. A resposta principal está clara?
7. O conteúdo possui profundidade suficiente?
8. A página é tecnicamente indexável?
9. Metadados estão corretos?
10. Existe structured data aplicável?
11. Performance está adequada?
12. Há conteúdo duplicado?
13. Existem links internos relevantes?
14. Alguma afirmação foi inventada?

---

# 86. Relação com outros itens

```text
01 - Estrutura de Projeto
03 - Plugins
05 - Conectores e Funções
07 - LinkedIn Manager Agent
09 - Skills
11 - CI/CD
16 - Arquitetura de Aplicações
17 - Agentic AI
18 - Kit IA Dev
```

---

# 87. Resumo

SEO busca tornar conteúdo:

```text
discoverable
+
indexable
+
relevant
```

AEO busca torná-lo:

```text
clear
+
structured
+
answerable
```

Uma aplicação moderna deve combinar:

```text
TECHNICAL SEO
+
CONTENT QUALITY
+
STRUCTURED DATA
+
PERFORMANCE
+
ACCESSIBILITY
+
AEO
```

No Kit IA Dev, SEO/AEO deve entrar no ciclo de desenvolvimento, conteúdo e Quality Gates, e não apenas ser aplicado depois que o site estiver pronto.

---

# 📁 Arquivo

```text
12-seo-aeo.md
```
