# Passos para a criação de uma aplicação usando o Sequelize

1. Iniciar a aplicação

~~~bash
npm init -y
~~~

2. Instalar o sequelize

~~~bash
npm install sequelize
~~~

3. Instalar a CLI

~~~bash
npm install sequelize-cli
~~~

4. Instalar o mysql2

~~~bash
npm install mysql2
~~~

- Atalho

~~~bash
npm install sequelize sequelize-cli mysql2 
~~~

5. Inicializar o Sequelize

~~~bash
npx sequelize-cli init
~~~

6. Configurar o arquivo config.json gerado pelo init do CLI

~~~JSON
// config/config.json

{
  "development": {
    "username": "root",
    "password": "",
    "database": "revisao_bloco_24",
    "host": "127.0.0.1",
    "dialect": "mysql"
  }

  // No resto do arquivo você vai encontrar as convenções para conectar o Sequelize em outros ambientes
}
~~~

7. Usando variáves de ambiente no config.
  
  > 7.1. Instale o dotenv na raiz da aplicação

~~~bash
npm install dotenv
~~~

> 7.2. Mude o nome do arquivo de config.json para config.js e exporte o objeto de configuração

~~~JavaScript
// config/config.js

module.exports = {
  "development": {
    "username": "root",
    "password": "",
    "database": "revisao_bloco_24",
    "host": "127.0.0.1",
    "dialect": "mysql"
  }

  // No resto do arquivo você vai encontrar as convenções para conectar o Sequelize em outros ambientes
}
~~~

> 7.3. Crie um arquivo .env na raiz do projeto e adicione as variáveis de ambiente nele

~~~env
<!-- .env -->

MYSQL_USER=root
MYSQL_PASSWORD=senha
MYSQL_DATABASE=database_development
MYSQL_HOSTNAME=127.0.0.1
~~~

> 7.4. Importe as variáves de ambiente dentro do config.js

~~~JavaScript
// config/config.js

require('dotenv').config(); // Possibilita o acesso às variáveis de ambiente de dentro deste arquivo

module.exports = {
  "development": {
    "username": process.env.MYSQL_USER,
    "password": process.env.MYSQL_PASSWORD,
    "database": process.env.MYSQL_DATABASE,
    "host": process.env.MYSQL_HOSTNAME,
    "dialect": "mysql"
  }

  // No resto do arquivo você vai encontrar as convenções para conectar o Sequelize em outros ambientes
}
~~~

> 7.5. Alterar dentro do arquivo models/index.js de config.json para config.js

~~~JavaScript
// models/index.js

// Antes
// [...]
const config = require(__dirname + '/../config/config.json')[env];
// [...]

// Depois
// [...]
const config = require(__dirname + '/../config/config.js')[env];
// [...]
~~~

8. Criar o banco usando o CLI do Sequelize

~~~bash
npx sequelize db:create
~~~

9. Criar um model

~~~bash
npx sequelize model:generate --name User --attributes fullName:string
~~~

10. Alterar o model do formato de classe:

~~~JavaScript
// models/user.js

'use strict';
const {
  Model
} = require('sequelize');
module.exports = (sequelize, DataTypes) => {
  class User extends Model {
    /**
     * Helper method for defining associations.
     * This method is not a part of Sequelize lifecycle.
     * The `models/index` file will call this method automatically.
     */
    static associate(models) {
      // define association here
    }
  };
  User.init({
    fullName: DataTypes.STRING
  }, {
    sequelize,
    modelName: 'User',
  });
  return User;
};
~~~

> Para função:

~~~JavaScript
// models/user.js

const User = (sequelize, DataTypes) => {
  const User = sequelize.define("User", {
    fullName: DataTypes.STRING,
  }, {
    underscored: true
  });

  return User;
};

module.exports = User;
~~~

11. Alterar as migrations, caso seja necessário

~~~JavaScript
// migrations/XXXXXXXXXXXXX-create-user.js

