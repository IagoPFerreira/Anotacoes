# Markdown

Markdown é uma linguagem simples de marcação originalmente criada por John Gruber e Aaron Swartz. Markdown converte seu texto em HTML válido. Markdown é frequentemente usado para formatar arquivos README, para escrever mensagens em fóruns de discussão online e para criar rich text usando um editor de texto simples.

Markdown serve basicamente para escrever textos. Como toda ferramenta, ele tem algumas desvantagens com relação à escrever em HTML:

- Você não consegue colocar atributos nos elementos (class, id, title, etc.), além dos poucos que ele permite por padrão;
Você não tem muito controle para fazer aninhamento de tags.
- Por isso é importante frisar que o uso do Markdown deve ser especificamente para a escrita de textos, artigos de blog, etc. Não é para simplesmente usá-lo no lugar do HTML!

---

# Sumário

- [Headers](#Headers)
- [Listas](#Listas)
  - [Ordenadas](#Ordenadas)
  - [Não ordendas](#Não-ordendas)
- [Enfâse](#Enfâse)
- [Links](#Links)
- [Imagens](#Imagens)
- [Citação (blockquote)](#Citação-(blockquote))
- [Código (Code Highlight)](#Código-(Code-Highlight))
- [Tabela](#Tabela)
- [Checkbox](#Checkbox)
- [Criando Sumário](#Criando-Sumário)

[Voltar ao sumário](#Sumário)

## Headers

Os títulos seguem uma lógica de quanto mais cerquilhas (ou jogo da velha ou hashtag) maior o número do título e assim como no HTML, quanto menor o número do título, maior destaque, ou seja, o título 1 é mais importante e tem maior destaque que o título 2 e assim por diante. No **Markdown**, assim como **HTML** os títulos vão até o sexto nível.

# H1

## H2

### H3

#### H4

##### H5

###### H6

[Voltar ao sumário](#Sumário)

---

## Listas

### Ordenadas

Use o número seguido de um ponto e então o texto:

1. Primeiro item;
2. Segundo item;
3. Terceiro item;

### Não ordendas

Use um asterísco, um sinal de menos ou um sinal de mais, seguido do texto.

- Item;

- Item;

- Item;

[Voltar ao sumário](#Sumário)

---

## Enfâse

- _Ateriscos *_ ou _underlines__ simples, para utilizar o _itálico_;
- **Ateriscos **** ou **underlines __** duplos, para utilizar o **negrito**;
- **Ateriscos e _underlines_** podem ser combinados para ter uma ênfase ainda maior;
- ~~Tils~~ duplos, esse acento pode ser utilizado para riscar frases;
- $Sifrão$ para utilizar uma fonte cursiva;

[Voltar ao sumário](#Sumário)

---

## Links

Tem duas formas de criar links, textos âncoras, onde o texto possui o link ou links diretos, onde a URL fica totalmente exposta:

**Âncora**
[exemplo](https://exemplo.com) use um colchete [] para escrever o texto e dentro dos parênteses () adicione o link;

**Link direto**
<https://exemplo.com> utilize o sinal de menor que (<) e o sinal de maior que (>) para envolver o conteúdo do link

[Voltar ao sumário](#Sumário)

---

## Imagens

Tem duas formas adicionar imagens no Markdown, de forma inline ou de forma referencial:

**Inline:**
![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1");

**Referencial:**
![Logo Title Text 2][logo]

[logo]: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png

[Voltar ao sumário](#Sumário)

---

## Citação (blockquote)

>Use o sinal de maior que (>) para fazer blocos de citação.
>Para adicionar mais uma linha à citação, basta teclar Enter para um novo
>código sinal. Isso gerará um novo parágrafo dentro do _blockquote_.
>Códigos de **negrito**, _itálico_ e <https://links.com> funcionam aqui.

[Voltar ao sumário](#Sumário)

---

## Código (Code Highlight)

Há duas formas de adicionar trechos de código em Markdow:

`Código em linha`: utilizando um acento grave (`) no início e no final do código.

```Múltiplas linhas de código```: utilizando 3 acentos graves ou 3 tils antes e depois do código. É recomendado que a linguagem que está sendo apresentada, seja especificidada. Ex: ~~~javascript, ~~~ruby, ~~~python, ~~~html, ~~~css

~~~javascript
const exemplo = 'Exemplo';
~~~

~~~python
exemplo = str('Exemplo')
~~~

~~~html
<h3>Exemplo</h3>
~~~

[Voltar ao sumário](#Sumário)

---

## Tabela

Usando o pipe (|) é possível delimitar colunas e usando o hífen (-) é possível delimitar linhas.

Exemplo | Quantidade
------- | -----------
Item 1  | 2
Item 2  | 5

Para especificar o tipo de alinhamento que deseja ter nas tabelas, utilize : ao lado do campo horizontal de hífens ---, na segunda linha da sua tabela. Veja abaixo:

- Alinhado a esquerda: usar : no lado esquerdo (alinhamento padrão);
- Alinhado a direita: usar : no lado direito;
- Centralizado: usar : dos dois lados.

Exemplo:

Alinhado a esquerda | Centralizado | Alinhado a direita
:--------- | :------: | -------:
Valor | Valor | Valor

[Voltar ao sumário](#Sumário)

---

## Checkbox

Checkboxs podem ser usados para demonstrar a conclusão ou não de tarefas, para isso use um marcador de lista, seguido de colchetes [], para marcar o checkbox use um x dentro dos colchetes. Exemplo:

- [x] Task 1
- [ ] Task 2
- [ ] Task 3

[Voltar ao sumário](#Sumário)

---

## Criando Sumário

Para criar um sumário é bem tranquilo, o primeiro passo é criar o header `Sumário` usando o marcador `#` de nível 1, depois criar uma lista com os pontos do sumário, essas listas devem ter `[](#)`, dentro dos colchetes vai o nome do header do jeito que ele está escrito no conteúdo e dentro do parênteses vai o nome do header sem espaços, os espaços entre palavras pode ser substituído por traços `-`. Indentação também pode ser usada. Também sempre é bom criar um link de retorno para o sumário, é possível usar links do tipo âncora. Exemplo:

~~~Markdown
# Sumário

- [Headers](#Headers)
- [Listas](#Listas)
  - [Ordenadas](#Ordenadas)
  - [Não ordendas](#Não-ordendas)

[Voltar ao sumário](#Sumário)
~~~

[Voltar ao sumário](#Sumário)
