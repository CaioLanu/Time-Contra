# Implantação

## Ambientes

| Ambiente | App | Supabase |
| --- | --- | --- |
| Local | `flutter run` no emulador, no aparelho ou no navegador | `supabase start`, em contêineres Docker na máquina |
| Produção | Google Play, App Store e um host do site web, a escolher | Um projeto no Supabase Cloud, com plano a escolher |

O host do site web e o plano do Supabase Cloud estão em aberto em [Riscos](risks.md).

## Entrega

Ainda não há CI nem processo de release. Os gates de cada entrega estão em `AGENTS.md` e `supabase/AGENTS.md`,
na seção Commands.
