# Checklist de adicionar um novo projeto ao Supabase

- [ ] Login
  - [ ] Acessou o site do [Supabase](https://supabase.io/)
  - [ ] Clicou em `sign-in`/`entrar` para fazer o login
  - [ ] Deu permissão ao Supabase à sua conta do Github (**Somente para caso seja o primeiro acesso**)

- [ ] Criando um novo projeto
  - [ ] Clicar em `New Project`/`Novo Projeto`
  - [ ] Selecionar a organização com o nome do seu usuário do GitHub
  - [ ] Nomear o seu banco de dados. Exemplo: `Testando_Supabase`
  - [ ] Escolha uma senha forte (Guarde essa senha em um local para você não esquecer, crie uma senha forte com letras, números e símbolos)
  - [ ] Escolha a região do seu banco de dados (Quanto mais perto de você, menor será a latência)
  - [ ] Mantenha o campo de Plano na opção Free
  - [ ] Clique em `Create new project`/`Criar novo projeto`

- [ ] Configurando o Sequelize
  - [ ] Ter iniciado um projeto Node e ter instalado todas as dependências

  ```bash
    mkdir supabase-with-sequelize && cd supabase-with-sequelize
    npm init -y
    npm install sequelize sequelize-cli express dotenv
    npm install pg pg-hstore
  ```

  - [ ] Iniciar a configuração do Sequelize

    ```bash
    npx sequelize-cli init

    ```

  - [ ] Mudar o arquivo de `config.json`para `config.js`
  - [ ] Alterar o arquivo `config.js` adcionando as variáveis de ambiente.

  ```JavaScript
  // config/config.js
  require('dotenv/config');

  const { HOST, PASSWORD_POSTGRES, DATABASE, DB_USERNAME, DB_PORT } = process.env;

  module.exports = {
    "development": {
      "username": DB_USERNAME,
      "password": PASSWORD_POSTGRES,
      "database": DATABASE,
      "host": HOST,
      "port": DB_PORT,
      "dialect": "postgres"
    },
    "test": {
      "username": DB_USERNAME,
      "password": PASSWORD_POSTGRES,
      "database": DATABASE,
      "host": HOST,
      "port": DB_PORT,
      "dialect": "postgres"
    },
    "production": {
      "username": DB_USERNAME,
      "password": PASSWORD_POSTGRES,
      "database": DATABASE,
      "host": HOST,
      "port": DB_PORT,
      "dialect": "postgres"
    }
  }
  ```

  - [ ] Adicionar ao arquivo `.env` as varáveis de ambiente

  ```env
  PASSWORD_POSTGRES= # aqui vai a senha que você criou no Supabase, se a sua senha tiver caracteres especiais coloque a senha entre aspas
  HOST= # o link de onde o banco está hospedado
  DATABASE=postgres
  DB_USERNAME=postgres
  DB_PORT= # porta que o Supabase fornece
  ```

  - [ ] Pegar as informações do banco na aba de `configurações` > `Database` > `Connection info`
  - [ ] Alterar o `index` do `model` para procurar pelo arquivo `config.js`

  ```JavaScript
  // models/index.js

  const config = require(__dirname + '/../config/config.js')[env];
  ```

  - [ ] Criar uma tabela de teste via `Sequelize`

  ```bash
  npx sequelize model:generate --name Product --attributes name:string,description:string
  ```

  - [ ] Executar a migration para criar a tabela

  ```bash
  npx sequelize model:generate --name Product --attributes name:string,description:string
  ```

  - [ ] Verificar no Supabase se a tabela foi criada na aba `Table Editor` > `All tables`
