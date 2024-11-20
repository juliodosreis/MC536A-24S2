# Gabarito Laboratório 6

Segue gabarito dos exercícios propostos para entrega no [Laboratório 6](../LAB06/enunciado.md).

## Exercício 3

### Pergunta

Escreva consulta em SPARQL para buscar: Gêneros distintos associados a artistas da MPB em ordem alfabética

### Resposta

```sql
SELECT DISTINCT ?genre
WHERE {
  ?artist dbo:genre dbr:Música_popular_brasileira;
          dbo:genre ?genre.
}
ORDER BY ?genre
```
ou
```sql
SELECT DISTINCT ?name
WHERE {
  ?artist dbo:genre dbr:Música_popular_brasileira.
  ?genre foaf:name ?name.
}
ORDER BY ?name
```

### Nota atribuída no exercício

- 10, para quem escreveu uma consulta capaz de trazer os dados solicitados;
- 0, caso contrário.

## Exercício 4

### Pergunta

Escreva consulta em SPARQL para buscar: Nome e quantidade de álbuns dos 10 artistas do gênero Pop_music com mais álbuns

### Resposta

```sql
SELECT ?name (COUNT(?album) AS ?albumCount)
WHERE {
  ?artist dbo:genre dbr:Pop_music;
        foaf:name ?name.
  ?album dbo:artist ?artist.
}
GROUP BY ?name
ORDER BY DESC(?albumCount)
LIMIT 10
```
ou
```sql
SELECT ?artist (COUNT(?album) AS ?albumCount)
WHERE {
  ?artist dbo:genre dbr:Pop_music ;
          dbo:album ?album.
}
GROUP BY ?artist
ORDER BY DESC(?albumCount)
LIMIT 10
```
ou
```sql
SELECT ?artist (COUNT(?album) AS ?albumCount)
WHERE {
  ?album dbo:artist ?artist;
        dbo:genre dbr:Pop_music.

}
ORDER BY DESC(?albumCount)
LIMIT 10
```

### Nota atribuída no exercício

- 10, para quem escreveu uma consulta capaz de trazer os dados solicitados;
- 5, para quem escreveu uma consulta sintaticamente correta, mas que não trouxe os dados solicitados;
- 0, caso contrário.

## Exercício 5

### Pergunta

Escreva consulta em SPARQL para buscar: 10 gêneros mais associados a artistas da MPB, com exceção do primeiro

### Resposta

```sql
SELECT DISTINCT ?genre
WHERE {
  ?artist dbo:genre dbr:Música_popular_brasileira;
          dbo:genre ?genre.
}
ORDER BY DESC(COUNT(?genre))
OFFSET 1
LIMIT 10
```
ou
```sql
SELECT ?genre (COUNT(?artist) AS ?artistCount)
WHERE {
  ?artist dbo:genre dbr:Música_popular_brasileira;
          dbo:genre ?genre.
}
GROUP BY ?genre
ORDER BY DESC(?artistCount)
OFFSET 1
LIMIT 10
```
ou
```sql
SELECT ?genre (COUNT(?artist) AS ?artistCount)
WHERE {
  ?artist a dbo:MusicalArtist;
            dbo:genre dbr:Música_popular_brasileira;
            dbo:genre ?genre
  FILTER (?genre != dbr:Música_popular_brasileira)
}
GROUP BY ?genre
ORDER BY DESC(?artistCount)
LIMIT 10
```

### Nota atribuída no exercício

- 10, para quem escreveu uma consulta capaz de trazer os dados solicitados;
- 0, caso contrário.

## Composição da nota final

Média aritmética entre notas obtidas nos exercícios 3, 4 e 5.