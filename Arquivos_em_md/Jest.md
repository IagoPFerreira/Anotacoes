# Jest

Jest é um framework de testes automatizados desenvolvido pelo facebook, onde vários testes podem ser feitos e rodados em diversos arquivos, simultaneamente.

Para adicionar o Jest ao projeto é sou usar o comando:

~~~bash
npm install –save-dev jest
~~~

Para escrever testes com jest é bem simples, só precisa usar a função `test`, que tem um alias chamado `it`, ou seja, ambas se referem a mesma função e qualquer uma delas pode ser usado. Essas funções são globais e ficam disponíveis nos arquivos que você está codando uma vez o que o jest é instalado.

A função test espera 3 argumentos, o primeiro argumento é o nome do teste, sendo este nome a identificação do teste e é também o texto que aparecerá quando os testes forem executados. O segundo argumento é uma função contendo as expectations, ou seja, contendo o que o teste receberá e o que espera que ele retorne. O terceiro argumento é opcional, que é o timeout, que indica quanto tempo o Jest deve esperar que o teste execute antes de abortá-lo.

~~~javascript
const sum = (a, b) => a + b;
test('sums two values', () => {
  expect(sum(2, 3)).toEqual(5);
});
~~~

Neste exemplo, tanto a implementação quanto os testes da função estão no mesmo arquivo. Na prática, porém, eles ficarão separados. Jest procura por arquivos com as extensões .js , .jsx , .ts e .tsx dentro de uma pasta com o nome `__tests__`, ou arquivos com o sufixo .test ou .spec . É comum que o arquivo de teste tenha o mesmo nome e fique na mesma pasta do arquivo que está sendo testado, acrescido da sufixo .test.js ou .spec.js.

~~~javascript
// sum.js
const sum = (a, b) => a + b;
module.exports = sum;

// sum.test.js
const sum = require('./sum');
test('sums two values', () => {
  expect(sum(2, 3)).toBe(5);
});
~~~

A linha `module.exports = sum` exporta a função sum no primeiro arquivo para que possa ser utilizada em outros módulos. No segundo arquivo, é utilizado o `require('./sum')` para importar a função sum .

---

## Matchers em Jest

Dentro de um test sempre existe um `expect`, que será o teste em sim e o `matcher`, que é o comparador entre o resultado do teste e o que é esperado, para ver garantir que o  que foi testado se encaixa no resultado esperado. Existem vários tipos de `matchers`, na seção comandos e propriedades deste arquivo, estarão descritos alguns.

---

## Falsy em Jest

Em JavaScript, existe um tipo de retorno, quando se espera valores boolenos, como em condições, esses valores recebem o nome de falsy. Existem 6 tipos de valores falsy em JavaScript, são eles: `false, 0, ‘’, null, undefined e NaN`. O Jest possui formas de testar cada um desses `falsy`, dependendo da situação é necessário testar qual deles é ou testar somente se o retorno é um `falsy`.

---

## Describe em Jest

A função `describe()` cria uma bloco para agrupar vários testes. Isso é útil para melhorar a organização dos teste, podendo utilizar o describe para separar testes de funções diferentes, dentro de um mesmo arquivo, ou agrupar testes relacionados dentro de uma função complexa, que requer muitos testes. É possível aninhar blocos describe arbitrariamente. Dentro de cada bloco, qualquer declaração de variáveis ou funções é local a este bloco.

---

## Erros em Jest

Testes podem retornar erros, devido a vários motivos, mas existem formas de capturar esses erros e mostrar o erro, uma dessas formas é usando o `.toThrow`, que é um matcher justamente para quando um erro é lançado.

~~~javascript
const multiplyByTwo = (number) => {
  if (!number) {
    throw new Error('number é indefinido');
  }
  return number * 2;
};
multiplyByTwo(4);

test('testa se multiplyByTwo retorna o resultado da multiplicação', () => {
  expect(multiplyByTwo(4)).toBe(8);
});
test('testa se é lançado um erro quando number é indefinido', () => {
  expect(() => {
    multiplyByTwo();
  }).toThrow();
});
test('testa se a mensagem de erro é "number é indefinido"', () => {
  expect(() => {
    multiplyByTwo();
  }).toThrowError(new Error('number é indefinido'));
});
~~~

