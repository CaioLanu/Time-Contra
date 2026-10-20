# Reservar um horário

M1. Cobre FR-SRC-01, FR-SRC-05, FR-BKG-01, FR-BKG-03 e BR-03.

1. O locatário escolhe um bairro no app, e o app pede ao banco os campos daquela área (HTTPS, API REST).
2. O banco devolve só campos com horário livre, filtrados por PostGIS e pelos filtros escolhidos.
3. O locatário abre o anúncio; o app grava uma visualização (FR-ANL-01).
4. O locatário escolhe o horário e o número de times, e o app grava a reserva (HTTPS, API REST).
5. O banco aceita a reserva ou a recusa pela constraint de horário único, se outro locatário reservou antes.
6. O app mostra a reserva confirmada, ou avisa que o horário acabou de ser ocupado.

Se a reserva depende de aprovação do gestor ainda está em aberto: Q4 em
[Perguntas em aberto](../../requirements/open-questions.md#q4).
