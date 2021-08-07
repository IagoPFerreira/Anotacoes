# HTML5 (HyperText Markup Language 5)

## TAGS

TAGS são marcações delimitadas pelos sinais de menor que e maior que, com alguma função escrita dentro, `<tag>`, algumas possuem fechamento, `</tag>` e outras não, elas afetam tudo aquilo a qual estão relacionadas, que estiver entre uma abertura e fechamento de TAG será afetado por ela, as que não possuem fechamento, normalmente apresentam suas peculiaridades dentro delas mesmas.

---

## Identificações em HTML

Quando existe mais de uma mesma tag, normalmente é dado a ela um parâmetro de identificação, existem alguns tipos desses parâmetros, os mais comuns são os de **id**, **name** e `class`. O `id` serve com forma de identificação uma única tag e o seu valor não pode ser repetido em outra tag, já `name` e `class` podem ter seus valores usados em mais de uma tag. Esses parâmetros de identificação podem ser usados no CSS para delimitar a formatação a somente aquela tag com aquele id, name ou class, sendo em CSS o id representado por **#** (hashtag ou cerquilha), já name e class por **.** (ponto).

---

## Unicode

O unicode é uma linguagem universal, que serve para representarmos alguns símbolos, todo Unicode tem a sua representação em código, número ou nome específico, cada linguagem interpreta uma dessas representações, no HTML nós vamos usar a forma de entidade, mas poderia ser usada a forma de código também.

* `<!DOCTYPE html>` - Indica para o navegador e para os desenvolvedores qual é a linguagem que está sendo usada para desenvolver essa página, o ponto de exclamação no início é essencial para que essa tag seja identificada como DOCTYPE. Na versão do 5 do HMTL não é necessário colocar o número da versão.
* `<html></html>` - Indica onde começa e onde termina o html, tudo deve ser desenvolvido dentro dessa tag. Essa tag recebe um atributo chamado `lang`, que significa language, que indica qual é o idioma do código, dentro desse lang nós colocamos `pt-br`, indicando que a linguagem vá ser português brasileiro, configurando assim para que os acentos e caracteres especiais sejam reconhecidos no codificador, então a tag fica assim: `<html lang="pt-br">`.

---

## Acessibilidade

Durante o desenvolvimento web sempre devemos ter a acessibilidade como padrão, assim como a usabilidade e a responsividade, existem muitas formas de se desenvolver um site mais acessível, uma delas é colocando a propriedade alt das imagens de forma descritiva, descrevendo o que tem na imagem, ou usar a propriedade aria-label para criar a descrição do elemento HTML e/ou o uso do title nos elementos HTML.

O uso de TAGs semânticas no lugar de TAGs generalistas ajuda em muito na acessibilidade de uma aplicação, logo, SEMPRE prefira usar TAGs semânticas ao invés de TAGs generalistas.

---

## Divisão do HTML

O HTML é divido em 2 partes o HEAD e o BODY, ou CABEÇA e o CORPO, a parte do HEAD é onde ficam as informações que serão dadas para o navegador saber com agir, já o BODY é onde ficam as informações que serão exibidas no navegador, cada uma dessas partes tem as suas TAGS específicas `<head></head>` e `<body></body>`, essas duas tags ficam dentro da tag html.

### HEAD

* `<meta>` - Serve para definir qual vai ser o conjunto de caracteres que serão usados no código, essa tag recebe um atributo chamado charset e dentro dele um padrâo, assim `<meta charset="UTF-8">`, esse padrão indica o padrão utilizado nas linguagens ocidentais, possibilitando a interpretação do navegador de caracteres especiais e acentos. `<meta name="viewport" content="width=device-width, initial-scale=1.0">` - Serve para começar a adaptar o conteúdo e o estilo da página para visualização em celulares, o parâmetro `content` diz o tamanho aproximado da página que será exibida, mas outras configurações no CSS precisam ser feitas.
* `<title></title>` - Serve para dar o título, ou nome da página, título esse que vai na aba do navegador.
* `<link>` - Serve para linkar um outro arquivo ao arquivo HTML, ou seja, eu posso linkar um arquivo em CSS ao HTML que estou usando e no CSS desenvolver todo o estilo da página e esse estilo pode ser usado em mais de uma página, desde que esteja linkadas da forma correta. Essa tag recebe 2 parâmetros, o primeiro parâmetro é o `rel`, de relationship, com o valor `stylesheet`, de folha de estilo, e o segundo parâmetro é o `href`, de hypertext reference, com o valor do nome do arquivo e sua extensão, `nome.css`. Ex: `<link rel = ”stylesheet” href = “style.css”>`.
* `<style></style>` - Serve para utilizar o CSS dentro do HTML sem que seja necessário criar um novo arquivo somente para o CSS, pode ser feito dentro do mesmo arquivo que o HTML, mas só serve para aquela página específica onde ele está escrito.
Existe uma variação da utilização do CSS dentro de cada tag, que não é muito recomendado por sua pouca praticidade, que é colocar style como um parâmetro dentro das tags. Ex: `<h1 style: font-size: 12pt;></h1>`. Desta forma essa formatação estará restrita somente a tag a qual ela estiver dentro e não funcionará em outras tags a não ser que seja copiada para dentro delas, o nome desse processo é CSS in line. NÃO RECOMENDADO.

