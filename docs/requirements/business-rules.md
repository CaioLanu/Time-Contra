# Regras de negócio

Políticas que valem em qualquer funcionalidade.

<a id="br-01"></a>

## BR-01 — Uso gratuito

Gestores e locatários se cadastram e usam o Time-Contra sem pagar mensalidade ou taxa de cadastro.

| Attribute | Value |
| --- | --- |
| Rationale | A receita vem da comissão por aluguel, não de assinatura |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

<a id="br-02"></a>

## BR-02 — Comissão por aluguel

A plataforma recebe 5% do valor de cada aluguel pago pelo app, descontados do valor repassado ao gestor.

| Attribute | Value |
| --- | --- |
| Rationale | É o modelo de receita do produto; o gestor paga porque a plataforma divulga o campo dele |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M2 |
| Since | v1.0.0 |

<a id="br-03"></a>

## BR-03 — Uma reserva por horário

Um horário de um campo aceita no máximo uma reserva.

| Attribute | Value |
| --- | --- |
| Rationale | Dois times não podem alugar o mesmo campo ao mesmo tempo |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

<a id="br-04"></a>

## BR-04 — Mínimo de dois times por reserva

Uma reserva tem no mínimo dois times e pode ter mais.

| Attribute | Value |
| --- | --- |
| Rationale | Uma partida exige dois times, e grupos maiores dividem o mesmo horário |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

<a id="br-05"></a>

## BR-05 — Um perfil por conta

Cada conta tem exatamente um perfil, gestor ou locatário, que não muda depois do cadastro. Quem é gestor e
locatário usa duas contas, com e-mails diferentes.

| Attribute | Value |
| --- | --- |
| Rationale | Um perfil fixo por conta mantém simples as permissões e o isolamento entre gestores |
| Source | Stakeholder, spec 1.1 de 2026-10-20 (resposta da Q7) |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.1.0 |
