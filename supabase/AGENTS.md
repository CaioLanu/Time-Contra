# supabase/

O backend: o schema do Postgres, as policies de acesso e as Edge Functions.

## Stack

- Supabase CLI para o ambiente local e as migrations.
- Postgres com a extensão PostGIS para a busca por localização.
- Edge Functions em TypeScript, executadas pelo Deno.

## Conventions

- O schema só muda por migration em `supabase/migrations/`, criada com `supabase migration new <name>`.
- Toda tabela tem RLS ligado e uma policy por operação permitida (NFR-SEC-01).
- Uma regra de negócio que uma constraint consegue garantir é uma constraint, como a reserva única por horário
  (BR-03).
- Uma Edge Function existe só para o que precisa de segredo ou de terceiro, como o gateway de pagamento (M2).

## Commands

O `supabase init` ainda não rodou, e o Supabase CLI e o Deno não estão instalados nesta máquina.

| Gate | Command |
| --- | --- |
| Static analysis | pendente: `supabase/` não foi inicializado |
| Type check | pendente: nenhuma Edge Function existe |
| Formatting | pendente: nenhuma Edge Function existe |
| Tests | pendente: `supabase/` não foi inicializado |

## Architecture

| Arquivo | Lugar |
| --- | --- |
| Configuração do projeto local | `supabase/config.toml` |
| Migration | `supabase/migrations/<timestamp>_<name>.sql` |
| Dados de desenvolvimento | `supabase/seed.sql` |
| Edge Function | `supabase/functions/<name>/index.ts` |

- O app fala com o Supabase só pelos services de `lib/data/services/`.
- Uma Edge Function é chamada por um service do app ou pelo webhook de um terceiro. Ela nunca chama outra.
