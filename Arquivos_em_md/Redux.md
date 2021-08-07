# Redux

O Redux é uma biblioteca muito adotada no desenvolvimento Front-end, ela pode ser implementada muito facilmente no JavaScript puro, assim como em frameworks do JS como o React, além disso também pode ser usada para arquitetura de desenvolvimento Android e iOS. O Redux é uma biblioteca de armazenamento de dados em forma de estado, ou seja, assim como componentes em React guarda informações que podem sofrer alterações em states e props, o Redux faz a mesma coisa, a diferença é que o Redux consegue armazenar dados de múltiplos componentes, sem a necessidade que esses componentes esteja diretamente interligados, e consegue fazer com que esses estados sejam passados para os componentes sem que caminhos entre esses componentes sejam criados em meio a outros componentes.

Não é necessário passar a informação do componente A para o componente B, para ele passar para o componente C que vai passar para o componente D, que ele sim irá usar a informação do componente A. O Redux nos permite cortar essa quantidade de intermediários, criando um intermediário só.

Vamos refazer esse caminho do componente A até o componente D utilizando o Redux, o componente A passa os estados para o Redux e o Redux passa os estados do componente A para o componente D, sem mais intermediários.

No cenário acima parece não fazer muita diferença, pois cortamos somente 1 intermediário, mas agora imagine se essa informação precisasse sair do componente A e ir até o componente J, quantos intermediários teriam no caminho? Quais seriam as chances de algum erro acontecer durante a passagem desses dados? E o trabalho que daria para ficar passando props e estados a todo tempo? Seria basicamente uma repetição de trabalho e linhas de código desnecessária, e como já aprendemos ao longo dos estudos em programação, existe uma máxima quanto a coisas repetidas: “Se você está repetindo o mesmo conjunto de código muitas vezes, é porque sua construção está errada, provavelmente uma função resolveria isso”. Dentro do Redux isso não é diferente, a biblioteca possui funções internas que nos permitem passar estados para um local de armazenamento e funções que nos permitem buscar essas informações, mas essas não são as únicas funções que ela possui, mais dessas funções serão descritas ao longo dessa seção.

Como visto acima, o Redux existe para auxiliar no fluxo de dados dentro de uma aplicação. Com ele é possível ter, além do estado local de cada componente, um estado global, acessível a todos os componentes, onde se pode armazenar e recuperar informações que precisam ser compartilhadas. Essa ferramenta pode ser dividida em três partes principais: Actions, Stores e Reducers. Cada uma dessas partes tem suas responsabilidades bem definidas.

---

## Configurações iniciais em Redux

O Redux pode ser instalado na aplicação usando o seguinte comando:

~~~unix
npm install react-redux
~~~

E para fazer a conexão entre essas 2 bibliotecas é necessário instalar outra biblioteca, essa biblioteca é a react-redux:

~~~unix
npm install --save redux react-redux.
~~~

Para instalar o Redux DevTools, que será necessário para criação da store, utilize o seguinte comando:

~~~unix
npm install --save redux-devtools-extension.
~~~

Caso não use o comando acima, no momento da criação da store será necessário atribuir um segundo parâmetro a createStore(), esse parâmetro é:

~~~unix
window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__(),
~~~

Também pode ser declarado dentro de uma constante e essa constante ser passada como parâmetro da createStore. Ex:

~~~JavaScript
const extension = window.devToolsExtension() || ((f) => f);
const store = createStore(rootReducer, extension);
~~~

Para instalar o redux-thunk, que é necessário para uso de códigos assíncronos:

~~~unix
npm install redux-thunk
~~~

---

## Stores em Redux

A store é onde o estado da sua aplicação fica registrado e protegido. As mudanças ou consultas feitas na store precisam estar definidas anteriormente numa action. Isso garante a integridade dos dados. Uma store é criada ao  passar um reducer, normalmente é um `rootReducer`. Ex:

