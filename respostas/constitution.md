# Constitution - Regras persistentes do projeto

## Regras Operacionais

1. Dinheiro é sempre **inteiro em centavos**. Proibido `float`, `Decimal` e divisão `/` em qualquer cálculo monetário.
2. Todo erro responde `{"erro": "<codigo>"}`. Só usar estes códigos: `placa_invalida`, `entrada_invalida`, `data_invalida`, `bilhete_nao_encontrado`, `bilhete_ja_encerrado`, `bilhete_nao_aberto`, `bilhete_em_aberto`.
3. Datas em ISO-8601 com fuso `-03:00`, por exemplo `2026-10-05T14:30:00-03:00`.
4. O serviço escuta na porta `PORTA_SERVICO`.
5. Todo endpoint documenta seus status de erro.
6. O contrato manda sobre qualquer exemplo. O exemplo do UC2 no enunciado (`{"id": 7, "valor": 12.50}`) está errado e não deve ser seguido.


## Parâmetros da variante
 
| Parâmetro | Valor | Para que serve |
| --- | --- | --- |
| `TARIFA_HORA_CENTAVOS` | 400 | preço da hora cheia |
| `FRACAO_MINUTOS` | 15 | de quantos em quantos minutos cobra |
| `TETO_DIARIO_CENTAVOS` | 6000 | o máximo que um bilhete pode custar |
| `TOLERANCIA_MINUTOS` | 0 | minutos grátis |
| `PORTA_SERVICO` | 8001 | porta do servidor |





