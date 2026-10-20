# 1.1 — Criar conta e entrar (gestor e locatário)

> **Status:** closed
> **Perfil:** UI
> **Módulo:** `lib/ui/accounts/`, `lib/data/`, `supabase/`
> **Épico:** —
> **Requisitos:** FR-ACC-01, FR-ACC-02, FR-ACC-03, BR-01, BR-05, NFR-INTR-01
> **Sprint:** 1

## Critérios de aceite

### Referência visual

N/A: ainda não há telas no Figma. O layout segue as regras desta spec e a largura de 390 px (NFR-INTR-01, todas
as telas usáveis no celular sem rolagem horizontal).

### Especificação das telas

| Tela | Rota | O que mostra |
| --- | --- | --- |
| Entrar | `/sign-in` | E-mail, senha, "Entrar", "Continuar com Google", "Continuar com Apple" e o link "Criar conta" |
| Criar conta | `/sign-up` | O formulário de cadastro por e-mail |
| Confirme seu e-mail | `/confirm-email` | O aviso de que o link foi enviado, "Reenviar e-mail" e "Voltar para entrar" |
| Complete seu cadastro | `/complete-profile` | Os dados que faltam depois do primeiro login com Google ou Apple |
| Meus campos | `/manager` | A tela inicial do gestor: cabeçalho com foto, nome e "Sair", e a lista de campos, vazia neste épico |
| Buscar campos | `/renter` | A tela inicial do locatário: cabeçalho com foto, nome e "Sair", e a busca, vazia neste épico |

### Caminho de menu

Sem sessão, o app abre em `Entrar`. Com sessão, abre em `Meus campos` (gestor) ou `Buscar campos` (locatário).

### Perfis e permissões

FR-ACC-01 define dois perfis: **gestor** (administra campos) e **locatário** (aluga campos). O perfil fica na
coluna `role` da tabela `profiles`, com os valores `manager` e `renter`.

| Perfil / Ação | Permissão | Observação |
| --- | --- | --- |
| Sem sessão | nenhuma | Vê só Entrar, Criar conta e Confirme seu e-mail |
| Sessão sem perfil | sessão do Supabase Auth | Vê só Complete seu cadastro |
| Gestor | `role = manager` | Vê só as rotas `/manager` |
| Locatário | `role = renter` | Vê só as rotas `/renter` |

---

## Regras de negócio

### 1. Acesso às telas

- Toda abertura do app e toda troca de rota confere a sessão e o perfil antes de desenhar a tela.
- Sem sessão, qualquer rota fora de Entrar, Criar conta e Confirme seu e-mail leva a Entrar, sem mensagem.
- Com sessão e sem linha em `profiles`, qualquer rota leva a Complete seu cadastro.
- Com sessão e perfil, Entrar, Criar conta e Confirme seu e-mail levam à tela inicial do perfil.

#### Origem do fluxo

O ícone do app, o link de confirmação do e-mail (regra 4) ou o endereço do app na web.

### 2. Funções por perfil (FR-ACC-03)

- Um gestor que abre uma rota `/renter` vai para `Meus campos` e vê:
  > "Esta área é só para locatários."
- Um locatário que abre uma rota `/manager` vai para `Buscar campos` e vê:
  > "Esta área é só para gestores."
- A proteção de dados não depende do app: a policy de RLS de `profiles` deixa cada usuário ler e alterar só a
  própria linha.

### 3. Cadastro por e-mail (FR-ACC-01)

- O cadastro é gratuito: nenhum passo pede pagamento (BR-01).
- "Criar conta" valida os campos (ver Dicionário de dados) e mostra cada erro abaixo do campo.
- Com tudo válido, o Supabase Auth cria o usuário com nome, telefone e perfil. Um trigger do banco grava a
  linha de `profiles` com esses dados no mesmo instante, e o app abre Confirme seu e-mail.
- Até a confirmação não há sessão, então a foto escolhida fica guardada no aparelho. Ela vai para o bucket
  `avatars` logo depois da primeira entrada nesse aparelho. Se a pessoa confirma o e-mail em outro aparelho, a
  conta fica sem foto.
