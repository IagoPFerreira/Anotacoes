# React

O React é, atualmente, uma das principais bibliotecas Javascript para construção de interfaces de usuário. Esta poderosa ferramenta foi criada pelos times de desenvolvimento do Facebook com objetivo de organizar, componentizar e, consequentemente, tornar muito mais eficiente cada parte das aplicações que a utilizam.

A ideia principal é tornar possível dividir a sua aplicação em pequenos blocos, reutilizáveis ou não, que podem fazer a gestão das suas próprias informações através do seu estado, ou seja, reagir a eventos, interações, dados, etc. Toda vez que houver uma mudança em um componente, o React atua especificamente na renderização dele, sem que seja necessário atualizar os outros blocos.

A componentização permite ainda utilizar funções específicas, estilizações, testes e outras tecnologias no exato local em que ela será utilizada, permitindo que qualquer possível refatoração do código se torne simples, bem endereçada e fácil de se encontrar.

O exemplo mais prático de uma aplicação React é a própria [documentação](https://pt-br.reactjs.org/) dela. Além de ser possível visualizar as principais componentizações, como header, menu lateral, conteúdo principal, barra lateral, submenus e footer, conseguimos acessar menus diferentes sem que a página recarregue. Super eficiente, certo? Existem diversas outras ferramentas, como o próprio Facebook e o Slido, que funcionam da mesma forma dinâmica.

## Gerenciadores de pacote

Gerenciadores de pacote são scripts que são utilizados para instalação de pacotes necessários para rodar certas aplicações, existem vários gerenciadores de pacotes, um deles é o npm. O npm  é o gerenciador de pacotes em si, ou seja, ele é quem será utilizado para instalar os pacotes, , enquanto o npx executa o comando de um pacote sem instalá-lo em si. Como o create-react-app é um pacote que a única coisa que faz é criar todos os arquivos necessários para termos um app React, não rodamos ele mais de uma vez por projeto, nem precisamos do pacote instalado em nossas máquinas, por isso **SEMPRE** executamos ele com o npx e não com o npm . Para rodar o npx é só fazer o seguinte passo a passo:
Na pasta onde deseja criar a aplicação React, pelo terminal insira o comando:

~~~unix
npx create-react-app testando-meu-computador 
~~~

Caso seja instalado o gerenciador de pacotes yarn ou algum outro diferente do npm, é só inserir o próximo comando:

~~~unix
npm install
~~~

Com o npx rodado e o npm instalado, é só entrar no diretório criado pelo npx e inserir o próximo comando:

~~~unix
npm start
~~~

Esse comando irá abrir em um navegador a tela do React, caso tudo tenha dado certo durante esse processo, e dentro do diretório criado pelo npx, terão os arquivos para serem utilizados na aplicação React.

## JSX

O JSX , ou Javascript Extension , como o próprio nome sugere, é uma extensão de sintaxe para Javascript. Sua utilização é recomendada pela documentação do React, pois ela demonstra como a interface deverá se comportar, de forma lógica e descritiva.
Exemplo:

~~~JavaScript
const element = <h1>Hello, world!</h1>;
~~~

A construção de um elemento JSX é bem parecida com um elemento HTML, com pequenas diferenças para que não haja conflito do HTML com o JS. Um exemplo disso é a declaração de uma class no HTML, que é substituída por className no JSX, pois haveria conflito de sintaxe com as classes do JS.

Caso fosse declarar a mesma variável sem o JSX, seria preciso utilizar funções como o createElement que recebe como parâmetro um componente, um objeto com as props e o conteúdo que será encapsulado por este componente. Seriam necessárias sequências relativamente longas de instruções de código para conseguir montar e manipular uma árvore de componentes. Para visualizar essa complexidade, o código acima foi refatorado sem o JSX:

~~~JavaScript
const element = React.createElement("h1", null, "Hello, world")
~~~

Agora imagine uma aplicação inteira sendo construída dessa forma. Ficaria muito mais difícil de ser compreendida, certo? O JSX encaixa-se perfeitamente para resolver este dilema.

É importante frisar que o uso do JSX em aplicações React não é obrigatório, mas a complexidade da construção de uma aplicação fica menor e o código fica mais intuitivo quando o utilizamos.

## Incorporando expressões no JSX

Por ser um código Javascript, o JSX permite que se faça injeções de algoritmos dentro da estrutura HTML. Portanto, é possível que se aplique diretamente na estrutura códigos que renderizarão outras diversas expressões, por exemplo:

~~~JavaScript
const nome = 'Jorge Maravilha';
const element = <h1>Hello, {nome}</h1>;
~~~

E se aprofundarmos um pouco mais chamando uma função na nossa constante element?

~~~JavaScript
function nomeCompleto (nome, sobrenome) {
  return `${nome} ${sobrenome}`;
}
const element = <h1>Hello, {nomeCompleto("Jorge", "Maravilha")}</h1>;
~~~

Agora, vamos incorporar a nossa constante element na função helloWorld , retornar um código JSX e encapsulá-la em uma div :

~~~JavaScript
function helloWorld (nome, sobrenome) {
  return <h1>Hello, {`${nome} ${sobrenome}`}</h1>;
}
const container = <div>{element}</div>;
~~~

Lembra que falamos sobre a substituição de class por className em JSX? Podemos também utilizar expressões Javascript para atribuir valor à este atributo.

~~~JavaScript
const nome = 'Jorge Maravilha';
const classe = 'hello-class';
const element = <h1 className={classe}>Hello, {nome}</h1>;
~~~

## Especificando atributos com JSX

O JSX permite usar aspas para especificar strings literals como atributos:

~~~JavaScript
const element = <div tabIndex="0"></div>
~~~

Permite também que sejam usadas chaves para incorporar uma expressão JavaScript em um atributo:

~~~JavaScript
const element = <h1 className={classe}>Hello, {nome}</h1>;
~~~

**OBSERVAÇÃO**: NÃO envolva chaves com aspas quando estiver incorporando uma expressão JavaScript em um atributo. Você deveria usar aspas (para valores strings) ou chaves (para expressões), mas não ambos no mesmo atributo.

## ReactDOM.render

O ReactDOM.render é o responsável por renderizar e atualizar seu código dentro do HTML , exibindo seus elementos React .

Todas as vezes que fizermos alguma alteração no código, seja através de uma função ou interação de quem usa, o React DOM compara o elemento novo e seus elementos filhos com os anteriores e aplica mudanças somente onde é necessário para levar a aplicação ao estado desejado. Exemplo:

~~~JavaScript
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById("root"));
}
setInterval(tick, 1000);
~~~

