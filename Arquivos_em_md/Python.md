# PYTHON

Python é uma linguagem muito utilizada na ciência de dados e desenvolvimento de aplicações. Assim como toda linguagem, Python também possui tipos primitivos das variáveis, tipos primitivos nada mais são do que como são representados os valores de uma variável. Os tipos primitivos mais comuns são Number (Int, Float, Infinity e NaN), String, Boolean, Null, Undefined, Object (Array), Function.

## Strings em Python

No Python é possível marcar uma string de 2 formas diferentes, usando aspas simples ou duplas (``, “”), para strings simples e para interpolar, ou seja, exibir uma variável do meio da string, sem precisar ficar abrindo e fechando a string, onde for a variável é só abrir um bloco usando chaves `{}` e depois da string é só adicionar um método chamado `.format()` escrever o nome da variável dentro dos parênteses do format. Ex: `.format(variavel)`, se for mais de uma variável, é só separa-las por vírgulas, na ordem em que elas aparecem na string. Ex: `.format(var1, var2, var3)`.

## Operadores em Python

Existem muitos tipos de operadores em Python, operadores são sinais que podem desencadear uma ação, ou interferir nela, alguns tipos de operadores são:

---

    • Aritméticos 
      ▪ + Adição
      ▪ - Subtração
      ▪ * Multiplicação
      ▪ / Divisão real
      ▪ % Resto da divisão inteira (Ex: 5%2 = 1)
      ▪ // Divisão inteira (Ex: 5//2 = 2)
      ▪ ** Potência

      ◦ Ordem de precedência
        ▪ ()
        ▪ **
        ▪ * / %
        ▪ + - 

      ◦ Raiz
        ▪ n**(1/2), só mudar o divisor da fração para mudar a potência da raiz

---

    • Atribuição
      ▪ Atribuição simples, quando um valor ou dado é atribuído a variável. Ex: a = 1;
      ▪ Auto atribuições, quando um valor ou dado é atribuído a uma variável e ela mesma é utilizada para mudar essa atribuição. Ex: n = 3; n = n + 3

---

    • Relacionais
      ▪ > Maior que
      ▪ < Menor que
      ▪ >= Maior igual
      ▪ <= Menor igual
      ▪ == Igual á
      ▪ != Diferente de
      ▪ === Identidade, confere se os valores são iguais em grandeza e tipo (Number, string, boolean,...).
      ▪ !== Diferente em identidade, confere se os valores são diferentes em grandeza e/ou tipo (Number, string, boolean,...).
      ▪ As respostas das expressões com operadores relacionais serão sempre em tipo booleano, ou seja, true ou false.

---

    • Lógicos
      ▪ ! Negação
      ▪ and Conjunção ou “E” lógico
      ▪ or Disjunção ou “OU” lógico

## Variáveis em Python

Em Python as variáveis são declaradas somente declarando o seu nome e atribuindo a ela um valor, de qualquer tipo primitivo, diferente de outras linguagens, Python não requer que uma palavra reservada seja atribuída a variável para que ela se torne uma variável. Ex: `a = 1`. Outro detalhe importante é que diferente de outras linguagens, Python utiliza o método Snake_Case para nomear as variáveis, normalmente as linguagens usam o padrão CamelCase, mas esse não é o padrão do Python. O padrão Python é o seguinte: `total_de_tentativas = 3`. Caso o nome da variável tenha mais de uma palavra, as palavras devem ser separadas por um underline `_`.

## Condições em Python

Condições são ocasiões que ocorrem em determinadas ocasiões que preencham pré-requisitos. Existem alguns tipo de condição, os mais usados são `if` e `else`. Condições simples são onde só existem `if`, condições composta são onde existem `if` e `else`, e condições aninhadas são onde existem condições dentro de outras condições. As condições devem ser feitas da seguinte forma: `if (teste): bloco de código`, `else: bloco de código`. Se o teste do `if` for verdadeiro o seu bloco será executado, senão será o do `else`. Existe também o `elif`, que é uma mistura de else com if, a forma de expressão dele é a mesma, assim como o if ele também recebe um teste, `elif (teste): bloco de código`.

## Laços em Python

Bem parecidos com as condições, mas as repetições além de testarem condições e executarem blocos específicos, elas também repetem esses testes enquanto a condição de repetição for verdadeira. 2 tipos são mais utilizados `while` e `for`. Eles devem ser montados da seguinte maneira: `while (teste lógico): bloco de código`, `for variável a ser testada in range (inicio, fim, passo): bloco de código`. No `for` o laço acaba sempre antes do final escolhido, na realidade o final não é exibido, caso queira a exibição do final é só adicionar `+1` após o fim. Além disso, o laço `for` já incrementa o contador sozinho, já o `while` não, no while é necessário criar um contador e uma atribuição a ele no final do laço. Caso seja necessário sair do laço antes dele ser concluído, caso uma condição específica seja cumprida, é só usar o comando `break`.

