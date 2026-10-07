# Tests — Cenários de teste (TDD)

Variante: tarifa 400, fração 15 (cada fração custa 100), teto 6000, tolerância 0.

> Para testar um bilhete de M minutos, abrir com `entrada` no passado (campo opcional do UC1) de modo que ele dure M minutos, e encerrar em seguida.

## Valor do bilhete (UC2 e UC7)

| Caso | minutos | `valor_centavos` |
| --- | --- | --- |
| Dentro da tolerância (0) | 0 | 0 |
| Passou da tolerância por 1 minuto | 1 | 100 |
| Quase uma fração | 14 | 100 |
| Fração exata | 15 | 100 |
| Fração + 1 minuto | 16 | 200 |
| Duas frações exatas | 30 | 200 |
| Hora cheia | 60 | 400 |
| Valor qualquer | 95 | 700 |
| Logo abaixo do teto | 885 | 5900 |
| Exatamente no teto | 900 | 6000 |
| Teto + 1 minuto | 901 | 6000 |
| Muito acima do teto | 1440 | 6000 |


> Em nenhum caso `valor_centavos` passa de 6000, e ele é sempre inteiro.

## Formato das respostas

| Caso | Esperado |
| --- | --- |
| Abrir bilhete com placa válida | 201 com `id`, `placa`, `entrada` e `status` `aberto` |
| Encerrar bilhete | 200 com `id`, `placa`, `entrada`, `saida`, `minutos` e `valor_centavos` |
| Cancelar bilhete aberto | 200 com `status` `cancelado`, sem `saida` e sem `valor_centavos` |

## Relatório (UC4)

| Caso | Esperado |
| --- | --- |
| Bilhetes de 2 e 3 minutos | `tempo_medio_minutos` 3 (média 2,5) |
| Bilhetes de 2, 2 e 3 minutos | `tempo_medio_minutos` 2 (média 2,33) |
| `data=05/10/2026` | 422 `{"erro": "data_invalida"}` |

## Conflitos e erros

| Caso | Status | Body |
| --- | --- | --- |
| Abrir placa que já tem bilhete aberto | 409 | `{"erro": "bilhete_em_aberto"}` |
| Abrir de novo depois de encerrar | 201 | novo bilhete |
| Abrir de novo depois de cancelar | 201 | novo bilhete |
| Encerrar duas vezes | 409 | `{"erro": "bilhete_ja_encerrado"}` |
| Cancelar bilhete encerrado | 409 | `{"erro": "bilhete_nao_aberto"}` |
| Cancelar duas vezes | 409 | `{"erro": "bilhete_nao_aberto"}` |
| Encerrar ou cancelar `id` 9999 | 404 | `{"erro": "bilhete_nao_encontrado"}` |

## Validação

| Entrada | Status | Body |
| --- | --- | --- |
| Placa `ABC1D2` (6 caracteres) | 422 | `{"erro": "placa_invalida"}` |
| Placa `ABC1D234` (8 caracteres) | 422 | `{"erro": "placa_invalida"}` |
| Placa `abc1d23` (minúscula) | 422 | `{"erro": "placa_invalida"}` |
| Placa ausente | 422 | `{"erro": "placa_invalida"}` |
| `entrada: "ontem"` | 422 | `{"erro": "entrada_invalida"}` |

## Listas (UC3 e UC6)

| Caso | Esperado |
| --- | --- |
| 2 bilhetes abertos | 2 itens, o último aberto primeiro |
| Bilhete encerrado ou cancelado | não aparece em ativos |
| Placa que nunca estacionou | `[]` |
| Placa com um bilhete encerrado e um cancelado | 2 itens |
