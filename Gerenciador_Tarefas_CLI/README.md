# 📝 Gerenciador de Tarefas CLI

## Visão Geral

Um gerenciador de tarefas que roda direto no terminal, sem depender de banco de dados ou frameworks. É o clássico "to-do list", mas feito do zero em Python puro: os dados ficam salvos num arquivo `tarefas.json` que é criado automaticamente na primeira vez que você roda o programa, então nada se perde quando você fecha o terminal.

A ideia aqui foi praticar manipulação de arquivos, serialização com JSON e organização de código em funções pequenas e independentes, cada uma cuidando de uma responsabilidade só.

## Funcionalidades

- Adicionar tarefa (com descrição, prioridade e prazo opcional)
- Listar tarefas (pendentes aparecem primeiro, ordenadas por prioridade)
- Marcar tarefa como concluída
- Editar prioridade e/ou prazo de uma tarefa já existente
- Remover tarefa (com confirmação antes de apagar)
- Tratamento de entradas inválidas (id que não existe, texto onde era esperado número, etc.) sem derrubar o programa

## Como Rodar

Precisa ter Python 3 instalado (nenhuma biblioteca externa é usada, só a standard library).

```bash
python gerenciador.py
```

Um menu numérico vai aparecer no terminal — é só digitar o número da opção desejada e seguir as instruções. Os dados ficam salvos automaticamente em `tarefas.json`, na mesma pasta do script.

## Conceitos Aplicados

- **Dataclasses** (`@dataclass`) pra representar a Tarefa sem precisar escrever `__init__` na mão
- **Persistência em JSON** (`json.load` / `json.dump`) com leitura e escrita de arquivos
- **Tratamento de exceções** (`try/except`) pra entrada inválida e arquivo corrompido não quebrarem o programa
- **Funções puras e separadas** por responsabilidade: carregar dados, salvar dados, e uma função pra cada ação do menu
- **Type hints** (`List`, `Optional`) pra deixar claro o que cada função espera e devolve
- **Dicionário de funções** no lugar de uma cadeia gigante de `if/elif` pra rotear as opções do menu

## Melhorias Futuras

- Ordenar/filtrar tarefas por prazo (ex: mostrar só as que vencem essa semana)
- Validar o formato da data de prazo de verdade (hoje é só texto livre)
- Categorias/tags além de prioridade
- Undo pra remoção de tarefa (hoje é definitivo depois da confirmação)
- Cores no terminal pra destacar tarefas atrasadas

## Autor

Rafael Costa
GitHub: [github.com/rafscorp](https://github.com/rafscorp)
