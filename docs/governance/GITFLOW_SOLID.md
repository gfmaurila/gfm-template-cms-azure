# GFM.Template.CMS — SOLID, GitFlow e Governança de Entrega


Este projeto adota **SOLID** como padrão obrigatório de design e **GitFlow** como fluxo oficial de versionamento e promoção entre ambientes.

## SOLID obrigatório

Toda implementação e revisão deve verificar:

- **SRP — Single Responsibility Principle**: cada classe/módulo possui uma responsabilidade clara;
- **OCP — Open/Closed Principle**: extensões devem evitar alterações desnecessárias em código estável;
- **LSP — Liskov Substitution Principle**: implementações devem respeitar os contratos das abstrações;
- **ISP — Interface Segregation Principle**: interfaces pequenas e específicas, sem contratos genéricos excessivos;
- **DIP — Dependency Inversion Principle**: Domain/Application dependem de abstrações, nunca diretamente de detalhes de Infrastructure.

SOLID é critério obrigatório nos Quality Gates e no AI Code Review. Violações relevantes devem ser corrigidas antes do merge.

## Branches permanentes

```text
main      -> produção
hml       -> homologação
develop   -> desenvolvimento/integração
```

`main`, `hml` e `develop` são protegidas. É proibido implementar diretamente ou fazer push direto nessas branches. Alterações entram por Pull Request.

## Fluxo obrigatório por Task

Cada task deve partir de `develop` e possuir branch própria:

```text
develop
   |
   +--> feature/task-XXXX-descricao
              |
              +--> implementação
              +--> testes
              +--> commit
              +--> push
              +--> Pull Request -> develop
                         |
                         +--> AI Code Review
                         +--> Quality Gates
                         +--> correções, se necessárias
                         +--> merge
```

Convenção: `feature/task-0001-create-auth-api`, `feature/task-0002-user-domain`, `feature/task-0003-azure-blob-storage`.

A IA deve executar `commit` e `push` da branch da task e criar o Pull Request. A IA deve revisar o PR e validar build, testes, arquitetura, SOLID, segurança, qualidade, documentação e impactos antes de permitir o merge.

## Promoção e Release

```text
feature/task-*
      |
      v
   develop
      | PR
      v
     hml
      | homologação aprovada
      v
release/1.0.0.0
      | PR + Quality Gates
      v
     main
      |
      +--> tag v1.0.0.0
      +--> produção
```

A branch `release/MAJOR.MINOR.PATCH.BUILD` deve ser criada a partir do conteúdo homologado em `hml`. Após aprovação, a IA cria PR da release para `main`. Depois do merge, deve criar a tag correspondente e garantir a sincronização necessária com `develop`/`hml`, evitando divergência entre as linhas de desenvolvimento e produção.

Versionamento oficial: `MAJOR.MINOR.PATCH.BUILD`, por exemplo `1.0.0.0`, `1.0.0.1`, `1.0.1.0`, `1.1.0.0`, `2.0.0.0`.

## Hotfix

Correções urgentes de produção usam `hotfix/<versao>-descricao`, partindo de `main`. O hotfix deve passar por PR, AI Code Review e Quality Gates e, após produção, ser sincronizado de volta para `develop` e `hml`.

## Regra de automação da IA

A IA pode operar Git/GitHub para executar o fluxo, mas nunca deve contornar proteção de branch, aprovação obrigatória ou Quality Gate. Quando credenciais/permissões não estiverem disponíveis, deve preparar os commits/branches e informar exatamente a ação externa pendente, sem simular sucesso.