- Se o e-mail já tem conta, o app mostra a mesma tela Confirme seu e-mail, sem dizer que a conta existe. Assim
  ninguém descobre quem está cadastrado.
- Se a rede ou o Supabase falham, o app fica em Criar conta, mantém o que foi digitado e mostra:
  > "Não foi possível criar a conta. Confira sua conexão e tente de novo."

### 4. Confirmação de e-mail

- O e-mail de confirmação leva um link que abre o app no aparelho (deep link `br.com.timecontra.app://login`)
  ou a web.
- O link vale por 1 hora. Ao abrir um link válido, a conta é confirmada e o app entra na tela inicial do perfil.
- Um link vencido ou já usado leva a Entrar com a mensagem:
  > "Este link expirou. Entre com seu e-mail e senha para receber um novo."
- "Reenviar e-mail" manda outro link e fica desabilitado por 60 segundos, mostrando:
  > "Você pode reenviar em {segundos} s."
- Depois do reenvio, a tela mostra:
  > "Enviamos um novo link para {e-mail}."

### 5. Entrar com e-mail e senha (FR-ACC-02)

- E-mail e senha corretos de uma conta confirmada abrem a tela inicial do perfil.
- E-mail ou senha incorretos mantêm Entrar e mostram:
  > "E-mail ou senha incorretos."
- Conta ainda não confirmada: o app manda um novo link e abre Confirme seu e-mail com a mensagem:
  > "Confirme seu e-mail para entrar. Enviamos um novo link para {e-mail}."
- Quando o Supabase limita as tentativas, o app mostra:
  > "Muitas tentativas seguidas. Espere alguns minutos e tente de novo."

### 6. Entrar com Google ou Apple

- "Continuar com Google" e "Continuar com Apple" abrem a autenticação do provedor.
- Se a pessoa cancela, o app volta para Entrar sem mensagem.
- Se o provedor falha, o app mostra:
  > "Não foi possível entrar com Google. Tente de novo."

  ou
  > "Não foi possível entrar com Apple. Tente de novo."
- No primeiro login, a conta ainda não tem perfil e o app abre Complete seu cadastro, com o nome e a foto que o
  provedor enviou já preenchidos.
- Se o e-mail do provedor é o de uma conta já confirmada, o Supabase Auth liga o provedor a essa conta e o app
  abre a tela inicial do perfil dela.

### 7. Perfil único e fixo (BR-05)

- Cada conta tem exatamente um perfil, escolhido em Criar conta ou em Complete seu cadastro.
- O perfil não muda depois de gravado. Quem é gestor e locatário usa duas contas, com e-mails diferentes.
- O banco recusa qualquer alteração de `role` numa linha existente de `profiles`.

### 8. Sessão e saída

- A sessão continua depois de fechar e reabrir o app, até a pessoa tocar em "Sair".
- "Sair" encerra a sessão no aparelho e abre Entrar.

### 9. Persistência e auditoria

- **Limite do usuário (visível):** "Criar conta", "Concluir", "Entrar", "Continuar com Google",
  "Continuar com Apple" e "Sair".
- **Ação do sistema (interna):** o Supabase Auth registra no seu log de auditoria *quem* (usuário e IP), *o
  quê* (cadastro, confirmação, login, saída) e *quando* (UTC). `profiles` guarda `created_at` e `updated_at` em
  UTC.

---

## Cenários de aceite (Gherkin)

### Cenário 1 — Cadastro por e-mail (caminho feliz)

```gherkin
Dado que a pessoa não tem conta
Quando ela preenche nome, e-mail, senha, telefone e perfil "Gestor de campo" e toca em "Criar conta"
Então o app abre "Confirme seu e-mail"
E o Supabase Auth envia o link de confirmação para o e-mail informado
E existe uma linha em profiles com role "manager"
```

### Cenário 2 — Confirmação abre o app no perfil

