# React Testing Library (RTL)

A RTL é uma biblioteca de testes automatizados direcionado ao React, existem muitas bibliotecas de testes para React, uma delas é a enzyme, desenvolvida pela Airbnb, entretanto a biblioteca que em maior recomendação pela documento do próprio React é a react-test-library (RTL).

Existem muitas bibliotecas de teste, tanto para JavaScript puro, como para React, Angular, Vue e diversos outras linguagens e frameworks, uma das mais utilizadas para JavaScript é a biblioteca Jest, que pode ser usada em conjunto com a RTL, na realidade é a biblioteca que é recomendada para testes pela própria documentação da RTL. Calma aí, uma biblioteca de testes recomenda o uso de outra biblioteca, como assim? Sabemos que React é um framework que usa JavaScript como base, mas possui algumas mudanças, como a utilização do JSX e a construção de componentes, dessa forma, os testes da biblioteca Jest, que foi feita para testes em JavaScript puro, não conseguiria fazer testes no React, por isso usamos uma biblioteca de testes especifica para o React, entretanto, o React ainda usa funcionalidades básicas do JavaScript, o que nos permite que utilizemos o Jest para verificar essas funcionalidades, dessa forma, do mesmo jeito que fazemos a integração entre JS e React, podemos fazer uma integração entre Jest e RTL. Uma outra diferença entre o Jest e a RTL é que o Jest testa funções, já a RTL testa comportamento, como o aparecimento ou não de um componente na tela, o comportamento de um botão, a mudança que acontece dentro de um campo de texto.

A RTL se tornou tão aceita pela comunidade de React que agora ela já vem instalada junto com os projetos, para criar o projeto só é necessário usar o comando

~~~unix
npx create-react-app nome-do-projeto
~~~

Quando criamos um projeto React novo, o arquivo App.test.js já vem com um teste implementado, teste esse que  verifica se algum elemento dentro do componente App possui o texto “learn react”.

~~~JavaScript
import React from 'react';
import { render } from '@testing-library/react';
import App from './App';

test('renders learn react link', () => {
  const { getByText } = render(<App />);
  const linkElement = getByText(/learn react/i);
  expect(linkElement).toBeInTheDocument();
});
~~~

Caso nenhuma alteração no componente App tenha sido feita, o teste continuará passando e só irá quebrar a partir do momento em que a frase “learn react” não esteja mais sendo renderizada.

## Testes em RTL

Para criar um teste na RTL, existe um passo a passo que se seguido deixa a compreensão do teste mais fácil e essa lógica ajuda na construção do teste, esse passo a passo é:

1. Acessar os elementos da tela
2. Interagir com eles (se houver necessidade)
3. Fazer o teste

É uma lógica bem natural de se pensar, visto que antes de fazer os testes é necessário acessar o elemento onde você quer fazer o teste e mudar o que for preciso depois de acessá-lo, mas antes de testar, se o seu teste precisar dessa modificação para realizar o teste. Para cada uma das 3 etapas existem muitas variantes do que usar, entretanto, veremos algumas delas.

O teste de um componente em RTL significa renderizá-lo na tela ou neste caso uma simulação de uma renderização, visto que este teste não via rodar no navegador em si, mas sim num navegador simulado pela RTL, e a partir dessa simulação testar o comportamento do componente. Como renderizar é uma parte essencial para o teste, é normal que exista uma função interna da RTL para isso, que é coincidentemente tem o mesmo nome da função no React que faz a renderização dos componentes, essa função é a `render()`, entretanto a `render()` da RTL vem de uma biblioteca diferente da do React, e esse render precisa ser importado da própria RTL, esse importe é feito da seguinte forma:

~~~JavaScript
import { render } from '@testing-library/react';
~~~

Dessa forma conseguimos acessar o render necessário para o teste, uma das grandes diferenças entre o render do React e o render da RTL é que o render da RTL retorna um objeto com muitas chaves e cada uma dessas chaves é uma callback que faz um teste diferente. Pera, ficou muito complicado ou muito abstrato? Vamos ver de outra forma:

~~~JavaScript
const render = {
  getByText: () => {},
  getByRole: () => {},
  getByLabelText: () => {},
  getByTitle: () => {},
  getByTestId: () => {},
...
}
~~~

