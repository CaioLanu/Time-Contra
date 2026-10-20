# Busca (SRC)

Como o locatário encontra um campo.

## FR-SRC-01 — Ver campos no mapa

> Como locatário, quero ver no mapa os campos do meu bairro ou zona, para achar um campo perto de mim.

O sistema deve exibir em um mapa os campos do bairro ou da zona que o locatário escolher.

| Attribute | Value |
| --- | --- |
| Rationale | A proximidade é o primeiro critério de quem procura campo |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-SRC-01.1** — Given campos cadastrados em um bairro, when o locatário escolhe esse bairro, then o mapa exibe esses campos.

## FR-SRC-02 — Filtrar por disponibilidade

> Como locatário, quero filtrar os campos por data e horário, para ver só os que estão livres quando meu time pode jogar.

O sistema deve filtrar os campos da busca pelos que têm horário livre na data e hora informadas.

| Attribute | Value |
| --- | --- |
| Rationale | Um campo ocupado no horário do jogo não serve ao locatário |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-SRC-02.1** — Given um campo reservado em uma data e hora, when o locatário filtra por essa data e hora, then esse campo não aparece no resultado.

## FR-SRC-03 — Filtrar por tipo de campo

> Como locatário, quero filtrar os campos pelo tipo, para achar o que serve à modalidade do meu time.

O sistema deve filtrar os campos da busca pelo tipo de campo escolhido.

| Attribute | Value |
| --- | --- |
| Rationale | Cada modalidade exige um tipo de campo |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-SRC-03.1** — Given campos de tipos diferentes, when o locatário filtra por um tipo, then só campos desse tipo aparecem no resultado.

## FR-SRC-04 — Filtrar por estrutura

> Como locatário, quero filtrar os campos por arquibancada, bar e vestiário, para achar um campo com o que meu time precisa.

O sistema deve filtrar os campos da busca pelos itens de estrutura escolhidos.

| Attribute | Value |
| --- | --- |
| Rationale | A estrutura pesa na escolha do campo |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-SRC-04.1** — Given campos com e sem vestiário, when o locatário filtra por vestiário, then só campos com vestiário aparecem no resultado.

## FR-SRC-05 — Ver detalhes do campo

> Como locatário, quero abrir o anúncio de um campo, para decidir se vou alugá-lo.

O sistema deve exibir o anúncio do campo com endereço, tipo, estrutura, preço e horários livres.

| Attribute | Value |
| --- | --- |
| Rationale | O locatário decide o aluguel a partir desses dados |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-SRC-05.1** — Given um campo no resultado da busca, when o locatário o abre, then o anúncio exibe endereço, tipo, estrutura, preço e horários livres.
