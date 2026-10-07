# Spec

## Casos de Uso

**UC1 — Abrir bilhete**

`POST /bilhetes` com `{"placa": "ABC1D23"}` o body aceita `"entrada"` opcional.

-   Resposta **201**: `{"id", "placa", "entrada", "status": "aberto"}`.
-   Sem `entrada`, usa a hora atual.
-   Com `entrada`, ela precisa ter fuso (`-03:00` ou `Z`). Sem fuso ou formato errado: 422 `entrada_invalida`.
-   A `entrada` sempre sai na resposta em `-03:00`.