Neste exemplo, estamos chamando a função tick que chama o ReactDOM.render a cada segundo, e injeta no elemento pai com id root um 'Hello World' e o horário. Diferente de elementos DOM do navegador, elementos React são objetos simples e utilizam menos recursos. Pela atualização precisa do DOM, e pela sua composição, o React apresenta grandes avanços na velocidade de processamento.

Como JSX é mais próximo de JavaScript do que HTML, o React DOM usa camelCase como convenção para nomes de propriedades ao invés dos nomes de atributos do HTML. Por exemplo, class se transforma em className em JSX, e tabindex se transforma em tabIndex.

## Renderizando um elemento no DOM

Elementos são os menores blocos de construção de aplicativos React, um elemento descreve o que você quer ver na tela. Exemplo:

~~~JavaScript
const element = <h1>Hello, world</h1>;
~~~

Diferente de elementos DOM do navegador, elementos React são objetos simples e utilizam menos recursos. O React DOM é o responsável por atualizar o DOM para exibir os elementos React. Pode-se confundir elementos com o conceito mais amplo de “componentes”.

Elementos React são imutáveis. Uma vez criados, você não pode alterar seus elementos filhos ou atributos, ou seja, você não pode fazer reatribuições diretas. Com o que aprendemos até agora, a única forma de atualizar a interface é criar um novo elemento e passá-lo para o `ReactDOM.render()`, mas na prática, a maioria das aplicações em React usam o `ReactDOM.render()` apenas uma única vez.

