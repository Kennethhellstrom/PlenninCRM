# ADR 0003: Estratégia de merge

- Status: aceito
- Data: 2026-11-17

## Contexto
Adotamos GitFlow (`main`, `develop`, `feature/*`, `release/*`, `hotfix/*`). Precisamos definir como cada tipo de branch entra no destino. O ruleset inicial ativava histórico linear, o que proíbe merge commit.

## Decisão
- `feature/*` → `develop`: **squash merge**. Cada feature vira um commit limpo e rastreável até a issue.
- `release/*` e `hotfix/*` → `main` e `develop`: **merge commit**. O commit de merge marca o release e liga `main` a `develop`, o que mantém os dois históricos conectados.
- A regra de histórico linear do ruleset é removida de `main` e `develop`.

## Alternativas consideradas
- **Histórico linear (squash/rebase em tudo):** histórico mais limpo, mas após cada release `main` e `develop` divergem e exigem sincronização extra. O GitFlow perde seu principal artefato, o merge de release.
- **Trunk-based:** mais simples e comum em times com deploy contínuo. Não é a prática que queremos estudar neste projeto.

## Consequências
- O histórico de `develop` e `main` tem merge commits de release e hotfix.
- Todo release ou hotfix exige um PR de volta para `develop`.
- Conventional Commits nos squash commits permitem gerar changelog automaticamente no futuro.