Basicamente é como se o render fosse o objeto acima, e cada uma das chaves fosse o acesso para uma callback, callback essa que irá realizar um teste, teste esse descrito no nome da chave, por mais que você não saiba como é a construção da callback e qual a lógica por trás dela, o nome dela já deixa bem claro qual será o retorno dela, relembrando constantemente a importância dos nomes semânticos para funções e componentes.

Sabendo que o render da RTL é um objeto de funções, onde cada chave é uma função e que a RTL usa o JS como base, podemos utilizar de um recurso do JS para facilitar o acesso a essas funções do render, esse recurso é as desestruturação ou o destructuring (caso você não saiba o que é destructuring, vá até a sessão de JavaScript no tópico Objetos em JS), dessa forma, podemos escrever o render assim:

~~~JavaScript
const { getByText } = render(<App />);
~~~

Forma essa que é empregada no exemplo do teste do App que já vem na criação de uma aplicação React.

## Querys em RTL

Querys são basicamente seletores que vão até o documento e procuram um ou mais determinados elementos, bons exemplos disso são o querySelector e o querySelectorAll utilizados no JS quando queremos acessar um elemento HTLM para utilizarmos na nossa lógica JS, o querySelector retorna somente 1 elemento, que é elemento que bate com o id ou classe passado para ele, enquanto o querySelectorAll retorna um array com todos os elementos que baterem com a classe ou name passados para ele. Essa lógica também se aplica aos querys da RTL, alguns retornarão somente 1 elemento outros retornarão uma array de elementos, essas querys são:

---
selector | No Match | 1 Match | 1+ Match | Await? |
:--------: | :--------: | :-------: | :--------: | :------: |
getBy | throw erro | 0 | throw erro | 0 |
findBy | throw erro | 0 | throw erro | 0 |
queryBy | 0 | 0 | throw erro | 0 |
getAllBy | throw erro | 0 | 0 | 0 |
findAllBy | throw erro | 0 | 0 | 0 |
queryAllBy | 0 | 0 | 0 | 0 |

---
As querys por si só não fazem busca dentro do RTL, elas precisam de um complemento para saber o que buscar, para saber o que comparar, para isso existem os types, todos os types podem ser usados com todas as querys, a seleção de cada um vai depender do objetivo e do que você deseja testar, os types são:

---
Types | Descrição | Exemplo
:--------: | :--------: | :-------: |
Role | Seleciona a tag pela role (cargo) | `<div role=’dialog’>...</div>` |
LabelText | Seleciona a tag pela label | `<label for=“element” />` |
PlaceholdertText | Seleciona a tag pelo placehlder  | `<input placeholder=“username” />` |
Text | Seleciona a tag pelo texto dentro da tag  | `<a href='/about'>About</a>` |
DisplayValue | Seleciona a tag pelo texto da prop value | `<input value=”display value” />` |
AltText | Seleciona a tag pelo texto da prop alt  | `<img alt=“movie poster” />` |
Title | Seleciona a tag pelo valor da prop title | `<span title='Delete' /> or <title />` |
TestID | Seleciona a tag pelo valor da prop data-testid | `<input data-testid='username-input' />` |

---

## Matchers em RTL

Como já sabemos o React é baseado em JS e que o JS possui a biblioteca Jest para testes, dessa forma, podemos fazer uma associação entre a RTL e o Jest para realizarmos nossos testes. Lá em Jest nós vimos sobre os matchers e como os utilizamos para montar nossos testes, na RTL usaremos o mesmo princípio. Lista de matchers: <https://jestjs.io/docs/expect>

## Eventos em RTL

Em componentes React é normal que existam elementos que possuam algum tipo de eventro atrelado a eles, como `onChange`, `onClick`, `onDrag`, `onMouseOver`, dentre outros. Muitas das vezes são esses eventos que acabam disparando outras partes do código, ou disparam uma mudança de comportamento, ou uma atualização, independente do que façam, normalmente disparam algum tipo de mudança, sendo assim, essa mudança e esse evento deveriam ser testados para se ter certeza que o esperado está acontecendo, da forma como vimos testes até o momento não é possível fazer isso, pois estávamos testando elementos estáticos já presentes na tela ou documento, podemos utilizar os recursos que vimos até agora para testar se o elemento que tem o evento atrelado está presente na tela ou documento, mas não podemos testar o evento em si ainda. Para testar eventos nós podemos usar 2 formas.