```gherkin
Dado que a pessoa criou uma conta de locatário e não confirmou o e-mail
Quando ela abre o link de confirmação em menos de 1 hora
Então a conta fica confirmada
E o app abre "Buscar campos"
```

### Cenário 3 — Campo inválido no cadastro

```gherkin
Dado que a pessoa está em "Criar conta"
Quando ela informa a senha "1234567" e toca em "Criar conta"
Então o app mostra "A senha precisa ter pelo menos 8 caracteres." abaixo da senha
E nenhuma conta é criada
```

### Cenário 4 — E-mail já cadastrado

```gherkin
Dado que já existe uma conta com o e-mail "ana@exemplo.com"
Quando outra pessoa cria conta com "ana@exemplo.com"
Então o app abre "Confirme seu e-mail"
E nenhuma conta nova é criada
E a tela não informa que o e-mail já existia
```

### Cenário 5 — Link vencido

```gherkin
Dado que o link de confirmação foi enviado há mais de 1 hora
Quando a pessoa abre o link
Então o app abre "Entrar"
E mostra "Este link expirou. Entre com seu e-mail e senha para receber um novo."
```

### Cenário 6 — Reenviar o link

```gherkin
Dado que a pessoa está em "Confirme seu e-mail"
Quando ela toca em "Reenviar e-mail"
Então o app mostra "Enviamos um novo link para {e-mail}."
E "Reenviar e-mail" fica desabilitado por 60 segundos
```

### Cenário 7 — Entrar com e-mail e senha (caminho feliz)

```gherkin
Dado que existe uma conta de gestor confirmada
Quando a pessoa informa o e-mail e a senha certos e toca em "Entrar"
Então o app abre "Meus campos" com o nome da pessoa no cabeçalho
```

### Cenário 8 — Senha errada

```gherkin
Dado que existe uma conta confirmada
Quando a pessoa informa a senha errada e toca em "Entrar"
Então o app continua em "Entrar"
E mostra "E-mail ou senha incorretos."
```

### Cenário 9 — Conta sem confirmação

```gherkin
Dado que existe uma conta que não confirmou o e-mail
Quando a pessoa informa o e-mail e a senha certos e toca em "Entrar"
Então o app abre "Confirme seu e-mail"
E mostra "Confirme seu e-mail para entrar. Enviamos um novo link para {e-mail}."
```

### Cenário 10 — Primeiro login com Google

```gherkin
Dado que a pessoa não tem conta no Time-Contra
Quando ela toca em "Continuar com Google" e autoriza
Então o app abre "Complete seu cadastro" com o nome vindo do Google
Quando ela informa telefone e perfil "Locatário" e toca em "Concluir"
Então o app abre "Buscar campos"
E existe uma linha em profiles com role "renter"
```

### Cenário 11 — Login com Apple cancelado

```gherkin
Dado que a pessoa está em "Entrar"
Quando ela toca em "Continuar com Apple" e cancela
Então o app continua em "Entrar" sem mensagem
```

### Cenário 12 — Locatário abre rota de gestor

```gherkin
Dado que um locatário está com a sessão aberta
Quando ele abre a rota "/manager"
Então o app abre "Buscar campos"
E mostra "Esta área é só para gestores."
```

### Cenário 13 — O perfil não muda

```gherkin
Dado que existe um gestor com role "manager"
Quando a sessão dele tenta gravar role "renter" na própria linha de profiles
Então o banco recusa a alteração
E role continua "manager"
```

### Cenário 14 — Um usuário não lê o perfil de outro

```gherkin
Dado que existem os usuários A e B
Quando A pede a linha de profiles de B
Então o banco devolve zero linhas
```

### Cenário 15 — Sessão continua e "Sair" encerra

```gherkin
Dado que um gestor entrou no app
Quando ele fecha e reabre o app
Então o app abre "Meus campos" sem pedir login
Quando ele toca em "Sair"
Então o app abre "Entrar"
E reabrir o app mostra "Entrar"
```

### Cenário 16 — Telas em 390 px