Para testar se um erro é lançado, passamos para o expect uma função. Chamamos multiplyByTwo dentro da arrow function . Chamar a função diretamente dentro de expect fará com que o erro não seja capturado. Assim, a asserção falhará, porque o erro acontecerá antes mesmo de expect ser executado e ter a chance de capturar o erro. Para testar a mensagem de erro, como fizemos no terceiro teste do exemplo acima, usamos o matcher toThrowError e passamos dentro do parênteses a mensagem que será mostrada em caso de erro: `new Error("number é indefinido")` . Observe que nos dois casos a função que queremos testar é chamada indiretamente por uma arrow function . Seguir essa sintaxe é importante para que o seu teste funcione corretamente.

---

## Teste assíncronos em Jest

É comum encontrar em JavaScript linhas de código que possuem comportamento assíncrono. Alguns comportamentos assíncronos já familiares são as `callbacks`, as `promisses` e o `async/await`. Para que seja possível testar estes casos, o Jest fornece algumas soluções com objetivo de que os testes saibam o momento em que a função a ser testada foi concluída, e a informação necessária foi retornada. Isto evita que falsos positivos aconteçam e garante segurança para a aplicação.

---

## Simulações em Jest

O Jest por ser uma ferramenta de testes, ele nos proporciona várias formas de fazer testes, uma dessas formas é simular testes, ou seja, pegar um código e simular um teste desenvolvido por nós, sem que o código em si rode, só para sabermos quais seriam as respostas desse código que queremos testar. Além de simular a funcionalidade do código, podemos criar uma funcionalidade nova para esse código, a nossa vontade, sem que isso interfira no código fonte. Para isso, utilizamos o mock, que nada mais é do que a forma de criar simulações dentro do Jest. Existem algumas formas para que o código seja ‘mockado’, uma delas é utilizando a função `fn()`, ela mocka somente um elemento específico, seja ele uma função, um objeto ou um array. Existem também o `mock()`, que diferente da `fn()`, mocka o arquivo inteiro, ou seja, todo o conteúdo do arquivo mockado pelo `mock()`, pode ser utilizado na simulação, ao invés de somente 1 elemento. E existe também o `spyOn`, que possui a capacidade de fazer o mock, sem alterar a funcionalidade original do elemento, de forma que você consiga preservar o comportamento inicial do elemento e simular ele.

---

## Comandos e propriedades em Jest

* `.toBe()` – Testa a igualdade estrita (===) entre o valor passado para o expect e seu argumento.  Ex: `expect(5).toBe("5")`. Neste exemplo, o teste falharia porque a string "5" não é igual ao número 5.
* `.toEqual()` – Testa a igualdade de objetos e arrays, acessando cada elemento do objeto ou array, fazendo uma comparação específica.
* `.toBeFalsy()` – Testa se o valor retornado do teste se encaixa como um falsy.
* `.toBeNull()` – Testa se o valor retornado é igual a null.
* `.toBeUndefined()` – Testa se o valor retornado é igual a undefined.
* `.toBeNan()` – Testa se o valor retornado é igual a NaN.
* `.toBeTruthy()` – Testa se o valor retornado é igual a true, independente de qual é o valor.
* `.toBeGreaterThan()` – Testa se o valor retornado é maior que o valor esperado. Ex: `expect(4).toBeGreaterThan(3);`.
* `.toBeGreaterThanOrEqual()` – Testa se o valor retornado é maior ou igual ao valor esperado.
* `.toBeLessThan()` – Testa se o valor retornado é menor que o valor esperado.
* `.toBeLessThanOrEqual()` – Testa se o valor retornado é menor ou igual ao valor esperado.
* `.toBeCloseTo()` – Testa se o valor retornado está próximo ao valor esperado. Bem útil em casos de arredondamento.
* `.not.toMatch()` – Testa se a string retornada não é igual a string esperada.
* `.toMatch()` – Testa se a string retornada é igual a string esperada.
* `.toThrow()` – Testa se uma função lança um erro quando é executada. Para testar se uma função está retornando um erro, é importante estar atento à sintaxe do .toThrow.

[Matchers mais comuns](https://jestjs.io/pt-BR/docs/using-matchers#números)

[Lista de todos os matchers](https://jestjs.io/docs/expect)