## Funções em Python

São linhas de códigos específicas que só serão executadas quando um evento ocorrer ou forem chamadas dentro do código, e essas linhas estarão dentro de um bloco. Os blocos são delimitados pela endentação, tudo que estiver dentro depois dos dois pontos e endentado para dentro da função, pertencerá a esse bloco.

Em Python uma função é definida usando a palavra chave `def` acompanhada do nome da função seguida de parênteses e dois pontos. Ex: `def jogar():`. Para executar uma função é só colocar o nome dela seguido de parênteses.

As funções também podem receber uma coisa chamada parâmetros, parâmetros são orientações do que o a função irá fazer com o dado que ela receber, esse parâmetros são repetidos dentro do bloco mostrando onde cada dado vai. Quando um dado é passado para a função em sua chamada, esse dado recebe o nome de argumento, o parâmetro pega o valor desse argumento e passa a valer o que foi passado. Ex:

~~~python
def soma (a, b):
  return a + b

s = soma (3, 5)
~~~

Neste exemplo `a` e `b` foram passados como parâmetros na construção da função e dentro do bloco de código foram somados um com o outro. No momento em que a função `soma` foi chamada lhe foi atribuídos 2 argumentos, `3` e `5`, argumentos esses que vão substituir `a` e `b`, respectivamente, e o código será executado com esses valores.

## Coleções em Python

Coleções são onde valores de qualquer tipo são guardados em conjunto, pode ser uma sequência ordenada ou não. Uma sequência é nada mais do que um conjunto de valores ordenados. Essa ordem é definida pelo índice. Por isso podemos acessar listas, tuplas ou strings através dos `[]` (colchetes). Listas, Tuplas, Strings e Ranges são tipos de sequências, dentre elas somente as listas são mutáveis.

`Listas` são feitas a partir da declaração de uma variável e utilização de `[]` após o =. Ex: `lista = [5, 6, 'Olá']`.

`Tuplas` são feitas a partir da declaração de uma variável e utilização de `()` após o =. Ex: `tupla = (5, 6, 'Olá')`. Ambas aceitam tipos diferentes de valores e podem ser acessadas pelo index, mas diferentes de listas, tuplas são imutáveis.

~~~python
lanche = ('Hambúrguer', 'Suco', 'Pizza', 'Pudim')

for comida in lanche:
    print(f'Eu vou comer {comida}')

for comida in range(0, len(lanche)):
    print(f'Eu vou comer {lanche[comida]}')

for pos, comida in enumerate(lanche):
    print(f'Eu vou comer {comida} na posição {pos}')

print('Comi pra caramba!')
~~~

Dentro de listas é possível criar listas aninhadas, da mesma forma como se é possível criar condições aninhadas, mas é necessário ter o cuidado de tirar uma cópia da lista e não criar a ligação de uma lista com a outra. Quando 2 listas estão ligadas e uma é alterada a outra também é, mas se for somente uma cópia, é possível alterar a cópia sem interferir na original, para isso é preciso usar os símbolos `[:]`, dessa forma uma cópia de uma lista pode ser adicionada em outra sem problemas.

Além de listas e tuplas existem um outro tipo de variável composta, chamada `Dicionário` são feitos a partir da declaração de uma variável e utilização de `{}` após o `=`. Ex: `dicionario = {'nome': 'Iago', 'idade': 24}`. Para adicionar um novo valor dentro de um dicionário, é só declarar a chave com o valor que ela vai receber. Ex:  `dicionario['sexo'] = 'M'`. Dessa forma foi automaticamente adicionado ao dicionário o valor `M` para a chave sexo. Para remover um elemento é só usar a propriedade del junto com o nome do item e a chave que específica. Ex: `del dicionario['idade']`.

O dicionário é dividido em 3 partes, `Item`, `Chave` e `Valor`. Neste exemplo o `Item` é o dicionario, as `Chaves` são `nome`, `idade` e `sexo`, e os `Valores` são `Iago`, `24` e `M`.

Existem também as sequências não ordenadas dentro delas está um grupo chamado set, este grupo, ao contrário das tuplas e das listas, não permite itens repetidos dentro da sua sequência. Entretanto, por não ser uma sequência ordenada, o set não possui acesso pelo index, caso tente ele retorna um erro. Um set é feito a partir da declaração de uma variável e utilização de `{}` após o = Ex: `set = {1, 9, 'Olá'}`. Set também aceita tipos diferentes de valores.

## Módulos em Python