~~~JavaScript
import { createStore } from 'redux';
import rootReducer from '../reducers';

// Criação da store
const store = createStore(rootReducer);

export default store;
~~~

---

## Actions em Redux

As actions, como o nome indica, são as possíveis ações que seu sistema pode executar na store. Elas atuam como uma regra de negócio para manter os dados da aplicação e as suas mudanças previsíveis e consistentes. É bem comum ouvirmos que as actions são intenções de mudança de estado. Uma action é um objeto JavaScript que possui uma chave `type`, a chave `type` deve ser uma string que dá a action um nome descritivo do que ela se propõe a fazer. É comum usar o estilo onde é passado primeiro o nome da feature ou categoria a qual essa action pertence e depois a ação específica. Ex: `domain/eventName`. Uma action pode ter outras chaves com informações adicionais sobre o que vai acontecer, por convenção, é utilizada uma chave chamada payload para isso. Um objeto action normalmente se parece com esse:

~~~JavaScript
const addTodoAction = {
  type: 'todos/todoAdded',
  payload: 'Buy milk',
}
~~~

---

## Actions Creators em Redux

Action creators são funções que criam e retornam uma action. Normalmente são usadas funções para criar o objeto action, para evitar que ela seja escrita múltiplas vezes. Um action creator é normalmente assim:

~~~JavaScript
const addTodoAction = text => {
  return {
    type: 'todos/todoAdded',
    payload: text,
  }
}
~~~

---

## Reducers em Redux

Os reducers são responsáveis por manipular a store seguindo as regras definidas pelas actions. Os reducers são importantes para evitar a manipulação direta da store e facilitam a manutenção do código. O reducer é uma função que recebe o estado atual e uma action, decide o que é necessário atualizar, e retorna o novo estado: `(state, action) => newState`. Você pode pensar no reducer como um `eventListener` que lida com os eventos baseado no que ele recebe do `type` da action (evento).

As funções `Reducers` recebem esse nome pelo fato de serem bem parecidas com a callback function passada para o método `Array.reduce()`.
Reducers devem sempre seguir algumas regras específicas:

- Eles só deve calcular o estado baseada nos argumentos `state` e `action`;

  ◦ Eles não podem modificar o estado existente diretamente, em vez disso, eles deve criar updates imutáveis, copiando o estado existente e fazendo mudanças nos valores copiados.

  ◦ Eles não devem fazer nenhuma logica assíncrona, calcular valores aleatórios ou causar outros “efeitos colaterais”.

---

A lógica dentro funções reducers normalmente seguem os mesmos passos:

- Verifica se o reducer atual cuida da ação passada no type;

  ◦ Se sim, faz uma cópia do estado, atualiza a cópia com o novo valor e retorna ele.

  ◦ Se não, retorna o valor existente sem mudanças.

---

A seguir, um exemplo de um reducer, mostrando os passos que cada reducer deveria seguir:

~~~JavaScript
const INITIAL_STATE = { state: '' };

const myReducer = (state = INITIAL_STATE, action) => {
  switch (action.type) {
  case '':
    return state;
  default:
    return state;
  }
};

export default myReducer;
~~~

Reducers podem usar qualquer tipo de lógica dentro deles para decidir qual estado será atualizado, podendo ser lógicas do tipo `if/else`, `switch`, loops, dentre outras.

É uma boa prática que seja criado um `rootReducer()`, esse `rootReducer` nada mais é do que como o próprio nome já diz um `reducer raiz`, o `rootReducer` é uma constante que recebe o retorno de uma função, outra diferença desse reducer para os outros é que ele tem o papel de juntar todos os reducers antes de enviá-los para a store, assim ele junta todos os reducers em um objeto, para ter certeza de que qualquer que sejam as atualizações feitas na store, sejam feitas da forma correta e total. O `rootReducer` recebe o retorno de uma função chamada `combineReducers()` e essa função retorna um objeto com todos os reducers, essa é uma função interna do próprio Redux, ou seja, ela deve ser importada da biblioteca `redux`. Ex:

