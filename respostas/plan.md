# Plan
 
Os valores da variante estão no `spec.md`.
 
## Decisões
 
| Decisão | Escolha | Por quê |
| --- | --- | --- |
| Dinheiro | Sempre centavos inteiros, nunca decimal | Com decimal o erro de arredondamento acumula (0.1 + 0.2 ≠ 0.3). Com inteiros esse bug não existe.[^centavos] |
| Testar com tempo | Usar o campo `entrada` opcional do UC1 | Sem ele, testar fração e teto exigiria esperar tempo real. Com ele, dá para abrir o bilhete no passado. |
| Fuso | Datas sempre em `-03:00` | É o fuso que o contrato pede nas respostas. |
| Porta | 8001 | É a `PORTA_SERVICO` da variante. |
| Linguagem | Livre | O enunciado não define linguagem. O agente escolhe uma e usa o linter dela. |
 
