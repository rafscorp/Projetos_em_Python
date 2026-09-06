# 📚 Sistema de Biblioteca

## Visão Geral

Um sistema de gerenciamento de biblioteca orientado a objetos, rodando em terminal. É o projeto mais "avançado" desse repositório: em vez de só manipular listas e dicionários soltos, aqui a modelagem gira em torno de três classes que representam o mundo real de uma biblioteca — **Livro**, **Membro** e **Empréstimo** — com regras de negócio de verdade aplicadas entre elas (não dá pra emprestar um livro que já está emprestado, cada membro tem um limite de empréstimos simultâneos, e todo empréstimo tem prazo de devolução com cálculo automático de atraso).

Os dados são salvos em `biblioteca_dados.json`, criado automaticamente na pasta do projeto.

## Funcionalidades

- Cadastrar livro (ISBN, título, autor, ano)
- Cadastrar membro (nome e limite de empréstimos simultâneos, padrão 3)
- Emprestar livro a um membro, com validação das regras de negócio
- Devolver livro, com aviso automático de atraso (em dias) se for o caso
- Listar acervo (mostrando se cada livro está disponível ou emprestado)
- Listar membros (com quantos empréstimos ativos cada um tem no momento)
- Listar todos os empréstimos (histórico completo, com status)
- Relatório de empréstimos atrasados

### Regras de negócio implementadas

- Um livro não pode ser emprestado se já existe um empréstimo dele em aberto
- Um membro não pode ultrapassar o limite de empréstimos simultâneos configurado pra ele
- Todo empréstimo tem uma data prevista de devolução (14 dias após a data do empréstimo)
- O atraso é calculado comparando a data de devolução (ou a data de hoje, se ainda não devolvido) com a data prevista

## Como Rodar

Precisa ter Python 3 instalado (nenhuma biblioteca externa é usada, só a standard library).

```bash
python main.py
```

Um menu numérico vai aparecer no terminal. Os dados ficam salvos automaticamente em `biblioteca_dados.json` depois de cada ação, então é seguro fechar o programa a qualquer momento sem perder o histórico.

## Estrutura do Código

O projeto é dividido em 3 arquivos, cada um com uma responsabilidade diferente:

- **`modelos.py`** — as classes de dados (`Livro`, `Membro`, `Empréstimo`) e regras que dizem respeito só a uma entidade (tipo um empréstimo calcular seu próprio atraso)
- **`biblioteca.py`** — a classe `Biblioteca`, que é o "cérebro" do sistema: guarda as coleções de livros/membros/empréstimos e aplica as regras de negócio que dependem de olhar tudo junto (ex: "esse livro já está emprestado?")
- **`main.py`** — só a interface de terminal (menu, `input`, `print`), que conversa com a classe `Biblioteca` sem saber como ela funciona por dentro

## Conceitos Aplicados

- **Programação Orientada a Objetos**: classes com atributos, métodos e responsabilidades bem definidas
- **Dataclasses** pra reduzir boilerplate nas entidades, sem abrir mão de métodos customizados (`__str__`, `esta_atrasado`, etc.)
- **Separação de responsabilidades** entre dado, regra de negócio e interface (arquitetura em camadas)
- **Persistência em JSON**, reconstruindo os objetos a partir dos dicionários salvos
- **Tratamento de exceções** com `ValueError` customizado pra cada regra de negócio violada, capturado e traduzido em mensagem amigável no menu
- **Datas** (`datetime.date`) pra calcular prazos e atrasos
- **Type hints** em todas as funções e métodos, incluindo `Dict`/`List`/`Optional` do módulo `typing`

## Melhorias Futuras

- Multas por atraso (valor por dia, com fechamento de conta)
- Busca de livro por título/autor em vez de só por ISBN
- Reserva de livro que já está emprestado (fila de espera)
- Editar/remover cadastro de livro e membro
- Testes automatizados pras regras de negócio da classe `Biblioteca`

## Autor

Rafael Costa
GitHub: [github.com/rafscorp](https://github.com/rafscorp)