Módulos são bibliotecas onde existem códigos já prontos feitos por outros programadores, ou funções que não vem pré-instaladas no Python, mas que importando elas, ficam acessíveis para utilizarmos em nossos códigos.

Existem duas formas de se importar um módulo em Python, a primeira é importando a biblioteca inteira através do comando `import` seguido do nome da biblioteca. Ex: `import math`. Ou importando somente o método desejado para o código, usando o `from...import...`, dessa forma colocamos primeiro o nome da biblioteca onde o método está guardado e depois o nome do método em si. Ex: `from math import hypot`. Dessa forma somente o método `hypot` foi importado de `math`, mas caso seja necessário importar outros métodos, é só separá-los por vírgula, desde que seja da mesma biblioteca, se forem de bibliotecas diferentes é necessário imports diferentes Ex:

~~~python
from math import cos, tan, sin
from math import floor
from random import choice
~~~

Caso a biblioteca inteira seja importada, na hora de declarar o método utilizado a biblioteca precisa ser referenciada. Ex: `hipotenusa = math.hypot(oposto, adjacente)`. Entretanto, caso somente o métodos sejam importados, não é necessário referenciar a biblioteca.  Ex: `hipotenusa = hypot(oposto, adjacente)`.

## Comandos em Python

* `variavel = 1` – Cria uma variável, não necessariamente precisa estar escrito variável, ela pode receber qualquer nome.
* `print()` – Escreve no console aquilo que estiver dentre parênteses, Strings precisam de aspas simples ou duplas para serem tratadas como strings.
* `input()` – Cria uma seção no console para a entrada de dados, e irá transformar aquele dado primeiramente em uma string.
* `int()` – Garante que o dado que seja passado dentro dos parênteses se torne em um número inteiro.
* `float()` - Garante que o dado que seja passado dentro dos parênteses se torne em um número real.
* `str()` - Garante que o dado que seja passado dentro dos parênteses se torne em uma string.
* `if():` – Cria uma condição, o teste lógico deve ser passado dentro dos parênteses, o que vier depois dos dois pontos será o bloco de código.
* `else:` – Cria uma condição de execução caso o if não seja atendido, o que vier depois dos dois pontos será o bloco de código, não precisa de teste lógico.
* `elif():` – É uma mistura entre o else e o if, precisa de um teste lógico e o que vier depois dos dois pontos será o bloco de código.
* `for...in range ():` – Cria um laço de repetição de código, dentro dos parênteses são definidos o início, o fim e o passo (1 em 1; 2 em 2; 3 em 3; assim vai, basta digitar o número do passo desejado) do laço, o que vier depois dos dois pontos será o bloco de código.
* `while ():` – Cria um laço de repetição do código, dentro dos parênteses fica o teste lógico que deve ser passado, o que vier depois dos dois pontos será o bloco de código.
* `break` – Caso queira sair do laço antes dele chegar até o final da sua execução normal, por conta de alguma condição específica que foi atendida, é só adicionar um break após essa condição.
* `continue` – Caso uma condição que não faz parte do seu objetivo seja atendida e caso você queira continuar o laço é só adicionar esse comando que ele passará para a próxima iteração, mas o contador irá aumentar.
* `abs()` – Mantém o valor absoluto de um número, independente do sinal, se for negativo ou positivo ele vai manter somente o número sem o sinal.
* `def` – Define uma função.
import – Utilizado para importar outros módulos e outros programas para dentro de um programa específico.
* `.sleep()` – Cria um delay na execução do código, precisa ser associado a quem deve estar no delay e dentro do seus parênteses deve ter o valor em segundos do delay. Deve ser importado da biblioteca `time`.
* `.capitalize()` – Coloca a primeira letra da string em maiúscula.
* `.lower()` – Transforma todas as letras da string para letras minúsculas.
* `.upper()` – Transforma todas as letras da string para letras maiúsculas.
* `.find()` – Encontra um determinado caractere na string.
* `.rfind()` – Encontra um determinado caractere começando da direita para a esquerda.
* `.count()` – Conta quantas vezes um determinado caractere apareceu dentro do intervalo selecionado. Ex: `frase.count('o', 0, 13)`. O `o` é o caractere desejado, `0` onde inicia e `13` onde termina a procura.
* `.index()` – Mostra a primeira ocorrência do item entre parênteses, dentro da variável composta ao qual o index está ligado.
* `.replace()` – Troca uma palavra por outra dentro de uma string. Ex: `frase.replace('Android', 'Python')`.
* `.title()` – Transforma a primeira letra de todas as palavras em maiúscula.
* `.strip()` – Remove os espaços no início e no final da string.
* `.rstrip()` – Remove os espaços a direita da string.
* `.lstrip()` – Remove os espaços a esquerda da string.
* `.split()` – Cria uma divisão nos espaços da string, criando novas listas de cada palavra.
* `.join()` – Juntas as listas das strings em uma lista só.
* `.startswith()` – Mostra true ou false se a string começa ou não com o caractere passado.
* `.endswith()` – Mostra true ou false se a string termina ou não com o caractere passado.
* `.append()` – Adiciona um novo item a uma lista.
* `.insert()` – Insere um item na posição indicada. Ex: `palavras.insert(5, 'video')`.
* `del lista[3]` – É utilizado para apagar um elemento de dentro de uma lista.
* `del dicionario['sexo']` – É utilizado para apagar um elemento dentro de um dicionário.
* `.pop()` – Deleta o item no índice passado dentro dos parênteses.
* `.remove()` – Deleta o item passado dentro dos parênteses.
* `.sort()` – Coloca os valores de uma lista em ordem. Para colocar em ordem inversa é só declarar o sort com o parâmetro `reverse = True`. Ex: `produto.sort(reverse=True)`.
* `.values()` – Pega somente os valores dentro de um dicionário.
* `.keys()` – Pega as chaves dentro de um dicionário.
* `.items()` – Pega as chaves es os valores dentro de um dicionário.
* `.copy()` – Faz uma cópia de um dicionário para ser atribuído a outra variável composta sem que hajam alterações nessa cópia.
* `.add()` – Função que adiciona uma novo item a um set.
`...in...` – É utilizado para verificar se algum dado está dentro de uma lista ou variável, pode ser usado com caracteres específicos ou para comparar variáveis dentro de listas. Ex: `'fruta' in frase`; `fruta_pedida in fruta`. Esse comando retorna valores booleanos.
* `min()` – Função que mostra o menor item dentro de uma lista, seja em valor ou tamanho. Só é possível usar em listas que seja composta por um só tipo primitivo de dado.
* `max()` – Função que mostra o maior item dentro de uma lista, seja em valor ou tamanho. Só é possível usar em listas que seja composta por um só tipo primitivo de dado.
* `len()` – Função que mostra o tamanho da lista ou de um item específico da lista.
* `list()` – Função que transforma o que estiver dentro dos parênteses em uma lista.
* `tuple()` – Função que transforma o que estiver dentro dos parênteses em uma tupla.
* `dict()` – Função que transforma o que estiver dentro dos parênteses em um dicionário.
* `open()` – Função utilizada para abrir arquivos foram do código, pode ser usada para escrever novos arquivos, ler arquivos já prontos ou adicionar novas informações ao arquivo. Essa função recebe 2 parâmetros, o primeiro sendo o nome do arquivo e o segundo qual função ele vai fazer, `a` de append, para adicionar, `w` de write, para escrever, `r` de read, para ler. Os 2 parâmetros devem ser passados em forma de string.
* `.close()` – Função utilizada para fechar arquivos externos abertos, todo arquivo aberto deve ser fechado.
* `.readline()` – Função utilizada para ler as linhas do arquivo, uma por uma.
* `end = ''` – Remove o pulo de linha de um print para outro.
* `\n` – Cria um pulo de linha dentro de um mesmo print.
* `bin()` – Função que transforma o que estiver dentro dos parênteses em binário.
* `hex()` – Função que transforma o que estiver dentro dos parênteses em hexadecimal.
* `oct()` – Função que transforma o que estiver dentro dos parênteses em octal.
* `factorial()` – Função que faz o fatorial do que estiver dentro dos parênteses, deve ser importado da biblioteca `math`.
* `{:^20}` – Recurso do Python que serve para centralizar uma string, o`^` indica que vai ser centralizado, o número indica em quantos caracteres, os `:` são necessários para funcionar, este recurso deve estar associado ao `.format`, e o que for ser escrito de estar dentro dos parênteses do format, se for string com as aspas, ou se for variável da forma normal.
* `{:>20}` – Recurso do Python que serve para alinhar a direita uma string, o`>` indica que vai ser alinhado a direita, o número indica em quantos caracteres, os `:` são necessários para funcionar, este recurso deve estar associado ao `.format`, e o que for ser escrito de estar dentro dos parênteses do format, se for string com as aspas, ou se for variável da forma normal.
* `{:<20}` – Recurso do Python que serve para alinhar a esquerda uma string, o`<` indica que vai ser alinhado a esquerda, o número indica em quantos caracteres, os `:` deseja adicionar após, este recurso deve estar associado ao `.format`, e o que for ser escrito de estar dentro dos parênteses do format, se for string com as aspas, ou se for variável da forma normal.
* `enumerate()` – Numera o que estiver dentro do parênteses, é bom para descobrir a posição de algo dentro de uma variável composta.
* `sorted()` – Mostra uma variável composta em ordem, não altera a tupla e sim a sua exibição.
