# Laboratorio 1
## 1. Objetivos

Este laboratório tem os seguintes objetivos de aprendizagem:
+ Uso inicial de SQL para criação do projeto físico de um banco de dados;
+ Criação de tabelas com base nos esquemas das relações;
+ Aplicação do conceito de integridade referencial;
+ Criação de índices.

## 2. Descrição

Neste laboratório, vamos criar um banco de dados para armazenar informações sobre Jogos Olímpicos. Sua tarefa será executar comandos em SQL para criar tabelas que contenham dados de atletas, suas participações em diferentes edições dos jogos e as medalhas nelas conquistadas. Também será preciso modificar a estrutura das tabelas inicialmente criadas, de modo que você tenha a experiência de atualizar um banco de dados já existente. 


### 2.1 Criação de um novo banco de dados

Acesse o site [sandboxsql](https://sandboxsql.com/). Selecione a opção "New Empty Database" para criar um banco de dados vazio. Crie as tabelas especificadas nas subseções seguintes nesse banco de dados.

<img src="/Images/sandbox.png">


### 2.2 Criação da tabela "atleta"
Crie a tabela "atleta" para armazenar dados de atletas, das medalhas que eles conquistaram e da edição dos Jogos Olímpicos nas quais elas foram conquistadas, com as seguintes colunas:
+ **id** (inteiro, chave primária): Identificador único do atleta.
+ **nome** (texto): Nome do atleta.
+ **pais** (texto): País de origem do atleta.
+ **ano_nascimento** (inteiro): Ano de nascimento do atleta.
+ **esporte** (texto): Esporte que o atleta compete.
+ **medalha** (texto): Tipo de medalha que o atleta ganhou (se aplicável)
+ **edicao_olimpiada** (inteiro): Ano da edição dos Jogos Olímpicos em que o atleta participou.

**Depois de criar essa tabela:**
+ Adicione uma nova coluna a ela chamada peso (decimal), para armazenar o peso do atleta;
+ Remova a coluna ano_nascimento;
+ Crie um índice nessa tabela que facilite a busca por atletas que ganharam medalhas de ouro com menos de 25 anos.

### 2.3 Criação da tabela "esporte" 
Crie a tabela "esporte" com as seguintes colunas e restrições:
+ **id_esporte**: número inteiro que identifica de forma única o esporte (maior que zero);
+ **nome_esporte**: cadeia de caracteres que representa o nome do esporte (não nulo, com pelo menos três caracteres);
+ **categoria**: cadeia de caracteres que indica se o esporte é individual ou em equipe (aceita apenas valores "individual" ou "equipe");
+ **regras_basicas**: cadeia de caracteres que descreve as regras básicas do esporte (opcional, mas, se presente, deve ter pelo menos 10 caracteres);

Feito isto, adicione mais uma coluna de preenchimento obrigatório na tabela. Ela deve guardar a informação que você julgar mais pertinente ao problema.

### 2.4 Criação da tabela "pais"
Crie a tabela "pais" com as seguintes colunas e restrições:

+ **id_pais**: número inteiro que identifica de forma única o país (maior que zero);
+ **nome_pais**: cadeia de caracteres que representa o nome do país (não nulo, com pelo menos três caracteres);
+ **sigla_pais**: cadeia de três caracteres que representa a sigla oficial do país (exatamente três caracteres);
+ **continente**: cadeia de caracteres que representa o continente ao qual o país pertence (não nulo).

### 2.5 Criação da tabela "competicoes"
 Crie a tabela "competicao" com as colunas descritas na Tabela, para salvar os resultados das competoções dos Jogos Olímpicos. Use as restrições de integridade que julgar mais adequadas, justificando-as.

 | Coluna           | Descrição                               |
|------------------|-----------------------------------------|
| id_competicao     | Identificador único da competição       |
| nome_esporte      | Nome do esporte                         |
| data_competicao   | Data da competição                      |
| local             | Local onde a competição ocorreu         |
| pais_sede         | País sede da competição                 |
| num_participantes | Número de participantes (não pode ser negativo) |
| id_edicao         | Deve referenciar uma edição dos Jogos Olímpicos |

### 2.6 Criação de uma nova tabela
Com base no contexto dos Jogos Olímpicos, proponha uma nova tabela para compor nosso banco de dados diferente das que já foram apresentadas ("atleta", "esporte", "pais" e "resultado"). Pense primeiro no nome e esquema da nova tabela. Depois, crie ela no banco de dados. Lembre de definir suas chaves primárias, estrangeiras (caso preciso) e restrições de integridade. Crie também um índice para essa tabela (Dica: tente pensar nos campos que mais seriam acessados nessa tabela, isto é, nos mais relevantes para uma aplicação no contexto dos Jogos Olímpicos).

## 3. Tarefas
Siga as instruções da **Seção 2** para:
+ Criar um novo banco de dados em sandboxsql;
+ Definir chaves primárias, estrangeiras e restrições de integridade para as tabelas desse banco de dados;
+ Criar e modificar tabelas;
+ Criar índices.