~~~JavaScript
import { combineReducers } from 'redux';

export const rootReducer = combineReducers({ myReducer });
~~~

---

## Provider em Redux

Bem parecido com o BrowserRouter do React, que nos permite acessar as informações de rota dos componentes, no Redux existe o Provider, que possibilita o compartilhamento de estado que o Redux propõe. Assim como o BrowserRouter, o Provider também requer que todos os componentes que usem ele estejam abaixo dele na árvore de componentes, por isso fazemos com que englobe o componente App, se houver um BrowserRouter, não há diferença entre o BrowserRouter estar dentro do Provider ou o Provider dentro do BrowserRouter.

~~~JavaScript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
// o provider é o meio pelo qual disponibilizamos o store
// com os estados de toda a aplicação para todos os demais componentes
import { Provider } from 'react-redux';
import App from './App';
import store from './store';

ReactDOM.render(
  <Provider store={ store }>
    <App />
  </Provider>,
  document.getElementById('root'),
);
~~~

O Provider recebe como propriedade a store, que foi criada para a aplicação dentro do diretório store, no arquivo index.js.

***Dica:*** ao importar um recurso de dentro de um arquivo index.js, não é necessário escreve index.js na importação, é possível usar somente o nome do diretório, como exemplo observe a importação da store no código acima.

---

## Dispatchs em Redux

Outro método presente na store é o `dispatch()`, esse método é a única forma de atualizar o estado da store e passar um objeto action. Após a chamada do `dispatch()` a store vai rodar os reducers e salvar o novo estado. Ex:

~~~JavaScript
dispatch({ type: 'counter/increment' })
~~~

Você pode pensar no dispatch como um “gatilho de eventos” na aplicação. Algo aconteceu, e queremos que a store saiba disso. Reducers agem com eventListeners, e quando ele captam uma action que lhes interessa, eles atualizam o estado, como resposta ao evento.

---

## MapDispatchToProps em Redux

Como visto acima, a forma como fazemos para mandar algo para store é através da função dispatch, no JavaScript puro, é necessário somente usar algo como `store.dispatch(action)`, mas no React é necessário um pouco mais de cuidado e passos. Para realizar o dispatch no React, precisamos da função `mapDispatchToProps`, que tem acesso a função `dispatch` em toda a sua capacidade, e é através dessa função que será possível enviar a action para a alteração de estado da  aplicação.

~~~JavaScript
const mapDispatchToProps = (dispatch) => (
  { myFirstDispatch: (state) => dispatch(newAction(state)) }
);
~~~

O `mapDispatchToProps`, ao contrário das outras partes do Redux vistas até agora, fica no mesmo arquivo do componente que está sendo utilizado, ou seja, cada componente terá o seu próprio `mapDispatchToProps`, pois essa função trabalha baseada no estado de cada componente especificamente, e é esse estado que será utilizado dentro dessa função.

Analisando o `mapDispatchToProps`:

- O `mapDispatchToProps` é uma função que recebe como parâmetro o `dispatch` e retorna um objeto;
- As chaves desse objeto serão as propriedades usadas pelo componente, ou seja, ao invés de um componente receber as suas propriedades do componente pai, ele vai receber da própria store;
- Cada chave desse objeto recebe como valor uma callback que recebe como parâmetro o estado do componente;
- Cada callback retorna o `dispatch` passado como parâmetro para `mapDispatchToProps`, chamando dentro dos seus parênteses uma `action`;
- Essa action recebe o estado do componente como parâmetro, esse estado é o mesmo que foi passado para a callback como parâmetro.

---

