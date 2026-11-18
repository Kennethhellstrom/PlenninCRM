# Plennin

Plennin é um SaaS multi-tenant de CRM + WebChat para clínicas. Também é um projeto de estudo: o objetivo é praticar
arquitetura, CI/CD, nuvem, mensageria e boas práticas como em um time de produto real.

Documentação de produto: ver `docs/` (a proposta de negócio completa é mantida fora do repositório).
Decisões de arquitetura: [`docs/adr/`](docs/adr/).

## Stack
.NET 10 (ASP.NET Core, EF Core) · PostgreSQL · SignalR · RabbitMQ + MassTransit · React + TypeScript · Docker · Azure

## Fluxo de trabalho (GitFlow)
| Branch | Uso |
|---|---|
| `main` | Produção. Só recebe `release/*` e `hotfix/*`. Cada merge recebe tag `vX.Y.Z`. |
| `develop` | Integração. Deploy automático em staging. |
| `feature/<issue>-<slug>` | Nova funcionalidade, sai de `develop`, volta por PR. |
| `release/X.Y.Z` | Estabilização, sai de `develop`, merge em `main` e `develop`. |
| `hotfix/<slug>` | Correção urgente, sai de `main`, merge em `main` e `develop`. |

Commits seguem [Conventional Commits](https://www.conventionalcommits.org/) (`feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`, `ci:`).
Toda mudança entra por Pull Request com CI verde.

### Feature
1. Crie `feature/<issue>-<slug>` a partir de `develop`.
2. Faça commits pequenos, no padrão Conventional Commits.
3. Abra um PR para `develop` e aguarde o CI verde.
4. Faça o merge (squash) e apague a branch.

### Release
Gerada ao concluir uma fase do roadmap, quando `develop` está estável.
1. Crie `release/X.Y.Z` a partir de `develop`. Nela entram apenas correções finais e o ajuste de versão.
2. Abra um PR de `release/X.Y.Z` para `main` e faça o merge (merge commit).
3. Crie a tag `vX.Y.Z` em `main` e publique o release no GitHub.
4. Abra um PR de `release/X.Y.Z` para `develop`, para que as correções feitas na release não se percam.
5. Apague a branch `release/X.Y.Z`.

### Hotfix
Apenas para um bug em produção que não pode esperar a próxima release.
1. Crie `hotfix/<slug>` a partir de `main`.
2. Corrija e adicione um teste que reproduza o bug.
3. Abra um PR para `main` e faça o merge (merge commit).
4. Crie a tag `vX.Y.Z` (incrementa o PATCH) e publique o release.
5. Abra um PR de `hotfix/<slug>` para `develop`. Sem esse passo, o bug volta no próximo release.
6. Apague a branch `hotfix/<slug>`.

### Versionamento
[SemVer](https://semver.org/lang/pt-BR/) (`vMAJOR.MINOR.PATCH`). Até o `v1.0.0` o produto está em desenvolvimento:
- Cada fase do roadmap concluída gera um MINOR (`v0.1.0`, `v0.2.0`, ...).
- Cada hotfix gera um PATCH (`v0.1.1`).
- O `v1.0.0` marca o lançamento para uso real.

### Estratégia de merge
| Origem → destino | Método |
|---|---|
| `feature/*` → `develop` | Squash: um commit limpo por feature |
| `release/*` → `main` e `develop` | Merge commit: preserva o marco do release |
| `hotfix/*` → `main` e `develop` | Merge commit |

Motivação e consequências em [ADR 0003](docs/adr/0003-merge-strategy.md).

## Roadmap
Ver milestones no GitHub (Fase 0 a Fase 11).