A primeira forma é usando o `fireEvent`, que é um recurso da  RTL e pode ser importado junto com o render na mesma chave de destructuring, o `fireEvent` possui várias funções internas, funções essas que simulam os eventos que acontecem quando interagimos com um elemento ou componente. A construção de um `fireEvent` é simples:

~~~JavaScript
const EMAIL_USER = 'email@email.com';
const btnSend = getByTestId('id-send');
const inputEmail = getByLabelText('Email');
fireEvent.change(inputEmail, { target: { value: EMAIL_USER } });
fireEvent.click(btnSend);
~~~

Alguns eventos precisam que sejam passados 2 parâmetros, o primeiro sendo o elemento que vai receber o evento e o que será passado para esse elemento, no caso do `change`, a chave value do target desse elemento vai receber o `EMAIL_USER`, para que futuramente seja testado qual é o valor que esse elemento possui, já no caso do `click`, como o evento é somente clicar no botão, o elemento não vai receber nenhum valor ou  ação adicional.

Link para a documentação do fireEvent: <https://testing-library.com/docs/dom-testing-library/api-events/>

A segunda forma de se testar um evento é utilizando o userEvent, que é bem semelhante ao `fireEvent` na questão de funcionalidade, além de ser bem parecido em termos de construção com o `fireEvent`, tendo pequenas mudanças, como a importação que é feita da biblioteca `@testing-library/user-event` não precisar de destructuring no segundo parâmetro e o quando se quer testar o evento `onChange` em campos de `input`, ao invés de usar a função `change`, se usa a função `type`. Exemplo:

~~~JavaScript
import userEvent from '@testing-library/user-event';
const EMAIL_USER = 'email@email.com';
const btnSend = getByTestId('id-send');
const inputEmail = getByLabelText('Email');
userEvent.change(inputEmail, EMAIL_USER);
userEvent.click(btnSend);
~~~

## Testando componentes em RTL

É possível testar somente 1 componente específico em RTL, ao invés de fazer testes em cadeias, ou seja testar o pai, para que ele teste o filho para que teste o neto e assim vai, para isso podemos testar direto o componente desejado, e a forma de fazer isso é renderizar o componente alvo dentro do teste, ou seja, ao invés de passar o componente App dentro do render como viemos fazendo nos exemplos, podemos passar direto o componente, como por exemplo:

~~~JavaScript
const { getByTestId, getByLabelText } = render(<Header />);
~~~

A partir disso, os testes podem ser montados com os mesmos recursos vistos anteriormente, somente adaptando-os ao conteúdo de cada componente.

## Mock em RTL

Assim como testamos eventos e conteúdos dos componente e/ou elementos, podemos testar também as funções que acontecem dentro de um componente, e de forma a evitar chamadas de funções encadeadas ou processos encadeados que não servem para o nosso teste, podemos fazer simulações dessas funções, ou seja, podemos mockar essas funções. Parando para pensar, mock foi algo visto em Jest e toda a explicação de como criar e manipular mocks está na seção de Jest. Sabendo que Jest e RTL se completam, iremos utilizar a capacidade do Jest de criar mocks para testar as funções do nosso componente.

Entretanto, existe uma função na Jest que possível usar para fazer o mock de um fetch, para que não tenhamos que criar a função do 0, para isso utilizamos o método global.fetch, contudo, é necessário fazer a parte de converter para JSON e a resolução da Promise. Podemos fazer isso de diversas formas, seguindo as formas descritas na seção de JavaScript, no tópico de Promises, ou podemos utilizar uma função do Jest chamada mockResolvedValue(response) e ela pode ser usada da seguinte forma:

~~~JavaScript
import React from "react";
import { render } from "@testing-library/react";
import App from "./App";

afterEach(() => jest.clearAllMocks());
it("fetch joke", async () => {
  const joke = {
    id: "7h3oGtrOfxc",
    joke: "Whiteboards ... are remarkable.",
    status: 200,
  };

  jest.spyOn(global, "fetch");
  global.fetch.mockResolvedValue({
    json: jest.fn().mockResolvedValue(joke),
  });
  const { findByText } = render(<App />);
  await findByText("Whiteboards ... are remarkable.");
  expect(global.fetch).toBeCalledTimes(1);
  expect(global.fetch).toBeCalledWith("https://icanhazdadjoke.com/", {
    headers: { Accept: "application/json" },
  });
});
~~~