'use strict';
module.exports = {
  up: async (queryInterface, Sequelize) => {
    await queryInterface.createTable('Users', {
      id: {
        allowNull: false,
        autoIncrement: true,
        primaryKey: true,
        type: Sequelize.INTEGER
      },
      fullName: {
        type: Sequelize.STRING
      },
      createdAt: {
        allowNull: false,
        type: Sequelize.DATE
      },
      updatedAt: {
        allowNull: false,
        type: Sequelize.DATE
      }
    });
  },
  down: async (queryInterface, Sequelize) => {
    await queryInterface.dropTable('Users');
  }
};
~~~

12. Executar a migration

~~~bash
npx sequelize db:migrate
~~~

> Caso queira reverter:

~~~bash
npx sequelize db:migrate:undo
~~~

> Caso seja necessária a modificação de alguma tabela, você pode rodar um comando para gerar uma nova migration e então fazer as alterações que você precisar:

~~~bash
npx sequelize migration:generate --name add-column-phone-table-users
~~~

~~~JavaScript
// migrations/XXXXXXXXXXXXX-add-column-XXXXXXX.js

'use strict';

module.exports = {
  up: async (queryInterface, Sequelize) => {
   await queryInterface.addColumn('Users', 'phone_num', {
     type: Sequelize.STRING,
   });
  },

  down: async (queryInterface, Sequelize) => {
    await queryInterface.removeColumn('Users', 'phone_num');
  }
};
~~~

> Em seguida rodar o comando para executar a nova migration:

~~~bash
npx sequelize db:migrate
~~~

> E alterar o model para incluit a nova coluna:

~~~JavaScript
// models/user.js

const User = (sequelize, DataTypes) => {
  const User = sequelize.define("User", {
    fullName: DataTypes.STRING,
    phone_num: DataTypes.STRING,
  });

  return User;
};

module.exports = User;
~~~

13. Criar um novo seed

~~~bash
npx sequelize seed:generate --name users
~~~

14. Adicionar as informações que serão colocadas no banco

~~~JavaScript
// seeders/XXXXXXXXXXXXX-user.js

'use strict';

module.exports = {
  up: async (queryInterface, Sequelize) => queryInterface.bulkInsert('Users',
    [
      {
        fullName: 'Leonardo',
        phone_num: '999999999',
        createdAt: Sequelize.literal('CURRENT_TIMESTAMP'),
        updatedAt: Sequelize.literal('CURRENT_TIMESTAMP'),
      },
      {
        fullName: 'Eduardo',
        phone_num: '999999998',
        createdAt: Sequelize.literal('CURRENT_TIMESTAMP'),
        updatedAt: Sequelize.literal('CURRENT_TIMESTAMP'),
      },
    ], {}),

  down: async (queryInterface) => queryInterface.bulkDelete('Users', null, {}),
};
~~~

15. Executar o seed

~~~bash
npx sequelize db:seed:all
~~~

> E para reverter:

~~~bash
npx sequelize db:seed:undo:all
~~~

---

## Criar a tabela sem as colunas `createdAt` e `updatedAt`

1. Adicionar um segundo objeto dentro do método `sequelize.define()` na model

~~~JavaScript
// models/user.js

const User = (sequelize, DataTypes) => {
  const User = sequelize.define("User", {
    fullName: DataTypes.STRING,
    phone_num: DataTypes.STRING,
  }, {
    timestamps: false,
  });

  return User;
};
~~~

2. Remover as referências das colunas na migration

~~~JavaScript
// migrations/XXXXXXXXXXXXX-create-user.js

'use strict';
module.exports = {
  up: async (queryInterface, Sequelize) => {
    await queryInterface.createTable('Users', {
      id: {
        allowNull: false,
        autoIncrement: true,
        primaryKey: true,
        type: Sequelize.INTEGER
      },
      fullName: {
        type: Sequelize.STRING
      }
    });
  },
  down: async (queryInterface, Sequelize) => {
    await queryInterface.dropTable('Users');
  }
};
~~~

3. Remover as referências das colunas no seeder

~~~JavaScript
// seeders/XXXXXXXXXXXXX-user.js

'use strict';

module.exports = {
  up: async (queryInterface, Sequelize) => queryInterface.bulkInsert('Users',
    [
      {
        fullName: 'Leonardo',
        phone_num: '999999999',
      },
      {
        fullName: 'Eduardo',
        phone_num: '999999998',
      },
    ], {}),

  down: async (queryInterface) => queryInterface.bulkDelete('Users', null, {}),
};
~~~
