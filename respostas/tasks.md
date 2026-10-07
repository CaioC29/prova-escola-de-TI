# Tarefas

Fazer na ordem. Os arquivos a gerar estão no `plan.md`, os casos de teste no `tests.md`.

| # | Tarefa | Pronto quando |
| --- | --- | --- |
| 1 | **Base do projeto:** criar o projeto em Python, o `requirements.txt` e o `Containerfile`, com o serviço na porta 8001. | O serviço sobe na porta 8001 e a imagem builda. |
| 2 | **UC1, UC8, UC3 e UC6:** abrir bilhete (com `entrada` opcional), impedir segunda abertura da mesma placa, listar ativos e listar histórico por placa. | Passam os casos de "Validação", "Conflitos e erros" e "Listas" do `tests.md`. |
| 3 | **UC2 e UC7:** encerrar bilhete e calcular o valor (fração de 15 minutos, teto de 6000, tolerância 0). | Passa toda a tabela "Valor do bilhete" do `tests.md`. |
| 4 | **UC5 e UC4:** cancelar bilhete e gerar o relatório diário. | Passam os casos de "Relatório" e de "Conflitos e erros" do `tests.md`. |
| 5 | **Testes e README:** testes próprios com os casos do `tests.md` e `README.md` explicando como instalar, rodar e testar. | Os testes passam e o `README.md` está completo. |
| 6 | **Revisão final:** comparar cada resposta com o `spec.md` (campos, status e erros iguais ao contrato) e rodar o linter da linguagem. | Nenhuma diferença em relação ao contrato e linter sem erros. |