O React DOM compara o elemento novo e seus filhos com os anteriores e somente aplica as modificações necessárias no DOM para levá-lo ao estado desejado, sem alterar ou recarregar os elementos que não sofreram alteração, dessa forma o React consegue aumentar a eficiência do código.

## Componentes e Props

Componentes permitem você dividir a UI em partes independentes, reutilizáveis e pensar em cada parte isoladamente. Conceitualmente, componentes são como funções JavaScript. Eles aceitam entradas arbitrárias  (chamadas “props”) e retornam elementos React que descrevem o que deve aparecer na tela.

A maneira mais simples de definir um componente é escrever uma função JavaScript:

~~~JavaScript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
~~~

Essa função é um componente React válido porque aceita um único argumetno de objeto “props” (que significa propriedades) com dados e retorna um elemento React. Nós chamamos esses componentes de “componentes de função” porque são literalmente funções JavaScript.

Também é possível utilizar uma classe no estilo ES6 para definir um componente:

~~~JavaScript
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
~~~

## Renderizando um Componente

Anteriormente, vimos apenas elementos React que representam tags do DOM. Exemplo:

~~~JavaScript
const element = <h1>Hello, world</h1>;
~~~

Entretanto, elementos também podem representar componentes definidos pelo usuário. Exemplo:

~~~JavaScript
const element = <Welcome name="Sara">
~~~

Quando o React vê um elemento representando um componente definido pelo usuário, ele passa atributos JSX e componentes filhos para esse componente como um único objeto, chamado de `props`. Exemplo:

~~~JavaScript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(element, document.getElementById("root"));
~~~

Recapitulando esse exemplo:

1. O `ReactDOM.render()` é chamado com o elemento `<Welcome name="Sara" />`
2. O React chama o componente Welcome com `{name: ‘Sara’}` como `props`.
3. O componente Welcome reorna um elemento `<h1>Hello, Sara</h1>` como resultado.
4. React DOM atualiza eficientemente o DOM para corresponder `<h1>Hello, Sara</h1>`.

**Observação:** Sempre inicie os nomes dos componentes React com uma letra maiúscula, o React trata componentes começando com letras minúsculas como tags do DOM. Por exemplo, `<div />` representa uma tag div do HTML, mas `<Welcome />` representa um componente e requer que Welcome esteja no escopo.

## Compondo componentes

Componentes podem se referir a outros componentes em sua saída. Isso nos permite usar a mesma abstração de componente para qualquer nível de detalhe. Um botão, um formulário, uma caixa de diálogo ou uma tela, em aplicativos React, todos esses são normalmente expressos como componentes. Por exemplo:

~~~JavaScript
function App() {
  return (
    <div className="App">
      <Header />
      <MovieLibrary movies={movies} />
    </div>
  );
}
~~~

Tipicamente, novas aplicações React possuem um único componente App no topo. Contudo, se você integrar o React em um aplicativo existente, você pode começar de baixo para cima com um pequeno componente como o Button e gradualmente chegar ao topo da hierarquia de exibição.

Não tenha medo de dividir um componente em componentes menores. Extrair componentes pode parecer um trabalho pesado no começo, mas ter uma paleta de coponentes reutilizáveis compensa em aplicações maiores. Uma boa regra é que se uma parte da sua UI for usada várias vezes (Button, Panel, Avatar) ou for complexa o suficiente por si só (App, FeedStory, Comment) é uma boa candidata ser extraída para uma componente separado.

## Props são somente para leitura

Independente se você declarar um componente como uma função ou uma classe, ele nunca deve modificar seus próprios props. Considere essa função:

