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

## Roadmap
Ver milestones no GitHub (Fase 0 a Fase 11).
