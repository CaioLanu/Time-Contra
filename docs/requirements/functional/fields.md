# Campos (FLD)

O cadastro de cada campo pelo gestor, que vira o anúncio visto pelos locatários.

## FR-FLD-01 — Cadastrar campo

> Como gestor, quero cadastrar meu campo, para que locatários o encontrem.

O sistema deve permitir ao gestor cadastrar um campo com endereço, tipo de campo e estrutura.

| Attribute | Value |
| --- | --- |
| Rationale | Sem campos cadastrados não há o que buscar nem alugar |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-FLD-01.1** — Given um gestor autenticado, when ele cadastra um campo com endereço, tipo e estrutura, then o anúncio do campo fica disponível na busca.

## FR-FLD-02 — Editar campo

> Como gestor, quero editar os dados do meu campo, para manter o anúncio correto.

O sistema deve permitir ao gestor alterar o endereço, o tipo e a estrutura de um campo seu.

| Attribute | Value |
| --- | --- |
| Rationale | Estrutura e dados de um campo mudam com o tempo |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-FLD-02.1** — Given um campo do gestor, when ele altera a estrutura, then o anúncio passa a exibir a estrutura nova.

## FR-FLD-03 — Definir horários disponíveis

> Como gestor, quero definir os dias e horários em que meu campo pode ser alugado, para receber reservas só quando o campo está livre.

O sistema deve permitir ao gestor definir os horários disponíveis de cada campo seu.

| Attribute | Value |
| --- | --- |
| Rationale | A busca por disponibilidade e as reservas dependem desses horários |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-FLD-03.1** — Given um campo do gestor, when ele define um horário disponível, then esse horário aparece como livre para os locatários.

## FR-FLD-04 — Definir preço do aluguel

> Como gestor, quero definir o preço do aluguel do meu campo, para que o locatário saiba quanto vai pagar.

O sistema deve permitir ao gestor definir o preço do aluguel de cada campo seu conforme o número de times da reserva.

| Attribute | Value |
| --- | --- |
| Rationale | O locatário compara campos pelo preço, e mais times numa reserva podem mudar o valor |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-FLD-04.1** — Given um campo do gestor, when ele define o preço, then o anúncio exibe esse preço.
- **FR-FLD-04.2** — Given um campo com preços diferentes para 2 e para 3 times, when o locatário informa 3 times, then o valor da reserva é o preço de 3 times.
