# ADR 0001: Monólito modular

- Status: aceito
- Data: 2026-11-17

## Contexto
O produto é um SaaS multi-tenant com um fluxo principal bem definido. A equipe é de uma pessoa e o objetivo inclui aprender operação e evolução de arquitetura.

## Decisão
Uma única aplicação ASP.NET Core dividida em módulos (Tenancy, Identity, Chat, CRM, Scheduling, Reporting), cada um com suas camadas Domain/Application/Infrastructure. Módulos não referenciam as entranhas uns dos outros; comunicam-se por contratos públicos e eventos.

## Consequências
- Deploy e operação simples.
- Fronteiras verificadas por testes de arquitetura.
- Extração futura de um módulo em serviço é possível se houver requisito mensurável de escala ou isolamento.