Vamos analisar o que está acontecendo:

1. A constante joke possui um objeto similar ao retorno da API
2. O jest.spyon espiona as chamadas a função fetch do objeto global, é por meio deste objeto que é possível acessas e usar qualquer função do sistema
3. Quando o fetch for chamado, ao invés de fazer uma requisição a API será chamado o mock. As funções .mockResolvedValue ficam no lugar dos .then, simulando o retorno do fetch, primeiro tem um retorno de um objeto com a função json e dentro dela tem outro mock que retorna a piada que irá ser testa.
4. Como estamos simulando um fetch que retorna uma Promise, é necessário incrementar funcionalidades que atuem como se esperassem uma Promise, ou seja, a resolução precisa ser assíncrona, para isso usamos o async e o await
5. As funções toBeCalledTimes e toBeCalledWith servem para garantir respectivamente, o número de chamadas ao nosso fetch e que ele foi chamado com os argumentos corretos
6. A linha afterEach(() => jest.clearAllMocks()); faz com que, após cada teste, o mock seja limpo, ou seja, no caso acima, garante que após o teste o fetch não seja mais um mock, isso é bem útil para que não tenha interferência entre um teste e outro.
Existem várias formas de realizar a mockagem de um elemento, para esse exemplo tem uma sugestão de mudança quanto a mockagem:

~~~JavaScript
...
global.fetch = jest.fn(()=> Promise.resolve({ json: ()=> Promise.resolve(joke)}));
...
~~~

Todo o código continua igual, só mudando a parte onde é feita o mock

## Testando rotas em RTL

Quando falamos em rotas em React já logo pensamos em BrowserRouter e Route, e quando falamos em testar essa rota já logo começamos a associar os testes com o BrowserRouter, entretanto na realidade isso não é algo possível pelo fato de que todos os testes precisam ser independentes uns dos outros, de forma que o que acontece em um teste não interfira em outros testes, sabendo disso, o BrowserRouter impossibilitaria o seu próprio uso durante os testes, visto que mesmo durante uma simulação de rotas, o BrowserRouter salvaria todas as rotas feitas em um teste e não apagaria depois que ele acabasse, ele somente começaria o próximo teste com o histórico de rotas do teste anterior salvo, possivelmente fazendo com que os teste quebrem. Logo, podemos ver que com o BrowserRouter seria quase impossível um teste não interferir no outro, mas para contornar esse problema, a própria RTL nos sugere utilizar um Router diferente, um Router personalizado, criado por nós mesmos, ou um Router criado pela própria RTL que serve para esse papel específico.

Esse novo Router tem como função criar a cada teste, ou a cada renderização, um novo caminho de rotas no histórico, de forma que quando o teste acabe, mesmo que essa informação fique salva, quando a próxima renderização acontecer, um novo histórico será gerado do 0, o que evita que os acontecimentos de um teste interferir em outro.

Antes de começar a desenvolver os testes, é preciso passar por alguns pontos para facilitar a compreensão:

- A biblioteca history é uma ferramenta que nos concede o acesso a sessão de histórico do navegador e também a localização atual (URL), aqui tem um link para a documentação do history: <https://reactrouter.com/web/api/history>

Nesta documentação, tem uma explicação sobre todos os métodos da biblioteca, mas para nossos teste aqui, os métodos mais utilizados serão o push, que nos permite mudar de rota dentro do ambiente de testes, e o location.pathnam, que nos retorna a URL exata em que estamos.
Dentro da biblioteca, também é possível importar a createMemoryHistory, que é feira para ser utilizada em ambientes que não possuem DOM, por exemplo, em testes automatizados. O trabalho dessa função é criar um novo histórico de navegação, para ser utilizado durante o teste.

- A função renderWithRouter é uma função customizada  para fazer testes com rotas, uma vez que a função render normal da RTL não dá suporte ao Router. Ela pode ser muito útil e usa o createMemoryHistory para embutir no seu componente renderizado a lógica de histórico de navegação, para uso nos testes.
