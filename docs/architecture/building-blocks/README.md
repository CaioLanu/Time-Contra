# Blocos

| Bloco | Tecnologia | Responsabilidade | Fala com | Marco |
| --- | --- | --- | --- | --- |
| [App](app.md) | Flutter (Dart) | Telas do gestor e do locatário em Android, iOS e web | Supabase (HTTPS), provedor de mapas (HTTPS) | M1 |
| [Supabase Auth](supabase.md#auth) | Supabase | Cadastro, login e sessão | App (HTTPS) | M1 |
| [Banco](supabase.md#banco) | Postgres com PostGIS | Dados, constraints e policies de RLS | App, pela API REST do Supabase (HTTPS) | M1 |
| [Edge Functions](supabase.md#edge-functions) | TypeScript no Deno | Pagamento e repasse | App (HTTPS), gateway de pagamento (HTTPS e webhook), banco (SQL) | M2 |