A função `mapDispatchToProps` é a responsável por disparar, fazer o `dispatch` de,  uma ação para o reducer . Para termos acesso às funcionalidades do Redux, seja a de ler os dados ou manipulá-los, precisamos acessá-las como props de um componente. Por isso, como explícito no nome da função, o `mapDispatchToProps` mapeia os `dispatchs` para o props.

---

## mapStateToProps

Assim como a função `mapDispatchToProps` transforma os dados das actions em props, para que sejam usadas dentro da aplicação, a função `mapStateToProps` transforma os estados da store em props, para que a aplicação consiga usar esses dados. Da mesma forma que o `mapDispatchToProps`, o `mapStateToProps` fica dentro do mesmo arquivo que o componente no qual ele será usado.

~~~JavaScript
const mapStateToProps = (state) => (
  { myFirstState: state.myReducer.state }
);
~~~

Os 2 possuem uma diferença usual, `mapStateToProps` é usado somente quando se precisa fazer a leitura dos estados e/ou exibi-los em algum lugar, já o `mapDispatchToProps` é utilizado quando é preciso fazer alguma alteração nos estados.

Analisando o `mapStateToProps`:

- O `mapStateToProps` é uma função que recebe o estado da store como parâmetro e retorna um objeto;
- As chaves desse objeto serão as propriedades usadas pelo componente, ou seja, ao invés de um componente receber as suas propriedades do componente pai, ele vai receber da própria store;
- Cada chave desse objeto recebe como valor uma chamada a um reducer;
- Os reducers estão guardados dentro do estado da store, ou seja, é necessário acessar as propriedades da store;
- Dentro do reducer é necessário acessar o estado, visto que os reducers retornam objetos que guardam o estado para modificação na store;
- Após esse acesso a chave terá o valor salvo dentro do estado do reducer.

Retornando um objeto o `mapStateToProps`, assim como o `mapDispatchToProps`, pode receber mais de uma chave, ou seja, mais de um reducer pode ser passado para ele, vai depender da quantidade de reducers utilizados no componente.

---

## Connect em Redux

Ao implementar componentes é preciso conectá-los ao Redux, para isso é usado o método `connect`, é ele que fornece o acesso ao `store` do Redux, esse método possui a seguinte estrutura `connect()()`.
Entre os primeiros parênteses, devem estar presentes os métodos nativos do Redux. No caso de utilizar somente o `mapDispatchToProps`, o primeiro parâmetro desse parênteses deverá ser null, já no caso de utilizar somente o `mapStateToProps` o segundo parâmetro desse parênteses deverá ser null . Portanto, no caso de utilizar ambos `mapStateToProps` e `mapDispatchToProps` , essa é a sintaxe que o connect apresentará:

~~~JavaScript
export default connect(mapStateToProps, mapDispatchToProps)(Home);
~~~

No segundo parênteses vai o componente que deverá ser conectado.

O connect, assim como os métodos que ele liga ao componente, por boa prática, deve estar no mesmo arquivo que o componente ao qual ele está fazendo a ligação.

---

## Seletores em Redux

Seletores são funções que sabem como extrair dados específicos de um estado da store. Conforme uma aplicação cresce, isso pode ajudar a evitar a repetição de lógica em diferentes partes do código que precisam ler o mesmo dado. Ex:

~~~JavaScript
const selectCounterValue = state => state.value

const currentValue = selectCounterValue(store.getState())
console.log(currentValue)
// 2
~~~

---

## Thunk em Redux

Durante o desenvolvimento de aplicações e uso delas no dia a dia, nos deparamos como muitos códigos assíncronos, como requisições, e esses códigos trazem dados que precisam ser armazenados, e muitas das vezes compartilhados entre componentes, como estamos vendo o Redux serve para a fazer essa parte do compartilhamento de uma forma bem eficaz, entretanto, como já vimos, o Redux só trabalha com informações de fluxo síncrono e isso cria uma incompatibilidade com códigos assíncronos. Pensando em solucionar esse problema foram desenvolvidos alguns pacotes para Redux, um desses pacotes é o `react-thunk`, que provê uma interface simples que dá suporte a action creators que geram actions assíncronas.

