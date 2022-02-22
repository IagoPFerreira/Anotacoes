# Docker

`Docker` é um conjunto de produtos de plataforma como serviço, e que usam de virtualização ao nível de sistema operacional para entregar softwares em pacotes chamados contêineres. Sendo criados de forma à isolar um `container` do outro, os contêineres agrupam seus próprios softwares, bibliotecas e arquivos de configuração. Dessa forma, aplicações podem ser disponibilizadas e rodadas em diversos ambientes diferentes, em sistemas operancionais diferentes, pois o local onde elas irão rodar será dentro desse ambiente virtual pré-configurado do `Docker`.

Containers são como "pacotes", entretanto, eles funcionam em uma dinâmica um tanto quanto diferente. Vamos distinguir o que é um `container` e o que é uma `imagem`:

- O `container` é um processo `Docker` que, internamente, possui tudo aquilo que é necessário para seu funcionamento: Sistema Operacional (Binários e Bibliotecas) e recursos necessários para sua aplicação;
- A `imagem` é uma espécie de "fotografia" de um `container`, nós resgatamos uma `imagem`, quando queremos iniciar um novo `container` a partir de uma estrutura já conhecida.

---

# Sumário

- [Containers](#Containers)
- [Imagens](#Imagens)
- [Fluxo Padrão](#Fluxo-Padrão)
- [Esqueleto de um comando em Docker](#Esqueleto-de-um-comando-em-Docker)
  - [Listando containers](#Listando-containers)
  - [Rodando um comando adicional antes de terminar o container](#Rodando-um-comando-adicional-antes-de-terminar-o-container)
- [Comandos do CLI](#Comandos-do-CLI)
  - [Criar e rodar um container](#Criar-e-rodar-um-container)
  - [Cria um container sem executá-lo](#Cria-um-container-sem-executá-lo)
  - [Listar Containers](#Listar-Containers)
  - [Iniciar, reiniciar, pausar, resumir e parar um container](#Iniciar-reiniciar-pausar-resumir-e-parar-um-container)
  - [Retomando o acesso a um container interativo rodando em segundo plano](#Retomando-o-acesso-a-um-container-interativo-rodando-em-segundo-plano)
  - [Excluindo containers específicos](#Excluindo-containers-específicos)
  - [Limpando containers que não estão sendo utilizados](#Limpando-containers-que-não-estão-sendo-utilizados)
  - [Monitorando os processos dentro de um container](#Monitorando-os-processos-dentro-de-um-container)
- [Parâmetros e flags](#Parâmetros-e-flags)
- [Dockerfile](#Dockerfile)
<!-- - [](#) -->

## Containers

`Containers` lembram muito - mas não são - máquinas virtuais*, já que podemos rodar uma aplicação Linux em qualquer ambiente (Windows, Mac ou no próprio Linux) através dele.

    * Máquinas virtuais são softwares que simulam (virtualizam) computadores completos (desde o hardware até o software).

Um `container` não é uma máquina virtual, pois embora compartilhem de mesmas características, o `container` é uma instância isolada (tem apenas uma finalidade) e compartilha dos mesmos recursos do sistema operacional hospedeiro, o que damos o nome de *Virtualização a nível de Sistema Operacional (OS-level virtualization*.

Um `container` não deve ser utilizado para abrigar várias aplicações, e é justamente por isso que ele ocupa muito menos espaço que uma VM. Sua tendência é de manter somente o essencial no seu conteúdo.

---

## Imagens

`Imagens` podem se referir a praticamente qualquer tipo de `container`. Um exemplo disso é pensar o próprio sistema operacional Ubuntu, que possui uma imagem oficial no [Docker Hub](https://hub.docker.com/_/ubuntu).

O `Docker Hub` é o principal repositório de `imagens` `Docker` atualmente. Nele, possuímos o que é chamado de [Registro](https://docs.docker.com/registry/introduction/) (Registry)*, onde requisitamos essas `imagens`.

    * O Registry é um sistema de armazenamento e entrega, no qual podemos ter um usuário com nossas próprias imagens. Algo que lembra muito o GitHub, já que podemos dar pull nessas imagens para uso posterior. Veremos isso mais adiante.

[Voltar ao sumário](#Sumário)

---

## Fluxo Padrão

![Fluxo Padrão](../imagens/docker-flow.png)

- Tudo começa em um arquivo chamado `Dockerfile`. Este arquivo possui as instruções necessárias para que possamos gerar uma `imagem`;
  - Aqui vão instruções de qual sistema operacional usar, tal como quais comandos devem ser executados quando a `imagem` for rodada em um `container`.

- Após isso, podemos dar `push` ou `pull` (como em um repositório do GitHub) em uma `imagem` no `Registry`;
  - Você pode dar `pull` na sua própria `imagem` (caso tenha dado push nela) ou em outra a sua escolha.
  - O Registro mais comum é o `Docker Hub`, mas temos outros exemplos, como mostrado na `imagem`.

- Por último, rodamos a `imagem` em um `container`, utilizando o comando run, que veremos mais adiante.
  - Após isso, temos que dizer pro `container` o que deve acontecer, se ele deve se manter ativo ou não, caso o contrário, o `container` é encerrado. O que faz parte de seu ciclo de vida.

[Voltar ao sumário](#Sumário)

---

## Esqueleto de um comando em Docker

Um ponto importante antes de começarmos, é entender que os comandos do `Docker` funcionam no seguinte formato:

~~~bash
docker <comando> <sub-comando> <parâmetros>
~~~

Sendo que é possível abreviar alguns comandos, como no caso do `docker run hello-world`, que também pode ser escrito como `docker container run hello-world`. Utilizaremos aqui a segunda forma, por ser mais atual e verbosa.

Como comentamos anteriormente, o comando `run` serve para rodar uma `imagem` em um `container`, vamos testar isso com a `imagem` oficial do Ubuntu;

O formato do comando para rodar um `container` é o seguinte:

~~~bash
docker container run <nome-da-imagem>:<tag>
~~~

Onde `<tag>` representa a versão daquela `imagem`, caso nenhuma seja passada, ele assumirá que é a última versão disponível (`latest`);

Então rode o comando:

~~~bash
docker container run ubuntu
~~~

Se tudo correr bem, você deve enxergar o seguinte resultado:

![Docker run ubuntu](../imagens/docker-run-ubuntu.png)

Aqui você deve ter notado duas coisas:

1. Uma vez que sua máquina local não possua a `imagem` do registro (`Unable to find image 'ubuntu:latest' locally`), o `Docker` deve se encarregar de baixar essa `imagem`, fazendo o `pull` automaticamente (`latest: Pulling from library/ubuntu`) ;
2. Uma vez que o `Docker` baixou a `imagem` e rodou o `container`, nada aconteceu! 🤔

Na verdade, esse é o comportamento normal! Lembram que comentamos que, se não dissermos para o `container` o que ele deve fazer a seguir, o `container` é simplesmente encerrado?

Pois foi isso mesmo que aconteceu! Um `container` foi criado e iniciado e, uma vez que não demos nenhuma outra instrução pra esse `container`, ele foi encerrado.

[Voltar ao sumário](#Sumário)

---

### Listando containers

No `Docker` é possível saber quais `containers` estão ativos com o seguinte comando:

~~~bash
docker container ls
~~~

Mas no nosso caso, o `container` iniciou e parou logo em seguida, então só é possível enxergar ele se passarmos o parâmetro `-a` para mostrar todos os `containers` incluindo os inativos.

~~~bash
docker container ls -a
~~~

![Docker container ls -a](../imagens/docker-container-ls-a.png)

Caso o comando `docker run <imagem>` tenha sido rodado mais de uma vez, para cada uma dessas vezes foi criado um `container`.

Isso significa que o comando `run` também cria um novo `container` para aquela `imagem` toda vez que é executado, mas não se preocupe! É possível remover esses `containers` que não estão sendo mais utilizados, veremos isso mais adiante.

E caso você queira saber somente sobre o último `container` criado (independente do status dele), você pode usar o parâmetro `-l`:

~~~bash
docker container ls -l
~~~

![Docker container ls -l](../imagens/docker-container-ls-l.png)

Vamos entender qual o significado de cada coluna:

- `CONTAINER ID`: Identificador único*;
- `IMAGE`: O nome da `imagem` utilizada para a criação do `container` ;
- `COMMAND`: O comando executado/ em execução dentro do `container` ;
- `CREATED`: Quando foi criado o `container` ;
- `STATUS`: O status atual do mesmo, no nosso caso, encerrado;
- `PORT`: A porta que estamos utilizando para nos comunicar com o `container`**;
- `NAMES`: O apelido do `container`, como não definimos nenhum, foi criado um aleatório.

      * Quando executamos algum comando relacionado ao container, podemos nos referenciar tanto pelo campo ID (inteiro ou parte dele), quanto pelo campo NAMES.
      ** Veremos isso mais adiante, mas o docker pode disponibilizar uma porta de acesso para aplicação.
      Para isso, conseguimos fazer uma atribuição de uma porta do sistema hospedeiro, apontando para uma outra porta, no sistema cliente, no formato <porta-do-host>:<porta-do-cliente>.
      Exemplo 8080:3000, em que a porta 8080 do meu sistema representa a porta 3000 do container.

[Voltar ao sumário](#Sumário)

---

### Rodando um comando adicional antes de terminar o container

No `Docker` é possível executar comandos de terminal no `container` antes que ele seja encerrado (sobretudo se quisermos manter ele ativo por mais tempo que o normal).

Para executar comandos no terminal do `container` é só adiciona-los no final da execução do `run`, conforme o modelo:

~~~bash
docker container run <nome-da-imagem>:<tag> <comando> <argumentos-do-comando>
~~~

Exemplo:

~~~bash
docker container run ubuntu echo 'Hello User!'
~~~

![Hello user](../imagens/docker-hello-user.png)

[Voltar ao sumário](#Sumário)

---

## Comandos do CLI

### Criar e rodar um container

- Cria um `container` e roda logo em seguida:

~~~bash
docker container run <parâmetros> <imagem>:<tag>
~~~

- O parâmetro `--name` define um `<nome-da-sua-escolha>` para aquele `container` (ao invés de um nome aleatório):

~~~bash
docker container run --name <nome-da-sua-escolha> <imagem>:<tag>
~~~

- O parâmetro `--rm` deve garantir que o `container` seja removido ao final da execução (útil para testar imagens sem ficar acumulando `containers` novos):

~~~bash
docker container run --rm <imagem>:<tag>
~~~

- O parâmetro `-d` (de `--detach`, desacoplado em português) rodará esse `container` em segundo plano:

~~~bash
docker container run -d <imagem>:<tag>
~~~

[Voltar ao sumário](#Sumário)

---

### Cria um container sem executá-lo

- Cria um `container` com a `imagem` de referência, mas não o executa imediatamente:

~~~bash
docker container create <parâmetros> <imagem>:<tag>
~~~

- O parâmetro `-it` nesse contexto, deve garantir que ao iniciar o `container`, ele se mantenha ativo e disponha de um terminal de acesso:

~~~bash
docker container create -it <imagem>:<tag>
~~~

[Voltar ao sumário](#Sumário)

---

### Listar Containers

- Lista (ls, list em inglês) todos os `containers` ativos:

~~~bash
docker container ls
~~~

- Lista todos os `containers` ativos e inativos:

~~~bash
docker container ls -a
~~~

- Lista o último `container` criado (independente do seu estado):

~~~bash
docker container ls -l
~~~

[Voltar ao sumário](#Sumário)

---

### Iniciar, reiniciar, pausar, resumir e parar um container

- Inicia um `container` usando referências de sua identificação única (campo `CONTAINER ID`, parcialmente ou inteiro), ou pelo nome (campo `NAMES`) que foi definido:

~~~bash
docker container start <CONTAINER ID || NAMES>
~~~

Note que o comando `start` difere do comando `run`. O `start` apenas inicia o `container` que já havia sido criado (mas estava inativo), enquanto o `run` cria e executa um novo `container`!

- Reinicia um `container` usando as referências citadas anteriormente:

~~~bash
docker container restart <CONTAINER ID || NAMES>
~~~

- Pausa um `container` usando as referências citadas anteriormente:

~~~bash
docker container pause <CONTAINER ID || NAMES>
~~~

- Tira um `container` do modo de pausa usando as referências citadas anteriormente:

~~~bash
docker container unpause <CONTAINER ID || NAMES>
~~~

- Encerra um `container` usando as referências citadas anteriormente:

~~~bash
docker container stop <CONTAINER ID || NAMES>
~~~

[Voltar ao sumário](#Sumário)

---

### Retomando o acesso a um container interativo rodando em segundo plano

- Caso você tenha iniciado um `container` em segundo plano utilizando `-dit`, você pode acessar esse `container` rodando o comando `attach`:

~~~bash
docker container attach <CONTAINER ID || NAMES>
~~~

[Voltar ao sumário](#Sumário)

---

### Excluindo containers específicos

- Se o `container` não estiver ativo, esse comando deve remover o mesmo:

~~~bash
docker container rm <CONTAINER ID || NAMES>
~~~

- Se o `container` estiver ativo, você deve passar o parâmetro `-f` (forçar) para parar sua execução e depois efetuar a remoção:

~~~bash
docker container rm -f <CONTAINER ID || NAMES>
~~~

[Voltar ao sumário](#Sumário)

---

### Limpando containers que não estão sendo utilizados

- ⚠️ Use com moderação ⚠️: Esse comando deve remover todos os `containers` inativos do seu computador. O comando pede confirmação.

~~~bash
docker container prune
~~~

[Voltar ao sumário](#Sumário)

---

### Monitorando os processos dentro de um container

- O comando top, assim como nos terminais linux, traz as informações sobre os processos que estão sendo rodados, mas dentro daquele `container`, o que não inclui, por exemplo, serviços que são compartilhados com o sistema hospedeiro. Ele é útil para quando estamos os rodando em segundo plano:

~~~bash
docker container top <CONTAINER ID || NAMES>
~~~

[Voltar ao sumário](#Sumário)

---

## Parâmetros e flags

- `-a` - Retorna todos os dados;
- `-d` - Roda um `container` em segundo plano;
- `-f` - Força a execução de algum comando, passando por cima de restrições padrões;
- `-i` - Estabelece uma interface de comunicação física com esse terminal, no caso, por meio do teclado;
- `-l` - Retorna os últimos dados;
- `--rm` - Remove um `container` ao final da execução;
- `-t` - Requisita um terminal no `container`, que consiga imprimir o retorno dos comandos;

[Voltar ao sumário](#Sumário)

---

## Dockerfile

~~~bash

~~~
