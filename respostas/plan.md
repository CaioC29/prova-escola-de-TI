# Plan — Arquitetura e decisões
 
Os valores da variante estão no `spec.md`.
 
## Stack
 
* Python 3.11 + FastAPI + uvicorn (justificativa: rápido de gerar e testar; contrato REST claro).
* Persistência em memória 
* Porta 8001 (`PORTA_SERVICO` da variante).


## Estrutura de arquivos a gerar
 
```
main.py          # app FastAPI, rotas
models.py        # dataclass Bilhete
service.py       # regras de negócio (minutos, valor, relatório)
store.py         # repositório em memória
test_app.py      # testes pytest (refletem tests.md)
requirements.txt # dependências
Containerfile    # roda o serviço na porta 8001
README.md        # como instalar, rodar e testar
```

## Decisões
 
1. Valores sempre em centavos inteiros, nunca decimal
2. Frações cobradas: `n = ceil(minutos / 15)` com divisão inteira; valor = `min(n * 100, 6000)`, e 0 se `minutos <= 0`.
3. Erros devolvidos como `{"erro": "<codigo>"}` por um tratamento único (justificativa: o contrato exige esse formato).
4. Tempo médio do relatório com 0,5 para cima, calculado com inteiros (justificativa: o contrato manda 2,5 virar 3).
5. `entrada` opcional do UC1 usada nos testes.
