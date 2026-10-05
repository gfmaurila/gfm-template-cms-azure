# KNOWLEDGE CONFLICTS

| Origem | Tipo | Descrição | Decisão | Justificativa |
|---|---|---|---|---|
| 20-setup-aws.md vs. arquitetura do projeto | CLOUD | O dicionário descreve setup AWS (S3/RDS/SQS/SNS/Lambda/ECS/LocalStack). | ADAPT | O projeto tem Azure como plataforma alvo. Toda decisão de cloud foi mapeada para o serviço Azure equivalente, conforme `KNOWLEDGE_DECISIONS.md`. Nenhuma dependência AWS foi introduzida. |
| 09-27-skills.md vs. `.claude/skills/` | SKILLS | O dicionário descreve um catálogo amplo de skills. | ADAPT | Foram instaladas as 10 Skills do Kit IA Dev (`3-Skills`), que são agnósticas de cloud e compatíveis com o padrão do Kit. Skills específicas de AWS foram substituídas por equivalentes Azure quando necessárias. |
| prompts.md §5 vs. README.md | ORDEM | O `prompts.md` lista `PROJECT_STRUCTURE.md`/`PROJECT_SKILLS.md` na raiz; a documentação foi organizada em `docs/`. | ADAPT | Documentação passou a residir em `docs/architecture/`, `docs/project/` e `docs/ai/`, conforme o padrão de organização documental. `prompts.md` e `README.md` permanecem na raiz. |
| README.md vs. diagramas | DOC | Os diagramas PNG estavam na raiz de `docs/`. | ADAPT | Movidos para `docs/architecture/diagrams/` e para `docs/architecture/` (diagramas Azure), mantendo os `.drawio` editáveis. |
| `docs/prompts.md` vs. `prompts.md` | SYNC | Existia uma cópia divergente de `prompts.md` em `docs/`. | RESOLVED | `docs/prompts.md` passa a ser espelho exato de `prompts.md` para eliminar divergência silenciosa. |