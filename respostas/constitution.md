# Constitution - Regras persistentes do projeto

## Regras Operacionais

1. Dinheiro é sempre **inteiro em centavos**. Proibido `float`, `Decimal` e divisão `/` em qualquer cálculo monetário.
2. Todo erro responde `{"erro": "<codigo>"}`. Só usar estes códigos: `placa_invalida`, `entrada_invalida`, `data_invalida`, `bilhete_nao_encontrado`, `bilhete_ja_encerrado`, `bilhete_nao_aberto`, `bilhete_em_aberto`.
3. Datas em ISO-8601 com fuso `-03:00`, por exemplo `2026-10-05T14:30:00-03:00`.
4. O serviço escuta na porta `PORTA_SERVICO`.
5. Todo endpoint documenta seus status de erro.
6. O contrato manda sobre qualquer exemplo. O exemplo do UC2 no enunciado (`{"id": 7, "valor": 12.50}`) está errado e não deve ser seguido.