```gherkin
Dado qualquer tela desta spec
Quando ela é aberta em 390 px de largura
Então a rolagem horizontal da página é de 0 px
```

### Cenário 17 — Falha de rede no cadastro

```gherkin
Dado que a pessoa está em "Criar conta" sem conexão
Quando ela toca em "Criar conta" com todos os campos válidos
Então o app continua em "Criar conta" com os campos preenchidos
E mostra "Não foi possível criar a conta. Confira sua conexão e tente de novo."
```

### Cenário 18 — Foto enviada depois da confirmação

```gherkin
Dado que a pessoa escolheu uma foto em "Criar conta" e ainda não confirmou o e-mail
Quando ela abre o link de confirmação no mesmo aparelho
Então a foto é gravada em avatars/<id do usuário>/
E aparece no cabeçalho da tela inicial do perfil
```

---

## Dicionário de dados da tela

### Criar conta e Complete seu cadastro

Os mesmos campos nas duas telas, exceto E-mail e Senha, que só existem em Criar conta.

| Campo | Tipo | Habilitado | Obrigatório | Regra / Validação |
| --- | --- | --- | --- | --- |
| `Nome` | Texto (80) | Sim | Sim | 2 a 80 caracteres sem espaços nas pontas. Em Complete seu cadastro, vem preenchido com o nome do provedor. Erro: "Informe seu nome, com pelo menos 2 letras." |
| `E-mail` | E-mail (254) | Sim | Sim | Formato de e-mail, até 254 caracteres, guardado em minúsculas. Erro: "Informe um e-mail válido." |
| `Senha` | Senha (72) | Sim | Sim | 8 a 72 caracteres, com botão para mostrar e esconder. Erro: "A senha precisa ter pelo menos 8 caracteres." |
| `Telefone` | Telefone | Sim | Sim | DDD + número, 10 ou 11 dígitos, com a máscara "(11) 91234-5678"; guardado só com dígitos. Erro: "Informe um telefone com DDD." |
| `Perfil` | Opção única | Sim | Sim | "Gestor de campo" grava `manager`; "Locatário" grava `renter`. Nenhuma opção vem marcada. Erro: "Escolha um perfil." |
| `Foto` | Imagem | Sim | Não | JPEG ou PNG, até 5 MB, da câmera ou da galeria. Em Complete seu cadastro, vem com a foto do provedor quando houver. Erro: "A foto precisa ser JPEG ou PNG de até 5 MB." |

### Entrar

| Campo | Tipo | Habilitado | Obrigatório | Regra / Validação |
| --- | --- | --- | --- | --- |
| `E-mail` | E-mail (254) | Sim | Sim | Formato de e-mail. Erro: "Informe um e-mail válido." |
| `Senha` | Senha (72) | Sim | Sim | Não vazia. Erro: "Informe sua senha." |

## Ações das telas

| Ação | Efeito | Regra para habilitar | Mensagens |
| --- | --- | --- | --- |
| Criar conta | Regra 3 | Sempre; valida ao tocar | Erro: "Não foi possível criar a conta. Confira sua conexão e tente de novo." |
| Concluir | Grava `profiles` e abre a tela inicial do perfil | Sempre; valida ao tocar | Erro: "Não foi possível salvar seus dados. Confira sua conexão e tente de novo." |
| Entrar | Regra 5 | Sempre; valida ao tocar | Erro: "E-mail ou senha incorretos." |
| Continuar com Google | Regra 6 | Sempre | Erro: "Não foi possível entrar com Google. Tente de novo." |
| Continuar com Apple | Regra 6 | Sempre | Erro: "Não foi possível entrar com Apple. Tente de novo." |
| Reenviar e-mail | Regra 4 | 60 segundos depois do último envio | Sucesso: "Enviamos um novo link para {e-mail}." |
| Voltar para entrar | Abre Entrar | Sempre | — |
| Criar conta (link) | Abre Criar conta | Sempre | — |
| Sair | Regra 8 | Sempre | — |

---

## Impacto na arquitetura