~~~JavaScript
function sum(a, b) {
  return a + b;
}
~~~

Funções assim são chamadas de “puras”, pois elas não tentam alterar suas entradas e sempre retornam o mesmo resultado para as mesmas entradas. Em contraste, existem funções impuras, que alteram suas próprias entradas. Exemplo:

~~~JavaScript
function withdraw(account, amount) {
  account.total -= amount;
}
~~~

O React é bastante flexível, mas tem uma única regra estrita:  **Todos os componentes React tem que agir como funções puras em relação ao seus props.**

Obviamente, as UIs de aplicações são dinâmicas e mudam com o tempo. O state permite aos componentes React alterar sua saída ao longo do tempo em resposta a ações do usuário, respostas de rede e quaisquer outras coisas, sem violar essa regra.

## Estado

States (Estados) são informações de um componente que podem sofrer alterações, e que normalmente são utilizados para realizar as atualizações de componentes React. Para adicionar um state no seu componente:

1. Crie um componente utilizando o formato de classe e dentro do JSX criado dentro do return do `render()`, onde você for chamar o dado que vai sofrer a atualização declare da seguinte forma:

~~~JavaScript
{this.state.dadoQueSeraAtualizado}
~~~

2. Adicione um construtor na classe, neste construtor é que será atribuído o valor inicial do state:

~~~JavaScript
constructor(props) {
  super(props);

  this.state = { name: 'Manuela' };
}
~~~

**Observação:** Segundo a documentação do React: Componentes de classes devem sempre chamar o construtor com props. Entretanto existem exemplos de várias aplicações React disponíveis que não passam props como parâmetro para constructor e super, quando não há utilização de props dentro do constructor, mas quando há utilização para qualquer que seja a finalidade, se torna obrigatório essa declaração de parâmetros.

Após esses dois passos o código deveria ficar parecido com isso:

~~~JavaScript
import React from "react";

class Welcome extends React.Component {
  constructor(props) {
    super(props);

    this.state = { name: "Manuela" };
  }

  render() {
    return (
      <div>
        <h1>Olá {this.state.name}</h1>
      </div>
    );
  }
}

ReactDom.render(<Welcome />, document.getElementById("root"));
~~~

## Adicionando métodos de ciclo de vida a uma classe

Em aplicações com muitos componentes, é muito importante limpar os recursos utilizados pelos componentes quando eles são destruídos.

Os componentes React , assim como os seres vivos, possuem um ciclo de vida. No caso do React, o ciclo é dividido em 4 etapas. São elas:

1. Inicialização é quando um componente recebe as props e os estados.
2. Montagem (mounting) é quando o componente é inserido no DOM.
3. Atualização é quando os props ou estados do componente são alterados.
4. Desmontagem (unmounting) quando o componente morre, sumindo do DOM.

Podemos declarar métodos especiais no componente de classe para executar algum código quando um componente é montado e desmontado.

~~~JavaScript
componenetDidMonunt() {}

componentWillUnmount() {}
~~~

Estes componentes são chamados de “métodos de ciclo de vida”.

O método componenteDidMount() é executado depois que a saída do componente é renderizada no DOM.

~~~JavaScript
componentDidMount() {
  this.timerID = setInterval(
    () => this.tick(),
    1000
  );
}
~~~

Enquanto this.props é configurado pelo próprio React e this.state tem um significado especial, você está livre para adicionar campos adicionais à classe manualmente se precisar armazenar algo que não participe do fluxo de dados (como um ID).

