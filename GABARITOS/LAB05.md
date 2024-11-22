# Gabarito Laboratório 5

Segue gabarito dos exercícios propostos para entrega no [Laboratório 5](../LAB05/enunciado.md).

## Exercício 5
### Pergunta
Escreva uma consulta para contar quantos usuários ouviram músicas do gênero "Pop".

### Resposta
```cypher
MATCH (user:User)-[:LISTENED]->(music:Music)-[:HAS_GENRE]->(genre:Genre {name: "Pop"})
RETURN COUNT(DISTINCT user)

```
### Nota atribuída no exercício
- 10, para quem escreveu uma consulta capaz de trazer os dados solicitados (a sintaxis pode mudar um pouco do mostrado);
- 8, não usou DISTINCT (isso pode duplicar usuario)
- 0, caso contrário.

## Exercício 6

### Pergunta
Encontre o total de músicas de cada gênero no banco de dados e ordene o resultado de forma decrescente com base na quantidade de músicas por gênero.

### Resposta
```cypher
MATCH (music:Music)-[:HAS_GENRE]->(genre:Genre)
RETURN genre.name, COUNT(music) AS total_musics
ORDER BY total_musics DESC

```
### Nota atribuída no exercício
- 10, para quem escreveu uma consulta capaz de trazer os dados solicitados;
- 0, caso contrário.


## Exercício 8

### Pergunta
Encontre todos as músicas lançadas no ano de 2016 ou posterior e retorne o nome da musíca (title) e o ano de lançamento.
### Resposta
```cypher
MATCH (music:Music)-[:RELEASED_IN]->(year:Year)
WHERE year.year >= 2016
RETURN music.title, year.year

```
### Nota atribuída no exercício
- 10, para quem escreveu uma consulta capaz de trazer os dados solicitados;
- 0, caso contrário.

## Exercício 10

### Pergunta
Retorne o total de álbuns criados por cada artista.
### Resposta
```cypher
MATCH (artist:Artist)-[:CREATED]->(album:Album)
RETURN artist.name, COUNT(album) AS total_albums

```
### Nota atribuída no exercício
- 10, para quem escreveu uma consulta capaz de trazer os dados solicitados;
- 0, caso contrário.
## Exercício 12

### Pergunta
```cypher
MATCH (user:User)-[:LISTENED]->(music:Music)-[:HAS_GENRE]->(genre:Genre)
RETURN user.username, genre.name
```
### Resposta
Essa consulta retorna o nome de usuário dos usuários que ouviram músicas e os gêneros dessas músicas. Ela percorre a relação entre os usuários, as músicas que eles ouviram e os gêneros dessas músicas.
### Nota atribuída no exercício
- 10, Explica adequadamente a saída.

- 0, Outro caso

## Exercício 15

### Pergunta
```cypher
MATCH (user:User)-[:LISTENED]->(music:Music)
RETURN user.username, COUNT(music) AS total_musics_listened
```
### Resposta
A consulta retorna o nome de cada usuário e o total de músicas que ele escutou. Ela conta o número de nós de Music conectados a cada User através da relação LISTENED.
### Nota atribuída no exercício
- 10, Explica adequadamente a saída.
- 0, Outro caso
## Exercício 24

### Pergunta
```cypher
MATCH (user:User)-[:DISLIKES]->(music:Music)
RETURN user.username, music.title
```
### Resposta
A relação DISLIKES conecta usuários a gêneros, não diretamente a músicas.
```cypher
MATCH (user:User)-[:DISLIKES]->(genre:Genre)<-[:HAS_GENRE]-(music:Music)
RETURN user.username, music.title

```

Corrige a relação para conectar usuários a gêneros que eles desgostam e, em seguida, encontra as músicas associadas a esses gêneros.
### Nota atribuída no exercício
- 10, conserto e explico o porque a query estava errada
- 8 conserto sem explicar ou conserto sem relacionar o genero com a musica.
- 6 aponto sem consertar a consulta
- 0, outro caso
## Exercício 25

### Pergunta
```cypher
MATCH (artist:Artist {name: "Taylor Swift"})-[:SIMILAR_TO]-(similar_artist)-[:CREATED]->(music:Music)
RETURN music.title
```
### Resposta
O relacionamento SIMILAR_TO deve ser direcionado corretamente com -[:SIMILAR_TO]->.

```cypher
MATCH (artist:Artist {name: "Taylor Swift"})-[:SIMILAR_TO]->(similar_artist)-[:CREATED]->(album:Album)-[:OWNS]->(music:Music)
RETURN music.title

```


A relação SIMILAR_TO precisa ser direcionada corretamente, e a conexão entre Album e Music foi adicionada.
### Nota atribuída no exercício
- 10, conserto e explico o porque a query estava errada
- 8 conserto sem explicar.
- 6 aponto sem consertar a consulta
- 0, outro caso