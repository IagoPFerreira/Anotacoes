# GIT & GITHUB

O GIT é um sistema de controle de versão, um sistema de controle de versão (como o próprio nome já diz) tem a finalidade de gerenciar diferentes versões de um documento. Com isso ele te oferece uma maneira muito mais inteligente e eficaz de organizar seu projeto, pois é possível acompanhar um histórico de desenvolvimento, desenvolver paralelamente e ainda te oferecer outras vantagens, como exemplo, customizar uma versão, incluir outros requisitos, finalidades especificas, layout e afins sem mexer no projeto principal ou resgatar o sistema em um ponto que estava estável, isso tudo sem mexer na versão principal.

[Artigo referência para esse texto](https://www.devmedia.com.br/sistemas-de-controle-de-versao/24574)

Branch é uma versão independente e editável do código, dentro das branches existe a branch master, que é a branch principal do código, ou seja, é a parte do código que irá para o ar, as mudanças feitas na branch são chamadas de Commit, esses commits podem ser feitas de forma isolada e depois adicionadas um sistema de controle de versão que fará a união da branch original com o Commit, eliminando partes repetitivas e mantendo as novas alterações, junto com a base do código que permaneceu no Commit.

Branch feature são independentes da Branch master, podendo ter modificações especificas para determinados locais do código, ou modificações para determinados clientes. Mas a junção dessas duas branches é possível, e é chamada de Merge.

---

# Sumário

- [Criando um repositório local](#Criando-um-repositório-local)
- [Comandos em GIT](#Comandos-em-GIT)

## Criando um repositório local

Antes de se criar um repositório é preciso criar uma pasta para ele. Para isso você deve utilizar o comando mkdir, como vimos anteriormente, e então navegar para a pasta criada com o comando cd.

Para criar um repositório você deve digitar o comando git init. É muito importante que esteja dentro da pasta criada para o repositório.

---

## Comandos em GIT

- `git init` – Como seu nome bem diz, esse comando é responsável por iniciar um repositório Git dentro da pasta em que foi executado.
- `git status` – Retorna o status do repositório.
- `git diff` – Mostra as modificações especificamente feitas no arquivo.
- `git add` – Adiciona ao stage as modificações que já foram feitas. Ex: git add comidas_maravilhosas.txt. Adiciona só as mudanças feitas neste arquivo ao stage.
- `git commit` -m “mensagem” – Comita as modificações para o git e junto com as modificações vai uma mensagem com a descrição resumida do que essas modificações fazem.
- `git commit` -am ‘mensagem’ – Adiciona todos os arquivos que estiver unstageds para o staged e adiciona uma mensagem ao commit.
- `git reset HEAD~1` – Desfaz o commit que ainda não foi feito o push.
- `git branch` – Mosta a Branch que você está e cria uma nova Branch. Ex: git branch azul. Criou uma nova branch chamada azul.
- `git branch -D` – Deleta uma branch. Ex: git branch -D exemplo. Deleta a branch exemplo.
- `git checkout` – Serve para fazer a mudança entra as Branchs.
- `git checkout` -b – Cria uma nova branch e já faz o checkout nela. Ex: git checkout -b exemplo. Assim o checkout cria a branch exemplo e já muda para ela.
- `git checkout 0ccb~1 sobremesas.txt` – Recupera arquivos deletados, a partir do log. Usando em conjunto com o git log –diff-filter=D -summary, e copiando os 4 primeiros dígitos da sequência hexadecimal do hash, colocando o ~ e indicando que ele será existente com o 1, mais o nome do arquivo que deseja recuperar, este arquivo será recuperado, mas será necessário adicioná-lo ao commit.
- `git merge` – Serve para juntar 2 Branchs em uma.
- `git clone` – Serve para fazer um clone de um projeto no Git. Ex: git clone urlDoRepositorio.
- `git reset` – Tira os arquivos que estiverem na área de staged e volta para a unstaged.
- `git log` – Mostra os registro de commits feitos no git.
- `git log` --diff-filter=D -summary – Mostra quais foram os logs onde algum arquivo foi deletado em forma de sumário.
- `git rm` – Remove arquivos de dentro do git.
- `gitignore` – Ignora arquivos que você não quer adicionar ao seu git. É preciso criar um arquivo onde você vai colocar as coisas que você vai ignorar, o nome dele precisa ser .gitignore, o ponto antes do nome é para ele ficar oculto, dentro do .gitignore, você adiciona as extensões, arquivos específicos ou diretórios que você deseja ignorar. O gitignore pode ser commitado.
- `git remote add origin URL` – Faz a conexão entre o repositório local e o repositório remoto.
- `git remote -v` – Mostra a situação da conexão do repositório remoto com o repositório local.
- `git push` – Manda as alterações feitas no repositório local para o repositório remoto. Na primeira vez que é feito o push é necessário fazer da seguinte forma = git push -u origin master (ou nome da branch que você estiver usando).
- `git fetch` – Verifica se existe alguma alteração no repositório remoto, comparando o repositório local com o remoto.
- `git pull` – Verifica se existe alguma alteração no repositório e faz um merge ao mesmo tempo, ou seja, traz as mudanças e já faz a junção delas com o repositório local.
- `git branch -M main` – Muda o nome da branch master para main, depois de já ter sincronizado repositório local com remoto.
- `git branch -d nome-da-branch` – Apaga a branch no repositório local
- `git push origin --delete nome-da-branch` – Apaga uma branch no repositório remoto.

[Voltar ao sumário](#Sumário)
