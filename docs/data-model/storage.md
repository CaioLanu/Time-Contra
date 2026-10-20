# Armazenamento

- **Motor:** Postgres gerenciado pelo Supabase, com a extensão PostGIS para localização e distância.
- **Migrations:** em `supabase/migrations/`, criadas com o Supabase CLI. Nenhuma existe ainda.
- **Políticas de acesso:** RLS em toda tabela, como descreve [Segurança](../architecture/concepts/security.md).
- **Arquivos:** bucket `avatars` no Storage, `avatars/<id do usuário>/`, uma foto JPEG ou PNG de até 5 MB, gravada no cadastro e lida só pelo dono.
- **Índices:** definidos com a primeira migration, a partir dos [padrões de acesso](access-patterns.md).