### BODY

* `<header></header>` - Utilizada para delimitar um cabeçalho dentro do body, ou seja, delimita a seção superior da página.
* `<main></main>` - Utilizada para delimitar a seção principal da página, dentro do body.
* `<footer></footer>` - Utilizada para delimitar a seção rodapé da página, dentro do body.
* `<nav></nav>` - Cria um menu de navegação, normalmente com uma lista dentro da nav, onde cada um dos itens é um link para outra página do mesmo site.
* `<section></section>` - Cria uma seção onde todo conteúdo possui um significado semântico, está tudo ligado.
* `<article></article>` - O elemento section representa uma seção do documento, agrupando conteúdos relacionados. Todo o conteúdo dentro desse elemento deve fazer sentido com o próprio elemento, de forma que se esse elemento seja retirado do local onde ele está e seja mandado para outro local, o seu conteúdo ainda faça sentido.
* `<aside></aside>` -  O elemento aside representa um conteúdo à parte. Alguns exemplos de sua utilização são: barras laterais e/ou conteúdos adjacentes à um conteúdo principal.
* `<strong></strong>` - Põe tudo aquilo que estiver dentro dela em negrito.
* `<em></em>` - Coloca em ênfase para os buscadores colocando o conteúdo em itálico.
* `<span></span>` - Cria um conteiner inline e pode ser utilizada para estilos diferentes dentro de uma mesma frase.
* `<figure></figure>` - Cria uma marcação para inserção de uma figura, ou seja, cria um área delimitada para a utilização de tags `<img>`.
* `<figcaption></figcaption>` - Permite que seja criada uma descrição para a imagem inserida dentro do figure. Ex:

~~~html
<figure>
  <img src=”exemplo-de-imagem.jpg” alt=”Imagem”>

  <figcaption>Figura 1. Imagem</figcaption>
</figure>
~~~

* `<cite></cite>` - Utilizada para declarar que naquele trecho do códio, existe uma citação, normalmente utilizado em conjunto com o elemento q.
* `<q></q>` - Utilizado para delimitar um texto retirado de uma fonte externa, ou seja, que não foi de criação do autor. Ex:

~~~html
<p>
  <q>Lorem ipsum dolor sit amet, consectetur </q> - <cite>http://exemplo.com/</cite>.
</p>
~~~

