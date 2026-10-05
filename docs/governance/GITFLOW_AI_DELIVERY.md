# GitFlow + AI Delivery

## Branches permanentes
- `main`: produção.
- `develop`: integração e desenvolvimento.
- `hml`: homologação.

## Branches de trabalho
- `feature/task-<id>-<slug>`: task/funcionalidade criada de `develop`.
- `bugfix/task-<id>-<slug>`: correção comum criada de `develop`.
- `hotfix/<versao-ou-slug>`: correção urgente de produção.
- `release/X.Y.Z.B`: preparação de versão homologada para produção.

## Fluxo de uma task
1. Atualizar `develop`.
2. Criar `feature/task-...`.
3. Implementar com SOLID, DDD, CQRS e Clean Code.
4. Executar lint/format, build, Unit Tests, Integration Tests, Architecture Tests e security checks.
5. Atualizar documentação.
6. Commit usando Conventional Commits.
7. Push da branch de trabalho.
8. Criar PR para `develop`.
9. AI Reviewer valida requisitos, testes, segurança, arquitetura e SOLID.
10. Corrigir reprovações e repetir gates.
11. Merge somente com checks/reviews aprovados.

## HML
Promoção por PR `develop -> hml`; merge dispara pipeline do GitHub Environment `hml`.

## Produção
Após homologação, criar `release/X.Y.Z.B`, atualizar changelog/release notes e executar todos os gates. Abrir PR para `main`. Após aprovação e merge, criar tag `vX.Y.Z.B`, GitHub Release e deploy no Environment `production`.

## Proteções
Nunca realizar push direto em `main`, `develop` ou `hml`. A IA pode criar commits, fazer push e abrir/atualizar PRs quando autorizada, mas nunca contornar branch protection, approvals ou required checks.

## Ambientes Azure

| Ambiente | Branch | Azure principal |
|---|---|---|
| Local | `feature/*` | Docker Compose + Azurite |
| Integração | `develop` | Azure Container Apps (dev) |
| Homologação | `hml` | Azure Container Apps (hml) |
| Produção | `main` / `vX.Y.Z.B` | Azure Container Apps / AKS (prod) |

Autenticação com Azure via **OpenID Connect** (`azure/login-action` com `id-token: write`).
Segredos em **Azure Key Vault**; imagens em **Azure Container Registry (ACR)**.