# Laboratório 6

## 1. Objetivos

- Fixar conhecimentos sobre consultas em SPARQL


## 2. Descrição

O sistema de músicas semelhante ao **Spotify** para o qual você trabalhou no passado está escalando pelo mundo todo. O banco de dados orientado a grafos que você desenvolveu traz informações sobre grandes artistas internacionais da música Pop. Agora, você foi contratado para levantar informações de outros artistas, álbuns e músicas que podem ser acrescidos no sistema.

Para isso, vamos executar consultas em SPARQL no dataset público de dados estruturados da Wikipedia, chamado DBpedia - basta acessar o [editor online de SPARQL do DBpedia](https://dbpedia.org/sparql)


### 2.1 Exemplos de dados estruturados de artistas, álbuns e músicas do DBpedia

Todas as informações disponíveis na Wikipedia sobre Nando Reis, ex-membro dos Titãs e produtor de grandes nomes da MPB como Cássia Eller, estão disponíveis em [https://dbpedia.org/page/Nando_Reis](https://dbpedia.org/page/Nando_Reis).

Informações sobre "O Mundo é Bão Sebastião", música que fez em homenagem a seu terceiro filho, estão disponíveis em [https://dbpedia.org/page/O_Mundo_%C3%89_B%C3%A3o,_Sebasti%C3%A3o!](https://dbpedia.org/page/O_Mundo_%C3%89_B%C3%A3o,_Sebasti%C3%A3o!).

Já informações sobre o álbum dos Titãs "A Melhor Banda de Todos os Tempos da Última Semana" podem ser vistas em [https://dbpedia.org/page/A_Melhor_Banda_de_Todos_os_Tempos_da_%C3%9Altima_Semana](https://dbpedia.org/page/A_Melhor_Banda_de_Todos_os_Tempos_da_%C3%9Altima_Semana).

*Dica: Atente-se às propriedades disponíveis na DBpedia sobre cada um desses tipos de dados. Usaremos tais propriedades para a construção de consultas em SPARQL*


### 2.2 Análise de consultas

Agora que você já viu exemplos de como os dados da DBpedia estão estruturados, explique o retorno das seguintes consultas em SPARQL:

1.
```sql
SELECT ?artist ?name ?birthName ?birthDate ?yearsActive ?abstract
WHERE {
  ?artist dbo:genre dbr:Música_popular_brasileira;
           foaf:name ?name;
          dbp:birthName ?birthName;
          dbo:birthDate ?birthDate;
          dbp:yearsActive ?yearsActive;
          dbo:abstract ?abstract.
FILTER langMatches(lang(?abstract), "pt")
}
```

2.
```sql
SELECT ?name ?writer ?album ?genre
WHERE {
  ?music dbo:artist dbr:Titãs;
   dbp:name ?name;
   dbp:writer ?writer;
   dbp:album ?album;
   dbp:genre ?genre.
}
```


### 2.3 Escrita de consultas

Escreva consultas em SPARQL para buscar:

3. Gêneros distintos associados a artistas da MPB em ordem alfabética

4. Nome e quantidade de álbuns dos 10 artistas do gênero *Pop_music* com mais álbuns

5. 10 gêneros mais associados a artistas da MPB, com exceção do primeiro


### 2.3 Identificação de erro em consultas

Aponte o erro de sintaxe das seguintes consultas:

6.
```sql
SELECT ?artist
WHERE {
  ?album dbo:artist dbr:Emicida.
}
```

7.
```sql
SELECT ?albumName ?artist
WHERE {
  ?album dbp:artist ?artist
         foaf:name ?albumName.
}
```

## 3. Tarefas

- Analisar consultas em SPARQL no DBpedia (Exercícios 1 e 2);
- Escrever consultas em SPARQL para consultar dados no DBpedia (Exercícios 3, 4 e 5);
- Identificar erros de sintaxe em consultas em SPARQL (Exercícios 6 e 7);

## 4. Submissão

Este laboratório pode ser feito em **dupla** ou **indiviual**. Submeta arquivos .pdf, .docx ou .txt no Google Classroom com a resolução apenas dos exercícios:

- Exercícios 3, 4 e 5 (Seção 2.3);

**Data de entrega**: Dia 08/10/2024 até às 23h59.

## 5. Critérios de Avaliação

Serão utilizados os seguintes critérios de avaliação:

- Corretude sintática e semântica das consultas escritas.
