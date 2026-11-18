# ADR 0002: Eventos entre módulos com Outbox + RabbitMQ (MassTransit)

- Status: aceito
- Data: 2026-11-17

## Contexto
Módulos precisam reagir a fatos de outros módulos (ex.: conversa encerrada gera métricas e tarefas) sem acoplamento direto e sem perder eventos se o processo cair.

## Decisão
Eventos de integração publicados via Transactional Outbox (MassTransit + EF Core) para RabbitMQ. Consumers idempotentes, com retry e dead-letter queue. Em produção no Azure o transporte pode migrar para Azure Service Bus sem mudar os contratos.

## Consequências
- Entrega at-least-once: todo consumer deve ser idempotente.
- Consistência eventual entre módulos.
- Mais uma peça de infraestrutura a operar e observar.
- A proposta inicial de produto considera mensageria desnecessária no MVP; adotamos por objetivo de aprendizado e por desacoplar módulos.
