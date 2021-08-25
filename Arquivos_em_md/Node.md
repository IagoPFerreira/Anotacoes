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

## Comandos

### npm

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
npm run lin
~~~

É possível criar quantos scripts forem necessários, para realizar quais tarefas quiser. Inclusive, pode criar scripts que chamam outros scripts, criando assim "pipelines". Esse tipo de coisa é muito útil, por exemplo, quando trabalhando supersets do JavaScript como o TypeScript, ou transpiladores como o Babel, pois ambos exigem que sejam executaods comandos adicionais antes de iniciar os pacotes.

- `npm start` - Age como um "atalho" para o comando `npm run start`, uma vez que sua função é executar o script `start` definido no `package.json`. Como convenção, todo pacote que pode ser executado pelo terminal (como CLIs, APIs e afins) deve ter um script start com o comando necessário para executar a aplicação principal daquele pacote. Por exemplo, se tiver um pacote que calcula o IMC (Índice de Massa Corporal) de uma pessoa cujo código está no arquivo imc.js, é comum criar o seguinte script:

~~~json
{
  // ...
  "scripts": {
    "start": "node imc.js"
  }
  // ...
}
~~~

- `npm install` - É o responsável por baixar e instalar pacotes `Node.js` do `NPM` para o pacote do projeto, e existem algumas formas de usá-lo:

  - `npm install <nome do pacote>` - Baixa o pacote do registro do `NPM` e o adiciona ao objeto `dependencies` do `package.json`
  - `npm install -D <nome do pacote>` - É semelhante ao comando anterior. Baixa o pacote do registro do `NPM`, porém o adiciona ao objeto `devDependencies` do `package.json`, indicando que o pacote em questão não é necessário para executar a aplicação, mas é necessário para desenvolvimento, ou seja, para alterar o código daquela aplicação. Isso é muito útil ao colocar a aplicação no ar, pois pacotes marcados como `devDependencies` podem ser ignorados, já que vamos apenas executar a aplicação, e não modificá-la.
  - `npm install` - Baixa e instala todos os pacotes listados nos objetos de `dependencies` e `devDependencies` do `package.json`. Sempre deve ser executado ao clonar o repositório de um pacote para garantir que todas as dependências desse pacote estão instaladas.

~~~JavaScript
~~~
