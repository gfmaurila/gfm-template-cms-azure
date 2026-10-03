# Arquitetura Azure — GFM.Template.CMS

Este diretório recebe os artefatos de arquitetura gerados após a criação/inspeção da estrutura do projeto.

Artefatos esperados:

- `azure-architecture.drawio` — diagrama principal editável;
- `structurizr/workspace.dsl` — modelo C4/Structurizr quando aplicável;
- diagramas UML e ER definidos pelo fluxo do `prompts.md`;
- ADRs referentes às decisões de arquitetura Azure.

Princípio de implantação:

`LOCAL FIRST → CONTAINER FIRST → CLOUD READY → AZURE TARGET`

O desenvolvimento local não deve depender de uma assinatura Azure real.
