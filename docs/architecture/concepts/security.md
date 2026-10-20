# Segurança

## Identidade

O Supabase Auth autentica gestores e locatários (FR-ACC-02) por e-mail e senha, Google ou Apple. O login por
senha só funciona depois de confirmar o e-mail. O cadastro com um e-mail que já existe mostra a mesma tela de um
cadastro novo, para não revelar quem tem conta. Cada usuário tem um perfil, gestor ou locatário
(FR-ACC-01), e o app mostra só as funções do perfil (FR-ACC-03). O app esconder a função não é a proteção: a
proteção é a policy do banco.

## Autorização

Toda tabela tem RLS ligado. A policy compara o dono do registro com o usuário da sessão e nega quando não há
usuário. Um gestor só alcança os dados dos próprios campos (NFR-SEC-01).

## Segredos

O app carrega só a chave pública do Supabase, que depende do RLS para ser segura. A chave de serviço do Supabase
e a chave do gateway de pagamento ficam só nas Edge Functions.

## Dados pessoais

Nome e contato de gestores e locatários são dados pessoais sob a LGPD. Como a exclusão da conta e dos dados
funciona ainda não está nos requisitos.