~~~JavaScript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }

  componentDidMount() {
    this.timerID = setInterval(() => this.tick(), 1000);
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date(),
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(<Clock />, document.getElementById("root"));
~~~

Analisando o código acima:

1. Quando `<Clock />` é passado para `ReactDOM.render()`, o React chama o construtor do componente `Clock`. Como `Clock` precisa exibir a hora atual, ele inicializa `this.state` com um objeto incluindo a hora atual.
2. React chama então o método `render()` do componente `Clock`. É assim que o React aprende o que deve ser exibido na tela. React em seguida, atualiza o DOM para coincidir com a saída de renderização do `Clock`.
3. Quando a saída do `Clock` é inserida no DOM, o React chama o método do ciclo de vida `componentDidMount()`. Dentro dele, o componente `Clock` pede ao navegador para configurar um temporizador para chamar o método `tick()` do componente uma vez por segundo.
4. A cada segundo o navegador chama o método `tick()`. Dentro dele, o componente `Clock` agenda uma atualização de UI chamando `setState()` com um objeto contendo a hora atual. Graças à chamada `setState()`, o método `render()` será diferente e, portanto, a saída de renderização incluirá a hora atualizada. React atualiza o DOM de acordo.
5. Se o componente `Clock` for removido do DOM, o React chama o método do ciclo de vida `componentWillUnmount()` para que o temporizador seja interrompido.

## Usando o State corretamente

Existem 4 coisas que você deve saber sobre o `setState()`.

1. Não modifique o state diretamente.

- Por exemplo, isso não renderizará novamente o componente:

~~~JavaScript
// Errado
this.state.comment = 'Hello';
~~~

- Em vez disso, use `setState()`:

~~~JavaScript
// Correto
this.setState({comment: 'Hello'});
~~~

2. O único lugar onde você pode atribuir `this.state` é o construtor.
3. Atualizações de state podem ser assíncronas

- O React pode agrupar várias chamadas `setState()` em uma única atualização para desempenho. Como `this.props` e `this.state` podem ser atualizados de forma assíncrona, você não deve confiarem seus valores para calcular o próximo `state`. Por exemplo, esse código pode falhar ao atualizar o contador:

~~~JavaScript
// Errado
this.setState({
  counter: `this.state`.counter + this.props.increment,
});
~~~

- Para concertá-lo, é necessário usar uma segunda forma de `setState()`, que aceite uma função ao invés de um objeto. Essa função receberá o state anterior como o primeiro argumento e as props no momento em que a atualização for aplicada como o segundo  argumento:

~~~JavaScript
// Correto
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
~~~

4. Atualizações de state são mescladas

- Quando o `setState()` é chamado, o React mescla o objeto que você fornece ao state atual. Por exemplo: seu state pode conter várias variáveis independentes:

~~~JavaScript
constructor(props) {
  super(props);
  this.state = {
    posts: [],
    comments: []
  };
}
~~~

- Então você pode atualizá-los independentemente com chamadas separadas do `setState()`:

~~~JavaScript
componentDidMount() {
  fetchPosts().then(response => {
    this.setState({
      posts: response.posts
    });
  });

  fetchComments().then(response => {
    this.setState({
      comments: response.comments
    });
  });
}
~~~

O merge é superficial, então this.setState({comments}) deixa this.state.posts intacto, mas substitui completamente this.state.comments

## Manipulando eventos

Manipular eventos em elementos React é muito semelhante a manipular eventos em elementos DOM. Existe algumas diferenças de sintaxe:

1. Eventos em React são nomeados usando camelCase ao invés de letras minúsculas.
2. Com o JSX você passa uma função como manipulador de eventos ao invés de um texto.

Por exemplo, com HTML:

~~~JavaScript
<button onclick="activateLasers()">
  Ativar lasers
</button>
~~~

Com React:

~~~JavaScript
<button onClick={activateLasers}>
  Ativar lasers
</button>
~~~

Outra diferença é que você não pode retornar false para evitar o comportamento padrão no React. Você deve chamar preventDefault explicitamente. Por exemplo, com HTML simples, para evitar que um link abra uma nova página, você pode escrever:

~~~JavaScript
<a href="#" onclick="console.log('O link foi clicado.'); return false">
  Clique Aqui
</a>
~~~

No React, isso poderia ser assim:

~~~JavaScript
function handleClick(e) {
  e.preventDefault();
  console.log('O link foi clicado.');
}

return (
  <a href="#" onClick={handleClick}>
    Clique Aqui
  </a>
);
~~~

## Single Page Application (SPA)

SPAs é um conceito de páginas que são carregadas somente no momento em que o usuário entra no site e toda a interação de mudanças de páginas é feito sem que o navegador precise recarregar o site, ou seja, o usuário entra no site e o navegador carrega somente 1 vez o site, através da URL utilizada pelo usuário, todas as interações feitas pelo usuário que o leve a outras páginas no mesmo site, serão feitas sem que o navegador precise reconstruir a página do 0, todo o conteúdo virá a partir de uma lógica criada em JavaScript, aumentando assim a performance do site.

## Definindo props.children

A propriedade props.children está disponível em todos os componentes. Ele contém o conteúdo entre as tags de abertura e fechamento de um componente. Por exemplo:

~~~JavaScript
<BemVindo >Hello, world!</BemVindo>
~~~

A string `Hello, world!` está disponível em `props.children` no componente BemVindo:

~~~JavaScript
function BemVindo(props) {
  return <p>{props.children}</p>;
}
~~~

Para componentes definidos como classes, use this.props.children:

~~~JavaScript
class BemVindo extends React.Component {
  render() {
    return <p>{this.props.children}</p>;
  }
}
~~~

## React Router DOM

Para poder fazer uso de React Router, é preciso que se instale em uma aplicação React o pacote react-router-dom.

~~~Unix
npm install react-router-dom
~~~

1. O BrowserRouter é o componente que encapsula a sua aplicação, de forma a te possibilitar fazer uso de navegação.
2. Route é o componente fundamental em React Router, que estabelece o mapeamento entre o caminho de URL declarado com o componente. Tal mapeamento, no que diz respeito à correspondência entre o caminho da URL atual e a presente no componente, pode ser feito das seguintes formas:

- `<Route path="/about" component={About} />` : lê-se que se o caminho da URL atual do navegador começa com o caminho /about , como declarado na prop path no componente Route , há uma correspondência entre os caminhos da URL e do componente Route , e o componente About será renderizado. Ou seja, se o caminho da URL atual for `/home` , não há correspondência, logo o componente About não será renderizado. Entretanto, se a URL atual for `/about` ou `/about/me` , há correspondência, e o componente About é renderizado. O parâmetro exact entra em ação quando você tem vários caminhos com nomes semelhantes.
- `<Route exact path="/about" component={About} />` : lê-se que, se houver uma correspondência exata entre o caminho da URL atual e o caminho `/about` declarado em Route , o componente será renderizado. Ou seja, se o caminho da URL atual for `/home` ou `/about/`me , não há correspondência exata, logo o componente About não será renderizado. Entretanto, se a URL atual for `/about` , há correspondência exata, e o componente About será renderizado.
- **OBS:** Além dessas duas formas de renderização de componente com Route , você pode fazer uso de elemento children . Ou seja, se você tiver a rota `<Route path="/about" component={About} />` , você também poderá fazer da seguinte forma:

~~~JavaScript
<Route path="/about" >
  <About />
</Route>
~~~

3. Se houver vários componentes apresentando correspondência entre seu caminho de URL e o caminho atual da aplicação, todos os componentes apresentando correspondência serão renderizados . Ou seja, suponha que houvesse a seguinte lista de componentes do tipo Route:

~~~JavaScript
<Route path="/about" component={About} />
<Route path="/contact" component={Contact} />
<Route path="/" component={Home} />
~~~

- Se o caminho atual da URL da aplicação for `/` , todos esses componentes serão renderizados, haja vista que todas as rotas não fazem correspondência exata entre o caminho da URL atual e o definido via prop path , e fazer `path="/"` faz correspondência com qualquer caminho de URL;
- Agora, se o caminho atual da URL da aplicação for /contact , os componentes Contact e Home serão renderizados. Isso pode ser um problema, e uma forma de atacá-lo é organizar essas rotas via componente Switch.

4. Link é o componente a ser usado no lugar de elementos com a tag a , de forma a disponibilizar navegação por URL na sua aplicação SPA sem o recarregamento de página que a tag a exige. Ou seja, se você quiser definir um link que leve quem usa sua aplicação para a URL com o caminho /about , você poderia chamar o componente Link da seguinte forma:

~~~JavaScript
<Link to="/about" > About </Link>
~~~

E lembre-se: palavras, imagens, até mesmo outros componentes podem ser componentes filhos do Link ! Ser filho do Link significa que, se você clicar neste filho, irá para onde o Link te direciona!

## Componentes Route com passagem de props

No que diz respeito ao componente Route , você pode associar um componente com o caminho da URL via children , component ou render.

Faz-se uso da prop component de Route quando não é necessário passar informações adicionais via props para o componente a ser mapeado. Ou seja, se você tem um componente About que não precisa de props setadas para ser chamado, e você precisa mapeá-lo para o caminho de URL /about , você poderia criar uma rota da seguinte forma:

~~~JavaScript
<Route path="/about" component={About} />.
~~~

Já a prop render de Route é usada quando é necessário passar informações adicionais via props para o componente a ser mapeado. Ou seja, se você tem um componente Movies que precisa receber uma lista de filmes via props movies , e você precisa mapeá-lo para o caminho de URL /movies , você poderia criar uma rota da seguinte forma:

~~~JavaScript
<Route path="/movies" render={(props) => <Movies {...props} movies={['Cars', 'Toy Story', 'The Hobbit']} />} />.
~~~

Tanto component quanto `render` permitem que você tenha acesso a informações de rota ( `match` , `location` e `history` ) via `props` do componente que você está mapeando. Ou seja, se você tem a rota:

~~~JavaScript
<Route path="/about" component={About} />, 
~~~

`About` terá `match` , `location` e `history` setadas via `props`.

## Rotas dinâmicas

O interessante em rotas dinâmicas é que podemos utilizar o mesmo componente para renderizar vários caminhos diferentes. Para fazer uso de parâmetro de URL em Route , é preciso fazer uso da sintaxe :nome_do_parametro dentro da propriedade path . Ou seja, `<Route path="/movies/:movieId" component={Movie} />` vai definir um parâmetro chamado movieID , e o componente Movie é mapeado a qualquer um dos seguintes caminhos de URL :
- /movies/1
- /movies/2
- /movies/thor

## Hooks

Hooks são funções que permitem a divisão de um componente em funções menores, baseadas em pedaços que são relacionados, em vez de forçar uma divisão baseada nos métodos de ciclo de vida.

Em React existem 2 formas de criar um componente, usando classe ou função, em componentes de classe é possível trabalhar com o uso de métodos de ciclo de vida, como `componentDidMount`, `componentDidUpdate`, `componentShouldUpdate` e `componentWillUnmount`, dentre outros, além de podermos declarar estados internos para armazenar dados que irão variar entre os componentes, entretanto, em componentes funcionais não temos acesso a esses métodos de ciclo de vida, para solucionar esse problema foram criados os ``Hooks``.

O React fornece alguns `Hooks` internos, mas é possível criar `Hooks` personalizados  para reutilizar o comportamento de state entre componentes diferentes. Vejamos alguns `Hooks` internos primeiramente.

## Hook de Estado

Assim como não existe o acesso a métodos de ciclo de vida em componentes funcionais, não há o acesso ao constructor também, dessa forma, não é possível criar e alterar estados da forma como já estamos familiarizados, entretanto, existe uma forma de criar e manipular um estado em componentes funcionais, essa forma é usando os Hooks, o Hook específico para isso é o Hook de Estado (`useState()`), o `useState()` retorna um par: o valor do estado atual e uma função que permite atualizá-lo. Essa função de atualização do estado pode ser chamada a partir de um manipulador de evento ou de qualquer outro lugar. Essa função é parecida com this.setState em uma classe, exceto que não mescla o estado antigo com o novo. O `useState()`  recebe um único parâmetro, que é o estado inicial, diferente do this.state, aqui o estado não precisa ser um objeto, a não ser que você queira, pois o estado inicial é utilizado apenas durante a primeira renderização. Ex:

~~~JavaScript
import React, { useState } from "react";

function Example() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Você clicou {count} vezes</p>
      <button type="button" onClick={() => setCount(count + 1)}>
        Clique
      </button>
    </div>
  );
}

