# Visão geral

## Partes interessadas

| Parte | Papel | Interesse |
| --- | --- | --- |
| Gestor de campo | Administra um ou mais campos de futebol | Controlar reservas, agenda, pagamentos e a audiência do anúncio |
| Locatário | Aluga um campo para o seu time jogar | Achar um campo perto, livre no horário e com a estrutura que procura |
| Plataforma | Donos do Time-Contra | Receber um percentual de cada aluguel |

## Ambiente de operação

App para Android e iOS, distribuído nas lojas, e a mesma aplicação na web, aberta no navegador do celular ou
do computador.

## Restrições

- A primeira entrega é um protótipo. Não há stack, prazo, orçamento nem hospedagem definidos.
- O sistema guarda dados pessoais de gestores e locatários, então a LGPD (Lei 13.709/2018) se aplica.

## Premissas e dependências

- A busca no mapa depende de um provedor de mapas e de geocodificação de endereços, a escolher na spec.
- O pagamento pelo app depende de um gateway que divida o valor entre gestor e plataforma, a escolher na spec.
