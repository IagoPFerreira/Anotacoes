# FLEXBOX

 O Flexbox é uma ferramenta que ajuda a estilizar o CSS de forma mais regulada, ajuda no posicionamento de objetos de forma mais responsiva. O flex pode ser usado no objeto pai, para que os filhos recebam o comportamento.

## Comandos FLEXBOX

* `display: flex;` - Cria um alinhamento flexível para os objetos, os coloca inline, mas não restringe a suas movimentações.
* `align-item: center` - Cria um alinhamento dos objetos dentro do container no centro do eixo Y.
* `justify-content: space-between;` - Coloca os objetos em forma justificada, ou seja, ocupando o espaço do inicio ao fim do eixo x, e o parâmetro ‘space-between’ coloca todo o espaço em brando do container entre os objetos.
* `justify-content: space-around;` - Distribui o espaço dentro do container, ao redor dos objetos.
* `flex-direction: column;` - Dita a direção que o flex adotará, por padrão ele é ‘row’, ou seja, em linha, inline, mas com o column é possível fazer com que os elementos fiquem um em baixo do outro.
* `flex-wrap: wrap;` - Cria uma quebra dentro do container, o que não couber dentro do tamanho do container será quebrado e realocado de seguindo o flex-direction.
* `flex-flow: column wrap;` - Dita a direção que o flex adotará e cria um quebra dentro do container, substituindo os dois comandos ‘flex-direction: column;’ e ‘flex-wrap: wrap;’.
* `order: -1;` - Ordena os itens dentro de uma flex-container, deve ser atribuído ao próprio item. Por padrão o order recebe 0, o -1 significa que aquele item vai vir em primeiro lugar.
* `flex-grow: 1;` - Divide em partes iguais o espaço em brando dentro da flex-container e divide em proporções para os flex-itens, neste caso, o flex-grow está dando 1 dos espaços divididos para o item a qual ele está ligado, se eu quisesse que ele desse 5 era só mudar o número 1 por 5. o flex-grow é acumulativo dentro de uma flex-container, ou seja, ele vai contar com os outros flex-grow dos outros flex-itens.
* `flex-shrink: 2;` - Diminui os flex-itens conforme o tamanho da tela vai diminuindo, igual o flex-grow, deve ser atribuido ao flex-item. O número indica o quanto vai diminuir em relação ao espaço, neste caso, o item vai diminuir duas vezes mais do que os outros itens.
* `flex-basis: 200px;` - Determina o tamanho base de um flex container, é bem parecido com o width, mas o flex-basis tem prioridade dentro de uma flex container. A medida pode ser passada em porcentagem também.
* `flex: 1 2 200px;` - Esse comando junta o flex-grow, flex-shrink e flex-basis, nesta ordem, o primeiro parâmetro é do grow, o segundo do shrink e o terceiro do basis. Esse comando serve para economizar linha.

Site com documentação de Flexbox: <https://css-tricks.com/snippets/css/a-guide-to-flexbox/>

Sites com jogos para treinar Flexbox: <http://flexboxfroggy.com/> <http://www.flexboxdefense.com/>
