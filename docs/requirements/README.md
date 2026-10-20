# Time-Contra — Software Requirements Specification

**Version:** 1.0.0 · **Date:** 2026-10-20 · [Changelog](CHANGELOG.md)

## Purpose

Quem quer alugar um campo de futebol para o seu time não tem um lugar único para achar campos livres perto de
casa. Quem administra campos controla reservas e pagamentos à mão. O Time-Contra liga os dois lados: o gestor
anuncia o campo e controla a agenda, e o locatário encontra e reserva.

## Scope

Em escopo:

- Contas com dois perfis: gestor e locatário.
- Cadastro de campos com horários e preço.
- Busca no mapa com filtros.
- Reservas com dois ou mais times e agenda do gestor, com registro de pagamento.
- Contagem de visualizações do anúncio.
- Pagamento pelo app com comissão de 5%, a partir do M2.
- Campeonatos, a partir do M2.

Fora de escopo:

- Stack e hospedagem: são decisões de arquitetura, registradas em `AGENTS.md` e em
  [architecture](../architecture/README.md).

## Contents

[Overview](overview.md) · [Glossary](glossary.md) · [Business rules](business-rules.md) ·
[Open questions](open-questions.md)

## Requirements

| ID | Name | Priority | Status | Milestone |
| --- | --- | --- | --- | --- |
| [FR-ACC-01](functional/accounts.md#fr-acc-01) | Cadastro com perfil | Must | approved | M1 |
| [FR-ACC-02](functional/accounts.md#fr-acc-02) | Entrar na conta | Must | approved | M1 |
| [FR-ACC-03](functional/accounts.md#fr-acc-03) | Funções por perfil | Must | approved | M1 |
| [FR-FLD-01](functional/fields.md#fr-fld-01) | Cadastrar campo | Must | approved | M1 |
| [FR-FLD-02](functional/fields.md#fr-fld-02) | Editar campo | Must | approved | M1 |
| [FR-FLD-03](functional/fields.md#fr-fld-03) | Definir horários disponíveis | Must | approved | M1 |
| [FR-FLD-04](functional/fields.md#fr-fld-04) | Definir preço do aluguel | Must | approved | M1 |
| [FR-SRC-01](functional/search.md#fr-src-01) | Ver campos no mapa | Must | approved | M1 |
| [FR-SRC-02](functional/search.md#fr-src-02) | Filtrar por disponibilidade | Must | approved | M1 |
| [FR-SRC-03](functional/search.md#fr-src-03) | Filtrar por tipo de campo | Must | approved | M1 |
| [FR-SRC-04](functional/search.md#fr-src-04) | Filtrar por estrutura | Must | approved | M1 |
| [FR-SRC-05](functional/search.md#fr-src-05) | Ver detalhes do campo | Must | approved | M1 |
| [FR-BKG-01](functional/bookings.md#fr-bkg-01) | Reservar horário | Must | approved | M1 |
| [FR-BKG-02](functional/bookings.md#fr-bkg-02) | Agenda do gestor | Must | approved | M1 |
| [FR-BKG-03](functional/bookings.md#fr-bkg-03) | Informar número de times | Must | approved | M1 |
| [FR-PAY-01](functional/payments.md#fr-pay-01) | Registrar pagamento da reserva | Should | approved | M1 |
| [FR-PAY-02](functional/payments.md#fr-pay-02) | Pagar a reserva pelo app | Must | approved | M2 |
| [FR-ANL-01](functional/analytics.md#fr-anl-01) | Contar visualizações do anúncio | Could | approved | M1 |
| [FR-TRN-01](functional/tournaments.md#fr-trn-01) | Campeonato do locatário | Could | approved | M2 |
| [FR-TRN-02](functional/tournaments.md#fr-trn-02) | Campeonato do gestor | Could | approved | M2 |
| [FR-TRN-03](functional/tournaments.md#fr-trn-03) | Inscrição em vaga paga | Could | approved | M2 |
| [NFR-INTR-01](non-functional/interaction-capability.md#nfr-intr-01) | Uso no celular | Must | approved | M1 |
| [NFR-SEC-01](non-functional/security.md#nfr-sec-01) | Isolamento entre gestores | Must | approved | M1 |
| [BR-01](business-rules.md#br-01) | Uso gratuito | Must | approved | M1 |
| [BR-02](business-rules.md#br-02) | Comissão por aluguel | Must | approved | M2 |
| [BR-03](business-rules.md#br-03) | Uma reserva por horário | Must | approved | M1 |
| [BR-04](business-rules.md#br-04) | Mínimo de dois times por reserva | Must | approved | M1 |
