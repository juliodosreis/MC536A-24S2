# Laboratório 3
## 1. Objetivos

*   Familiazar-se com operações de junção, funções agregadas e ordenação.
*   Criar consultas SQL que utilizem comandos:
      + JOIN
      + WHERE
      + GROUP BY
      + HAVING
      + ORDER BY
      + CASE
      

## 2. Descrição
Por ter demonstrado excelência em seu trabalho no COB (Comitê Olímpico do Brasil), foi contratado para explorar e analisar os dados relevantes das últimas edições dos Jogos Olimpicos.
Para isso voce usará uma amostra dos [Dados historicos das olimpiadas](https://basedosdados.org/dataset/62f8cb83-ac37-48be-874b-b94dd92d3e2b?table=08089f55-ccf3-474e-80c7-d531d859689a), com o objetivo de agilizar seu trabalho, vamos focar em três relações: **atlethe**,**results** e **medals** que disponibilizamos no [link](https://drive.google.com/drive/folders/1-CMY5wzDEAABgSuQ3QjaC1mGyqGnrmL8?usp=sharing), nós detalharemos as relações nos próximos parágrafos.

### 2.1 Relações

#### atlethe
Representa um atleta olímpico e conte os seguintes atributos do atleta:
+ athlete_id : representa o identificador. 
+ name: nome
+ sex: sexo
+ birth_year: ano de nascimento.
+ height: peso
+ weight: altura
+ country: país
+ country_noc: código do país

A seguir, é apresentada uma tabela que ilustra os dados armazenados na mesma.
|       |   athlete_id | name                   | sex   | birth_date   |   birth_year |   height |   weight | country               | country_noc   |
|------:|-------------:|:-----------------------|:------|:-------------|-------------:|---------:|---------:|:----------------------|:--------------|
| 1 |        54029 | Frank Otto             | Male  | 1958-02-10   |         1958 |      193 |       94 | Germany  West Germany | GER           |
| 2 |        54886 | Dave Ashleigh          | Male  | 1943-08-08   |         1943 |      183 |       77 | United States         | USA           |
| 3 |        74767 | Kazimierz Kropidłowski | Male  | 1931-08-16   |         1931 |      174 |       78 | Poland                | POL           |
| 4 |        71247 | Miklós Németh          | Male  | 1946-10-23   |         1946 |      193 |       95 | Hungary               | HUN           |
| 5 |        79267 | Horacio Esteves        | Male  | 1941-07-06   |         1941 |      175 |       73 | Venezuela             | VEN           |

#### results
Conjunto de dados de resultados de evento para atleta. 
+ edition: edicão no formato *Ano - Verão / Inverno - Jogos Olímpicos*
+ edition_id: identificador da edicão dos jogos
+ country_noc: código do país dos jogos
+ sport: esporte
+ event: evento especifico para um esporte
+ result_id: identificador do resultado
+ athlete: nome do atleta
+ athlete_id: identificador do atleta
+ position: posição no resultado
+ medal: se o atleta ganhou uma medalha ou não, e se sim, ouro, prata ou bronze

+ is_team_sport: se o evento é um esporte de equipe ou não



|    | edition              |   edition_id | country_noc   | sport      | event            |   result_id | athlete        |   athlete_id |   position | medal   | is_team_sport   |
|---:|:---------------------|-------------:|:--------------|:-----------|:-----------------|------------:|:---------------|-------------:|-----------:|:--------|:----------------|
|  0 | 1936 Summer Olympics |           11 | GER           | Rowing     | Coxed Fours, Men |      157975 | Fritz Bauer    |        37754 |          1 | Gold    | True            |
|  1 | 1900 Summer Olympics |            2 | GER           | Rowing     | Coxed Fours, Men |      157515 | Hugo Rüster    |        37978 |          3 | Bronze  | True            |
|  2 | 1972 Summer Olympics |           18 | ROU           | Handball   | Handball, Men    |       34518 | Werner Stöckl  |        32605 |          3 | Bronze  | True            |
|  3 | 1960 Winter Olympics |           36 | USA           | Ice Hockey | Ice Hockey, Men  |       20243 | Bobby Cleary   |        84800 |          1 | Gold    | True            |
|  4 | 1984 Winter Olympics |           42 | TCH           | Ice Hockey | Ice Hockey, Men  |       20516 | Jaromír Šindel |        97564 |          2 | Silver  | True            |


#### medals
Representa o registro dos países que obtiveram medalhas em cada edição dos Jogos Olímpicos, considerando os resultados de todos os eventos.
+ year: ano em que o evento foi realizado
+ edition: edicão no formato *Ano - Verão / Inverno - Jogos Olímpicos*
+ edition_id: identificador da edicão dos jogos
+ country: país que participou nessa edicão dos jogos
+ country_noc: código do país que participou nessa edicão dos jogos
+ gold: quantidade de medalhas de ouro
+ silver: quantidade de medalhas de prata
+ bronze: quantidade de medalhas de bronze
+ total: total de medalhas

|    |   year | edition              |   edition_id | country                  | country_noc   |   gold |   silver |   bronze |   total |
|---:|-------:|:---------------------|-------------:|:-------------------------|:--------------|-------:|---------:|---------:|--------:|
|  0 |   1936 | 1936 Winter Olympics |           32 | Canada                   | CAN           |      0 |        1 |        0 |       1 |
|  1 |   1920 | 1920 Summer Olympics |            7 | Brazil                   | BRA           |      1 |        1 |        1 |       3 |
|  2 |   1948 | 1948 Summer Olympics |           12 | Türkiye                  | TUR           |      6 |        4 |        2 |      12 |
|  3 |   1980 | 1980 Summer Olympics |           20 | Hungary                  | HUN           |      7 |       10 |       15 |      32 |
|  4 |   1948 | 1948 Summer Olympics |           12 | Islamic Republic of Iran | IRI           |      0 |        0 |        1 |       1 |














Suas primeiras tarefas estão descritas nas seções seguintes.

### 2.2 Acesso ao ambiente de execução SQL

Nós usaremos novamento o SQL Online IDE (https://sqliteonline.com/) do anterior laboratório. Selecione a opção "PotsgreSQL" no menu lateral esquerdo para executar consultas SQL através do SGBD open source PostgreSQL.
Para este laboratório, utilizaremos as relações descritas na Seção 2.1 que pode ser baixado no [link](https://drive.google.com/drive/folders/1-CMY5wzDEAABgSuQ3QjaC1mGyqGnrmL8?usp=sharing).

Para este laboratório, escolhemos a opção **Import** e selecionamos os arquivos baixados um de cada vez.
<img src="/Images/sql-online-ide.jpeg">
Figura 1: Interface do SQL Online IDE

Abaixo, é mostrada uma imagem que exemplifica como a configuração deve ser feita após ter carregado o arquivo.
Você pode editar a tabela na opção **Table Name**. Recomendamos usar os nomes descritos nesse tutorial para evitar confusões.

Além disso, é necessário selecionar a opção **Column name** e colocá-la na linha inicial (First line).
<img src="/Images/import.png"> 
Figura 2: Importando arquivo no sqliteonline




### 2.3 Escrita de Consultas SQL



Você recebeu uma lista de desafio para testar suas habilidades na linguagem SQL
1. Escreva uma consulta que liste o nome do atleta, o país e o esporte para os atletas que ganharam medalhas. Use a tabela **athlete** e a tabela **result**.

2. Crie uma consulta que retorne o nome do atleta e sua posição, incluindo os atletas que não participaram de nenhuma edição dos jogos. 
3. Escreva uma consulta para listar o nome do atleta e o evento, mostrando todos os eventos, incluindo aqueles sem atletas associados. 
4. Escreva uma consulta para listar o nome do atleta e a medalha conquistada, incluindo atletas que não conquistaram nenhuma medalha.
3. Escreva uma consulta que retorne o total de medalhas de ouro conquistadas por cada país.
4. Crie uma consulta que agrupe os atletas pelo país e mostre a quantidade de atletas em cada país.
5. Escreva uma consulta que retorne a altura média dos atletas por sexo.
6. Escreva uma consulta que agrupe os atletas pelo país e mostre a média de altura, considerando apenas os países que têm mais de 10 atletas.
7. Escreva uma consulta que retorne o país, a edição dos Jogos Olímpicos e o número de atletas que participaram dessa edição.
7. Escreva uma consulta que retorne o nome dos atletas, o esporte, o país, e a edição dos Jogos Olímpicos em que competiram, apenas para as edições realizadas no verão.
8. Escreva uma consulta que retorne os atletas, ordenados pelo ano de nascimento em ordem crescente.
9. Escreva uma consulta que liste os países ordenados pelo total de medalhas em ordem decrescente.
10. Crie uma consulta que liste os atletas ordenados primeiro pelo país (ascendente) e depois pela altura (descendente).
11. Escreva uma consulta que exiba o nome do atleta e uma coluna indicando se ele ganhou uma medalha ou não, usando o comando **CASE**.
12. Crie uma consulta que retorne o país e o total de medalhas, diferenciando entre esportes de equipe e individuais, usando o comando **CASE**.
13. Escreva uma consulta que agrupe os países pela quantidade total de medalhas e categorize o país como "Alta Performance" se o total de medalhas for maior que 50, ou "Baixa Performance" caso contrário.

### 2.4 Análise de Consultas SQL

Agora, você terá de analisar o resultado de algumas consultas SQL.
17. Explique o resultado da seguinte consulta:
```sql
SELECT a.name, r.event
FROM athlete a
LEFT JOIN results r ON a.athlete_id = r.athlete_id;

```
18. Analise a consulta a seguir:
```sql
SELECT r.event, a.name
FROM results r
RIGHT JOIN athlete a ON r.athlete_id = a.athlete_id;

```
19. Analise a consulta e explique o que ela faz:
```sql
SELECT m.country, SUM(m.gold) AS total_ouro
FROM medals m
GROUP BY m.country;

```
20. Analise a consulta abaixo:
```sql
SELECT country, MAX(weight) AS max_peso, MIN(weight) AS min_peso
FROM athlete
GROUP BY country;
```
21. Explique o que a seguinte consulta retorna:
```sql
SELECT country, COUNT(*) AS total_atletas
FROM athlete
GROUP BY country
HAVING COUNT(*) > 50;
```
22. Analise a consulta a seguir:
```sql
SELECT r.sport, SUM(CASE WHEN r.medal = 'Gold' THEN 1 ELSE 0 END) AS ouro,
             SUM(CASE WHEN r.medal = 'Silver' THEN 1 ELSE 0 END) AS prata
FROM results r
GROUP BY r.sport;

```
23. Analise o que a consulta faz:
```sql
SELECT a.name, a.height
FROM athlete a
ORDER BY a.height ASC;
```
### 2.5 Identificação e Correção de Erros em Consultas SQL

Você recebeu uma série de consultas SQL para revisar. Cada consulta contém erros de sintaxe ou semântica que precisam ser identificados e corrigidos. Analise cada uma das seguintes consultas SQL e identifique os erros presentes. Para cada consulta, explique o tipo de erro (sintaxe ou semântica) e forneça a versão corrigida da consulta.
24. Corrija o erro de lógica na consulta abaixo:
```sql
SELECT country, COUNT(weight)
FROM athlete
GROUP BY country;

```
25. Corrija o erro na seguinte consulta:
```sql
SELECT a.name, r.sport
FROM athlete a
INNER JOIN results r;
```
26. Corrija a seguinte consulta que retorna o número de atletas por país:
```sql
SELECT country, COUNT(*)
FROM athlete;
```
27. Corrija o erro nesta consulta:
```sql
SELECT country, SUM(gold)
FROM medals
GROUP BY country;
```
28. Corrija a seguinte consulta para calcular a altura média dos atletas que têm resultados:
```sql
SELECT AVG(height)
FROM athlete;
```
29. Corrija o erro de sintaxe na consulta abaixo:
```sql
SELECT country, COUNT(*)
FROM athlete
HAVING COUNT(*) > 50;
```
30. Corrija a consulta para filtrar atletas do sexo feminino:
```sql
SELECT sex, COUNT(*)
FROM athlete
GROUP BY sex
HAVING sex = 'F';
```
31. Corrija o erro na consulta abaixo:
```sql
SELECT country, COUNT(*), AVG(height)
FROM athlete;

```
32. Corrija o erro na consulta abaixo:
```sql
SELECT r.edition, COUNT(a.athlete_id) AS total_atletas
FROM athlete a
JOIN results r ON a.athlete_id = r.athlete_id
GROUP BY r.edition
ORDER BY a.name ASC;
```
## 3. Tarefas


*   Criar consultas SQL (Tarefas 1-16);
*   Analisar resultado de consultas SQL (Tarefas 17-23);
*   Identificar e corrigir erros de consultas SQL (Tarefas 24-32).

## 4. Submissão

Este laboratório pode ser feito em **dupla** ou **indiviual**. Submeta apenas a resposta das:
+ Seção 2.3 (Tarefas 1, 5, 8, 16)
+ Seção 2.4 (Tarefas 17, 19, 22)
+ Seção 2.5 (Tarefas 27, 28, 32)
 utilizando o ambiente **Google Classroom** (googleapps.unicamp.br). Serão aceitos arquivos *.pdf*, *.docx* ou *.txt*. Demais tarefas não precisam ser entregues, mas elas são importantes para garantir a conformidade de suas respostas com os resultados esperados pela correção.

**Data de entrega**: Dia 27/09/2024 até às 23h59.

## 5. Critérios de Avaliação

Serão utilizados os seguintes critérios de avaliação:

*   Descrição correta e em alto nível do resultado de consultas SQL;
*   Identificação de falha semântica em uma consulta SQL

Você pode executar as consultas disponibilizadas nas tarefas no site https://sqliteonline.com/ para verificar seus resultados, mas eles não necessariamente precisam ser entregues. Você pode usar os resultados das consultas para embasar sua explicação, mas o que será avaliado no final é sua capacidade de entender o contexto de execução de uma consulta SQL.