export default Example;
~~~

Neste exemplo o estado foi declarado como `count`, a função que altera o estado foi declarada como `setCount` e o `useState()` recebeu como parâmetro inicial 0. Dessa forma, toda vez que o botão for clicado a função `setCount` será chamada e irá alterar o estado da forma como a lógica dela foi construída, que neste caso é aumentar em 1 o número do contador.

É possível usar o `useState()` mais de uma vez em um único componente. Ex:

~~~JavaScript
function ExampleWithManyStates() {
  const [count, setCount] = useState(0);
  const [age, setAge] = useState(42);
  const [fruits, setFruits] = useState("banana");
  const [todos, setTodos] = useState([{ text: "Aprenda Hooks!" }]);

  //...
}
~~~

A sintaxe de desestruturação de arrays nos permite atribuir diferentes nomes para as variáveis de state que declaramos chamando useState. Esses nomes não fazem parte da API useState. Em vez disso, React presume que se você chamar useState muitas vezes, você faz isso na mesma ordem a cada renderização. Mais tarde, voltaremos no porquê disso funcionar e quando será útil.

## Hook de Efeito

Ao longo dos estudos de React nós realizamos várias vezes obtenções de dados, subscrições ou mudanças manuais no DOM através de componentes React. Essas operações são chamadas de “efeitos colaterais” (side effects ou apenas effects) porque eles podem afetar outros componentes e não podem ser feitos durante a renderização.