Esse pacote é o pacote recomendado na documentação do próprio Redux. O comando para instalação do `redux-thunk` pode ser encontrado no tópico de configurações iniciais do Redux, nesta mesma sessão. Após a instalação do pacote é necessário importar a função `apllyMiddleare()` direto da biblioteca `redux`, fazer uso dela na criação da store e importa o `thunk` direto da biblioteca `redux-thunk`. Ex:

~~~JavaScript
import { createStore, apllyMiddleWare } from 'redux';
import thunk from 'redux-thunk';
import reducer from '/path/to/your/root/reducer';

...

const store =createStore(reducer, apllyMiddleWare(thunk));

...
~~~

O `thunk` nada mais é do que uma função que encapsula uma operação para que ela seja feita posteriormente. Em termos práticos, isso significa que está sendo defininda uma função que vai ser retornada por uma outra função com mais lógica adicionada a ela.

Com `redux-thunk` , é posspivel definir uma `action` creator que retorna uma função (que será invocada pelo `redux-thunk` ) em vez de retornar somente um objeto. Na função retornada é possível realizar uma operação assíncrona, como fazer chamadas de API e, uma vez finalizada a operação, é possível enviar uma `action` com os dados obtidos por ela. Note a conveniência que isso traz: toda essa lógica de lidar com operações assíncronas está encapsulada na sua respectiva `action` assíncrona, deixando transparente para quem for fazer uso dela, que para esse caso seriam os componentes React ! Sob a perspectiva do componente, ele estaria consumindo uma `action` como uma outra qualquer!

Para ser devidamente usada pelo `redux-thunk` a `action` creator precisa retornar uma função, que pode fazer uso de `dispatch` e `getState` da store como parâmetros. Segue um exemplo de uma `action creator` definida em conformidade com tais requisitos:

~~~JavaScript
export const REQUEST_MOVIES = 'REQUEST_MOVIES';
export const RECEIVE_MOVIES = 'RECEIVE_MOVIES';

// action creator que retorna um objeto, que você tem feito até então
const requestMovies = () => ({ type: REQUEST_MOVIES });

// outro action creator que retorna um objeto, que você tem feito até então
const receiveMovies = (movies) => ({ type: RECEIVE_MOVIES, movies });

// action creator que retorna uma função, possível por conta do pacote redux-thunk
export function fetchMovies() {
  return (dispatch) => { // thunk declarado
    dispatch(requestMovies());
    return fetch('alguma-api-qualquer.com')
      .then((response) => response.json())
      .then((movies) => dispatch(receiveMovies(movies)));
  };
}

// componente onde você usaria a action creator fetchMovies assíncrona como uma outra qualquer
...
class MyConectedAppToRedux extends Component {
...
componentDidMount() {
  const { dispatch, fetchMovies } = this.props;
  dispatch(fetchMovies()); // enviando a action fetchMovies
}
...
}
...
~~~

### Esqueleto padrão de um Redux

~~~JavaScript
// src/index.js

import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import store from './store';
import App from './App';
import './index.css';

// Implementação do Provider
ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
     <App />
    </Provider>
  </React.StrictMode>,
  document.getElementById('root'),
);
~~~

### Esqueleto padrão, sem separar em diretórios e arquivos específicos

~~~JavaScript
import React from 'react';
import { connect } from 'react-redux';
import { combineReducers, createStore } from 'redux';

// Criação da action creator
const NEW_ACTION = 'NEW_ACTION';

export const newAction = (state) => ({ type: NEW_ACTION, payload: state });

// Criação do reducer
const INITIAL_STATE = { state: [] };

export const myReducer = (state = INITIAL_STATE, action) => {
  switch (action.type) {
  case NEW_ACTION:
    return ({ ...state, state: action.payload });
  default:
    return state;
  }
};

