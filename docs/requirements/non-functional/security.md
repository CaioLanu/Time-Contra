# Segurança (SEC)

Quem pode ver e alterar cada dado.

## NFR-SEC-01 — Isolamento entre gestores

O sistema deve restringir cada gestor às reservas, pagamentos e anúncios dos seus próprios campos.

| Attribute | Value |
| --- | --- |
| Rationale | A agenda e os pagamentos de um gestor são dados do negócio dele e incluem dados pessoais de locatários (LGPD) |
| Source | Restrição de LGPD, ver [overview](../overview.md#restrições) |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

**Acceptance criteria**
- **NFR-SEC-01.1** — Given dois gestores, when um deles tenta abrir a agenda de um campo do outro, then o acesso é negado em 100% das tentativas.
