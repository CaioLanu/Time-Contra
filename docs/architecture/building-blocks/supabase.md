# Supabase

O backend gerenciado: login, banco e as funções de servidor. O código fica em `supabase/`, com regras próprias em
`supabase/AGENTS.md`.

## Auth

Cadastro, login e sessão de gestores e locatários (FR-ACC-01, FR-ACC-02). Os provedores são e-mail e senha,
com confirmação do e-mail por link, Google e Apple. O perfil de cada usuário fica na tabela `profiles`, ligada
ao usuário do Auth. Detalhes na [spec 1.1](../../specs/1-accounts-access/sign-up-and-sign-in.md).

## Storage

O bucket `avatars` guarda as fotos de perfil, uma pasta por usuário, que só o dono lê e grava. M1.

## Banco

Postgres com a extensão PostGIS. Guarda campos, horários, preços, reservas e visualizações, e garante:

- uma reserva por horário de cada campo, por constraint (BR-03);
- no mínimo dois times por reserva, por constraint (BR-04);
- cada gestor só alcança os dados dos próprios campos, por RLS (NFR-SEC-01).

O app lê e grava pela API REST que o Supabase gera a partir do schema. O modelo está em
[Modelo de dados](../../data-model/README.md).

## Edge Functions

M2. Funções em TypeScript que recebem o pagamento da reserva pelo gateway, retêm a comissão de 5% e repassam o
restante ao gestor (FR-PAY-02, BR-02). Só elas guardam a chave do gateway.

## O que nunca faz

- Uma Edge Function não chama outra.
- O schema não muda fora de uma migration.
