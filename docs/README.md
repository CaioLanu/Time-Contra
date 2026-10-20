# Documentação do Time-Contra

O Time-Contra é um marketplace de aluguel de campos de futebol. Esta pasta reúne tudo o que se decide sobre ele
antes e durante a construção.

## Mapa

| Pasta | O que tem |
| --- | --- |
| [Requisitos](requirements/README.md) | O SRS versionado: o que o produto faz, com IDs e critérios de aceite |
| [Arquitetura](architecture/README.md) | Os blocos do sistema, como conversam e onde rodam (arc42 e C4) |
| [Modelo de dados](data-model/README.md) | Entidades, relações, invariantes e armazenamento |
| [Design](design/README.md) | Marca, tokens e as telas de cada feature, desenhadas no Figma |
| [Roadmap](roadmap/README.md) | Marcos, épicos, cobertura dos requisitos e o plano de cada sprint |

As specs (`specs/`) e as ADRs (`decisions/`) nascem no primeiro `/tightship:spec`.

## Abrir o site local

Com o [uv](https://docs.astral.sh/uv/) instalado, rode na raiz do repo:

```sh
uvx zensical==0.0.71 serve --open
```

O site abre em `http://localhost:8000`, com busca e tema claro ou escuro. No VS Code, a task `docs: serve` roda o
mesmo comando.
