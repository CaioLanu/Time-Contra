# Contas (ACC)

Cadastro, entrada e perfis de quem usa o Time-Contra.

## FR-ACC-01 — Cadastro com perfil

> Como pessoa sem conta, quero me cadastrar como gestor ou como locatário, para usar as funções do meu perfil.

O sistema deve permitir criar uma conta com um dos perfis: gestor ou locatário.

| Attribute | Value |
| --- | --- |
| Rationale | Os dois lados do marketplace usam funções diferentes |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-ACC-01.1** — Given uma pessoa sem conta, when ela conclui o cadastro escolhendo um perfil, then a conta é criada com o perfil escolhido.

## FR-ACC-02 — Entrar na conta

> Como usuário cadastrado, quero entrar na minha conta, para acessar as minhas informações.

O sistema deve autenticar o usuário cadastrado antes de liberar as funções do seu perfil.

| Attribute | Value |
| --- | --- |
| Rationale | Reservas, pagamentos e agenda são dados de uma pessoa |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-ACC-02.1** — Given uma conta existente, when o usuário informa credenciais válidas, then ele acessa as funções do seu perfil.
- **FR-ACC-02.2** — Given uma conta existente, when o usuário informa credenciais inválidas, then o acesso é negado.

## FR-ACC-03 — Funções por perfil

> Como gestor, quero que só gestores acessem a gestão de campos, para que locatários não alterem meus dados.

O sistema deve oferecer a cada usuário somente as funções do seu perfil.

| Attribute | Value |
| --- | --- |
| Rationale | Gestor e locatário têm permissões diferentes |
| Source | Stakeholder, entrevista de 2026-10-20 |
| Priority | Must |
| Status | approved |
| Milestone | M1 |
| Since | v1.0.0 |

**Acceptance criteria**
- **FR-ACC-03.1** — Given um locatário autenticado, when ele tenta abrir uma função de gestor, then o acesso é negado.
