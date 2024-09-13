# Laboratório 2
## 1. Objetivos

*   Familiazar-se com a sintaxe SQL;
*   Criar consultas que utilizem comandos INSERT, UPDATE, DELETE, SELECT, LIKE, DISTINCT, UNION e EXCEPT.

## 2. Descrição

Você foi contratado pelo COB (Comitê Olímpico do Brasil) para dar manutenção no banco de dados olímpico do país e levantar estatísticas relevantes sobre a participação do Brasil na última edição das Olimpíadas - Paris 2024.

A princípio, você vai trabalhar apenas com a relação *atleta*, cujo esquema é: atleta(\_id\_: integer, nome: varchar, pais: varchar, ano_nascimento: integer, esporte: varchar, medalha: varchar, edicao_olimpiada: integer). Note que já trabalhamos com ela no laboratório passado.

Suas primeiras tarefas estão descritas nas seções seguintes. Elas devem ser executadas em ordem, pois o resultado de uma consulta SQL pode afetar as seguintes.

### 2.1 Acesso ao ambiente de execução SQL

Dessa vez, acesse o SQL Online IDE (https://sqliteonline.com/) para executar as tarefas solicitadas neste laboratório. Selecione a opção "PotsgreSQL" no menu lateral esquerdo para executar consultas SQL através do SGBD open source PostgreSQL, um dos mais usados no mundo para implementação de bancos de dados relacionais. Escreva as consultas SQL na janela central e as execute clicando no botão "Run" do menu superior.

<img src="/Images/sql-online-ide.png">

Figura 1: Interface do SQL Online IDE

### 2.2 Escrita de Consultas SQL

Você recebeu uma lista de instruções a serem operadas na tabela *atleta*. Para cada uma delas, escreva a consulta SQL correspondente.

1. Inserir as seguintes tuplas com dados dos medalhistas brasileiros das Olimíadas de Paris 2024
 na tabela *atleta*:

| **id** | **nome**                  | **pais** | **ano_nascimento** | **esporte**         | **medalha** | **edicao_olimpiada** |
|---------------|---------------------------|----------|--------------------|---------------------|-------------|----------------------|
| 1             | Beatriz Souza | Brasil   | 1998               | Judô           | Ouro        | 2024       |
| 2             | Rebeca Andrade | Brasil   | 1999               | Ginástica Artística           | Ouro        | 2024       |
| 3             | Ana Patrícia Ramos           | Brasil   | 1997               | Vôlei de Praia                | Ouro       | 2024     |
| 4             | Caio Bonfim             | Brasil   | 1991               | Atletismo           | Prata        | 2024          |
| 5             | Willian Lima               | Brasil   | 2000               | Judô             | Prata        | 2024          |
| 6             | Rebeca Andrade             | Brasil   | 1999               | Ginástica Artística                | Prata        | 2024             |
| 7             | Rebeca Andrade          | Brasil   | 1999               | Ginástica Artística            | Prata       | 2024          |
| 8             | Tatiana Weston-Webb            | Brasil   | 1996              | Surfe | Prata       | 2024          |
| 9            | Isaquias Queiroz               | Brasil   | 1994               | Canoagem          | Prata      | 2024          |
| 10            | Brasil              | Brasil   | null               | Futebol Feminino          | Prata      | 2024          |
| 11            | Larissa Pimenta               | Brasil   | 1999               | Judô          | Bronze      | 2024          |
| 12            | Rayssa Leal               | Brasil   | 2008               | Skate Street          | Bronze      | 2024          |
| 13            | Bia Ferreira               | Brasil   | 1992               | Boxe          | Bronze      | 2024          |
| 14            | Gabriel Medina               | Brasil   | 1993               | Surfe          | Bronze      | 2024          |
| 15            | Augusto Akio               | Brasil   | 2000               | Skate Park          | Bronze      | 2024          |
| 16            | Edival Pontes               | Brasil   | 1997               | Taekwondo          | Bronze      | 2024          |
| 17            | Alison dos Santos               | Brasil   | 2000               | Atletismo          | Bronze      | 2024          |
| 18            | Brasil               | Brasil   | null               | Vôlei Feminino          | Bronze      | 2024          |
| 19            | Laura Pigossi               | Brasil   | 1994               | Tênis          | null      | 2024          |
| 20            | Amanda Schott               | Brasil   | 1996               | Levantamento de Peso          | null      | 2024          |

Obs: Se você não criou ou não salvou a relação atleta no laboratório passado, será preciso criá-la antes de fazer a inserção das tuplas.

2. Atualizar o nome dos medalhistas de "Brasil" para "Disputa por equipes".

3. Remover os medalhistas sem ano de nascimento.

4. Listar todos os atletas.

5. Listar o nome de todos os atletas nascidos em 1999.

6. Buscar o nome e esporte de todos os atletas que ganharam medalha de ouro.

7. Buscar os atletas que ganharam medalha de prata ou bronze (Dica: pesquise comando IN do SQL).

8. Listar todos os atletas que ganharam medalhas de ouro, mas não de prata nem de bronze.

9. Listar todos os atletas que ganharam medalha no Judô.

10. Buscar nome, medalha e esporte de medalhistas na edição de 2024 com menos de 25 anos.

11. Listar nome e ano de nascimento de atletas com nome começado com a letra A.

12. Listar nome e ano de nascimento de atletas com nome terminado com a letra E.

13. Listar, sem repetições, esportes que contém mais de uma palavra.

14. Listar os esportes praticados por atletas brasileiros medalhistas na edição de 2024.

### 2.3 Análise de Consultas SQL

Agora, você terá de analisar o resultado de algumas consultas SQL já existentes no sistema da COB.

15. Explique o resultado da seguinte consulta:
```
SELECT nome_pais, esporte, edicao_olimpiada
FROM atleta
WHERE edicao_olimpiada = '2024'
EXCEPT
SELECT nome_pais, esporte, edicao_olimpiada
FROM atleta
WHERE medalha IS NOT NULL AND edicao_olimpiada = '2024';
```

16. Explique o resultado das seguintes consultas. Qual a diferença entre eles?
```
SELECT nome_pais, esporte, medalha
FROM atleta
WHERE medalha = 'Ouro'
UNION
SELECT nome_pais, esporte, medalha
FROM atleta
WHERE medalha = 'Prata';
```
```
SELECT nome_pais, esporte, medalha
FROM atleta
WHERE medalha = 'Ouro'
UNION ALL
SELECT nome_pais, esporte, medalha
FROM atleta
WHERE medalha = 'Prata';
```

17. Por que não podemos usar a seguinte consulta para listar sem repetições o nome de todos os medalhistas olímpicos nascidos em 1999? O que precisa ser ajustado nela para que isso seja possível?
```
SELECT DISTINCT nome, medalha
FROM atleta
WHERE ano_nascimento > 2000;
```

### 2.4 Identificação e Correção de Erros em Consultas SQL

Você recebeu uma série de consultas SQL para revisar. Cada consulta contém erros de sintaxe ou semântica que precisam ser identificados e corrigidos. Analise cada uma das seguintes consultas SQL e identifique os erros presentes. Para cada consulta, explique o tipo de erro (sintaxe ou semântica) e forneça a versão corrigida da consulta.

18.
```
INSERT INTO atleta (id, nome, pais, ano_nascimento, esporte, medalha, edicao_olimpiada)
VALUES (1, 'João', 'Brasil', '1985', 'Natação', 'Ouro', 2024);
```

19.
```
UPDATE atleta WHERE nome = 'Rayssa Leal';
```

20.
```
SELECT nome FROM atleta WHERE pais = 'Brasil'
UNION
SELECT ano_nascimento FROM atleta WHERE medalha = 'Ouro';
```

21.
```
SELECT nome, pais FROM atleta WHERE esporte = 'Futebol'
EXCEPT
SELECT medalha FROM atleta WHERE edicao_olimpiada = 2024;
```

## 3. Tarefas


*   Criar consultas SQL (Exercícios 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13 e 14);
*   Analisar resultado de consultas SQL (Exercícios 15, 16 e 17);
*   Identificar e corrigir erros de consultas SQL (Exercícios 18, 19, 20 e 21).

## 4. Submissão

Este laboratório é **indiviual**. Submeta apenas a resposta das **tarefas 15, 16 e 17** utilizando o ambiente **Google Classroom** (googleapps.unicamp.br). Serão aceitos arquivos *.pdf*, *.docx* ou *.txt*. Demais tarefas não precisam ser entregues, mas elas são importantes para garantir a conformidade de suas respostas com os resultados esperados pela correção.

**Data de entrega**: Dia 20/09/2024 até às 23h59.

## 5. Critérios de Avaliação

Serão utilizados os seguintes critérios de avaliação:

*   Descrição correta e em alto nível do resultado de consultas SQL;
*   Identificação de falha semântica em uma consulta SQL envolvendo comandos SELECT e DISTINCT.

Você pode executar as consultas disponibilizadas nas tarefas 15, 16 e 17 no site https://sqliteonline.com/ para verificar seus resultados, mas eles não necessariamente precisam ser entregues. Você pode usar os resultados das consultas para embasar sua explicação, mas o que será avaliado no final é sua capacidade de entender o contexto de execução de uma consulta SQL.
