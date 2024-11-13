# Gabarito Laboratório 4

Segue gabarito dos exercícios propostos para entrega no [Laboratório 4](../LAB04/enunciado.md).

## Exercício 9

### Pergunta

Crie consultas em MongoDB para buscar: Nome dos medalhistas de ouro na edição de 2024 dos Jogos Olímpicos

### Resposta

```sql
db.atletas.find(
    { conquistas: { $elemMatch: { ano: 2024, medalhas: "Ouro" } } },
    { nome: 1, _id: 0 }
)
```
ou
```sql
db.atletas.find(
    { "conquistas.ano": 2024, "conquistas.medalhas": "Ouro" },
    { nome: 1, _id: 0}
)
```

### Nota atribuída no exercício

- 10, para quem escreveu uma consulta capaz de trazer os dados solicitados;
- 0, caso contrário.

## Exercício 14

### Pergunta

Crie consultas em MongoDB para buscar: Medalhista mais velho a receber medalha de ouro nas olímpiadas

### Resposta

```sql
db.atletas.find(
    { 'conquistas.medalhas': 'Ouro' }
).sort(
    { ano_nascimento: 1 }
).limit(1)
```

ou consultas correlatas que alteraram os operadores usados para buscar pela medalha de Ouro.

### Nota atribuída no exercício

- 10, para quem escreveu uma consulta capaz de trazer os dados solicitados;
- 9, para quem fez o sort em ordem descendente ao invés de ascendente;
- 0, caso contrário.

## Exercício 17

### Pergunta
Explique, em alto nível, o resultado da seguinte consulta:
```sql
db.atletas.find({
    "conquistas.medalhas": "Prata"
})
```

### Resposta

Documentos de atletas que receberam uma medalha de Prata em alguma edição dos Jogos Olimpícos.

### Nota atribuída no exercício

- 10, para quem explicou corretamente o resultado da consulta;
- 0, caso contrário.

## Exercício 18

### Pergunta
Explique, em alto nível, o resultado da seguinte consulta:
```sql
db.atletas.find({
    "conquistas.medalhas": { $all: ["Ouro", "Prata"] }
})
```

### Resposta

Documentos de atletas que receberam ao menos uma medalha de Ouro e uma de Prata, não necessariamente na mesma edição dos Jogos Olímpicos.

### Nota atribuída no exercício

- 10, para quem explicou corretamente o resultado da consulta (inclusive para os que comentaram que ambas as medalhas deveriam ser ganhas na mesma edição dos Jogos Olímpicos, uma vez que a equivalência do operador ```$all``` com um ```$and``` foi abordada neste exercício mas não nos slides da aula);
- 0, caso contrário.

## Exercício 19

### Pergunta
Explique, em alto nível, o resultado da seguinte consulta:
```sql
db.atletas.find({
    "conquistas.medalhas": ["Ouro", "Prata"]
})
```

### Resposta

Documentos de atletas que apenas receberam uma medalha de Ouro e outra de Prata em uma mesma edição dos Jogos Olimpícos, nessa ordem.

### Nota atribuída no exercício

- 10, para quem explicou corretamente o resultado da consulta;
- 8, para quem não citou que a ordem de recebimento das medalhas (primeiro "Ouro" e depois "Prata") era necessária;
- 0, caso contrário.

## Exercício 20

### Pergunta
Explique, em alto nível, o resultado da seguinte consulta:
```sql
db.atletas.find({
    conquistas: { $size: 1 }
}).sort({
    ano_nascimento: -1
}).limit(3)
```

### Resposta

Documentos dos 3 atletas mais jovens que só receberam medalhas em 1 edição dos Jogos Olímpicos.

### Nota atribuída no exercício

- 10, para quem explicou corretamente o resultado da consulta (incluindo quem não comentou que os atletas só deveriam ter conquistas em 1 edição dos Jogos Olímpicos, pois o operador ```$size``` não foi visto em aula teórica);
- 0, caso contrário.

## Exercício 22

### Pergunta
Aponte o erro da seguinte consulta:
```sql
db.atletas.find({
    ano_nascimento: { $gt: "1995" },
    ano_nascimento: { $lt: "2000" }
})
```

### Resposta

Os operadores ```$gt``` e ```$lt``` só funcionam quando aplicados a números inteiros. Ademais, o MongoDB exige que múltiplos filtros aplicados a um mesmo atributo sejam combinados num mesmo objeto. Nesse sentido, a sintaxe correta dessa consulta seria:
```sql
db.atletas.find({
    ano_nascimento: { $gt: 1995, $lt: 2000 }
})
```

### Nota atribuída no exercício

- 10, para quem apontou ao menos um dos erros da consulta;
- 0, caso contrário.

## Exercício 25

### Pergunta
Aponte o erro da seguinte consulta:
```sql
db.atletas.find({
  conquistas: {
    medalhas: {
        $elemMatch: { $in: ["Ouro", "Prata"] }
    }
  }
})
```

### Resposta

O operador ```$elemMatch``` precisa ser usado logo após indicarmos o caminho completo até o array em que desejamos aplicá-lo. Como queremos acessar o array ```medalhas``` dos objetos salvos no array ```conquistas```, o correto seria reescrever a consulta com a seguinte sintaxe:
```sql
db.atletas.find({
  "conquistas": {
    $elemMatch: { 
        medalhas: { $in: ["Ouro", "Prata"] }
    }
  }
})
```
ou
```sql
db.atletas.find({
    "conquistas.medalhas": {
        $elemMatch: { $in: ["Ouro", "Prata"] }
    } 
})
```
ou, se quisermos simplificar a consulta:
```sql
db.atletas.find({
    "conquistas.medalhas": { $in: ["Ouro", "Prata"] }
})
```

### Nota atribuída no exercício

- 10, para quem apontou o erro da consulta corretamente;
- 0, caso contrário.

## Composição da nota final

Média aritmética entre notas obtidas nos exercícios 9, 14, 17, 18, 19, 20, 22 e 25.