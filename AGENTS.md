# Time-Contra

Marketplace de aluguel de campos de futebol: o gestor anuncia o campo e controla a agenda, o locatário busca no
mapa e reserva. Os requisitos estão em [docs/requirements/](docs/requirements/README.md).

## Stack

- **App:** Flutter, um código só para Android, iOS e web.
- **Backend:** Supabase: Postgres com PostGIS, Auth, Storage e Edge Functions. As regras dessa parte estão em
  [supabase/AGENTS.md](supabase/AGENTS.md).
- **Estado e injeção de dependência:** `ChangeNotifier` e `package:provider`.
- **Pacotes:** pub, pelo Flutter SDK.

## Linguagens e scripts

- O app é escrito em Dart. O backend é SQL (migrations) e TypeScript (Edge Functions).
- Um script novo do repo é escrito em Dart e roda com `dart run`.

## Commands

O projeto Flutter ainda não foi criado e o Flutter SDK não está instalado nesta máquina, então nenhum gate roda
ainda. Cada um entra aqui, com o comando exato, na entrega que cria o app.

| Gate | Command |
| --- | --- |
| Static analysis | pendente: o projeto Flutter não existe |
| Type check | pendente: o projeto Flutter não existe |
| Formatting | pendente: o projeto Flutter não existe |
| Build | pendente: o projeto Flutter não existe |
| Tests | pendente: o projeto Flutter não existe |
| Docs site | pendente: entra com o site de docs |

## Architecture

O app segue o [guia de arquitetura do Flutter](https://docs.flutter.dev/app-architecture/guide), no layout do
[estudo de caso](https://docs.flutter.dev/app-architecture/case-study) dele. O fluxo de dados é sempre:

```text
view → view model → repository → service → Supabase
```

### Onde cada arquivo novo vai

| Arquivo | Lugar |
| --- | --- |
| Tela de uma feature e seus widgets | `lib/ui/<feature>/widgets/<feature>_screen.dart` |
| View model de uma tela | `lib/ui/<feature>/view_models/` |
| Widget ou tema usado por mais de uma feature | `lib/ui/core/ui/`, `lib/ui/core/themes/` |
| Tipo de dado do app | `lib/domain/models/` |
| Use-case | `lib/domain/use_cases/` |
| Fonte da verdade de um tipo de dado | `lib/data/repositories/` |
| Acesso a uma fonte de dados (Supabase, plataforma) | `lib/data/services/` |
| Formato de dado da API | `lib/data/model/` |
| Rotas | `lib/routing/` |
| Teste | `test/`, espelhando `lib/`; fakes em `testing/` |

As features de `lib/ui/` são as áreas do SRS: `accounts`, `fields`, `search`, `bookings`, `payments`,
`analytics`, `tournaments`.

### Quem importa quem

- Um arquivo em `ui/<feature>/widgets/` importa só o view model da sua tela, `ui/core/` e `domain/models/`.
  Nunca importa `data/`.
- Um view model importa `data/repositories/`, `domain/use_cases/` e `domain/models/`. Nunca importa
  `data/services/` nem `supabase_flutter`.
- Cada view tem exatamente um view model.
- Um repository importa `data/services/`, `data/model/` e `domain/models/`. Nunca importa outro repository nem
  `ui/`. Dados de dois repositories se juntam no view model ou num use-case.
- Só `data/services/` importa `supabase_flutter`. Um service não guarda estado e cobre uma fonte de dados.
- `domain/` não importa `ui/` nem `data/`.
- Um use-case só existe quando a lógica junta repositories ou é usada por mais de um view model.
- Uma regra que o banco pode garantir (uma constraint ou uma policy de RLS) fica no Postgres, não no app.

## Branches

`main` é o único branch de longa duração, e todo PR vai para ela. Ela ainda não tem proteção configurada.

## Design

As telas são desenhadas no Figma. Os links dos arquivos e as imagens exportadas ficam em
[docs/design/](docs/design/README.md).

## Language

O repo é em PT-BR: docs, textos da interface e este arquivo. Código, nomes de arquivos e pastas, branches e
commits são em inglês.
