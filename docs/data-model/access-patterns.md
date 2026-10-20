# Padrões de acesso

Os volumes ainda não foram medidos. São estimados quando a cidade de lançamento for decidida (Q5).

| Operação | Lê ou grava | Filtro e ordem | Requisito |
| --- | --- | --- | --- |
| Buscar campos numa área | Lê | Área no mapa, tipo, estrutura e horário livre; por distância | FR-SRC-01 a 04 |
| Abrir o anúncio | Lê | Campo por id, com preços e horários livres | FR-SRC-05 |
| Contar uma visualização | Grava | Campo por id | FR-ANL-01 |
| Cadastrar ou editar campo | Grava | Campo do gestor | FR-FLD-01, FR-FLD-02 |
| Definir horários e preços | Grava | Campo do gestor | FR-FLD-03, FR-FLD-04 |
| Reservar um horário | Grava | Campo e intervalo; recusa sobreposição | FR-BKG-01, FR-BKG-03 |
| Ver a agenda | Lê | Campos do gestor num período; por início | FR-BKG-02 |
| Marcar pagamento | Grava | Reserva por id, do gestor | FR-PAY-01 |
| Ver total de visualizações | Lê | Campos do gestor; total por campo | FR-ANL-01 |
