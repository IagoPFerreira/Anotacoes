# CSS3 (Cascading Style Sheet 3)

O CSS é responsável pelo estilo da página, é onde são feitas as configurações de design do site, no CSS não são utilizadas tags, mas existem comandos específicos para cada tipo de ajuste. Os ajustes em CSS são feitos em blocos, esses blocos são identificados pelas tags utilizadas no HTML e delimitados pelo uso de chaves, Ex: `h1 {...}`. Tudo que for h1 vai receber as configurações feitas dentro das chaves, caso seja utilizado somente o h ao invés de h1, todos os títulos, independentes dos números irão receber as configurações.

---

## Identificações em CSS

Quando existe mais de uma mesma tag, normalmente é dado a ela um 'id', 'name' ou ‘class’, que servem como formas de identificação exclusiva daquela tag e que pode ser usada no CSS para delimitar a formatação a somente aquela tag com aquele id, name ou class, sendo id representado por ' # ' (hashtag ou cerquilha), name e class por ' . ' (ponto)

---

## Valores em CSS

Todos os valores em CSS3 são atribuídos a uma propriedade usando um ‘ : ’ e no final é usado um ‘ ; ’ para indicar o final da propriedade. `Ex: font-size (propriedade): 12pt (valor);`.

---

## Cores em CSS

A primeira coisa sobre a qual precisamos falar são alfabetos. Temos o nosso alfabeto padrão, abcde e por aí vai. Esse é o alfabeto que usamos no português. Os alfabetos para computação são um pouco diferentes. Por exemplo, temos o binário 0 e 1. Temos o numérico, que vai do 0 ao 9. E aí conseguimos representar todos os números com isso. Ainda temos o dicionário hexadecimal, que é a mesma coisa que o dicionário numérico adicionando as letras **abcdef**. Com esse dicionário conseguimos representar muito mais coisas do que só com o dicionário numérico. É ele que usamos para marcar cores.

Vamos voltar e entender como funcionam as cores para nós. Nós conseguimos enxergar três espectros de cor, e o HTML monta isso. Nós enxergamos o espectro **RGB**, que quer dizer **Red Green Blue**, ou seja, vermelho, verde e azul.

### Padrão Hexadecimal (HEX)

Montamos a cor seguindo essa mesma característica, usando o dicionário hexadecimal. Para fazer isso, colocamos # e marcamos seis elementos. Os 2 primeiros para marcar o vermelho  os 2 segundos para marcar o verde e os 2 últimos para marcar o azul  Como é a representação numérica, ou em hexadecimal, para esses números? O zero é a ausência de cor, e o F é o máximo de cor. Então, se eu quiser representar, por exemplo, o preto  que é a ausência de todas as cores, coloco #000000. Ou seja, 00 para vermelho, 00 para verde e 00 para o azul. Se eu quiser representar o branco  coloco #FFFFFF. FF para o vermelho, FF para o verde e FF para o azul.

Se usarmos a representação #CCCCCC e olharmos no espectro do hexadecimal, o CC é quase o branco. Não é o preto completo e nem o branco completo. Essa é a representação dos elementos.

Como faríamos, por exemplo, para representar a cor vermelha em hexadecimal? Precisamos colocar # e precisamos que o vermelho seja completo, ou seja, no máximo, e que todas as outras cores não existam: #FF0000, assim, marcamos o vermelho em hexadecimal.

### Padrão Red-Green-Blue (RGB)

É importante saber também que existe outra forma de representar as cores, além das que já vimos. Temos as cores básicas, a linguagem hexadecimal e a RGB. O mesmo padrão RGB que falamos sobre as cores que conseguimos enxergar, temos um dicionário RGB. Um alfabeto. Ele vai do 0 até 255. Ou seja, ele tem 256 níveis de representação de cada cor. Para isso, o 0 também é a ausência e o 255 é o máximo. A representação no CSS é um pouco diferente. Ao invés de colocar #, eu coloco RGB( , , ), separando as cores por vírgula. Antes da primeira vírgula vem o vermelho. Então, se eu quiser representar o branco, coloco RGB(255, 255, 255). Se eu quiser representar só o azul, RGB(0, 0, 255). Essa é a forma que usamos para representar as cores com esses alfabetos no CSS e isso ser renderizado pelo nosso navegador.