* `<time></time>` - É utilizado para representar datas, caso seja necessário apresentar a data na qual um objeto foi criado, adicionando o atributo `datetime` é possível colocar a data por extenso, a quesito de padronização. Ex:
`<time datetime=”2021-25-02”>25/02</time>`
* `<h></h>` - Utilizada para títulos, existem 6 tipos de `<h>`, indo desde `<h1>` até `<h6>`.
* `<p></p>` - Utilizada para delimitar parágrafo
* `<img>` - Utilizada para adicionar imagens no HTML, mas é necessário que seja adicionado um parâmetro nessa tag para que a imagem seja adicionada, o parâmetro é `src`, de source, e o valor que ele recebe é o local onde se encontra a imagem junto com a sua extensão, as pastas são separadas por ‘ / ’. Ex: `<img src = “imagens/banner.jpg”>`
* `<ul></ul>` - Cria listas não ordenadas, existem três tipos de marcadores para listas não ordenadas, square, circle e disk, cada um desses marcadores devem ser especificados no parâmetro `type` dentro da tag ul. Ex: `<ul type = “square”>`.
* `<ol></ol>` - Cria listas ordenadas, existem três tipos de listas ordenadas, tipo numerado (1, 2, 3,...), tipo em letras (a, b, c,...; A, B, C,...) e algarismos romanos (i, v, x,...; I, V, X,...). Para selecionar o tipo desses ordenadores é necessário adicionar o parâmetro `type` a tag ol e colocar um representante do tipo, se for em maiúsculo os mascadores serão em maiúsculos, se em minúsculo os marcadores serão em minúsculos. Ex: `<ol type = “A”></ol>`, os marcadores serão em ordem alfabética em maiúsculo. Para selecionar em qual número ou letra começar é só adicionar o parâmetro `start` e adicionar um número relativo ao início, o parâmetro `start` só reconhece número. Ex: `<ol type = “A” start = “6” ></ol>`, significa que será o tipo alfabético mas iniciará na letra F.
* `<li></li>` - Cria itens para as listas, todo item deve ser aberto e fechado individualmente
* `<div></div>` - Cria divisões dentro do código e dentro da página, como se fosse blocos separados, não interferem por si só na apresentação da página, para isso é necessário que seja feitas mudanças no CSS.
* `<form></form>` - Cria uma área de formulário.
* `<label></label>` - Cria uma etiqueta para o input, é o que vem escrito antes da caixa para identificar o campo. Essa 2 tags sempre andam juntas. Ela pode ser aberta e fechada antes do input. Existe um parâmetro dentro de label chamado `for`, esse parâmetro indica a qual input esse label está ligado, para fazer essa ligação é só colocar o id do input neste parâmetro. Ex: `<label for = “iNome”>Nome</label>  <input type = “text” id = “iNome”>`. O input e outras tags de formulário podem ser criados dentro do tag label
* `<input>` - Cria um campo de entrada de dados, permitindo ao usuário a inserir alguma informação ali. Existe o parâmetro `type`, que indica o tipo do input, existe vários tipos como `text`, que cria uma caixa de texto pequena para colocar pequenos textos; `submit`, que cria um botão para envio do formulário e se caso queira mudar o texto dentro do botão, é só criar o parâmetro `value` e o texto que for atribuído a ele vai aparecer no botão; `radio`, que cria botões circulares para serem marcados, possuem o parâmetro `value` que não é o nome dele, mas sim o seu valor, precisam de um `id` que serão ligados a um `for` do label e um `name`, para que enquanto um esteja selecionado outros não estejam; `checkbox`, que cria uma caixa para check;  `email`, cria uma caixa configura para receber uma conta de email; `tel` cria uma caixa configura para receber um número de telefone, além desses 2 últimos servirem para uma melhor interação quando se está usando o celular; `file` cria uma caixa para adicionar um arquivo, dessa forma permitindo uma seleção de um arquivo no computador do usuário . Existe um atributo específico que indica que o campo precisa ser preenchido obrigatoriamente para que o formulário seja enviado, esse atributo é o `required`.
* `<button></button>` - Cria um botão, onde a esse botão podem ser atruídas várias funções.
* `<textarea></textarea>`- Cria uma caixa de texto onde o usuário pode escrever mais do que só uma linha, como no input. No textarea existem os parâmetros `cols` e `rows`, que indicam os números de colunas e linhas, respectivamente. Também precisa de um label e um `id` ligado ao `for` do label.
* `<select></select>` - Cria uma caixa de seleção de opções, que são criadas pela tag `option`.
* `<option></option>` - Cria uma opção pra ser selecionada dentro da caixa select. O que estiver escrito entre as tags é que aparecerá na caixa.
* `<fieldset></fieldset>` - Usada para agrupar múltiplos inputs dentro de um formulário.
* `<legend></legend>` - Usado para colocar o título do fieldset.
* `<table></table>` - Cria tabelas, dentro dela são necessárias especificar as tags para cada coluna e para cada célula. Dentro da tabela é possível criar seções como head, body e foot.
* `<thead></thead>` - Delimita o cabeçalho da tabela.
* `<th></th>` - Serve para especificar a célula como sendo do cabeçalho.
* `<tbody></tbody>` - Delimita o corpo da tabela.
* `<tr></tr>` - Cria as linhas para a tabela, `tr` de table-row.
* `<td></td>` - Cria as células para a tabela, `td` de table-data cell. As tabelas também oferecem a possibilidade de juntar células e montar um visual diferente. Por exemplo, quando uma linha, que deveria ter 5 células, passa a mostrar só "uma célula". Esse efeito é conseguido através da propriedade `colspan`. Ex: `<td colspan = "5">Rio de Janeiro</td>`. Portanto, em uma tabela de 5 colunas, para ter uma célula única na linha.
* `<foot></foot>` - Delimita o rodapé da tabela.
* `<iframe></iframe>` - Abre um espaço, uma espécie de janela, no navegador que permite que sejam adicionados conteúdos externos, como imagens, vídeos, mapas, entre outros, que esteja localizados em sites externos, usando o parâmetro `src`, indicamos a fonte do conteúdo e com width e height delimitamos a largura e altura dessa janela, muitos sites como google maps, youtube, entre outros possuem a função de atribuição dos seus conteúdos aos sites, disponibilizando um código html5 para os objetos. Para tratar um `iframe` no CSS, é mais recomendado que crie uma `div` é adicione o iframe dentro dessa `div`.
* `<script></script>` - Serve para utilizar o JavaScript dentro do HTML sem que seja necessário criar um novo arquivo somente para o CSS, pode ser feito dentro do mesmo arquivo que o HTML, mas só serve para aquela página específica onde ele está escrito. Adicionando o parâmetro `src` dentro da tag script, é possível linkar um arquivo JS externo, ao arquivo HTML, bem parecido com o que o link faz com o CSS.
