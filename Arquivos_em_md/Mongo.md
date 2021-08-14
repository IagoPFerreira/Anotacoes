# Mongo

Mongo é uma lingaguem de banco de dados, parecida com MySQL, a diferença é que Mongo é usada em Banco de Dados não relacionais, ou seja, não existem interações entre bancos e/ou tabelas.

A estrutura do Mongo se consiste em:

- diversos bancos de dados;
- diversas coleções dentro desses bancos;
- diversos documentos dentro dessas coleções.

Fazendo um paralelo, as coleções são equivalentes às tabelas dos bancos de dados relacionais e os documentos são equivalentes aos registros, como linhas e colunas.

---

## Sumário

- [Configurando a inicialização do servidor do MongoDB](#Configurando-a-inicialização-do-servidor-do-MongoDB)
- [Bancos de Dados](#Bancos-de-Dados)
- [Coleções](#Coleções)
  - [Criando uma coleção](#Criando-uma-coleção)
  - [Criação explícita](#Criação-explícita)
- [Documentos](#Documentos)
- [BSON Types](#BSON-Types)
- [Insert](#Insert)
- [Find](#Find)
  - [Projection](#Projection)
- [Operadores em Mongo](#Operadores-em-Mongo)
- [Comandos em Mongo](#Comandos-em-Mongo)
  - [CRUD](#CRUD)
  - [Outros métodos](#Outros-métodos)
  - [Operadores de comparação](#Operadores-de-comparação)
  - [Operadores lógicos](#Operadores-lógicos)
  - [Operador de existência](#Operador-de-existência)

---

## Configurando a inicialização do servidor do MongoDB

Por padrão, após a instalação, seu servidor vai estar configurado para não iniciar junto ao sistema. Caso queira ativar o início automático quando ligar o computador, utilize o comando:

~~~bash
sudo systemctl enable mongod.service
~~~

Caso não queira mais que isso aconteça (para poupar memória RAM, por exemplo), você pode desativar o início automático utilizando o comando:

~~~bash
sudo systemctl disable mongod.service
~~~

Na primeira vez que for utilizar o `MongoDB` após ligar o computador, será necessário iniciar o servidor com o comando:

~~~bash
sudo service mongod start
~~~

---

## Bancos de Dados

Assim como nos sistemas gerenciadores de bancos de dados relacionais, dentro de uma mesma instância do `MongoDB` é possível ter um ou vários bancos de dados. Uma grande diferença, é que não existe a formalidade de criar um banco de dados antes de fazer uma operação nele.

Por exemplo, quando é feito um insert , o `MongoDB` cuida disso para você: criando o banco e a coleção (caso não existam previamente) juntos com o documento inserido. Tudo isso em uma mesma operação.

Uma vez conectado à uma instância do `MongoDB` através do `MongoDB Shell` , só é preciso especificar o contexto em que essa escrita acontecerá. Nesse caso, o contexto é o nome do banco de dados que você quer criar:

~~~JavaScript
  use nomeDoBanco;
  db.nomeDaColecao.insertOne( { x: 1 });
~~~

Feito! A função `insertOne()` cria tanto o banco de dados nomeDoBanco , como a coleção nomeDaColecao , caso eles não existam. Se existirem, apenas mapeia o documento a ser inserido dentro deles e, por fim, executa a operação.

---

## Coleções

Como citado anteriormente, os documentos no `MongoDB` são armazenados dentro das coleções . Lembrando que uma coleção é equivalente à uma tabela dos bancos de dados relacionais.

### Criando uma coleção

Como visto anteriormente, se uma coleção não existe, o `MongoDB` cria essa coleção no momento do primeiro insert .

~~~JavaScript
db.nomeDaColecao1.insertOne({ x: 1});
db.nomeDaColecao2.createIndex({ y: 1});
~~~

Veja que tanto as operações `insertOne()` e `createIndex()` criam uma nova coleção (caso ela não exista).

### Criação explícita

Também é possível utilizar o método db.`createCollection()` para criar uma coleção e especificar uma série de parâmetros, como o tamanho máximo do documento ou as regras de validação para os documentos.

~~~JavaScript
db.createCollection( "nomeDaColecao", { collation: { locale: "pt" } });
~~~

---

## Documentos

Como dito, os documentos são equivalentes aos registros ou linhas de uma tabela nos bancos de dados relacionais. Além disso, cada atributo (campo) é equivalente a uma coluna de uma linha da tabela. Sua diferença é que documentos podem conter estruturas mais ricas, diferentes entre documentos, e armazenar muito mais informações do que você consegue em uma "linha simples" de uma tabela relacional. Abaixo, temos uma representação de um registro numa tabela relacional, e também o seu correspondente em um documento:

_id | nome | endereco | cidade | uf
:-: | :--: | :--: | :--: | :--:
1 | Jose | Rua 1 | São Paulo | SP
2 | Maria | Rua 2 | Belo Horizonte | MG

~~~JavaScript
{
  "_id": 1,
  "nome": "Jose",
  "endereco": {
    "logradouro": "Rua 1",
    "regiao": "Zona Norte",
    "cidade": "São Paulo",
    "uf": "SP"
  }
},
{
  "_id": 2,
  "nome": "Maria",
  "endereco": {
    "logradouro": "Rua 2",
    "cidade": "Belo Horizonte",
    "uf": "MG"
  }
}
~~~

Como visto acima, um insert recebe como parâmetro um `JSON` . Esse parâmetro define os dados e a estrutura do documento. É importante ressaltar que, por ser schemaless , ou seja, sem esquema por padrão, a estrutura não faz parte da coleção, e sim do documento . Com isso, é possível ter várias "estruturas" por coleção. No exemplo acima, podemos observar essa diferença entre os documentos. No primeiro, temos o atributo `regiao` , que não existe no segundo documento.

Quando fizer uma alteração, faça-a em nível de documento. Pois caso a faça em nível de coleção, muitos documentos com estruturas diferentes poderão ser impactados com a criação, alteração ou remoção de um atributo que não faz parte da estrutura de todos.

---

## BSON Types

Por mais que o insert ocorra recebendo um documento `JSON` , internamente, o `MongoDB` armazena os dados em um formato chamado `BSON (ou Binary JSON)`. Esse formato é uma extensão do `JSON` e permite que você tenha mais tipos de dados armazenados no `MongoDB` , não somente os tipos permitidos pelo `JSON`.

---

## Insert

Em `Mongo` existem 2 métodos para inserir novos dados, o `insertOne()` e o `insertMany()`, cada um deles com as suas peculiaridades e limitações. Enquanto um faz a inserção de um único documento por vez, o outro pode inserir milhares de documentos em uma única operação. Portanto, saber quando e onde aplicar fará toda a diferença na hora de codar. Quando são usados os `inserts` e a propriedade `_id` não é especificada, o próprio Mongo gera um `_id` automáticamente.

---

## Find

O método `find()` serve para selecionar os documentos de uma `coleção` e retorna um `cursor` com esses `documentos`.

Este método pode receber 2 parâmetros:

~~~JavaScript
db.collection.find(query, projection);
~~~

- `query` (opcional):
  - Tipo: documento;
  - Descrição: especifica os filtros da seleção usando os `query operators`. Para retornar todos os documentos da coleção, é só omitir esse parâmetro ou passar um documento vazio `({})`.
- `projection` (opcional):
  - Tipo: documento;
  - Descrição: especifica quais atributos serão retornados nos documentos selecionados pelo parâmetro query . Para retornar todos os atributos desses documentos, é só omitir esse parâmetro.

### Projection

Como dito, o parâmetro projection determina quais atributos serão retornados dos documentos que atendam aos critérios de filtro. O formato recebido por ele é algo como:

~~~JavaScript
{ "atributo1": valor, "atributo2": valor ... }
~~~

O `valor` pode ser uma das seguintes opções:

- 1 ou true para incluir um campo nos documentos retornados;
- 0 ou false para excluir um campo;
- Uma expressão usando Projection Operators.

É possível escolher exibir no resultado da consulta apenas certos atributos.
A projeção é sempre o segundo parâmetro do método find().

~~~JavaScript
db.movies.insertOne({
  title: "Forrest Gump",
  category: ["drama", "romance"],
  imdb_rating: 8.8,
  filming_locations: [
    { city: "Savannah", state: "GA", country: "USA" },
    { city: "Monument Valley", state: "UT", country: "USA" },
    { city: "Los Anegeles", state: "CA", country: "USA" },
  ],
  box_office: {
    gross: 557,
    opening_weekend: 24,
    budget: 55,
  },
});

db.movies.findOne(
  { title: "Forrest Gump" },
  { title: 1, imdb_rating: 1 }
);
~~~

E como resultado:

~~~JavaScript
{
  "_id": ObjectId("5515942d31117f52a5122353"),
  "title": "Forrest Gump",
  "imdb_rating": 8.8
}
~~~

Note que o atributo _id também foi retornado. Isso acontece porque ele é o único atributo que não precisa ser especificado para que seja retornado. O movimento aqui é ao contrário, caso ele não seja necessário no retorno, é só suprimí-lo da seguinte forma:

~~~JavaScript
db.movies.findOne(
  { title: "Forrest Gump" },
  { title: 1, imdb_rating: 1, _id: 0 }
);
~~~

Dessa forma o resultado será:

~~~JavaScript
{
  "title": "Forrest Gump",
  "imdb_rating": 8.8
}
~~~

---

## Operadores em Mongo

Como em toda linguagem, `Mongo` também possui operadores, que podem ser usados de muitas formas durante as querys. Os operadores seguem uma sintaxe padrão que é composta por um subdocumento, como no exemplo abaixo:

~~~JavaScript
{ campo: { operador: valor } }
~~~

Em `Mongo` os operadores são identificados pelo prefixo `$`.

    • Comparação
      ▪ $lt - less than, menor que, <;
      ▪ $lte - less than or equal, menor ou igual a, <=;
      ▪ $gt - greater than, maior que, >;
      ▪ $gte - greater than or equal, maior ou igual a, >=;
      ▪ $eq - equal, igual a, =;
      ▪ $ne - not equal, diferente de, !=, <>;
      ▪ $in - in, dentro de;
      ▪ $nin - not in, não está dentro de;

---

    • Lógicos
      ▪ $and - and, se todas as condições forem verdadeiras retorna true;
      ▪ $or - or, se apenas uma condição for verdadeira retorna true;      
      ▪ $not - not, inverte o resultado da expressão;
      ▪ $nor - not or, semelhante ao or, porém trabalha com a condição false;

---

    • Existência
      ▪ $exists - exists, verifica a existência de um atributo;

---

~~~JavaScript
~~~

---

## Comandos em Mongo

### CRUD

#### Create

- `insertOne()` - Insere um documento novo em uma coleção. Ex:

~~~JavaScript
db.collection.insertOne({
  "productName": "banana",
  "price": 1.99
});
~~~

- `insertMany()` - Insere vários documentos simultâneamente em uma coleção, para inserir esses múltiplos documentos é necessário que eles sejam passados dentro de um `Array`. Ex:

~~~JavaScript
db.collection.insertMany([
  {
  "productName": "maçã",
  "price": 3.49
  },
  {
  "productName": "laranja",
  "price": 2.99
  },
  {
  "productName": "limão",
  "price": 2.59
  },
]);
~~~

#### Reade

- `find()` - Seleciona os documentos de uma coleção e retorna um cursor com esses documentos. Caso o `find()` seja passado sem uma query como parâmetro ou com as chaves da query como vazia, ele vai retornar todos os documentos do banco de dados. Exemplos:

~~~JavaScript
db.collection.find({ _id: 1 });
db.collection.find();
db.collection.find({});
~~~

#### Update

#### Delete

- `deleteOne()` - Remove apenas um documento, que deve satisfazer o critério de seleção, mesmo que muitos outros documentos também se enquadrem no critério de seleção. Se nenhum valor for passado como parâmetro, a operação removerá o primeiro documento da coleção. Exemplo:

~~~JavaScript
db.collection.deleteOne({ status: "D" });
~~~

- `deleteMany()` - Remove todos os documentos que satisfaçam o critério de seleção. Exemplo:

~~~JavaScript
db.collection.deleteMany({ status: "D" });
~~~

### Outros métodos

- `count()` - Retorna o número de documentos de uma coleção, e também pode receber um critério de seleção para retornar apenas o número de documentos que atendam a esse critério.
- `limit()` - Limita quantidade de resultados retornados. Exemplo:

~~~JavaScript
db.collection.find(`query`).limit(`numero`);
~~~

- `pretty()` - Deixa os resultados exibidos no **MongoDB Shell** um pouco mais legíveis, aplicando identações na exibição do resultado. Exemplo:

~~~JavaScript
db.collection.find(`query`).limit(`numero`).pretty();
~~~

- `skip()` - Pula uma quantidade de documentos antes de fazer a query, a quantidade pode ser especificada dentro dos parênteses. Podendo ser combinado com outros métodos. Exemplos:

~~~JavaScript
db.collection.find().skip(2);
db.collection.find().limit(10).skip(5);
~~~

- `sort()` - Ordena os documentos por algum atributo. Usando um valor positivo ( 1 ) como valor do atributo, os documentos da consultas são ordenados de forma crescente ou alfabética (também ordena por campos com strings ). Em complemento, usando um valor negativo ( -1 ), os documentos de saída estarão em ordem decrescente ou contra alfabética. Exemplos:

~~~JavaScript
db.collection.find({}, { value, name }).sort({ value: -1 }, { name: 1 });
db.collection.find().sort({ nomeDoAtributo: 1 });
~~~

### Operadores de comparação

- `$lt` - Seleciona os documentos em que o valor do atributo filtrado é menor do que (<) o valor especificado. Exemplo:

~~~JavaScript
db.collection.find({ qty: { $lt: 5 } });
~~~

- `$lte` - Seleciona os documentos em que o valor do atributo filtrado é menor ou igual (<=) ao valor especificado. Exemplo:

~~~JavaScript
db.collection.find({ qty: { $lte: 5 } });
~~~

- `$gt` - Seleciona os documentos em que o valor do atributo filtrado é maior do que (>) o valor especificado. Exemplo:

~~~JavaScript
db.collection.find({ qty: { $gt: 5 } });
~~~

- `$gte` - Seleciona os documentos em que o valor do atributo filtrado é maior ou igual (>=) ao valor especificado. Exemplo:

~~~JavaScript
db.collection.find({ qty: { $gte: 5 } });
~~~

- `$eq` - Seleciona os documentos em que o valor do atributo filtrado é igual ao valor especificado. Esse operador é equivalente ao filtro `{ campo: valor }` e não tem nenhuma diferença de performance. Exemplo:

~~~JavaScript
db.collection.find({ qty: { $gte: 5 } });
db.collection.find({ qty: 5 });
~~~

- `$ne` - Seleciona os documentos em que o valor do atributo filtrado não é igual ao valor especificado, incluindo os documentos em que o atributo não existe. Exemplo:

~~~JavaScript
db.collection.find({ qty: { $ne: 5 } });
~~~

- `$in` - Seleciona os documentos em que o valor do atributo filtrado corresponde à algum dos valores especificados pelo operador. Exemplo:

~~~JavaScript
db.collection.find({ qty: { $in: [ 5, 10 ] } });
~~~

- `$in` - Seleciona os documentos em que o valor do atributo filtrado não é igual ao especificado no array , ou o campo não existe. Exemplo

~~~JavaScript
db.collection.find({ qty: { $nin: [ 5, 10 ] } });
~~~

### Operadores lógicos

- `$not` - Executa uma operação lógica de `NEGAÇÃO` no operador ou expressão especificado e seleciona os documentos que não correspondam ao operador ou expressão . Isso também inclui os documentos que não contêm o atributo. Exemplo:

~~~JavaScript
db.collection.find({ qty: { $not: { $gt: 5 } } });
~~~

- `$or` - Executa a operação lógica `OU` em um array de uma ou mais expressões e seleciona os documentos que satisfaçam ao menos uma das expressões. Exemplo:

~~~JavaScript
db.collection.find({ $or: [{ qty: { $lt: 20 } }, { price: 10 }] });
~~~

- `$nor` - Executa uma operação lógica de `NEGAÇÃO` , porém, em um array de uma ou mais expressões, e seleciona os documentos em que todas essas expressões falhem , ou seja, seleciona os documentos em que todas as expressões desse array sejam falsas. Exemplo:

~~~JavaScript
db.collection.find({ $nor: [{ price: 1.99 }, { sale: true }] });
~~~

- `$and` - Executa a operação lógica `E` num array de uma ou mais expressões e seleciona os documentos que satisfaçam todas as expressões no array. Exemplo:

~~~JavaScript
db.collection.find({
  $and: [
    { price: { $ne: 1.99 } },
    { price: { $exists: true } }
  ]
});
~~~

### Operador de existência

- `$exists` - Quando o `boolean` é verdadeiro ( `true` ), o operador `$exists` encontra os documentos que contêm o atributo , incluindo os documentos em que o valor do atributo é igual a null . Se o `boolean` é falso ( `false` ), a consulta retorna somente os documentos que não contêm o atributo. Exemplos:

~~~JavaScript
db.collection.find({ qty: { $exists: true } });
db.collection.find({ qty: { $exists: true, $nin: [ 5, 15 ] } });
~~~

~~~JavaScript
~~~