### Padrão Alfa

O alfa também pode ser chamado de opacidade ou transparência, a opacidade é o contrário da nitidez, quanto mais opacidade menos nítido um elemento fica. No CSS podemos usar o alfa para regular a transparência de um elemento ou sua cor, dessa forma podemos fazer com que a cor do elemento no background se misture com a cor do elemento que estamos mexendo.

O padrão alfa em hexadecimal vai de 00 até ff, onde ff é nitidez total e 00 é opacidade total, ou seja, no ff você consegue ver perfeitamente o elemento, no 00 o elemento some por completo. Em Hex o alfa adiciona somente dois novos dígitos.

O padrão alfa em RGB vai do 1 ao 0, onde 1 é nitidez total e 0 é opacidade total, ou seja, no 1 você consegue ver perfeitamente o elemento, no 0 o elemento some por completo. Em RGB o alfa adiciona uma nova letra, ao invés de ser rgb(), passa a ser rgba().

O padrão alfa é adicionado normalmente como o próximo elemento após as cores básicas de cada padrão. Ex: `rgba(240, 248, 255, 0.965)`, `#f0f8fff6`.

**Observação:**

Existem diversos tipos de padrão de cores com RGB, HEX, HSL e outros, para saber mais sobre cada padrão, acesse o [tutorial de cores do W3Schools](https://www.w3schools.com/colors/colors_hsl.asp).

---

## Dimensões em CSS

Existem quatro formas de se regular as dimensões de um objeto em CSS, por altura, por largura, por espaçamento interno e por espaçamento externo, sendo respectivamente, height, width, padding e margin, sendo que os 2 primeiros podem receber valores numéricos em px, porcentagem ou outras formas, e os 2 últimos podem receber valores numéricos com qualquer medida ou valores escritos, como auto. As dimensões podem receber vários tipos de medidas, como px (pixel), pt (pontos), % (porcentage), vh (altura da página) ou vw (largura da págia), em (tamanho do elemento), cm (centímetros), in (inches), dentre outros.

---

## Hierarquia no CSS

A tag tem como se fosse uma força 1, a classe uma força 10, e o identificador uma força 100. Toda vez que temos um seletor, por exemplo, `p`, isso quer dizer que a força desse seletor é 1. Quando temos o `form p` a força disso é 1+1, a força disso é 2. Então 2, como é mais forte que o 1, o estilo aplicado vai ser o segundo, do `form p`. O que acontece então se colocarmos a classe `teste` aplicada àquele `p` com a cor, por exemplo, amarela? Ao salvar e recarregar isso no navegador, a cor do nosso texto fica amarelo, porque a classe tem uma força 10, ela é superior aos dois marcadores que foram utilizados. Então `.teste 10`.

O que acontece se criarmos um marcador com a seguinte configuração: `p.teste`? Só os parágrafos que têm aquela classe vão ter essa cor. E aí definimos para mudar para a cor laranja. Nós somamos, a classe tem a força 10, e a tag tem a força 1, então com 11 ele vai ser mais forte que o teste especificamente. E recarregando nossa página, o texto fica em laranja.

Por último, o mais forte deles é o identificador. Então se usarmos o identificador e colocar que a cor dele é rosa, no navegador, a cor do texto vai ser rosa, porque o identificador tem a força 100. Então sempre que estamos criando CSS, precisamos pensar em o quão específico é o marcador e o quão forte ele vai ser para que não seja sobrescrito por qualquer outro, e que nenhum erro no código seja cometido. Por isso a recomendação de criar sempre classes para os elementos é muito boa, ele não é genérico o suficiente para que todas as vezes que a tag seja mudada, ele seja alterado; e ele não é específico igual a um identificador para que só funcione naquele elemento. Ele é um estilo que pode ser replicado várias vezes como a classe, e várias vezes em vários elementos.
A única forma de alterar isso e alguma coisa mais forte que o identificador é quando temos o estilo inline. Então se adicionarmos uma propriedade `style`, e colocarmos o color igual a roxo, no navegador, ao recarregar, a cor vai ser roxo. Nada substitui o inline, ele é muito específico, ele está no elemento, e por isso ele é o mais forte. Ele teria o que seria equivalente a uma força 1000, e nada substitui isso.

---

## Comandos em CSS

* `font-size: 12pt;` - Tamanho da fonte, o número diz o tamanha e o ‘pt’ significa pontos. O tamanho também pode ser relativo usando o ‘em’, que pega o tamanho da fonte da página, que pode ter sido definido no body, ou deixado pelo padrão do navegador, e multiplica esse tamanho quantas vezes você quiser. Ex: `font-size 2em;` Vai fazer com que o tamanho da fonte seja 2 vezes maior que o tamanho padrão da página.
* `font-weight: bold;` - Peso da fonte, podendo ser bold (negrito), bolder (mais negrito ainda), lighter (leve), entre outras.
* `font-style: italic;` - Estilo da fonte, podendo ser itálica, obliqua, entre outros.
* `font-family: cursive;` - Tipo da fonte.
* `text-align: justify;` - Alinhamento do texto, ‘justify’ é justificado, existem outros tipos como ‘left’, ‘right’, ‘center’, dentre outros.
* `text-transform: uppercase;` - Transforma o texto, neste caso em tudo maiúscula com o uppercase, mas pode ter o lowercase, capitalize, entre outros.
* `text-decoration: none;` - Define a decoração do texto, podendo ser underline, overline, solid ou neste caso none, que também serve para retirar a formatação de link feita pelo navegador.
* `list-style-type: none;`  - Remove os marcadores de lista.
* `line-height: 1.5;` - Altura da linha, no caso a altura da linha mais 50%.
* `background: #cccccc;` - Define o fundo de um objeto, neste caso está definindo a cor como sendo cinza, mas existem outras variações desse comando que funcionam para outras utilizações como adicionar imagens (utilizando o parâmetro ‘url(“”)’), posição, tamanho, origem, dentre outros.
* `background: linear-gradient (#fefefe, #888888);` - Dentro de background existem muitas formas de alterar o fundo, uma delas é o linear-gradient, que faz um gradiente de transição de uma cor para outra automaticamente, podendo ser mudado o grau de angulação (45deg, 90deg ou qualquer outro valor) e podendo ser trocado o linear por radial, para que seja um gradiente circular.
* `background-image: url (caminho para a imagem)` - Coloca uma imagem no fundo da div.
* `background-position: x y` - Define a posição do elemento em background, primeiro no eixo x, depois no y.
* `background-size: cover` - Define o tamanho do elemento em background, o parâmetro ‘cover’ faz com que o elemento cubra todo o espaço de fundo da div.
* `color: red;` - Define a cor de um conteúdo específico, pode ser uma palavra, um objeto, dentre outros, mas é a cor em si, não a cor de fundo, cor de fundo é feito pelo background.
* `height: 100%;` - Define a tamanho da altura de um objeto, neste caso 100% da área que ele está ligado.
* `width: 100%;` - Define a largura de um objeto, neste caso 100% da área que ele está ligado. Outra funcionalidade é a de usar o próprio CSS para fazer o calculo do tamanho de um objeto em diferentes telas, para isso podemos o usar a propriedade ‘calc()’. Ex: `width: calc(40% -  (26px));`. Assim o objeto ocupará 40% da tela, menos 26 pixels.
* `max-width: 600px` - Define o tamanho máximo que um objeto pode ter.
* `padding: 25px;` - Define o espaçamento interno de um objeto, podendo ser em todos os lados, ou em um lado específico usando uma variável desse comando chamado `padding-top`, `right`, `bottom` ou `left`, nesta mesma ordem utilizando somente o `padding` dá para definir os espaçamento de cada um dos lados, colocando somente 1 valor ele atribui ele para todos os quatro cantos.
* `margin: 25px;` - Define o espaçamento externo de um objeto, podendo ser em todos os lados, ou em um lado específico usando uma variável desse comando chamado `margin-top`, `right`, `bottom` ou `left`, nesta mesma ordem utilizando somente o `margin` dá para definir os espaçamento de cada um dos lados, colocando somente 1 valor ele atribui ele para todos os quatro cantos.
* `display: inline-block;` - Define se o espaçamento lateral vai ser todo ocupado ou não, mesmo que o conteúdo não ocupe todo o espaço, quando conteúdo ocupa todo o espaço lateral mesmo sem preencher esse espaço por completo ele é chamado de conteúdo block, quando ele deixa livre o espaço lateral e só preenche até o seu tamanho, é chamado de conteúdo inline, textos geralmente são block e imagens geralmente são inline, mas existe um método para unir os 2 tipo que é o inline-block.
* `vertical-align: top;` - Define o alinhamento vertical dos objetos, neste caso alinhamento no topo, mas existem outros valores como bottom, initial, entre outros.
* `position: absolute;` - Define a posição de um objeto, podendo ela ser static, relative, absolute, entre outros, sendo absoluta é possível que o posicionamento desse objeto seja manipulado através de outros comandos em CSS para qualquer lugar da página, mas o posicionamento é absoluto em relação a página e não outros objetos, o relativo faz o posição a partir do pondo de criação dele e o static mantém ele no posicionamento que ele foi indicado no  código.
* `box-sizing: border-box;` - Define uma caixa com o tamanho absoluto indicado pelo width e que caso sejam feitas mudanças no margin ou no padding isso não interfira no posicionamento delimitado pelo width.
* `border: 2px solid #000000;` - Define uma borda no objeto entre o padding e o margin, primeiro o tamanho da espessura da borda, depois o tipo da borda (solid, dashed, dotted, entre outros) e em seguida a cor da borda.
* `border-radius: 10px;` - Define o arredondamento dos cantos da borda, pode ser declarado de forma geral com apenas um valor, ou para um canto específico. Exs: `border-bottom-left-radius: 10px;` (arredondando o canto inferior esquerdo) ou `border-top-right-radius: 10px;`(arredondando o canto superior direito) ou `border-radius: 10px 20px 30px 40px` (arredondando cada canto de um tamanho começando no superior esquerdo e indo no sentido horário). O tamanho do arredondamento é medido em ‘px’.
* `transition: 1s;` - Cria uma transição entre um estado e outro da configuração de um objeto, essa transição pode ser ativada por um `hover`, um `active`, por outro método ou por recarregar a página.
* `cursor: pointer;` - Transforma o cursor, nesse caso para a mãozinha.
* `transform: scale(1.2);` - Transforma o objeto por inteiro, respeitando todas as características pré definidas, ‘scale’ é um dos valores que esse parâmetro pode receber, no caso aumentamos o objeto em 20%.
* `float: left;` - É uma forma de mover o objeto, mas diferente do display e do position, o float “descola” o objeto da página, é como se o objeto estivesse flutuando, mas o local onde seria a sua sombra, ou seja, onde ele estava antes continua sendo ocupado, essa configuração pode ser usada para alinha imagens e textos. Há a opção de escolher o local onde a imagem vai ficar.
* `clean: left;` - Limpa a configuração float, após utilizado o float interferem um tudo que vem abaixo dele na página, para remover essa influência é só adicionar o clean com o mesmo valor do float.
* `opacity: 0.5;` - Regula a opacidade de um objeto, neste caso o objeto está com 50% da sua opacidade, a regulação desse comando é 1 sendo 100% de opacidade, onde é possível ver o elemento normalmente e 0 sendo 0%, onde não se é possível enxergar o objeto.
* `box-shadow: 10px 10px 10px 0 #black;` - Cria uma sombra em uma caixa ou objeto, o primeiro parâmetro é para o deslocamento no eixo X, o segundo parâmetro é a para o eixo Y, o terceiro parâmetro é para o espalhamento da sombra, o quarto é para a intensidade da borda, que indicam que a partir da borda do objeto o quão mais a sombra vai se espalhar, por fim vem a cor da sombra, é possível adicionar mais de uma sombra, utilizando uma vírgula após a cor e adicionando os parâmetros da nova sombra. É possível criar sombras internas também, é só adicionar o parâmetro ‘inset’ antes dos valores da sombra.
* `text-shadow: 10px 10px 10px 0 #black;` - Cria uma sombra no texto, o primeiro parâmetro é para o deslocamento no eixo X, o segundo parâmetro é a para o eixo Y, o terceiro parâmetro é para o espalhamento da sombra, o quarto é para a intensidade da borda, que indicam que a partir da borda do objeto o quão mais a sombra vai se espalhar, por fim vem a cor da sombra
* `overflow: auto;` - Cria uma barra de rolagem dentro da div utilizando o parâmetro ‘auto’. Utilizando o ‘hidden’ tudo que estiver fora do tamanho da div ficará escondido
* `@media screen and (max-width: 480px) {}` – Indica o CSS e ao navegador que tudo que toda tela que tiver uma largura máxima de 480px, exibirá no navegador o estilo da forma que estiver dentro do bloco.

---

## Pseudo elementos

São métodos, que podem ser de interação ou exibição, restritos somente a objetos aos quais eles estão ligados:

* `hover` - Método de interação do CSS que reflete  na página, serve para executar um bloco de configurações de design somente quando o mouse estiver sobre o objeto ao qual ele está ligado, ele precisa ser atribuído ao objeto com o ‘nome do objeto:hover{}’. Ex: `nav a:hover{}`.
* `active` - Método de interação do CSS que reflete  na página, serve para executar um bloco de configurações de design somente quando o mouse clicar dentro do objeto ao qual ele está ligado, ele precisa ser atribuído ao objeto com o ‘nome do objeto:active{}’. Ex: `produtos li:active{}`.
* `first-child` - Este pseudo elemento serve para selecionar somente o primeiro filho de uma tag, existem variantes como last-child (que seleciona somente o último filho), nth-child() (que pega qualquer filho indicado, por número, entre parentes), entre outros.
* `before` - Serve para adicionar coisas antes do objeto ao qual está ligado. Dentro do seu bloco deve ser adicionado o comando `content: “teste”;` .
* `after` - Serve para adicionar coisas após o objeto ao qual está ligado. Dentro do seu bloco deve ser adicionado o comando `content: “teste”;` .

## Seletores avançados

São ferramentas que permitem a seleção de objetos específicos sem que seja preciso ser feita uma mudança no HTML, são seletores de dentro do CSS.

* `>` - Seleciona todos os filhos diretos de uma tag específica. Ex: `main > p {}`. Todos os filhos diretos ‘p’ de ‘main’ serão selecionados e somente eles.
* `+` - Seleciona o próximo irmão após um objeto. Ex: `img + p {}`. Vai selecionar somente o próximo parágrafo após uma imagem, mas só se o parágrafo for filho do mesmo pai que a imagem.
* `~` - Seleciona todos os irmãos após um objeto. Ex: `img ~ p {}`. Vai selecionar somente todos os próximos parágrafos após uma imagem, mas só se os parágrafos forem filhos do mesmo pai que a imagem.
* `:not()` - Seleciona somente o item dentro do parênteses e exclui ele da configuração que for feita dentro do bloco. Ex: `.principal p:not(#missao) {}`. A instrução que for passada dentro do bloco não funcionará no ‘p’ com ‘id = “missão”’.
