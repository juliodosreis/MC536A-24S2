# Gabarito Laboratório 2

Segue gabarito dos exercícios propostos para entrega no [Laboratório 2](../LAB02/enunciado.md).

## Exercício 15

### Pergunta

Explique o resultado da seguinte consulta:
```sql
SELECT nome_pais, esporte, edicao_olimpiada
FROM atleta
WHERE edicao_olimpiada = '2024'
EXCEPT
SELECT nome_pais, esporte, edicao_olimpiada
FROM atleta
WHERE medalha IS NOT NULL AND edicao_olimpiada = '2024';
```

### Resposta

Com o primeiro SELECT:
```sql
SELECT nome_pais, esporte, edicao_olimpiada
FROM atleta
WHERE edicao_olimpiada = '2024'
```
selecionamos os atributos nome_pais, esporte e edicao_olimpiada de atletas que participaram dos Jogos Olímpicos de 2024.

Com o segundo SELECT:
```sql
SELECT nome_pais, esporte, edicao_olimpiada
FROM atleta
WHERE medalha IS NOT NULL AND edicao_olimpiada = '2024';
```
selecionamos os atributos nome_pais, esporte e edicao_olimpiada de atletas que participaram dos Jogos Olímpicos de 2024 e ganharam medalhas.

Ao aplicarmos o comando ```EXCEPT``` entre essas consultas, temos como resultado tuplas retornadas no primeiro SELECT que não foram retornadas no segundo.

Em alto nível, estamos falando de atributos nome_pais, esporte e edicao_olimpiada de atletas que participaram dos Jogos Olímpicos de 2024 mas **não** ganharam medalhas.

### Nota atribuída no exercício

- 10, para quem identificou que apenas atletas dos Jogos Olímpicos de 2024 sem medalhas seriam retornados;
- 0, caso contrário.

## Exercício 16

### Pergunta

Explique o resultado das seguintes consultas. Qual a diferença entre eles?
```sql
SELECT nome_pais, esporte, medalha
FROM atleta
WHERE medalha = 'Ouro'
UNION
SELECT nome_pais, esporte, medalha
FROM atleta
WHERE medalha = 'Prata';
```
```sql
SELECT nome_pais, esporte, medalha
FROM atleta
WHERE medalha = 'Ouro'
UNION ALL
SELECT nome_pais, esporte, medalha
FROM atleta
WHERE medalha = 'Prata';
```

### Resposta

Ambas as consultas trazem os atributos nome_pais, esporte, medalha de atletas que já ganharam medalhas de Ouro ou Prata em uma das edições dos jogos olímpicos. A diferença entre elas está na remoção de tuplas duplicadas dos resultados, que acontece apenas na primeira consulta devido ao uso do comando UNION. Ao usarmos UNION ALL, estamos forçando nosso SGBD a ignorar o comportamento padrão do UNION e retornar tuplas duplicadas no resultado.

### Nota atribuída no exercício

- 10, para quem explicou corretamente a diferença entre os comandos UNION e UNION ALL;
- 0, caso contrário.

## Exercício 17

### Pergunta
Por que não podemos usar a seguinte consulta para listar sem repetições o nome de todos os medalhistas olímpicos nascidos em 1999? O que precisa ser ajustado nela para que isso seja possível?
```sql
SELECT DISTINCT nome, medalha
FROM atleta
WHERE ano_nascimento > 2000;
```

### Resposta

Há 3 erros que precisam ser corrigidos nessa consulta para que ela traga o dado esperado:

1. É preciso filtrar atletas cujo ano de nascimento é exatamente 1999, e não maior que 2000;

2. É preciso filtrar atletas que receberam alguma medalha, uma vez que o atributo ```medalha``` pode ser nulo e desejamos apenas o nome de medalhistas olímpicos;

3. Para selecionar o nome dos medalhitas sem repetições, só devemos aplicar o comando DISTINCT ao atributo ```nome``` - se aplicarmos o DISTINCT à combinação de atributos ```nome``` e ```medalha```, só estaremos garantindo que essa combinação não vai se repetir nos resultados; isto é, se um mesmo atleta receber tipos de medalhas distintas em sua carreira, seu nome vai aparecer duplicado nos resultados - uma vez ao lado de cada tipo de medalha que ele já ganhou.

Ao ajustarmos esses 3 erros, a consulta poderia ser reescrita numa das seguintes formas:

```sql
SELECT DISTINCT nome
FROM atleta
WHERE ano_nascimento = 1999
AND medalha IS NOT NULL;
```

```sql
SELECT DISTINCT nome
FROM atleta
WHERE ano_nascimento = 1999
AND medalha IN ('Ouro', 'Prata', 'Bronze');
```

### Nota atribuída no exercício

- 10, para quem apontou e corrigiu adequadamente os 3 erros da consulta;
- 8, para quem só apontou e corrigiu os erros 1 e 3;
- 7, para quem só apontou e corrigiu os erros 1 e 2;
- 5, para quem só apontou e corrigiu erro 3;
- 0, para quem não apontou nem corrigiu nenhum dos erros.