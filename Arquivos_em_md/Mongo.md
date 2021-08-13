# Mongo

Mongo é uma lingaguem de banco de dados, parecida com MySQL, a diferença é que Mongo é usada em Banco de Dados não relacionais, ou seja, não existem interações entre bancos e/ou tabelas.

A estrutura do Mongo se consiste em:

- diversos bancos de dados;
- diversas coleções dentro desses bancos;
- diversos documentos dentro dessas coleções.

Fazendo um paralelo, as coleções são equivalentes às tabelas dos bancos de dados relacionais e os documentos são equivalentes aos registros, como linhas e colunas.

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
  use nomeDoBanco
  db.nomeDaColecao.insertOne( { x: 1 })
~~~

Feito! A função `insertOne()` cria tanto o banco de dados nomeDoBanco , como a coleção nomeDaColecao , caso eles não existam. Se existirem, apenas mapeia o documento a ser inserido dentro deles e, por fim, executa a operação.

---

## Coleções

Como citado anteriormente, os documentos no `MongoDB` são armazenados dentro das coleções . Lembrando que uma coleção é equivalente à uma tabela dos bancos de dados relacionais.

### Criando uma coleção

Como visto anteriormente, se uma coleção não existe, o `MongoDB` cria essa coleção no momento do primeiro insert .

~~~JavaScript
db.nomeDaColecao1.insertOne({ x: 1})
db.nomeDaColecao2.createIndex({ y: 1})
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
db.collection.find(query, projection)
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
{ "atributo1": <valor>, "atributo2": <valor> ... }
~~~

---

## Comandos em Mongo

### CRUD

- `insertOne()` - Insere um documento novo em uma coleção. Ex:

~~~JavaScript
db.collection.insertOne({
  "productName": "banana",
  "price": 1.99
})
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
])
~~~
