# Pagar a reserva pelo app

M2. Cobre FR-PAY-02 e BR-02. O gateway ainda será escolhido na spec de pagamento.

1. O locatário toca em pagar, e o app chama uma Edge Function com a reserva (HTTPS).
2. A Edge Function cria a cobrança no gateway, com 5% para a plataforma e o restante para o gestor (HTTPS).
3. O app abre o pagamento do gateway para o locatário.
4. O gateway avisa a Edge Function do pagamento aprovado (webhook HTTPS).
5. A Edge Function marca a reserva como paga no banco (SQL).
6. A agenda do gestor passa a mostrar a reserva como paga.