- **App:** a feature `accounts` em `lib/ui/accounts/`, as rotas da regra 1 em `lib/routing/`, um repository de
  sessão e perfil, e services para o Supabase Auth, a tabela `profiles` e o Storage.
- **Supabase Auth:** provedores e-mail (com confirmação), Google e Apple; link de confirmação com validade de
  1 hora; redirecionamento para `br.com.timecontra.app://login` e para o endereço da web.
- **Storage:** bloco novo no mapa, com o bucket `avatars` para as fotos de perfil. M1.
- **Cenários em execução:** novo cenário "Criar conta e entrar", do cadastro à tela inicial.
- **Implantação:** o identificador `br.com.timecontra.app` no Android e no iOS, e o deep link registrado nas duas
  plataformas.
- **Segurança:** OAuth do Google e da Apple, e confirmação de e-mail obrigatória antes do primeiro login por senha.

## Impacto no modelo de dados

- **Usuário** ganha os atributos nome, telefone, foto e perfil. Fica na tabela `profiles`:
  `id` (o id do usuário no Supabase Auth, chave primária e estrangeira, apagado junto com o usuário),
  `role` (`manager` ou `renter`, não muda), `name`, `phone` (10 ou 11 dígitos), `avatar_path` (opcional),
  `created_at` e `updated_at` (instantes UTC).
- Um trigger em `auth.users` grava a linha de `profiles` com o nome, o telefone e o perfil enviados no cadastro
  por e-mail. No login com Google ou Apple, a linha nasce em Complete seu cadastro.
- RLS em `profiles`: cada usuário lê, cria e altera só a própria linha, e nunca altera `role`.
- Bucket `avatars` no Storage: um arquivo por usuário em `avatars/<id do usuário>/`, que só o dono lê e grava.

## Fora do escopo

- Recuperar a senha esquecida, trocar e-mail ou senha, e excluir a conta: ficam para depois do M1. A exclusão
  está em [Riscos](../../architecture/risks.md) por causa da LGPD.
- Editar nome, telefone ou foto depois do cadastro: fica para quando houver uma tela de perfil.
- Verificar o telefone por SMS: o telefone só tem o formato validado.
- Login por telefone ou por outros provedores além de Google e Apple.
- O conteúdo de "Meus campos" (épico #2) e de "Buscar campos" (épico #3).
- Criar a conta no Apple Developer Program e o projeto no Google Cloud: são contas do dono do produto e
  precisam existir antes da tarefa 5.
- Rodar e assinar o build de iOS: exige um Mac. A tarefa 1 deixa o projeto de iOS pronto, e o teste em iOS
  é feito num Mac.

## Divisão em tarefas

| # | Título | Escopo | Critério de aceite | Depende de |
| --- | --- | --- | --- | --- |
| 1 | Montar o esqueleto do app e do Supabase | Instalar Flutter SDK, Supabase CLI e Deno; `flutter create` com `br.com.timecontra.app`; `supabase init`; `lib/` no layout do `AGENTS.md`; gates na seção Commands | O app abre uma tela vazia no Android e na web, e todos os gates do `AGENTS.md` rodam com código de saída 0 | — |
| 2 | Criar perfis e fotos no Supabase | Migration de `profiles` com RLS, o trigger de cadastro e a regra de `role` fixo; bucket `avatars` com policies | Cenários 13 e 14 | 1 |
| 3 | Entrar com e-mail, manter a sessão e separar as telas por perfil | Telas Entrar, Meus campos e Buscar campos; rotas e proteção da regra 1; "Sair" | Cenários 7, 8, 12, 15 e 16 | 2 |
| 4 | Criar conta por e-mail com confirmação | Telas Criar conta e Confirme seu e-mail; foto; deep link; reenvio | Cenários 1, 2, 3, 4, 5, 6, 9, 17 e 18 | 3 |
| 5 | Entrar com Google e Apple | Botões sociais, Complete seu cadastro, configuração dos provedores no Supabase | Cenários 10 e 11 | 4 |
