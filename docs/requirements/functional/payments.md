# Pagamentos (PAY)

O controle do pagamento das reservas e o pagamento pelo app.

<a id="fr-pay-01"></a>

## FR-PAY-01 — Registrar pagamento da reserva

> Como gestor, quero marcar se uma reserva foi paga, para saber quem ainda me deve.

O sistema deve permitir ao gestor marcar cada reserva dos seus campos como paga ou pendente.

| Attribute | Value |
| --- | --- |
| Rationale | O gestor controla os pagamentos recebidos |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Should |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-PAY-01.1** — Given uma reserva pendente, when o gestor a marca como paga, then a agenda exibe a reserva como paga.

<a id="fr-pay-02"></a>

## FR-PAY-02 — Pagar a reserva pelo app

> Como locatário, quero pagar a reserva pelo app, para garantir o horário sem acertar à parte com o gestor.

O sistema deve receber o pagamento da reserva, reter a comissão
([BR-02](../business-rules.md#br-02)) e repassar o restante ao gestor.

| Attribute | Value |
| --- | --- |
| Rationale | A comissão da plataforma só é cobrada quando o aluguel é pago pelo app |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M2 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-PAY-02.1** — Given uma reserva de R$ 100,00, when o locatário a paga pelo app, then a reserva fica paga, a plataforma retém R$ 5,00 e o gestor recebe R$ 95,00.
