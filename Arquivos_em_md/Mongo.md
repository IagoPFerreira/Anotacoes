# Mongo

Mongo é uma lingaguem de banco de dados, parecida com MySQL, a diferença é que Mongo é usada em Banco de Dados não relacionais, ou seja, não existem interações entre bancos e/ou tabelas.

A estrutura do Mongo se consiste em:

- diversos bancos de dados;
- diversas coleções dentro desses bancos;
- diversos documentos dentro dessas coleções.

Fazendo um paralelo, as coleções são equivalentes às tabelas dos bancos de dados relacionais e os documentos são equivalentes aos registros, como linhas e colunas.

---

# Sumário

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
- [Arrays em Mongo](#Arrays-em-Mongo)
- [Tipos de dados](#Tipos-de-dados)
- [Comandos em Mongo](#Comandos-em-Mongo)
  - [CRUD](#CRUD)
  - [Outros métodos](#Outros-métodos)
- [Operadores](#Operadores)
  - [Operadores de comparação](#Operadores-de-comparação)
  - [Operadores lógicos](#Operadores-lógicos)
  - [Operador de existência](#Operador-de-existência)
  - [Operadores de atualização](#Operadores-de-atualização)
  - [Operadores de atualização de Arrays](#Operadores-de-atualização-de-Arrays)
  - [Agregação](#Agregação)
  - [Acumulação](#Acumulação)
  - [Expressões](#Expressões)

---

## Configurando a inicialização do servidor do MongoDB

Por padrão, após a instalação, seu servidor vai estar configurado para não iniciar junto ao sistema. Caso queira ativar o início automático quando ligar o computador, utilize o comando:

~~~bash
# Linux
sudo systemctl enable mongod.service
~~~

Caso não queira mais que isso aconteça (para poupar memória RAM, por exemplo), você pode desativar o início automático utilizando o comando:

~~~bash
sudo systemctl disable mongod.service
~~~

Na primeira vez que for utilizar o `MongoDB` após ligar o computador, será necessário iniciar o servidor com o comando:

~~~bash
# Linux
sudo service mongod start

# macOS
brew services start mongodb-community
~~~

Verificar se o MongoDB foi iniciado com sucesso:

~~~bash
# Linux
sudo service mongod status

# macOS
brew services list | grep mongodb-community

~~~

Parando o MongoDB:

~~~bash
# Linux
sudo service mongod stop

# macOS
brew services stop mongodb-community
~~~

---

## Bancos de Dados

Assim como nos sistemas gerenciadores de bancos de dados relacionais, dentro de uma mesma instância do `MongoDB` é possível ter um ou vários bancos de dados. Uma grande diferença, é que não existe a formalidade de criar um banco de dados antes de fazer uma operação nele.

Por exemplo, quando é feito um insert, o `MongoDB` cuida disso para você: criando o banco e a coleção (caso não existam previamente) juntos com o documento inserido. Tudo isso em uma mesma operação.

Uma vez conectado à uma instância do `MongoDB` através do `MongoDB Shell`, só é preciso especificar o contexto em que essa escrita acontecerá. Nesse caso, o contexto é o nome do banco de dados que você quer criar:

~~~JavaScript
  use nomeDoBanco;
  db.nomeDaColecao.insertOne( { x: 1 });
~~~

Feito! A função `insertOne()` cria tanto o banco de dados nomeDoBanco, como a coleção nomeDaColecao, caso eles não existam. Se existirem, apenas mapeia o documento a ser inserido dentro deles e, por fim, executa a operação.

---

## Coleções

Como citado anteriormente, os documentos no `MongoDB` são armazenados dentro das coleções. Lembrando que uma coleção é equivalente à uma tabela dos bancos de dados relacionais.

### Criando uma coleção

Como visto anteriormente, se uma coleção não existe, o `MongoDB` cria essa coleção no momento do primeiro insert.

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

Como visto acima, um insert recebe como parâmetro um `JSON`. Esse parâmetro define os dados e a estrutura do documento. É importante ressaltar que, por ser schemaless, ou seja, sem esquema por padrão, a estrutura não faz parte da coleção, e sim do documento. Com isso, é possível ter várias "estruturas" por coleção. No exemplo acima, podemos observar essa diferença entre os documentos. No primeiro, temos o atributo `regiao`, que não existe no segundo documento.

Quando fizer uma alteração, faça-a em nível de documento. Pois caso a faça em nível de coleção, muitos documentos com estruturas diferentes poderão ser impactados com a criação, alteração ou remoção de um atributo que não faz parte da estrutura de todos.

---

## BSON Types

Por mais que o insert ocorra recebendo um documento `JSON`, internamente, o `MongoDB` armazena os dados em um formato chamado `BSON (ou Binary JSON)`. Esse formato é uma extensão do `JSON` e permite que você tenha mais tipos de dados armazenados no `MongoDB`, não somente os tipos permitidos pelo `JSON`.

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
  - Descrição: especifica quais atributos serão retornados nos documentos selecionados pelo parâmetro query. Para retornar todos os atributos desses documentos, é só omitir esse parâmetro.

### Projection

Como dito, o parâmetro projection determina quais atributos serão retornados dos documentos que atendam aos critérios de filtro. O formato recebido por ele é algo como:

~~~JavaScript
{ "atributo1": valor, "atributo2": valor... }
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

[Comparação](#Comparação)

    ▪ $lt - less than, menor que, <;
    ▪ $lte - less than or equal, menor ou igual a, <=;
    ▪ $gt - greater than, maior que, >;
    ▪ $gte - greater than or equal, maior ou igual a, >=;
    ▪ $eq - equal, igual a, =;
    ▪ $ne - not equal, diferente de, !=, <>;
    ▪ $in - in, dentro de;
    ▪ $nin - not in, não está dentro de;

---

[Lógicos](#Lógicos)

    ▪ $and - and, se todas as condições forem verdadeiras retorna true;
    ▪ $or - or, se apenas uma condição for verdadeira retorna true;      
    ▪ $not - not, inverte o resultado da expressão;
    ▪ $nor - not or, semelhante ao or, porém trabalha com a condição false;

---

[Existência](#Existência)

    ▪ $exists - exists, verifica a existência de um atributo;

---

[Atualização](#Atualização)

    ▪ $set - set, define um novo valor;
    ▪ $mul - mul, multiplica o valor do campo;
    ▪ $inc - inc, incrementa ou decrementa o valor de um campo;
    ▪ $min - min, altera os valores de um campo para o mínimo; 
    ▪ $max - max, altera os valores de um campo para o máximo;
    ▪ $currentDate - currentDate, atribui ao valor de um campo a data corrente;
    ▪ $rename - rename, remoneia um determinado atributo de um ou mais documentos;
    ▪ $unset - unset, remove um ou mais campos de um documento;

---

[Atualização de Arrays](#Atualização-de-Arrays)

    ▪ $push - push, adiciona um valor a um array;
      ◦ $each - each, adiciona múltiplos valores a um array;
      ◦ $slice - slice, limita o número de elementos do array;
      ◦ $sort - sort, ordena os elementos do array;
      ◦ $position - position, especifica a posição do elemento que está sendo inserido no array;
    ▪ $pop - pop, remove o primeiro ou o último elemento de um array;
    ▪ $pull - pull, remove um ou mais elementos de um array;
    ▪ $addToSet - addToSet, adiciona somente valores únicos ao array;
    ▪ $all - all, seleciona todos os elementos com um ou mais valores específicos;
    ▪ $elemMatch - elemMatch, seleciona os arrays com pelo menos um campo específico;
    ▪ $size - size, seleciona arrays com um tamanho específico;
    ▪ $expr - expr, usa expressões de agregação;
    ▪ $regex - regex, usa expresões regulares;
    ▪ $text - text, buscas textuais por campos indexados;
    ▪ $mod - mod, usa o módulo de uma divisão;
---

[Agregação](#Agregação)

    ▪ $match - match, seleciona os documentos que passarem no filtro;
    ▪ $limit - limit, limita o número de documentos a serem retornados;
    ▪ $project - project, passa somente alguns campos para o método seguinte do pipeline;
    ▪ $group - group, agrupa valores de diferentes documentos;
    ▪ $unwind - unwind, desconstroi um campo com array em vários documentos, sendo um documento para cada elemento do array;
    ▪ $lookup - lookup, faz a junção de documentos de coleções diferentes

---

## Arrays em Mongo

Assim como em muitas linguages, `Mongo` também possui Arrays, e assim como objetos Arrays são muito úteis para guardar muitas informações. Entretanto, diferente de muitas linguagens a navegação dentro de um Array, em `Mongo` não se dá pela utilização de colchetes `[]` com o número do indice de um item dentro deles,  mas sim como navegamos dentro de objetos, por `dot notation`, mas ainda se fazendo necessário especificar o número do indice de cada item. Exemplo:

~~~JavaScript
db.collection.insertOne({
  _id: 1,
  quantity: 250,
  details: { model: "14Q2", make: "xyz" },
  tags: [ "apparel", "clothing" ],
  ratings: [ { by: "ijk", rating: 4 } ]
});

db.collection.updateOne(
  { _id: 1 },
  { $set: {
      "tags.1": "rain gear",
      "ratings.0.rating": 2
    }
  }
);
~~~

Existem formas de deixar o valor do indice dinâmico, para que não necessário sempre passa-lo de forma hardcode. Para isso basta usar a seguinte sintaxe `$[elemento]`, dessa forma é possível usar o indice de um elemento de forma dinâmica. Exemplo:

~~~JavaScript
db.recipes.updateMany(
  {},
  {
    set:: {
      "ingredients.$[elemento].unit": "xícara", 
      "ingredients.$[elemento].name": "Farinha Integral", 
    },
  ,
  { arrayFilters: [ { "elemento.name": "Farinha" } ] },
);
~~~

---

## Tipos de dados

O `Mongo` possui vários tipos de dados, vamos escrever sobre alguns deles aqui:

### Data

Existem vários formas de retornar a data, seja ela como uma string ou como um objeto.

- `Date()` - retorna a data atual como uma string. Exemplo:

~~~JavaScript
var myDateString = Date();

myDateString;

// Saída: Tue Aug 17 2021 16:51:19 GMT-0300 (Brasilia Standard Time)
~~~

- `new Date()` - retorna a data em formato de objeto. Exemplo:

~~~JavaScript
var myDate = new Date();

myDate;

// Saída: { "$date": "2021-08-17T19:54:01.162Z" }
~~~

- `ISODate()` - retorna a data em formato de objeto. Exemplo:

~~~JavaScript
var isoDate = ISODate();

isoDate;

// Saída: { "$date": "2021-08-17T19:54:54.816Z" }
~~~

### NumberLong

Todos os números longos, com muitas casas, são considerados com `NumberLong`, os números podem ser passados como strings ou não. Exemplo:

~~~JavaScript
NumberLong("2090845886852");
NumberLong(2090845886852);
~~~

### NumberInt

É utilizado para especificar números inteiros, ou seja, sem casas decimais. Exemplo:

~~~JavaScript
NumberInt(5);
~~~

### NumberDecimal

É utilizado para especificar os números com casas decimais, o `Mongo` considera os números por padrão como NumberDecimal, entretanto é possível especificar. Exemplo:

~~~JavaScript
NumberDecimal("1000.55");
NumberDecimal("1000.55555555555");
NumberDecimal(1000.55);
NumberDecimal(1000.55555555555);
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

- `aggregate()` - Agrega documentos que possuam propriedades que passem nos mesmo filtros, reduzindo assim o possível relatório e juntando um ou mais resultados com informações duplicadas. Esse método recebe como primeiro parâmetro um array de documentos, que nada mais são do que os estágios do pipeline. É possível ter quantos estágios forem necessários dentro do mesmo `aggregate`. Exemplo:

~~~JavaScript
db.collection.aggregate([
  { $match: { status: "A" } },
  { $group: { _id: "$cust_id", total: { $sum: "$amount" } } }
]);
~~~

A operação acima tem 2 estágios:

- **Primeiro Estágio**: O estágio `$match` filtra os documentos pelo campo `status` , e passam para o próximo estágio somente os documentos que têm `status` igual a `A`.
- **Segundo Estágio**: O estágio `$group` agrupa os documentos pelo campo `cust_id` para calcular a soma dos valores do campo `amount` para cada `cust_id` único.

#### Update

- `updateOne()` - Altera apenas o primeiro documento que satisfaça critério de seleção, mesmo que muitos outros documentos também se enquadrem no critério de seleção. Se nenhum valor for passado como parâmetro, a operação alterará o primeiro documento da coleção. São passados 2 parâmetros para esse método, o primeiro é o filtro e o segundo é a operação de `update` em si. Exemplo:

~~~JavaScript
db.collection.updateOne(
  { item: "paper" },
  { $set: { "size.uom": "cm", status: "P" } }
);
~~~

- `updateMany()` - Altera todos os documento que satisfaçam o critério de seleção. Se nenhum valor for passado como parâmetro, a operação alterará todos os documentos da coleção. São passados 2 parâmetros para esse método, o primeiro é o filtro e o segundo é a operação de `update` em si. Exemplo:

~~~JavaScript
db.collection.updateMany(
  { qty: { $lt: 50 } },
  { $set: { "size.uom": "in", status: "P" } }
);
~~~

Os métodos de `update` possuem o parâmetro `upsert`, que caso nenhum documento combine com o filtro, um novo documento será criado, atendendo aos requisitos do filtro.

#### Delete

- `deleteOne()` - Remove apenas um documento, que deve satisfazer o critério de seleção, mesmo que muitos outros documentos também se enquadrem no critério de seleção. Se nenhum valor for passado como parâmetro, a operação removerá o primeiro documento da coleção. Exemplo:

~~~JavaScript
db.collection.deleteOne({ status: "D" });
~~~

- `deleteMany()` - Remove todos os documentos que satisfaçam o critério de seleção. Se nenhum valor for passado como parâmetro, a operação removerá todos os documentos da coleção. Exemplo:

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

- `createIndex()` - Cria indeces que podem ser utilizados em buscas dentro dos documentos. Recebe como parâmetro um objeto, onde a chave é o nome do campo onde será feita a busca e o valor é o tipo de dado. Exemplo:

~~~JavaScript
db.collection.createIndex({ campo: "text" })
~~~

## Operadores

### Comparação

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

- `$in` - Seleciona os documentos em que o valor do atributo filtrado não é igual ao especificado no array, ou o campo não existe. Exemplo

~~~JavaScript
db.collection.find({ qty: { $nin: [ 5, 10 ] } });
~~~

### Lógicos

- `$not` - Executa uma operação lógica de `NEGAÇÃO` no operador ou expressão especificado e seleciona os documentos que não correspondam ao operador ou expressão. Isso também inclui os documentos que não contêm o atributo. Exemplo:

~~~JavaScript
db.collection.find({ qty: { $not: { $gt: 5 } } });
~~~

- `$or` - Executa a operação lógica `OU` em um array de uma ou mais expressões e seleciona os documentos que satisfaçam ao menos uma das expressões. Exemplo:

~~~JavaScript
db.collection.find({ $or: [{ qty: { $lt: 20 } }, { price: 10 }] });
~~~

- `$nor` - Executa uma operação lógica de `NEGAÇÃO`, porém, em um array de uma ou mais expressões, e seleciona os documentos em que todas essas expressões falhem, ou seja, seleciona os documentos em que todas as expressões desse array sejam falsas. Exemplo:

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

### Existência

- `$exists` - Quando o `boolean` é verdadeiro ( `true` ), o operador `$exists` encontra os documentos que contêm o atributo, incluindo os documentos em que o valor do atributo é igual a null. Se o `boolean` é falso ( `false` ), a consulta retorna somente os documentos que não contêm o atributo. Exemplos:

~~~JavaScript
db.collection.find({ qty: { $exists: true } });
db.collection.find({ qty: { $exists: true, $nin: [ 5, 15 ] } });
~~~

### Atualização

- `$set` - Define um novo valor para uma ou mais propriedades e caso o campo não exista ele será criado, também vale para campos com `dot notation`. É possível especificar múltiplos pares de campos valores e o operador `$set` alterará ou criará cada um desses campos. Pode ser utilizado em conjunto com outros operadores. Exemplos:

~~~JavaScript
db.collection.updateMany({}, { $set: { creator: "Me" } });
db.collection.updateOne(
  { _id: 100 },
  { $set: {
      quantity: 500,
      details: { model: "14Q3", make: "xyz" },
      tags: [ "coats", "outerwear", "clothing" ]
    }
  }
);
db.collection.updateOne(
  { _id: 100 },
  { $set: { "details.make": "zzz" } }
);
~~~

- `$mul` - multiplica o valor de um campo por um número especificado, persistindo o resultado dessa operação sem a necessidade do operador $set. Caso esse operador seja usado em um campo inexistente, o campo será criado e terá como valor inicial o valor 0 com o mesmo tipo númerico do multiṕlicador. Exemplo:

~~~JavaScript
db.collection.updateOne(
  { _id: 1 },
  { $mul: { price: NumberDecimal("1.25"), qty: 2 } }
);
~~~

Neste caso o campo `price` terá seu valor multiplicado por `1.25` e o campo `qty` terá seu valor multiplicado por `2`.

- `$inc` - Incrementa ou decrementa valores em um campo específico, utilizando tanto valores positivos quanto negativos, utilizando valores positivos acontece a incrementação, usando valores negativos acontece a decrementação. Exemplo:

~~~JavaScript
db.increment.updateOne(
  { sku: "abc123" },
  { $inc: { quantity: -2, "metrics.orders": 1 } }
);
~~~

- `$min` - Altera o valor do campo para o valor especificado se esse valor especificado é menor do que o atual valor do campo, ou seja, arrasta os valores maiores que o especificado para o mesmo valor que o especificado. Exemplo:

~~~JavaScript
db.collection.updateMany({}, { $min: { campo: 25 } });
// Todos os valores acima de 25 foram alterados para 25
~~~

- `$max` - Altera o valor do campo para o valor especificado se esse valor especificado é maior do que o atual valor do campo, ou seja, arrasta os valores menores que o especificado para o mesmo valor que o especificado. Exemplo:

~~~JavaScript
db.collection.updateMany({}, { $max: { campo: 75 } });
// Todos os valores abaixo de 75 foram alterados para 75
~~~

- `$currentDate` - Atribui ao valor de um campo a data corrente, utilizando um tipo Date ou timestamp. Se não for especificado o tipo, por padrão, o MongoDB atribuirá o valor do tipo Date. Exemplo:

~~~JavaScript
db.collection.updateOne(
  { _id: 1 },
  { $currentDate: {
      lastModified: true,
      "cancellation.date": { $type: "timestamp" }
    }, $set: {
      "cancellation.reason": "user request",
      status: "D"
    }
  }
);
~~~

- `$rename` - Remoneia um determinado atributo de um ou mais documentos, esse operador recebe um documento contendo o nome atual do campo e o novo nome. Pode ser utilizado com os métodos `updateOne()` ou `updateMany()`, e também pode receber um critério de seleção de documentos. Exemplo:

~~~JavaScript
db.collection.updateOne(
  { name: "Banana" },
  { $rename: {
      "name": "productName"
    }
  }
);
~~~

- `$unset` - Remove um ou mais campos de um documento ao passar o nome do campo e como valor uma string vazia. Exemplo:

~~~JavaScript
db.collection.updateMany(
  { productName: "Banana" },
  { $unset: { quantity: "" } }
);
~~~

### Atualização de Arrays

- `$push` - Adiciona um valor a um array. Se o campo não existir no documento, um novo array com o valor em um elemento será adicionado. Em conjunto com o $push, é possível utilizar os modificadores. Cada um desses modificadores tem funções específicas.

---

    • Modificadores
      ▪ `$each` : Adiciona múltiplos valores a um array;
      ▪ `$slice` : Limita o número de elementos do array. Requer o uso do modificador `$each`;
      ▪ `$sort` : Ordena os elementos do array. Requer o uso do modificador `$each`;
      ▪ `$position` : Especifica a posição do elemento que está sendo inserido no array. Requer o modificador `$each`. Sem o modificador `$position`, o operador `$push` adiciona o elemento no final do array.

---

    • Ordem de ação dos modificadores

      1. Altera o array para adicionar os elementos na posição correta;
      2. Aplica a ordenação ( $sort ), se especificada;
      3. Limita o array ( $slice ), se especificado;
      4. Armazena o array.

---

Exemplo:

~~~JavaScript
db.collection.updateOne(
  { _id: 1 },
  {
    $push: {
      items: {
        $each: [
          {
            name: "notepad",
            price: 35.29,
            quantity: 2,
          },
          {
            name: "envelopes",
            price: 19.95,
            quantity: 8,
          },
          {
            name: "pens",
            price: 56.12,
            quantity: 5,
          },
        ],
        $sort: { quantity: -1 },
        $slice: 2,
      },
    },
  },
  { upsert: true }
);
~~~

- `$pop` - Remove o primeiro ou o último elemento de um array. Passando o valor -1 o primeiro elemento será removido. Já ao passar o valor 1 , o último elemento do array será removido. Exemplos:

~~~JavaScript
db.collection.updateOne({ _id: 1 }, { $pop: { items: -1 } });
db.collection.updateOne({ _id: 1 }, { $pop: { items: 1 } });
~~~

- `$pull` - Remove de um array existente todos os elementos com um ou mais valores que atendam à condição especificada. Exemplos:

~~~JavaScript
db.collection.updateMany(
  {},
  { $pull: { items: { name: { $in: ["pens", "envelopes"] } } } },
);

db.collection.updateOne(
  { _id: 1 },
  { $pull: { votes: { $gte: 6 } } },
);

db.collection.updateMany(
  {},
  { $pull: { results: { score: 8 , item: "B" } } },
);
~~~

- `$addToSet` - Adiciona valores no array somente quando o valor já não está presente dentro do array, garantindo que o array possui somente valores únicos. Esse operador tem 3 pontos de atenção:
  - Caso o campo no qual ele está sendo utilizado não exista, ele criará esse campo;
  - Se for usado em um campo que não é um array, a operação não funcionará;
  - Se o valor passado for um documento, o MongoDB o considerará como duplicado se um documento existente no array for exatamente igual ao documento a ser adicionado, ou seja, possui os mesmos campos com os mesmos valores, e esses campos estão na mesma ordem.

Também é possível usar o modificador $each, mantendo as características do `$addToSet`.

Exemplos:

~~~JavaScript
db.collection.updateOne(
  { _id: 1 },
  { $addToSet: { tags: "camera"  } },
);

db.collection.updateOne(
  { _id: 2 },
  {
    addToSet: {
      tags: {
        each: ["camera", "electronics", "accessories"],
      },
    },
  },
);
~~~

- `$all` - Seleciona todos os documentos em que o valor do campo é um array que contenha todos os elementos especificados. Utiliza-se $all sempre que é preciso passar mais de um valor de comparação, e é irrelevante para a verificação tanto a existência de mais elementos no array quanto a ordem em que esses elementos estão.

~~~JavaScript
db.collection.find({ tags: { $all: ["red", "blank"] } });
~~~

- `$elemMatch` - Seleciona os documentos que contêm um campo do tipo array com pelo menos um elemento que satisfaça todos os critérios de seleção especificados.

~~~JavaScript
db.collection.find(
  { results: { $elemMatch: { $gte: 80, $lt: 85 } } }
);
~~~

- `$size` - Seleciona documentos em que um array contenha um número de elementos especificado. É importante saber que o operador `$size` aceita apenas valores númericos, não sendo possível, por exemplo, trazer arrays com comprimento maior do que 2 (`$gt: 2`). Caso seja necessário selecionar documentos com base em valores diferentes, a solução é criar um campo que se incremente quando elementos forem adicionados ao array.

~~~JavaScript
db.collection.find(
  { tags: { $size: 2 } }
);
~~~

- `$expr` - Permite que você utilize expressões de agregação e construa queries que comparem campos no mesmo documento. A query abaixo utiliza o operador `$expr` para buscar os documentos em que o valor de `spent` exceda o valor de `budget`:

~~~JavaScript
db.collection.find(
  {
    $expr: { $gt: [ "$spent", "$budget" ] }
  }
);
~~~

Note que, na query , nenhum valor foi especificado explicitamente. O que acontece é que o operador `$expr` entende que deve comparar os valores dos dois campos. Por isso o `$` é utilizado, indicando que a string entre aspas referencia um campo.

- `$regex` - Fornece os "poderes" das expressões regulares ( regular expressions ) para seleção de strings. Um uso muito comum para o operador `$regex` é fazer consultas como o `LIKE` do `SQL`. Exemplos:

~~~JavaScript
db.collection.find({ sku: { $regex: /789$/ } }); // retorna os documentos em que o campo "sku" termine em "789"

db.collection.find({ sku: { $regex: /$xyz/ } }); // retornar os documentos em que o campo "sku" comece com "xyz"

db.collection.find({ sku: { $regex: /^ABC/i } }); //retorna os documentos em que o campo "sku" possua em algum lugar o trecho "abc", independente do case
~~~

- `$text` - Faz uma busca "textual" em um campo indexado por um text index, index esse que é criado pelo método `createIndex()`, esse operador possui alguns atributos que auxiliam nas buscas.

---
    • $search : Uma string com os termos que o MongoDB utilizará para fazer o parse e utilizará como filtro. Internamente, o MongoDB faz uma busca lógica ( OR ) sobre os termos, a menos que seja especificado como uma frase inteira;

    • $language : Opcional. Esse campo determina a lista de stop words que será utilizada na tokenização da busca. Caso seja passado o valor none , a busca utilizará uma tokenização simples sem utilizar nenhuma lista de stop words (Stop word: Também conhecido como palavra vazia , é uma palavra que é removida antes ou após o processamento de um texto em linguagem natural);

    • $caseSensitive : Opcional. Recebe um valor booleano para habilitar ou desabilitar buscas case sensitive. O valor default é false , o que faz com que as buscas sejam case-insensitive;

    • $diacriticSensitive : Opcional. Recebe um valor booleano para habilitar ou desabilitar busca diacritic sensitive. O valor default também é false.
---

~~~JavaScript
db.collection.createIndex({ campo: "text" }); // cria o index do tipo texto

db.collection.find({ $text: { $search: "coffee" } }); // busca todos os documentos que contenham o termo coffee

db.collection.find({ $text: { $search: "bake coffee cake" } }); // busca todos os documentos que contenham qualquer um desses argumentos

db.collection.find({ $text: { $search: "\"coffee shop\"" } }); // busca todos os documentos que contenham essa frase específica
~~~

- `$mod` - Seleciona todos os documentos em que o valor do campo dividido por um divisor seja igual ao valor especificado, ou seja, executa a operação matemática módulo, ou seja, encontra o resto da divisão de um número por outro. A query a seguir seleciona todos os documentos da coleção em que o valor do campo qty módulo 4 seja 0:

~~~JavaScript
db.collection.find({ qty: { $mod: [4, 0] } });
~~~

### Agregação

- `$match` - Filtra os documentos da mesma maneira que o método `find()`, entretanto, esse operador pode ser usado em métodos de agreagação. Exemplo:

~~~JavaScript
db.collection.aggregate([{ $match: { author: "dave" } }]);

db.collection.aggregate([
    {
      $match: {
        $or: [
          { score: { $gt: 70, $lt: 90 } },
          { views: { $gte: 1000 } }
        ]
      }
    }
  ]);
~~~

- `$limit` - Limita o número de documentos que será passado para o próximo estágio do pipeline. Ele sempre recebe um valor do tipo inteiro e positivo.

~~~JavaScript
db.collection.aggregate([{ $limit : 5 }]);
~~~

- `$project` - Passa adiante no pipeline apenas alguns campos dos documentos vindos do estágio anterior, fazendo isso por meio de uma "projeção", como no método `find({}, { $project })`. Entretanto, existe a diferença de que esses campos podem ser novos, sendo resultado de um cálculo ou de uma concatenação. Assim como numa projeção comum, o único campo que precisa ser negado explicitamente é o _id. E caso um campo especificado seja inexistente, o `$project` simplesmente ignorará esse campo, sem afetar a projeção. Exemplo:

~~~JavaScript
db.collection.aggregate([
    {
      $project : {
        title : 1,
        author : 1,
        _id: 0,
      }
    }
  ]);

db.collection.aggregate([
  {
    $project : {
      "author.first": 0,
      copies: 0
    }
  }
]);

// É possível usar uma string iniciada com o caractere $ para indicar que queremos projetar um campo, assim: "$nomeDoCampo".
db.collection.aggregate([
  {
    $project: {
      title: 1,
      isbn: {
        prefix: { $substr: ["$isbn", 0, 3] },
        group: { $substr: ["$isbn", 3, 2] },
        publisher: { $substr: ["$isbn", 5, 4] },
        title: { $substr: ["$isbn", 9, 3] },
        checkDigit: { $substr: ["$isbn", 12, 1] }
      },
      lastName: "$author.last",
      copiesSold: "$copies"
    }
  }
]);
~~~

- `$group` - Agrupa valores de diferentes documentos, aceitando outros operadores dentro dele, o que pode refinar os filtros. O principal parâmetro do `$group` é o `_id` (que não tem nada a ver com o campo `_id` das coleções). Neste caso, ele é responsável por conter o campo ou os campos que serão utilizados no agrupamento. No documento de saída, o `_id` contém um agrupamento exclusivo para cada valor. Esses documentos de saída também podem conter campos calculados , que conterão valores de alguma expressão de acumulação.

~~~JavaScript
db.collection.aggregate([
  {
    $group: {
      _id: null,
      count: { $sum: 1 }
    }
  }
]);
~~~

- `$unwind` - "Desconstrói" um campo array do documento de entrada e gera como saída um documento para cada elemento do array. Cada documento de saída é o documento de entrada com o valor do campo array substituído por um elemento do array.

~~~JavaScript
db.inventory.insertOne({ _id: 7, item: "ABC1", sizes: ["S", "M", "L"] });

db.inventory.aggregate([{ $unwind : "$sizes" }]);

// Resultado
// { "_id" : 7, "item" : "ABC1", "sizes" : "S" }
// { "_id" : 7, "item" : "ABC1", "sizes" : "M" }
// { "_id" : 7, "item" : "ABC1", "sizes" : "L" }
~~~

- `$lookup` - Faz a junção de documentos de coleções diferentes. Como resultado dessa junção, um elemento do tipo array é adicionado a cada documento da coleção de entrada, contendo os documentos que deram `match` na coleção com a qual se faz o `join`. Existem quatro parâmetros básicos para montar um `$lookup` :

  - `from`: uma coleção no mesmo database para executar o join;
  - `localField`: o campo da coleção de onde a operação de agregação está sendo executada. Será comparado por igualdade com o campo especificado no parâmetro `foreingField`;
  - `foreingField` : o campo da coleção especificada no parâmetro from que será comparado com o campo `localField` por igualdade simples;
  - `as`: o nome do novo array que será adicionado.
  - `let`: define as variáveis que serão utilizadas no estágio pipeline dentro do `$lookup`. É necessário porque o estágio `pipeline` não consegue acessar diretamente os campos dos documentos de entrada, então esses campos precisam ser definidos previamente e transformados em variáveis;
  - `pipeline`: define as condições ou o pipeline que será executado na coleção de junção. Se precisar de todos os documentos da coleção de junção, é só especificá-lo como vazio ( [] ).

Os parâmetros `let` e `pipeline` são opicionais.

Exemplos:

~~~JavaScript
// Com localField e foreingField

// orders
db.orders.insertMany([
  { _id: 1, item: "almonds", price: 12, quantity: 2 },
  { _id: 2, item: "pecans", price: 20, quantity: 1 },
  { _id: 3 }
]);

// inventory
db.inventory.insertMany([
  { _id: 1, sku: "almonds", description: "product 1", instock: 120 },
  { _id: 2, sku: "bread", description: "product 2", instock: 80 },
  { _id: 3, sku: "cashews", description: "product 3", instock: 60 },
  { _id: 4, sku: "pecans", description: "product 4", instock: 70 },
  { _id: 5, sku: null, description: "Incomplete" },
  { _id: 6 }
]);

db.orders.aggregate([
  {
    $lookup: {
      from: "inventory",
      localField: "item",
      foreignField: "sku",
      as: "inventory_docs"
    }
  }
]);

// Resultado esperado
{
  "_id" : 1,
  "item" : "almonds",
  "price" : 12,
  "quantity" : 2,
  "inventory_docs" : [
    {
      "_id" : 1,
      "sku" : "almonds",
      "description" : "product 1",
      "instock" : 120
    }
  ]
}
{
  "_id" : 2,
  "item" : "pecans",
  "price" : 20,
  "quantity" : 1,
  "inventory_docs" : [
    {
      "_id" : 4,
      "sku" : "pecans",
      "description" : "product 4",
      "instock" : 70
    }
  ]
}
{
  "_id" : 3,
  "inventory_docs" : [
    {
      "_id" : 5,
      "sku" : null,
      "description" : "Incomplete"
    },
    {
      "_id" : 6
    }
  ]
}
~~~

~~~JavaScript
// Com let e pipeline

// orders
db.orders.insertMany([
  { _id: 1, item: "almonds", price: 12, ordered: 2 },
  { _id: 2, item: "pecans", price: 20, ordered: 1 },
  { _id: 3, item: "cookies", price: 10, ordered: 60 }
]);

// warehouses
db.warehouses.insertMany([
  { _id: 1, stock_item: "almonds", warehouse: "A", instock: 120 },
  { _id: 2, stock_item: "pecans", warehouse: "A", instock: 80 },
  { _id: 3, stock_item: "almonds", warehouse: "B", instock: 60 },
  { _id: 4, stock_item: "cookies", warehouse: "B", instock: 40 },
  { _id: 5, stock_item: "cookies", warehouse: "A", instock: 80 }
]);

db.orders.aggregate([
  {
    $lookup: {
      from: "warehouses",
      let: { order_item: "$item", order_qty: "$ordered" },
      pipeline: [
        {
          $match: {
            $expr: {
              $and: [
                { $eq: [ "$stock_item",  "$$order_item" ] },
                { $gte: [ "$instock", "$$order_qty" ] }
              ]
            }
          }
        },
        { $project: { stock_item: 0, _id: 0 } }
      ],
      as: "stockdata"
    }
  }
]);

// Resultado esperado
{
  "_id" : 1,
  "item" : "almonds",
  "price" : 12,
  "ordered" : 2,
  "stockdata" : [
    {
      "warehouse" : "A",
      "instock" : 120
    },
    {
      "warehouse" : "B",
      "instock" : 60
    }
  ]
}
{
  "_id" : 2,
  "item" : "pecans",
  "price" : 20,
  "ordered" : 1,
  "stockdata" : [
    {
      "warehouse" : "A",
      "instock" : 80
    }
  ]
}
{
  "_id" : 3,
  "item" : "cookies",
  "price" : 10,
  "ordered" : 60,
  "stockdata" : [
    {
      "warehouse" : "A",
      "instock" : 80
    }
  ]
}
~~~

### Acumulação

Usados para fazer operações sobre os campos de documentos agrupados.

- `$addToSet` -  retorna um array com os valores únicos da expressão para cada grupo;

- `$avg` : retorna a média de valores numéricos. Valores não numéricos são ignorados;
- `$first` : retorna um valor do primeiro documento de cada grupo;
- `$last` : retorna um valor do último documento de cada grupo;
- `$max` : retorna o maior valor de cada grupo;
- `$sum` : retorna a soma de valores numéricos. Valores não numéricos são ignorados.

### Expressões

- `$add` - Soma valores numéricos e datas. Se um dos argumentos for do tipo `date`, o outro argumento será tratado como milissegundos e adicionado à data. Exemplos:

~~~JavaScript
db.collection.aggregate([
  { $project: { item: 1, total: { $add: ["$price", "$fee"] } } }
]);

db.collection.aggregate([
  { $project: { item: 1, billing_date: { $add: ["$date", 3 * 24 * 60 * 60000] } } }
]);
~~~

- `$subtract` - Subtrai valores numéricos e retorna a diferença entre eles, ou duas datas para retornar a diferença entre elas  em milisegundos. O segundo argumento sempre será subtraído do primeiro. Exemplo:

~~~JavaScript
db.collection.aggregate([
  {
    $project: {
      item: 1,
      total: {
        $subtract: [
          { $add: ['$price', '$fee'] },
          '$discount'
        ]
      }
    }
  }
])

db.collection.aggregate([
  {
    $project: {
      item: 1,
      dateDifference: {
        $subtract: [ '$$NOW', '$date']
      }
    }
  }
]);
~~~

- `$ceil` - Arredonda o número especificado para "cima".

~~~JavaScript
db.collection.aggregate([
  { $project: { value: 1, ceilingValue: { $ceil: '$value' } } }
]);
~~~

- `$floor` - Arredonda o número especificado para "baixo".

~~~JavaScript
db.collection.aggregate([
  { $project: { value: 1, ceilingValue: { $floor: '$value' } } }
]);
~~~

- `$round` - Arredonda o número especificado para o número inteiro mais perto e também permite definir a quantidade de casas decimais a manter ao arredondar. O `$round` recebe um array, onde o primeiro item é o que será arredondado e o segundo item é o número de casas decimais que serão mantidas.

~~~JavaScript
db.collection.aggregate([
  { $project: { value: 1, ceilingValue: { $round: ['$value', 1] } } }
]);
~~~

- `$abs` - Retorna o valor absoluto de um número.

~~~JavaScript
db.collection.aggregate([
  { $project: { value: 1, ceilingValue: { $abs: { $subtract: ['$start', '$end'] } } } }
]);
~~~

- `$multiply` - Multiplica 2 valores numéricos, esses valores devem ser passados em um array.

~~~JavaScript
db.collection.aggregate([
  {
    $project: {
      date: 1,
      item: 1,
      total: {
        $multiply: ["$price", "$quantity"]
      }
    }
  }
]);
~~~

- `$divide` - Divide dois valores, sendo que o primeiro argumento é o dividendo, e o segundo é o divisor.

~~~JavaScript
db.planning.aggregate([
  {
    $project: {
      name: 1,
      workdays: {
        $divide: ["$hours", 8]
      }
    }
  }
]);
~~~

- `$addFields` - Adiciona novos campos aos documentos. A saída desse estágio conterá todos os campos existentes nos documentos de entrada e adicionará os novos campos especificados.

~~~JavaScript
db.scores.aggregate([
  {
    $addFields: {
      totalHomework: { $sum: "$homework" } ,
      totalQuiz: { $sum: "$quiz" }
    }
  },
  {
    $addFields: {
      totalScore: {
        $add: [ "$totalHomework", "$totalQuiz", "$extraCredit" ]
      }
    }
  }
]);
~~~
