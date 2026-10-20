# Campeonatos (TRN)

Campeonatos disputados em um campo, criados pelo locatário ou pelo gestor.

<a id="fr-trn-01"></a>

## FR-TRN-01 — Campeonato do locatário

> Como locatário, quero criar um campeonato com times que eu já tenho, para organizar os jogos entre eles no campo que aluguei.

O sistema deve permitir ao locatário criar um campeonato com os times que ele indicar.

| Attribute | Value |
| --- | --- |
| Rationale | Grupos de times fechados alugam campo para disputar campeonato |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Could |
| Status | approved |
| Milestone | M2 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-TRN-01.1** — Given um locatário autenticado, when ele cria um campeonato indicando os times, then o campeonato fica registrado com esses times.

<a id="fr-trn-02"></a>

## FR-TRN-02 — Campeonato do gestor

> Como gestor, quero criar um campeonato no meu campo com vagas abertas, para atrair times.

O sistema deve permitir ao gestor criar um campeonato em um campo seu com um número de vagas para times.

| Attribute | Value |
| --- | --- |
| Rationale | O gestor gera receita organizando campeonatos |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Could |
| Status | approved |
| Milestone | M2 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-TRN-02.1** — Given um gestor autenticado, when ele cria um campeonato com N vagas, then o campeonato aparece para os locatários com N vagas abertas.

<a id="fr-trn-03"></a>

## FR-TRN-03 — Inscrição em vaga paga

> Como locatário, quero inscrever meu time em uma vaga de campeonato, para participar dele.

O sistema deve permitir ao locatário inscrever um time em uma vaga aberta mediante o pagamento da inscrição pelo app.

| Attribute | Value |
| --- | --- |
| Rationale | As vagas do campeonato do gestor são pagas |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Could |
| Status | approved |
| Milestone | M2 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-TRN-03.1** — Given um campeonato com uma vaga aberta, when o locatário paga a inscrição, then o time ocupa a vaga e o campeonato tem uma vaga a menos.
