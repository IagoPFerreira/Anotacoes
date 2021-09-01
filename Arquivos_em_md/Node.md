# Node

O `Node.js` surgiu do `V8`, que é a ferramenta do Google Chrome responsável por ler e executar as instruções são escritas em `JavaScript`, processo comumente chamado de interpretar o código. Ao software responsável por interpretar o código dá-se o nome de interpretador, engine e, por vezes, de `runtime`. Por isso, é comum dizer que o `Node.js` é um `runtime` `JavaScript`. Apesar de ser baseado no `V8`, o `Node.js` possui algumas diferenças em relação ao interpretador que funciona nos navegadores. Dentre elas, as principais são a ausência de métodos para manipulação de páginas web e a presença de métodos que permitem acessar o sistema de arquivos e a rede mais diretamente.

---

# Sumário

- [Visão geral](#Visão-geral)
- [Sitema de módulos](#Sitema-de-módulos)
  -[Módulos internos](#Módulos-internos)
  - [Módulos locais](#Módulos-locais)
  - [Módulos de terceiros](#Módulos-de-terceiros)
- [Exportando e importando módulos](#Exportando-e-importando-módulos)
  - [Exportando módulos](#Exportando-módulos)
  - [Importando módulos](#Importando-módulos)
    - [Locais](#Locais)
    - [Internos](#Internos)
    - [Terceiros](#Terceiros)
- [NPM](#NPM)
- [HTTP](#HTTP)
- [API](#API)
- [Express](#Express)
  - [Começando com o Express](#Começando-com-o-Express)
  - [Nodemon](#Nodemon)
  - [Roteamento](#Roteamento)
  - [Parâmertos de rota](#Parâmertos-de-rota)
  - [Query String](#Query-String)
  - [Recebendo dados no body](#Recebendo-dados-no-body)
    - [Post](#Post)
    - [Put](#Put)
    - [Delete](#Delete)
- [Comandos NPM](#Comandos-NPM)
- [Métodos HTTP](#Métodos-HTTP)
  - [CRUD](#CRUD)

---

## Visão geral

Quando comparado a outras grandes tecnologias, o `Node.js` permite escrever softwares servidores de requisições `HTTP` de forma muito mais eficiente. Isso se dá pelo fato de que toda leitura e escrita que ele realiza, tanto no disco quanto na rede, é feita de forma **não bloqueante**. Ou seja, quando o servidor recebe uma requisição e precisa, por exemplo, buscar dados no banco de dados, as demais requisições não precisam esperar que a primeira termine para que possam ser atendidas. Em outras palavras, o NodeJS realiza todas as suas operações de entrada e saída de dados de forma **assíncrona**, utilizando processamento concorrente. Por serem mais eficientes e otimizadas que outras tecnologias, as aplicações feitas em `Node.js` acabam por consumir menos recursos dos servidores que as executam, tornando o `Node.js` uma tecnologia, em geral, mais barata que suas concorrentes.

A natureza não bloqueante do `Node.js` permite que alguns recursos sejam implementados na plataforma para facilitar o trabalho com operações em tempo real. Bibliotecas como o [socket.io](https://socket.io/) permitem que, com poucas linhas de código, aplicações em tempo real relativamente complexas (como chats com suporte a múltiplos usuários, conversas privadas e em grupo e outros recursos) sejam criadas por completo. Num mundo em que a tecnologia está cada vez mais inserida em diversas áreas, ter suporte nativo da plataforma que utilizamos para aplicações em tempo real com certeza é muito bem-vindo.

Muitas das vantagens do `Node.js` vêm do fato de que a linguagem executada por ele é o `JavaScript`, que tem se mostrado uma linguagem extremamente versátil, estando presente em diversos ambientes, como a Web, Desktop, Mobile, dispositivos IoT (internet das coisas) e até mesmo em televisões!

A versatilidade e baixa curva de aprendizado do `JavaScript` conferem ao `Node` um poder incrível para resolver as mais diversas situações.

No entanto, é importante lembrar que não existe somente uma solução quando o assunto é tecnologia: a melhor ferramenta sempre depende do caso de uso e dos recursos disponíveis para desempenhar uma determinada tarefa.

[Voltar ao sumário](#Sumário)

---

## Sitema de módulos

Uma das maiores vantagens do `Node.js` é a grande quantidade de pacotes e bibliotecas disponíveis publicamente no `npm`, agora chegou a hora de aprender o que é um pacote `Node` e como podem ser utilizados no código.

Um módulo em `Node.js` é um "pedaço de código" que pode ser organizado em um ou mais arquivos, e que possui escopo próprio, ou seja: suas variáveis, funções, classes e afins só estão disponíveis nos arquivos que fazem parte daquele módulo. Em outras palavras, um módulo é uma funcionalidade ou um conjunto delas que se encontram isoladas do restante do código.

O `Node.js` possui 3 tipos de módulos:

1. Internos;
2. Locais;
3. De Terceiros;

### Módulos internos

Também conhecidos como *core modules*, são módulos inclusos no `Node.js` e instalados junto com ele quando o runtime em si é baixado. Alguns exemplos são:

- [fs](https://nodejs.org/api/fs.html) - Fornece uma `API` para interagir com o sistema de arquivos de forma geral;
- [url](https://nodejs.org/api/url.html) - Provê utilitários para ler e manipular URLs;
- [querystring](https://nodejs.org/api/querystring.html) - Disponibiliza ferramentas para leitura e manipulação de parâmetros de URLs;
- [util](https://nodejs.org/api/util.html): Oferece ferramentas e funcionalidades comumente úteis a pessoas programadoras.

### Módulos locais

Módulos locais são aqueles definidos juntamente à aplicação. Representam funcionalidades ou partes do programa que foram separados em arquivos diferentes. Módulos locais podem ser publicados no `NPM` para que outras pessoas possam baixá-los e utilizá-los

### Módulos de terceiros

Módulos de terceiros são aqueles criados por outras pessoas e disponibilizados para uso através do `npm`.
Também é possível criar e publicar seus próprios módulos, quer seja para utilizar em diversas aplicações diferentes, quer seja para permitir que outras pessoas os utilizem.

[Voltar ao sumário](#Sumário)

---

## Exportando e importando módulos

Como visto módulos são muito importantes em Node, mas para que seja possível acessá-los é preciso importar-los de algum lugar e para importar um módulo ele precisa ter sido exportado também, pra isso existem formas de exportar e importar módulos, dois sistemas são muito difundidos na comunidade JavaScript:

- Módulos ES6;
- Módulos CommonJS.

---

    ES6

    O nome ES6 vem de ECMAScript 6, que é a especificação seguida pelo JavaScript.

    Na especificação do ECMAScript 6, os módulos são importados utilizando a palavra-chave import, tendo como contrapartida a palavra-chave export para exportá-los.

    O Node.js não possui suporte a módulos ES6 por padrão, sendo necessário o uso de transpiladores, como o Babel, ou supersets da linguagem, como o TypeScript, para que esse recurso esteja disponível. Transpiladores são ferramentas que leêm o código-fonte escrito em uma linguagem como o Node.js e produz o código equivalente em outra linguagem.

    Supersets são linguagens que utilizam um transpilador para adicionar novas funcionalidades ao JavaScript.

---

    CommonJS

    O CommonJS é o sistema de módulos implementado pelo Node.js nativamente e que usa as palavras chaves module.exports, para exportar um módulo, e require para importar um módulo.

---

*Visto que o sistema do CommonJS é o nativo do Node, será esse que usaremos.*

[Voltar ao sumário](#Sumário)

### Exportando módulos

Para exportar algo no sistema CommonJS, utilizamos a variável global module.exports, atribuindo a ela o valor que desejamos exportar. Exemplo:

~~~JavaScript
const brl = 5.37;

module.exports= brl;
~~~

O `module.exports` permite definir quais "objetos" internos do módulo serão exportados, ou seja, serão acessíveis a arquivos que importarem aquele módulo. O `module.exports` pode receber qualquer valor válido em JavaScript, incluindo objetos, classes, funções e afins.

Quando é necessário exportar mais de uma coisa no mesmo módulo, é necessário declarar o `module.exports` como um objeto. Exemplo:

~~~JavaScript
const brl = 5.37;

const usdToBrl = (valueInUsd) => valueInUsd * brl;

module.exports = {
  brl,
  usdToBrl,
};
~~~

[Voltar ao sumário](#Sumário)

### Importando módulos

Para cada tipo de módulo o `require` é usado de forma diferente. Entretanto, a variável que vai receber o `require` pode receber qualquer nome, mas há um consenso de que seja um nome semântico.

#### Locais

Quando é necessário importar um módulo local, é preciso passar para o `require`o caminho do módulo. Entretanto, não é necessário passar a extensão `.js`, o próprio Node, por padrão, já procura por arquivos terminados em `.js` e `.json` e os considera como módulos. Exemplo:

~~~JavaScript
const modulo = require('./meuModulo');
~~~

Além de importar um arquivo como módulo, é possível importar uma pasta. Isso é útil, pois muitas vezes um módulo está dividido em vários arquivos, mas é necessário importar todas as suas funcionalidades de uma vez só. Nesse caso, a pasta precisa conter um arquivo chamado index.js, que importa cada um dos arquivos do módulo e os exporta da forma mais conveniente. Exemplo:

~~~JavaScript
// meuModulo/funcionalidade-1.js

module.exports = function () {
  console.log('funcionalidade1');
};
~~~

~~~JavaScript
// meuModulo/funcionalidade-2.js

module.exports = function () {
  console.log('funcionalidade2');
};
~~~

~~~JavaScript
// meuModulo/index.js
const funcionalidade1 = require('./funcionalidade-1');
const funcionalidade2 = require('./funcionalidade-2');

module.exports = { funcionalidade1, funcionalidade2 };
~~~

Para importar e utilizar o módulo meuModulo, basta passar o caminho da pasta como argumento para a função `require`. Exemplo:

~~~JavaScript
// minha-aplicacao/index.js
const meuModulo = require('./meuModulo');1

console.log(meuModulo); // { funcionalidade1: [Function: funcionalidade1], funcionalidade2: [Function: funcionalidade2] }

meuModulo.funcionalidade1();
~~~

[Voltar ao sumário](#Sumário)

#### Internos

Para utilizar um módulo interno, é necessário passar o nome do pacote como parâmetro para a função `require`. Por exemplo, `require('fs')` importa o pacote `fs`, responsável pelo sistema de arquivos.
Uma vez que um pacote é importado, é possível utilizá-lo no no código como uma variável, dessa forma:

~~~JavaScript
const fs = require('fs');

fs.readFileSync('./meuArquivo.txt');
~~~

#### Terceiros

Módulos de terceiros são importados da mesma forma que os módulos internos: passando seu nome como parâmetro para a função require. A diferença é que, como esses módulos não são nativos do `Node.js`, é preciso primeiro instalá-los na pasta do projeto em que serão utilizá-los. O registro oficial do `Node.js`, em que milhares de pacotes estão disponíveis para serem instalados, é o `npm`. Além disso, `npm` também é o nome da ferramenta de linha de comando (CLI - command line interface ) responsável por baixar e instalar esses pacotes. O `CLI` `npm` é instalado juntamente com o `Node.js`.

Quando importamos um módulo que não é nativo do `Node.js`, e não aponta para um arquivo local, o Node inicia uma busca por esse módulo. Essa busca acontece na pasta node_modules. Caso um módulo não seja encontrado na node_modules mais próxima do arquivo que o chamou, o Node procurará por uma pasta node_modules na pasta que contém a pasta atual. Caso encontrado, o módulo é carregado. Do contrário, o processo é repetido em um nível de pasta acima. Isso acontece até que o módulo seja encontrado, ou até que uma pasta node_modules não exista no local em que o Node está procurando.

[Voltar ao sumário](#Sumário)

---

## NPM

O `NPM` (sigla para Node Package Manager ) é o repositório oficial para publicação de pacotes `NodeJS`. É para ele que realizamos upload dos arquivos de nosso pacote quando queremos disponibilizá-lo para uso de outras pessoas ou em diversos projetos. Atualmente, uma média de 659 pacotes são publicados no `NPM` todos os dias, segundo o site [ModuleCounts.com](https://www.modulecounts.com/).

Um pacote é um conjunto de arquivos que exportam um ou mais módulos `Node`. Nem todo pacote `Node` é uma biblioteca, visto que uma `API` desenvolvida em `Node` também tem um pacote.

### Utilizando o CLI npm

O `CLI` do `npm` é uma ferramenta oficial que nos auxilia no gerenciamento de pacotes, sejam eles dependências da aplicação ou pacotes próprios.

É através dele que é possível criar um projeto, instalar e remover pacotes, publicar e gerenciar versões de pacotes próprios. Publicar um pacote público no `npm` é gratuito e não há um limite de pacotes que se pode publicar. Existem, no entanto, taxas de assinaturas, caso deseje hospedar pacotes de forma privada, ou seja, pacotes sob os quais só o pessoa que subir o pacote tem o controle de acesso.

[Voltar ao sumário](#Sumário)

---

## HTTP

`Hypertext Transfer Protocol`, ou `HTTP`, é nome dado a um protocolo de transferência de dados pela web. Ele é a base para a comunicação de dados da `World Wide Web`. Hipertexto é o texto estruturado que utiliza ligações lógicas entre nós contendo texto.Existem muitos tipos de requisições `HTTP`, cada uma delas exercendo uma função específica e desencadeando diferentes resultados. Entretanto, existe uma estrutura básica que as requisições `HTTP` seguem, exemplo:

~~~HTTP
GET / HTTP/1.1
Host: developer.mozilla.org
Accept: text/html
~~~

Analisando as informações presentes nessa requisição:

- O método HTTP, definido por um verbo em inglês. Nesse caso, o `GET`, que normalmente é utilizado para "buscar" algo do servidor, e é também o método padrão executado por navegadores quando acessamos uma URL;
- O caminho, no servidor, do recurso que estamos tentando acessar. Nesse caso, o caminho é `/`, pois estamos acessando a página inicial;
- A versão do protocolo (1.1 é a versão nesse exemplo).
- O local (`host`) onde está o recurso que se está tentando acessar, ou seja, a URL ou o endereço IP servidor. Nesse caso, utilizamos developer.mozilla.org, mas poderia ser `localhost:3000`, caso esteja trabalhando localmente.
- Os `headers`. São informações adicionais a respeito de uma requisição ou de uma resposta. Eles podem ser enviados do cliente para o servidor, ou vice-versa. Na requisição de exemplo, temos o `header Host`, que informa o endereço do servidor, e o `header Accept`, que informa o tipo de resposta que esperamos do servidor. Um outro exemplo bem comum são os **tokens de autenticação**, em que o cliente informa ao servidor quem está tentando acessar aquele recurso: `Authorization: Bearer {token-aqui}`.

Esses são os dados transmitidos em uma request do tipo `GET`. No entanto, o `GET` não é o único método `HTTP` existente. Na verdade, existem 39 métodos diferentes! Os mais comuns são cinco: `GET`, `PUT`, `POST`, `DELETE` e `PATCH`, além do método `OPTIONS`, utilizado por clientes para entender como deve ser realizada a comunicação com o servidor.

A principal diferença entre os métodos é o seu significado. Cada método costuma dizer para o servidor que uma operação diferente deve ser executada. O método `POST`, por exemplo, costuma ser utilizado para criar um determinado recurso naquele servidor.

Além da diferença de significado, requisições do tipo `POST`, `PUT` e `PATCH` carregam mais uma informação para o servidor: o corpo, ou `body`. É no corpo da requisição que as informações de um formulário, por exemplo, são transmitidas.

Quando um servidor recebe uma requisição, ele envia de volta uma **resposta**. Veja um exemplo:

~~~HTTP
HTTP/1.1 200 OK
Date: Sat, 09 Oct 2010 14:28:02 GMT
Server: Apache
Last-Modified: Tue, 01 Dec 2009 20:18:22 GMT
ETag: "51142bc1-7449-479b075b2891b"
Accept-Ranges: bytes
Content-Length: 29769
Content-Type: text/html

<!DOCTYPE html... (aqui vêm os 29769 bytes da página solicitada)
~~~

A composição da resposta é definida por:

- A versão do protocolo (1.1 no nosso exemplo);
- O código do status, que diz se a requisição foi um sucesso ou não (nesse caso, deu certo, pois recebemos um código 200 ), acompanhado de uma pequena mensagem descritiva (OK, nesse caso).
- Os `Headers`, no mesmo esquema da requisição. No caso do exemplo acima, o `Content-Type` diz para o navegador o que ele precisa fazer. No caso do HTML, ele deve renderizar o documento na página.
- Um `body`, que é opcional. Por exemplo, caso você submeta um formulário registrando um pedido em uma loja virtual, no corpo da resposta pode ser retornado o número do pedido ou algo do tipo.

Após a resposta, a conexão com o servidor é fechada ou guardada para futuras requisições (o navegador faz essa parte automáticamente).

Note que tanto requisições quanto respostas podem ter `headers` e um `body`. No entanto, é importante não confundir uma coisa com a outra: o `body` e os `headers` da **requisição** representam a informação que o **cliente está enviando para o servidor**. Por outro lado, o `body` e os `headers` da **resposta** representam a informação que o **servidor está devolvendo para o cliente**.

[Voltar ao sumário](#Sumário)

---

## API

`API` é uma sigla para `A`pplication `P`rogramming `I`nterface. Ou seja, Interface de programação de aplicação.
Isso quer dizer que uma `API` é, basicamente, qualquer coisa que permita a comunicação, de forma programática, com uma determinada aplicação.

Um tipo muito comum de `API` são as `APIs` `HTTP`, que permitem que códigos se comuniquem com aplicações através de requisições `HTTP`. É desse tipo de `API` que boa parte da web é feita.

Elas são extremamente importantes nos dias de hoje, em que temos múltiplos clients (web, apps mobile, tvs, smartwatches etc.) se comunicando com o mesmo servidor! É assim que seu Netflix está sempre sincronizado entre seu celular, seu computador e sua televisão.

[Voltar ao sumário](#Sumário)

---

## Express

O `Express` é um framework `Node.js` criado para facilitar a criação de `APIs` `HTTP` com Node. Ele fornece uma série de recursos e abstrações que facilitam a vida na hora de decidir quais requisições tratar, como tratá-las, quais regras de negócio aplicar e afins.

O framework foi construído pensando em um padrão de construção de `APIs` chamado de `REST`. Seu objetivo é ajudar a construir `APIs` de forma mais fácil, essencialmente permitindo criar `APIs` altamente funcionais com metade do trabalho que teria para fazer isso "na mão".

Existem outras ferramentas semelhantes no mercado, mas o `Express` é largamente adotado na comunidade hoje, e dois dos motivos são:

- Ele foi lançado no final de 2010, ou seja, é um framework maduro e “testado em batalha”;
- Ele é um "unopinionated framework" (framework sem opinião). Isso significa que ele não impõe um padrão de desenvolvimento na hora de escrever sua aplicação.

Hoje, o `Express` faz parte da `Node.js Foundation`. Isso demonstra o quão relevante ele é para a comunidade.

### Começando com o Express

Assim como qualquer tipo de projeto, criamos sempre um diretório para armazenar tudo referente àquele projeto, com o `express` não é diferente, caso não exista um diretório para o projeto, criamos ele. Exemplo:

~~~bash
mkdir hello-express && cd hello-express && npm init -y
~~~

Após a criação do diretório e iniciar um pacote `Node.js` dentro dele, é necessário fazer a instalação do `express` dentro do diretório. E como toda e qualquer aplicação `Node.js`, essa precisa de um `entrypoint`, ou seja, um ponto de partida, por convenção será usado o `index.js`

~~~bash
npm i express && touch index.js
~~~

Agora vamos ao código

~~~JavaScript
const express = require('express');

const app = express(); // 1

app.get('/hello', handleHelloWorldRequest); // 2

app.listen(3001, () => {
  console.log('Aplicação ouvindo na porta 3001');
}); // 3

function handleHelloWorldRequest(req, res) {
  res.status(200).send('Hello World!'); // 4
};
~~~

Com esse script é possível:

1. Criar uma nova aplicação `Express`;
2. Dizer ao `Express` que, quando uma requisição com método `GET` for recebida no caminho `/hello`, a função `handleHelloWorldRequest` deve ser chamada;
3. Pedir ao `Express` que crie um servidor `HTTP` e escute por requisições na porta `3001`;
4. Ao tratar uma requisição com método `GET` no caminho `/hello`, enviar o status `HTTP 200` que significa `OK` e a mensagem `"Hello world!"`.

Para iniciar a aplicação, é só executar o comando abaixo no diretório da aplicação

~~~bash
node index.js
~~~

Diferente dos outros scrpits nodes desenvolvidos até aqui, que executavam e acabavam quando chegava ao final do script essa aplicação vai ficar executando `ad eternum`. Para parar a aplicação pressione `CTRL+C` no terminal.

[Voltar ao sumário](#Sumário)

### Nodemon

Uma vez que a API está rodando e são feitas modificações no código, é preciso parar e reiniciar a aplicação executando novamente o node index.js. Entretanto, para facilitar o fluxo de desenvolvimento é possível utilizar um pacote chamado `Nodemon`,  que reinicia a aplicação toda vez que alguma alteração é salva nos arquivos da aplicação. Para utilizar esse pacote é necessário instalá-lo na aplicação.

~~~bash
npm i nodemon -D
~~~

Observe que foi passado o parâmetro `-D` que indica ao npm que esse pacote deve ser instalado como uma dependência de desenvolvimento. Para poder automatizar o uso do nodemon, abra o arquivo package.json e adicione a seguinte linha:

~~~JavaScript
//...
// "scripts": {
//    "test": "echo \"Error: no test specified\" && exit 1",
      "dev": "nodemon index.js"
//  },
//...
~~~

Assim para executar a aplicação basta utilizar o comando:

~~~bash
npm run dev
~~~

⚠️ **Atenção** ⚠️ Apesar de ser uma ferramenta muito útil para desenvolvimento, o Nodemon não deve ser utilizado para rodar a aplicação, pois caso seja disponibilizada para a pessoa usuária final (ou seja, em produção), podemos ter problemas de reinicialização da aplicação, devido ao fato de que qualquer alteração em qualquer arquivo afete a aplicação, fazendo com que toda ela seja reiniciada. Para executar uma aplicação em produção, deve-se utilizar o script `start` com o comando `node index.js`.

[Voltar ao sumário](#Sumário)

### Roteamento

O aspecto mais básico de uma `API HTTP` se dá através de suas `rotas`, também chamadas de `endpoints`. Uma `rota` ou `endpoint` é definida pelo método `HTTP` e caminho.

Na aplicação de "Hello, world!", por exemplo, foi registrada uma `rota GET /hello`. Repare que, se tentarmos utilizar qualquer outro método ou qualquer outro caminho para acessar essa `rota`, receberemos um erro do `Express`, juntamente com um `status 404 - Not Found`.

o roteamento consiste em "direcionar" uma requisição para que seja atendida por uma determinada parte do nosso sistema.

No Express, nós registramos uma rota utilizando a assinatura app.METODO(caminho, callback), onde a função de callback recebe três parâmetros: `request`, `response` e `next`.

- `request`: comumente chamado de `req`; contém as informações enviadas pelo cliente ao servidor.
- `response`: geralmente chamado de `res`; permite o envio de informações do servidor de volta ao cliente.
- `next`: função que diz para o `Express` que aquele callback terminou de ser executado, e que ele deve prosseguir para executar o próximo callback para aquela rota. Este parâmetro é opcional e está ligado o uso de `middlewares`.

As rotas respondem a requisições que satisfaçam a condição método `HTTP + caminho`.

~~~JavaScript
const express = require('express');
const app = express();

/* Rota com caminho '/', utilizando o método GET */
app.get('/', function (req, res) {
  res.send('hello world');
});

/* Rota com caminho '/', utilizando o método POST */
app.post('/', function (req, res) {
  res.send('hello world');
});

/* Rota com caminho '/', utilizando o método PUT */
app.put('/', function (req, res) {
  res.send('hello world');
});

/* Rota com caminho '/', utilizando o método DELETE */
app.delete('/', function (req, res) {
  res.send('hello world');
});

/* Rota com caminho '/' para qualquer método HTTP */
app.all('/', function (req, res) {
  res.send('hello world');
});

/* Ou podemos encadear as requisições para evitar repetir o caminho */
app
  .route('/')
  .get(function (req, res) {
        // Requisições para rota GET `/` são resolvidas aqui!
    res.send('hello world get');
  })
  .post(function (req, res) {
        // Requisições para rota POST `/` são resolvidas aqui!
    res.send('hello world post');
  });

app.listen(3000, function () {
  console.log('Example app listening on port 3000!');
});
~~~

[Voltar ao sumário](#Sumário)

---

### Parâmertos de rota

São informações passadas na URL, normalmente são ids ou nomes, mas são parâmetros que vão retornar algo específico. Esses valores que são passados nas rotas que geralmente devolvem uma página seguindo o mesmo template mas com um conteúdo diferente é implementado graças ao parâmetro de rota.

Imagina se para cada nova notícia ou pedido você tivesse que criar uma rota específica exatamente com `/noticias/489` ou `/pedidos/713`? o trabalho das pessoas desenvolvedoras seria passar o dia inteiro escrevendo rotas.

Para facilitar esse processo, utilizamos parâmetros de rota, que no Express, podem ser definidos da seguinte forma: `/<rota>/<:parametro>` onde `:parametro` vai servir para qualquer valor que vier na URL com aquele prefixo específico. Exemplo:

~~~JavaScript
const express = require('express');
const app = express();

const recipes = [
  { id: 1, name: 'Lasanha', price: 40.0, waitTime: 30 },
  { id: 2, name: 'Macarrão a Bolonhesa', price: 35.0, waitTime: 25 },
  { id: 3, name: 'Macarrão com molho branco', price: 35.0, waitTime: 25 },
];

app.get('/recipes', function (req, res) {
 res.json(recipes);
});

app.get('/recipes/:id', function (req, res) {
  const { id } = req.params;
  const recipe = recipes.find((r) => r.id === parseInt(id));

  if (!recipe) return res.status(404).json({ message: 'Recipe not found!'});

  res.status(200).json(recipe);
});

app.listen(3001, () => {
  console.log('Aplicação ouvindo na porta 3001');
});
~~~

No código acima foi criada uma rota onde é possível acessar um item específico através da informação passada pela rota, independente do `id` ser um número ou string vai cair nessa segunda rota, em vez de cair na rota `/recipes`.

Para acessar o valor do parâmetro enviado na URL foi feita a desestruturação do atributo `id` do objeto `req.params`. O que indica que o parâmetro `req` traz informações a respeito da requisição.

É importante que o nome do parâmetro nomeado na rota seja igual ao atributo que está sendo desestruturando. Por exemplo, se na definição da rota estivesse escrito `/recipes/:nome` seria necessário usar `const { nome } = req.params`.

Em seguida foi usado um `find()` para encontrar a receita que tem o `id` igual ao `id` passado na rota, só que antes foi feita a conversão do `id` que veio pela rota para um número inteiro, visto que os parâmetros de sempre são `strings`.

⚠️ **Atenção** ⚠️ Perceba que na linha com o `if` foi colocado um `return`. Isso serve para indicar para o express que ele deve quebrar o fluxo e não executar a linha `res.status(200).json(recipe);`. Caso não seja colocado o `return` , a requisição vai funcionar mas terá um erro como este abaixo no log do terminal:

~~~bash
Error [ERR_HTTP_HEADERS_SENT]: Cannot set headers after they are sent to the client
~~~

Esse erro significa que o `Express` entendeu que o código está tentando retornar 2 respostas para o cliente. Por isso é preciso ter cuidado para sempre que existir uma condição que pode quebrar o fluxo principal colocar um `return` antes do `res.json` para não ter esse problema.

[Voltar ao sumário](#Sumário)

### Query String

Também é comum se deparar com `URLs` nesse formato `/produtos?q=Geladeira&precoMaximo=2000`. Essa string depois do `?` é uma `query string`. Nesse caso está sendo passado dois parâmetros: `q` com o valor `Geladeira` e `precoMaximo` com o valor `2000`.

Para nosso exemplo, vamos definir uma rota `/recipes/search?nome=Macarrão` que permita, inicialmente, buscar uma lista de receitas filtrando pelo nome.

~~~JavaScript
//...

app.get('/recipes/search', function (req, res) {
  const { name } = req.query;
  const filteredRecipes = recipes.filter((r) => r.name.includes(name));
  res.status(200).json(filteredRecipes);
});


// app.get('/recipes/:id', function (req, res) {
//  const { id } = req.params;
//  const recipe = recipes.find((r) => r.id === parseInt(id));
//  if (!recipe) return res.status(404).json({ message: 'Recipe not found!'});
//
//  res.status(200).send(recipe);
// });

//...
~~~

Nessa rota foi utilizado o `req.query` e desestruturado o atributo nome, para na sequencia usar como parâmetro de busca. Dessa vez a `HOF` usada foi a `filter()`, para filtrar os receitas que contenham ( `.includes` ) o nome recebido através da query string e no final devolver a lista de receitas obtidas por esse filtro.

Note que a rota ficou apenas com o prefixo `/recipes/search` já que os parâmetros enviados query string, não dependem desse prefixo e sim das informações que vem após o uso da `?` na `URL`. É importante entender que na `URL` é possível colocar quantos parâmetros desejar, desde que eles sigam o formato `<chave>=<valor>` e que entre cada parâmetro, exista o `&` para definir que ali está sendo passado um novo parâmetro.

⚠️ **Observação** ⚠️: Quando houver rotas com um mesmo radical e uma destas utilizar parâmetro de rota, as rotas mais específicas devem ser definidas sempre antes. Isso porque o `Express` ao resolver uma rota vai olhando rota por rota qual corresponde a `URL` que chegou. Se colocar a rota `/recipes/search` depois da rota `/recipes/:id`, o `Express` vai entender que a palavra `search` como um `id` e vai chamar a callback da rota `/recipes/:id`. Tenha atenção a esse detalhe ao utilizar rotas similares na definição da sua `API`.

[Voltar ao sumário](#Sumário)

### Recebendo dados no body

Toda requisição `HTTP`, possui um cabeçalho e um corpo, como foi mencionado anteriormente. Mas o que isso significa na prática?

Acabamos de ver que é possível receber dados da `URL`, via `query string`, porém vamos imaginar que precisamos salvar dados sensíveis como uma senha, número de algum documento importante. Se enviarmos isso na `URL` qualquer pessoa que conseguir espiar o tráfego de rede entre o cliente e o servidor vai ter acesso a essas informações. Uma forma que o protocolo `HTTP` encontrou para resolver isso foi criando o tráfego através do corpo da requisição, praticamente o que acontece é uma compressão dos dados enviados que só serão descomprimidos do lado do back-end. Isso além de não deixar as informações trafegadas tão expostas acaba deixando a requisição um pouco mais rápida já que ocorre um processo de serialização dos dados enviados. Porém aqui cabe um detalhe, geralmente para enviar dados no body da requisição você precisa usar algum tipo específico de requisição, como por exemplo, utilizando o verbo `HTTP` `POST`.

#### Post

Até então só vimos exemplos de rotas mapeadas para o verbo `GET`, Vamos ver como fica agora para esse novo verbo.

Antes disso, precisamos fazer uma pequena etapa que é instalar o pacote `bodyParser`. Como explicamos, os dados enviados pelo front-end são comprimidos, e para que conseguimos remontar os dados enviados precisamos parsear as informações para um formato compreensível para o back-end, esse formato no caso vai ser JSON. Para instalar esse pacote execute o comando:

~~~bash
npm i body-parser
~~~

E no arquivo onde está sendo feito o script de requisições é preciso fazer a seguinte mudança:

~~~JavaScript
// const express = require('express');
const bodyParser = require('body-parser');

// const app = express();
app.use(bodyParser.json());

//...
~~~

Agora implementando a rota que vai receber dados no body da requisição:

~~~JavaScript
//...
app.post('/recipes', function (req, res) {
  const { id, name, price } = req.body;
  recipes.push({ id, name, price});
  res.status(201).json({ message: 'Recipe created successfully!'});
});
~~~

Perceba, que repetimos a rota `/recipes` , só que agora usando o método `.post`. No Express, é possível ter rotas com o mesmo caminho desde que o método (ou verbo) `HTTP` utilizado seja diferente, na outra rota definimos o que acontece para o método `GET`. Por falar nisso, fica a pergunta, como vamos conseguir fazer requisições já que por padrão as requisições que fazemos ou no navegador ou no fetch api são do tipo `GET`?

Vamos começar pelo `fetch-api`, usando o código abaixo.

~~~JavaScript
fetch(`http://localhost:3001/recipes/`, {
  method: 'POST',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    id: 4,
    title: 'Macarrão com Frango',
    price: 30
  })
});
~~~

Diferente do usado para fazer um requisição do tipo `GET`, dessa vez foi passado um segundo parâmetro que éum objeto formado pelos atributos `method`, `headers` e `body`.

- `method`: Método HTTP utilizado (`GET`, `POST`, `PUT` e `DELETE`).
- `headers`: Define algumas informações sobre a requisição como o atributo `Accept` que diz qual o tipo de dado esperado como resposta dessa requisição e o `Content-Type` que sinaliza que no corpo da requisição está sendo enviado um `JSON`.
- `body`: É o corpo da requisição. Como no `HTTP` só é possível trafegar texto, é necessário transformar o objeto JavaScript que quizer enviar para uma `string JSON`. Por isso que do lado do back-end é preciso utilizar o `bodyParser` para transformar as informações que foram trafegadas como `string JSON`, de volta para um `objeto JavaScript`.

Não é possível fazer requisições POST diretamente pelo navegador como a requisição para rota `GET /recipes`. Por isso é necessário utilizar aplicações como o `Insomnia`, `Postman` ou a extensão `Thunder Client` do `VSCode` para fazer requisições de qualquer tipo diferente do `GET`.

Reanalizando a implementação do post:

~~~JavaScript
//...
app.post('/recipes', function (req, res) {
  const { id, name, price } = req.body;
  recipes.push({ id, name, price});
  res.status(201).json({ message: 'Recipe created successfully!'});
});
~~~

Na primeira linha foram desestruturados os atributos `id`, `name` e `price` do objeto `req.body` para na segunda linha usar esses valores para inserir um novo objeto dentro da array `recipes`. Na terceira e última linha foi retornada uma resposta com o `status 201`, que serve para sinalizar que ocorreu uma operação de persistência de uma informação e um `json` com o atributo `message`.

[Voltar ao sumário](#Sumário)

#### Put

Além de `GET` e `POST`, o `HTTP` também possui os métodos `PUT` e `DELETE` que são convencionalmente utilizados para rotas que, respectivamente, editam e removem objetos. O `Express` tem métodos específicos para definir rotas para esses dois verbos. Vamos começar dando um exemplo do uso do `PUT`.

~~~JavaScript
//...

app.put('/recipes/:id', function (req, res) {
  const { id } = req.params;
  const { name, price } = req.body;
  const recipeIndex = recipes.findIndex((r) => r.id === parseInt(id));

  if (recipeIndex === -1) return res.status(404).json({ message: 'Recipe not found!' });

  recipes[recipeIndex] = { ...recipes[recipeIndex], name, price };

  res.status(204).end();
});
//...
~~~

Observe que o `id` foi desestruturado do `req.params` enquanto que o `name` e o `price` foram desestruturados do `req.body`. É um padrão sempre mandar o `id` como parâmetro de rota e os atributos que vão ser alterados, no `body`, pois é uma boa prática do `RESTful`. Depois apenas foi usado o `findIndex()` para encontrar a receita correspondente ao `id` e atualizar os atributos para os valores recebidos. Por fim, foi devevolvida a resposta `HTTP` com o `status 204`, que serve para indicar que algo foi atualizado e foi utilizado o método `.end()` que indica que a resposta vai ser retornada sem retornar nenhuma informação.

[Voltar ao sumário](#Sumário)

#### Delete

~~~JavaScript
app.delete('/recipes/:id', function (req, res) {
  const { id } = req.params;
  const recipeIndex = recipes.findIndex((r) => r.id === parseInt(id));

  if (recipeIndex === -1) return res.status(404).json({ message: 'Recipe not found!' });

  recipes.splice(recipeIndex, 1);

  res.status(204).end();
});
~~~

Observe que novamente o `id` foi desestruturado do `req.params`. Essa é uma convenção que serve para sempre que for preciso trabalhar com `id` seja para pesquisar, editar e remover objetos através da `API`.

É possível fazer a mesma coisa enviando o id como query string ou no body da requisição, mas usar parâmetro de rota acaba sendo a forma mais simples de mandar esse tipo de dado entre todas as opções disponíveis.

E novamente como nada precisa ser retornado, somente alterado, o `status` foi o `204` e o método `end()` foi utilizado.

No front-end, para fazer requisições do tipo `PUT` e `DELETE` através do `fetch api` é possível utilizar os exemplos de código abaixo:

~~~JavaScript
// Requisição do tipo PUT
fetch(`http://localhost:3001/recipes/2`, {
  method: 'PUT',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    name: 'Macarrão ao alho e óleo',
    price: 40
  })
});

// Requisição do tipo DELETE
fetch(`http://localhost:3001/recipes/4`, {
  method: 'DELETE',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'application/json',
  }
});
~~~

~~~JavaScript
~~~

[Voltar ao sumário](#Sumário)

---

## Comandos NPM

- `npm init` - Permite criar, de forma rápida e simplificada, um novo pacote Node.js na pasta onde é executado. Ao ser executado, o comando pede para quem executou algumas informaçãoes sobre o pacote como nome, versão, nome das pessoas autoras e afins. Esse comando cria um arquivo `package.json`, com as respostas respondias e com alguns outros metadados, dentro desse arquivo ficam algumas configurações importantes para o pacote como nome, versão, dependências e scripts.

- `npm init -y` - Permite criar, de forma automática com os valores padrões, um novo pacote Node.js na pasta onde é executado. Ao invés de ficar respondendo as perguntas do comando anterior, esse comando já responde eles de forma automática, colocando os valores padrões.

- `npm run` - Faz com que o npm execute um determinado script configurado no `package.json`. Scripts são "atalhos" que podem ser definidos para executar determinadas tarefas relacionadas ao pacote atual. Para criar um script, é preciso alterar o `package.json` e adicionar uma nova chave ao objeto scripts. O valor dessa chave deve ser o comando que deseja que seja executado quando chamar aquele script. Exemplo:

~~~json
{
  "scripts": {
    "lint": "eslint"
  }
},
~~~

Para executar esse script é só rodar `npm run <nome do script>`. Exemplo:

~~~bash
npm run lint
~~~

É possível criar quantos scripts forem necessários, para realizar quais tarefas quiser. Inclusive, pode criar scripts que chamam outros scripts, criando assim "pipelines". Esse tipo de coisa é muito útil, por exemplo, quando trabalhando supersets do JavaScript como o TypeScript, ou transpiladores como o Babel, pois ambos exigem que sejam executaods comandos adicionais antes de iniciar os pacotes.

- `npm start` - Age como um "atalho" para o comando `npm run start`, uma vez que sua função é executar o script `start` definido no `package.json`. Como convenção, todo pacote que pode ser executado pelo terminal (como CLIs, APIs e afins) deve ter um script start com o comando necessário para executar a aplicação principal daquele pacote. Por exemplo, se tiver um pacote que calcula o IMC (Índice de Massa Corporal) de uma pessoa cujo código está no arquivo imc.js, é comum criar o seguinte script:

~~~json
{
  //...
  "scripts": {
    "start": "node imc.js"
  }
  //...
}
~~~

- `npm install` - É o responsável por baixar e instalar pacotes `Node.js` do `NPM` para o pacote do projeto, e existem algumas formas de usá-lo:

  - `npm install <nome do pacote>` - Baixa o pacote do registro do `NPM` e o adiciona ao objeto `dependencies` do `package.json`
  - `npm install -D <nome do pacote>` - É semelhante ao comando anterior. Baixa o pacote do registro do `NPM`, porém o adiciona ao objeto `devDependencies` do `package.json`, indicando que o pacote em questão não é necessário para executar a aplicação, mas é necessário para desenvolvimento, ou seja, para alterar o código daquela aplicação. Isso é muito útil ao colocar a aplicação no ar, pois pacotes marcados como `devDependencies` podem ser ignorados, já que vamos apenas executar a aplicação, e não modificá-la.
  - `npm install` - Baixa e instala todos os pacotes listados nos objetos de `dependencies` e `devDependencies` do `package.json`. Sempre deve ser executado ao clonar o repositório de um pacote para garantir que todas as dependências desse pacote estão instaladas.

[Voltar ao sumário](#Sumário)

---

## Métodos HTTP

- `.listen()` - Especifica a porta onde a aplicação ficará ouvindo as requisições, pode receber uma callback como parâmetro. Exemplo:

~~~JavaScript
app.listen(3000, () => console.log('exemplo'))
~~~

- `.status()` - Retorna o status da resposta, esse status está ligado com os [códigos HTTP](../imagens/HTTP_Status_Code.jpg) de resposta. Exemplo:

~~~JavaScript
res.status(200);
~~~

- `.send()` - Retorna a resposta de uma requisição de uma forma genérica, adaptando o tipo de retorno ao que vai ser retornado. Exemplo:

~~~JavaScript
res.status(200).send('Hello, world!');
~~~

- `.json()` - Retorna a resposta em forma de JSON. Exemplo:

~~~JavaScript
res.status(200).json('Hello, world!');
~~~

- `.route()` - Especifica uma rota para que vários métodos possam ser encadeados nessa mesma rota. Exemplo:

~~~JavaScript
app
  .route('/')
  .get(function (req, res) {
        // Requisições para rota GET `/` são resolvidas aqui!
    res.json('hello world get');
  })
  .post(function (req, res) {
        // Requisições para rota POST `/` são resolvidas aqui!
    res.json('hello world post');
  });
~~~

- `.end()` - Indica que a requisição será retornada sem nenhuma informação. Exemplo:

~~~JavaScript
res.status(204).end();
~~~

[Voltar ao sumário](#Sumário)

**Métodos de tipos de requisição podem ser encadeados em routes, como visto acima, entretanto, caso não haja um método `route()` é necessário especificar no método de requisição qual será a rota utilizada, aqui especificaremos todos os métodos de requisição como senão estivessem ligados a um método `route()`.**

### CRUD

- `.get()` - Faz uma requisição de leitura e espera a resposta de algo que possa ser exibido. Exemplo:

~~~JavaScript
app.get('/recipes/search', function (req, res) {
  const { name } = req.query;
  const filteredRecipes = recipes.filter((r) => r.name.includes(name));
  res.status(200).json(filteredRecipes);
});
~~~

- `.post()` - Faz uma requisição de escrita, ou seja, adiciona algo no back-end. Exemplo

~~~JavaScript
app.post('/recipes', function (req, res) {
  const { id, name, price } = req.body;
  recipes.push({ id, name, price});
  res.status(201).json({ message: 'Recipe created successfully!'});
});
~~~

- `.put()` - Faz uma requisição de atualização, ou seja, atualiza informações no back-end. Exemplo:

~~~JavaScript
app.put('/recipes/:id', function (req, res) {
  const { id } = req.params;
  const { name, price } = req.body;
  const recipeIndex = recipes.findIndex((r) => r.id === parseInt(id));

  if (recipeIndex === -1) return res.status(404).json({ message: 'Recipe not found!' });

  recipes[recipeIndex] = { ...recipes[recipeIndex], name, price };

  res.status(204).end();
});
~~~

- `.delete()` - Faz uma requisição de deleção, ou seja, deleta informações no back-end. Exemplo:

~~~JavaScript
app.delete('/recipes/:id', function (req, res) {
  const { id } = req.params;
  const recipeIndex = recipes.findIndex((r) => r.id === parseInt(id));

  if (recipeIndex === -1) return res.status(404).json({ message: 'Recipe not found!' });

  recipes.splice(recipeIndex, 1);

  res.status(204).end();
});
~~~

~~~JavaScript
~~~

[Voltar ao sumário](#Sumário)