O Hook de Efeito (`useEffect()`) adiciona a funcionalidade de executar efeitos colaterais através de um componente funcional. Seguindo a mesma funcionalidade do componentDidMount, componentDidUpdate e componentWillUnmount em classes React, mas unificado em uma mesma API. Ex:

~~~JavaScript
import React, { useEffect, useState } from "react";

function ExampleWithManyStates() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `Você clicou ${count} vezes`;
  });

  return (
    <div>
      <p>Você clicou {count} vezes</p>
      <button type="button" onClick={() => setCount(count + 1)}>
        Clique
      </button>
    </div>
  );
}

export default ExampleWithManyStates;
~~~

Neste exemplo a cada vez que o botão for clicado o título que fica na aba do navegador será atualizado como número de cliques. Quando o `useEffect()` é chamado ele diz ao React para executar a sua função de “efeito” após liberar as mudanças para o DOM. Efeitos são declarados dentro do componente, para que eles tenham acesso as suas props e state. Por padrão, o React executa os efeitos após cada renderização, incluindo a primeira renderização.

Efeitos também podem opcionalmente especificar como “limpar” retornando uma função após a execução deles. Ex:

~~~JavaScript
import React, { useEffect, useState } from "react";

function FriendStatus() {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    };
  });
  if (isOnline === null) {
    return "Loading...";
  }
  return isOnline ? "Online" : "Offline";
}
~~~

Neste exemplo o componente usa um efeito para se subscrever ao status online de um amigo e limpa-se cancelando a sua subscrição, dessa forma, o React cancelaria a subscrição da ChatAPI quando o componente se desmontar, e também antes de reexecutar o efeito devido a uma renderização subsequente. Assim como o `useState()` é possível usar o useEffect mais de uma vez.
