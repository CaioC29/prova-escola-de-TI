# Spec

## Casos de Uso

**UC1 — Abrir bilhete**

`POST /bilhetes` com `{"placa": "ABC1D23"}` o body aceita `"entrada"` opcional.

-   Resposta **201**: `{"id", "placa", "entrada", "status": "aberto"}`.
-   Sem `entrada`, usa a hora atual.
-   Com `entrada`, ela precisa ter fuso (`-03:00` ou `Z`). Sem fuso ou formato errado: 422 `entrada_invalida`.
-   A `entrada` sempre sai na resposta em `-03:00`.

**UC2 — Encerrar bilhete**
 
`POST /bilhetes/{id}/encerramento` responde **200**: `{"id", "placa", "entrada", "saida", "minutos", "valor_centavos"}`.
 
Como calcular o valor:
- Cobra por fração de 15 minutos, arredondando para cima. Cada fração custa 100.
- Passou de 0 minutos, cobra desde o primeiro minuto (UC7).
- O valor nunca passa de 6000.
- O valor é sempre inteiro, em centavos.

**Teto:** `valor_centavos` nunca passa de 6000, por mais tempo que passe.

**Aceite**
- 15 min: 100.
- 16 min: 200.
- 900 min: 6000.
- 901 min: 6000.
- `valor_centavos` é inteiro, sem ponto decimal.
- Encerrar duas vezes dá 409 `bilhete_ja_encerrado`.


**UC3 — Listar ativos**
 
`GET /bilhetes/ativos` responde **200** com os bilhetes abertos, do mais recente para o mais antigo.
 
**Aceite**
- Com 2 abertos, a lista tem 2 itens e o último aberto vem primeiro.
- Bilhete encerrado ou cancelado não aparece.


**UC4 — Relatório diário**
 
`GET /relatorios/diario?data=AAAA-MM-DD` responde **200**: `{"data", "total_bilhetes", "faturamento_centavos", "tempo_medio_minutos"}`.
 
- `tempo_medio_minutos` usa só bilhetes encerrados no dia e arredonda 0,5 para cima.
- `data` fora do formato: 422 `data_invalida`.



**UC5 — Cancelar bilhete**
 
`POST /bilhetes/{id}/cancelamento` responde **200** com `status: "cancelado"`. Só cancela bilhete aberto. Não tem `saida` nem `valor_centavos`.
 
Erros: 404 `bilhete_nao_encontrado`; bilhete não aberto dá 409 `bilhete_nao_aberto`.


**UC6 — Histórico por placa**
 
`GET /bilhetes?placa=ABC1D23` responde **200** com todos os bilhetes da placa, de qualquer status, do mais recente para o mais antigo. Placa sem histórico dá `[]`.


**UC7 — Tolerância**
 
A tolerância é 0 minutos. Com 0 minutos o valor é 0. Passou disso, mesmo por 1 minuto, cobra tudo desde o primeiro minuto.


**UC8 — Uma vaga por placa**
 
Abrir bilhete para placa que já tem um aberto dá **409** `bilhete_em_aberto`. Depois de encerrar ou cancelar, pode abrir de novo.
 
**Aceite**
- Abrir a mesma placa duas vezes: a segunda dá 409 `bilhete_em_aberto`.
- Abrir, encerrar e abrir de novo: a segunda abertura dá 201.


**Erros**
 
| Situação | Status | Body |
| --- | --- | --- |
| Placa ausente ou inválida | 422 | `{"erro": "placa_invalida"}` |
| `entrada` fora de ISO-8601 | 422 | `{"erro": "entrada_invalida"}` |
| `data` fora de `AAAA-MM-DD` | 422 | `{"erro": "data_invalida"}` |
| Bilhete inexistente | 404 | `{"erro": "bilhete_nao_encontrado"}` |
| Encerrar bilhete já encerrado | 409 | `{"erro": "bilhete_ja_encerrado"}` |
| Cancelar bilhete não aberto | 409 | `{"erro": "bilhete_nao_aberto"}` |
| Abrir bilhete com placa já ocupada | 409 | `{"erro": "bilhete_em_aberto"}` |