// Criação do rootReducer
export const rootReducer = combineReducers({ myReducer });

// Criação da store
const extension = window.devToolsExtension() || ((f) => f);
export const store = createStore(rootReducer, extension);

// Criação do componente
class Home extends React.Component {
  constructor(props) {
    super(props);
    this.state = { anyState: '' };
  }

  render() {
    const { myFirstDispatch, myFirstState } = this.props;
    const { anyState } = this.state;
    return (
      <>
        <input
          type="text"
          onChange={(event) => this.setState({ anyState: event.target.value })}
        />
        <button
          onClick={() => myFirstDispatch(anyState)}
          type="button"
        >
        Executar qualquer tarefa
        </button>
        <div>
          Aqui
          {
            myFirstState.map((element) => (
              <p>{element}</p>
            ))
          }
      </div>
      </>
    );
  }
}

// Criação do mapStateToProps
const mapStateToProps = (state) => (
  { myFirstState: state.myReducer.state }
);

// Criação do mapDispatchToProps
const mapDispatchToProps = (dispatch) => (
  { myFirstDispatch: (state) => dispatch(newAction(state)) }
);

// Criacação do connect
export default connect(mapStateToProps, mapDispatchToProps)(Home);
~~~

---

## Checklist do react-redux

(Não sou o autor desse checklist, me foi fornecido pela Trybe)

### Antes de começar

- [ ] pensar como será o formato do seu estado global
- [ ] pensar quais actions serão necessárias na sua aplicação

### Instalação

- [ ] npm install;
- [ ] npx create-react-app my-app-redux;
- [ ] npm install --save redux react-redux;
- [ ] npm install --save redux-devtools-extension;
- [ ] npm eslint –init;

### Criar dentro do diretório src

- [ ] diretório actions;
- [ ] diretório reducers;
- [ ] diretório store.

### Criar dentro do diretório actions

- [ ] arquivo index.js.

### Criar dentro do diretório reducers

- [ ] arquivo index.js.

### Criar dentro do diretório store

- [ ] arquivo index.js.

### No arquivo App.js

- [ ] definir o Provider, `<Provider store={ store }>`, para fornecer os estados à todos os componentes encapsulados em `<App />`.

### No arquivo store/index.js

- [ ] importar o rootReducer e criar a store
- [ ] configurar o Redux DevTools

### Na pasta reducers

- [ ] criar os reducers necessários
- [ ] configurar os exports do arquivo index.js

### Na pasta actions

- [ ] criar os actionTypes, por exemplo: const ADD_TO_CART = 'ADD_TO_CART';
- [ ] criar os actions creators necessários

### Nos componentes

- [ ] criar a função mapStateToProps
- [ ] criar a função mapDispatchToProps
- [ ] fazer o connect

---

## Comandos REDUX

- `configureStore({ reducer: exempleReducer });` - Configura uma store, normalmente é atribuído a uma constante. Ex: const store = configureStore({ reducer: exampleReducer });.
- `.createStore()` - Cria uma store, dentro dos parênteses recebe um reducer, por boas práticas esse reducer recebe o nome de rootReducer. Ex:

~~~JavaScript
const store  = creatStore(rootReducer);
~~~

Como segundo parâmetro essa função pode receber uma configuração, caso a biblioteca Redux DevTools não esteja instalada, para ver esse segundo parâmetro vá até o tópico de “Configurações iniciais em Redux” e veja a parte sobre Redux DevTools.

- `.getState()` - Retorna os valores atuais dos estados salvos na store.
- `combineReducers()` - Esse método como o próprio nome diz, serve para combinar os reducers, sem ele, só seria possível usar um reducer por aplicação. Observação: mesmo que exista somente um reducer na aplicação, é uma boa prática que o combineReducers seja utilizado, pois caso a aplicação cresça e necessite de outros reducers, não será necessária a alteração de lógica.
