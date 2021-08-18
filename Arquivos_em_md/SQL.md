# Structured Query Language (SQL)

SQL é a linguagem usada para criar, pesquisar, extrair e também manipular dados dentro de um banco de dados relacional. Para que isso seja possível, existem comandos como o SELECT, UPDATE, DELETE, INSERT e WHERE, entre outros.

Todas as pesquisas realizadas dentro de um banco de dados são feitas em tabelas. Tabelas possuem linhas e colunas. Linhas representam um exemplo, ou instância, daquilo que se deseja representar, ao passo que colunas descrevem algum aspecto da entidade representada.

## Configurando a inicialização e senha do servidor MYSQL

Por padrão, após a instalação, seu servidor vai estar configurado para iniciar junto ao sistema. Caso não queira que isso aconteça, para poupar memória RAM, você pode desativar o início automático utilizando o comando:

~~~bash
# Linux
sudo systemctl disable mysql

# macOS
brew services stop mysql
# Esse comando remove os serviços não utilizados
brew services cleanup
~~~

A primeira vez que for utilizar após iniciar o computador, será necessário iniciar o servidor com o comando:

~~~bash
# Linux
sudo systemctl start mysql

# macOS
brew services run mysql
~~~

Se desejar ativar novamente que ele inicie junto ao computador, basta usar o comando:

~~~bash
# Linux
sudo systemctl enable mysql

# macOS
brew services start mysql
~~~

---

## Constrains

Uma das grandes vantagens de armazenar seus dados em um banco de dados é de possibilitar a criação de regras e restrições ( constraints , em inglês), que ditam exatamente como os dados podem ou não ser manipulados em suas tabelas.

Como as constraints são aplicadas às colunas das tabelas, é possível assegurar que os dados inseridos nelas serão consistentes conforme as regras definidas . São constraints :

- `NOT NULL` - Garante que aquele campo não pode conter valores nulos , ou seja, se não houver um valor padrão ( DEFAULT ) definido, será sempre necessário passar um valor para esse campo durante um INSERT , por exemplo.
- `UNIQUE` - Garante que o valor inserido na coluna da tabela é único , isto é, não pode haver outro valor igual para esta coluna registrado nesta tabela.
- `PRIMARY KEY` - A chave primária de uma tabela garante que a coluna em que essa constraint está sendo aplicada é o identificador único da tabela . Ela também é, por definição, não nula (mesmo efeito da constraint NOT NULL ) e única (mesmo efeito da constraint UNIQUE ).
- `FOREIGN KEY` - A chave estrangeira de uma tabela faz referência a uma chave primária (valor em uma coluna com a constraint PRIMARY KEY ) de outra tabela , permitindo um relacionamento entre as duas.
- `DEFAULT` - Garante que, caso nenhum valor seja inserido na coluna (ou caso a pessoa usuária insira um valor nulo), a constraint colocará o valor padrão que for passado para ela .

Assim, durante a criação de uma tabela, ao se pensar em suas colunas, podemos avaliar quais constraints podemos aplicar àquela informação. Por exemplo, imagine uma tabela que liste os sabores de sorvete de uma sorveteria. Nessa tabela, temos três colunas: um código identificador, o nome do sabor do sorvete e o código identificador de quem fornece. Vamos ver cada coluna e pensar em quais constraints podemos adicionar a elas:

- `Código identificador (id)` - Para o id do sorvete, precisamos que ele identifique e represente o sabor do sorvete na tabela, então podemos adicionar como constraint a PRIMARY KEY .
- `Nome` - Aqui, queremos que os valores sejam únicos, afinal, não temos a necessidade de cadastrar um novo sabor de sorvete que já conste na tabela. Além disso, queremos que, ao cadastrar, o valor não seja nulo. Então, como constraints , podemos adicionar UNIQUE e NOT NULL .
- `Código identificador de quem fornece (id)` - Suponha que já possuímos uma tabela onde listamos todas as empresas fornecedoras, e que nessa tabela, os valores estão sendo representados por uma primary key . Então, podemos atribuir como constraint a FOREIGN KEY .

---

## Entidades

Quando se fala de entidades de um banco de dados, estamos normalmente falando de uma tabela que representa algum conceito do mundo real que você quer descrever (pessoa, eventos, acontecimentos) e suas propriedades (altura, horário do evento, nome do acontecimento). A entidade pessoa , por exemplo, pode ter as propriedades de altura, peso e idade. Uma entidade festa pode possuir as propriedades horário do evento, público-alvo e data da festa. Por fim, uma entidade venda pode possuir as propriedades valor da venda, dia da venda, produto vendido etc.

- `Entidade` : Pessoa
- `Propriedades` : Altura, peso, idade.

A entidade é a tabela dentro de um banco de dados e as propriedades fazem parte dessa tabela.

Em alguns desses casos, as entidades são individuais e não se relacionam entre si, porém às vezes elas são ligadas umas com as outras através de relacionamentos. Vamos ver mais sobre isso a seguir.

## Querys

Queries são os comandos digitados dentro de uma janela ou linha de comando, com a intenção de interagir de alguma maneira com uma base de dados. Em banco de dados é possível tanto recuperar dados, quanto alterar, atribuir permissões de acesso e manipulação, dentre outras coisas.

Existem muitos tipos de queries, as principais são:

### DDL

Data Definition Language, são os comandos que lidam com o esquema, a descrição e o modo como os dados devem existir em um banco de dados:

- `CREATE` - Cria banco de dados, tabelas, índices, views, procedures, functions e triggers
- `ALTER` - Altera a estrutura de qualquer objeto
- `DROP` - Permite a deleção de objetos
- `TRUNCATE` - Esvazia os dados de uma tabela, mas mantém a tabela no banco de dados;

### DML

Data Manipulation Language, são os comandos usados para manipular dados. São utilizados para armazenar,modificar, buscar e excluir dados em um banco de dados:

- `SELECT` - Busca dados em um banco de dados;
- `INSERT` - Insere dados em uma tabela;
- `UPDATE` - Altera dados dentro de uma tabela;
- `DELETE` - Deleta dados de uma tabela;

### DCL

Data Control Language, são os comandos que concedem direitos, permissões e outros tipos de controle ao sistema de banco de dados:

- ``GRANT`` - Concede acesso a um usuário;
- ``REVOKE`` - Recome acessos concedidos através do ``GRANT``;

### TCL

Transactionl Control Language, são comandos que lidam com as transações dentro de pesquisas:

- `COMMIT` - Muda as alterações temporárias para permanetes no banco de dados;
- `ROLLBACK` - Desfaz todo o impacto realizado por um comando;
- `SAVEPOINT` - Define pontos para quais uma transação pode voltar. É uma maneira de voltar para pontos específicos da query;
- `TRANSACTION` - Comandos que definem onde, como e em ue escopo as transações são executadas

---

## Operadores em SQL

Existem muitos tipos de operadores em SQL, operadores são sinais que podem interferir nos filtros de uma Query, aumentando ou não os filtros, alguns tipos de operadores são:

    • Relacionais
        ▪ > Maior que
        ▪ <  Menor que
        ▪ >= Maior igual
        ▪ <= Menor igual
        ▪ = Igual á
        ▪ <> Diferente de
        ▪ ===  Identidade, confere se os valores são iguais em grandeza e tipo (Number, string, boolean,...).
---
    • Lógicos
      ▪ NOT Negação
      ▪ AND Conjunção ou “E” lógico
      ▪ OR Disjunção ou “OU” lógico
      ▪ IS Compara com valores booleanos (TRUE, FALSE, NULL)
---
    • Ordem de precedência
      ▪ Parênteses
      ▪ Multiplicação, Divisão
      ▪ Subtração, Adição
      ▪ NOT
      ▪ AND
      ▪ OR

O operador NOT tem preferência sobre o AND e o AND sobre o OR, ou seja, mesmo que o AND venha depois do OR, ele será executado primeiro, o mesmo acontece com NOT e AND. Exemplo:

~~~SQL
SELECT * FROM sakila.payment
WHERE amount = 0.99 OR amout = 2.99 AND staff_id = 2;
~~~

Nesse caso os registros buscados são aqueles nos quais `amount = 2.99` e `staff_id = 2`. Na sequência são buscados os registros nos quis `amount = 0.99`, independente do valor de `staff_id`. O valores serão os resultados dessas duas buscas. Ou seja, a Query será executada como se tivesse os seguintes parênteses: `amount = 0.99 OR (amount = 2.99 AND staff_id = 2)`.

Entretanto, quanto há a adição de parênteses, a coisa muda de figura, os parênteses possuem o maior ordem de precedência, ou seja, o que estiver dentro dos parênteses acontece primeiro. Exemplo:

~~~SQL
SELECT * FROM sakila.payment
WHERE (amount = 0.99 OR amout = 2.99) AND staff_id = 2;
~~~

Primeiramente, a expressão dentro dos parênteses é avaliada, e todos os resultados que satisfazem a condição `amount = 0.99 OR amount = 2.99` são retornados. Na sequência, a expressão do lado direito do `AND` é avaliada, e todos os resultados que satisfazem a condição `staff = 2` são retornados. O `AND` então compara o resultado de ambos os lados e faz com que somente os resultados que satisfazem ambas as condições sejam retornados.

---

## Manipulando strings

O SQL permite a manipulação de strings, ou seja, mexer na formatação quanto ao case da string, seleção de caracteres dentro de uma string, tamanho, entre outros. Para realizar essas manipulações existem os métodos `UCASE()`, `LCASE()`, `REPLACE()`, `LEFT()`, `RIGHT()`, `LENGTH()`, `SUBSTRING()`, dentre outros. Diferente de outras linguagens, em SQL as strings são indexadas a partir do indice 1 e não do 0.

---

## Condições em SQL

Assim como em muitas outras linguagens, SQL também possuem como base para a criação de códigos dinâmicos o uso de condicionais, para isso essa linguagem dispõe de `IF()` e `CASE()`. Quando é feita uma condição ela cria uma nova coluna, para que essa nova coluna tenha um nome próprio é possível usar o comando `AS`, assim ele cria um apelido para a coluna.
Exemplo:

~~~SQL
SELECT first_name, IF(active, 'Cliente Ativo', 'Cliente Inativo') AS status
FROM sakila.customer
LIMIT 20;
~~~

Dessa forma a coluna onde vai aparecer o resultado dessa condição agora terá um nome, que neste caso é `status`.

O `IF()` é mais recomendado para condições simples, para fazer comparações mais complexas é preferível usar o `CASE()`.

---

## Junções de tabelas

Em alguns casos, uma tabela pode não possuir toda a informação necessária. Em função disso, existe a opção de usar os diversos tipos de `JOIN` para combinar em um mesmo resultado registros de duas ou mais tabelas. Esses tipos são: `INNER JOIN` , `LEFT JOIN` e `RIGHT JOIN` , para combinar duas ou mais tabelas, e `SELF JOIN` , quando uma tabela precisa ser combinada consigo mesma. Você verá detalhes de cada um desses tipos de `JOIN` a seguir.

---

## Variáveis

O MySQL possui a funcionalidade de criar e usar variáveis, assim como em outras linguagens de programação.

No MySQL existem três tipos principais de variáveis, sendo elas:

- User-defined variables;
- Local Variables;
- Server System Variables.

A forma mais comum é por meio da User-defined variables que para criar variáveis e atribuir valores a ela, pode ser feito da seguinte maneira:

~~~SQL
SET @exemplo = 'Este é o exemplo';
SELECT @exemplo;
~~~

---

## Tipos de dados

Existem vários tipos de dados no MySQL que vão além de apenas numéricos e strings, esses tipos no MySQL são determinados por meio de algumas características:

- Tipo de valor que representa;
- O espaço ocupado e se possui comprimento fixo ou variável;
- Se os valores podem ser indexados ou não;
- Comparação de valores de um tipo de dado específico pelo MySQL.

Os principais tipos de dados do MySQL são:

### Tipo String

- `VARCHAR` : Uma string não binária de comprimento variável, recebe entre parenteses o tamanho máximo da string. Exemplo: `VARCHAR(50)`. Neste caso é uma string de até 50 caracteres;
- `CHAR` : Uma string não binária (caractere) de comprimento fixo;
- `TEXT` : Uma pequena string não binária.

### Tipo Numérico

- `TYNINT` : Um número inteiro muito pequeno;
- `INT` : Um inteiro padrão;
- `BIGINT` : Um grande número inteiro;
- `DECIMAL` : Um número de ponto fixo.

---

## Blocos de códigos reutilizáveis

Existem formas de ser armazenar blocos de códigos (querys) no MySQL para que elas sejam usadas posteriormente, duas dessas formas são usando as `Stored Procedures` e/ou `Stored Functions`.

`Stored` significa armazenamento e como próprio nome indica, o código fica armazenado, neste caso, no servidor do banco de dados para que possa ser utilizado sem a necessidade de reescrever uma funcionalidade.

Tanto as `Procedures` quanto as `Functions` seguem um padrão de nomenclatura, isso facilita a leitura e a manutenção do código. Exemplo:

~~~SQL
-- Verbo + Resultado
-- Utilizando PascalCase

ObterTotalDeVendas
ExibirRankMaximo
ObterClienteMaisAtivo
CalcularNivelEngajamento
MontarNomeCompleto
~~~

---

## Stored Procedures

Também conhecido como procedimenos armazenados, são procedimentos que estarão armazenados no banco de dados, esses procedimentos são queries que podem ser reutilizadas em vários pontos do banco de dados.

### Pontos Fortes

- Centraliza o código SQL em um servidor de banco de dados, o que possibilita que a manutenção das queries seja feita diretamente no servidor. Assim, as mudanças são refletidas imediatamente em aplicações que utilizam o banco de dados sem haver a necessidade de refazer o deploy;
- Evita a necessidade de reescrever algo específico para cada linguagem, plataforma ou framework;
- Propaga mudanças feitas em uma `stored procedure` imediatamente para todas as aplicações que a usam, reduzindo a necessidade de refatorar o código em todos os ambientes que utilizam o banco de dados.

### Pontos fracos

- Viola ums princípios de `separation of concerns` ou separação de conceitos, que diz respeito a focar em resolver um único problema na sua regra de negócio, dados e apresentação permitindo então estarem separados e desacoplados, uma vez que `stored procedures` podem conter regras de negócio e ficam armazenadas no banco de dados;
- Debugar esse código armazenado é mais difícil;
- Não há como versionar o código de uma stored procedure tão facilmente.

### Estrutura de uma Stored Procedure

~~~SQL
USE banco_de_dados; -- Obrigatório para criar a procedure no banco correto
DELIMITER $$ -- Definindo delimitador

CREATE PROCEDURE nome_da_procedure(@parametro1, parametro2, ..., parametroN) -- Parâmetros
BEGIN -- Dilimita o início do código SQL

END $$ -- Delimita o final do código SQL

DELIMITER ; -- Muda o delimitador de volta para ; * O espaço entre o DELIMITER e o ; é necessário
~~~

### Elementos de uma Stored Procedure

1. `Delimiter` - A palavra-chave `DELIMITER` é usada para definir qual símbolo representa o final da procedure declarada. Aqui estamos usando `$$` , porém é permitido usar outros símbolos como `//` ou até mesmo ; para retornar ao DELIMITER como padrão default. **Atenção**, não é permitido usar `\` , pois é um caractere especial do MySQL. O `DELIMITER` precisa ser usado para que o MySQL não interprete o primeiro ponto e vírgula encontrado como o final da declaração na sua procedure;
2. `Variáveis`;
3. `Tipos de dados`;

### Existem 4 tipos de Procedures

    1. Procedures sem parâmetros;
    2. Procedures com parâmetro IN;
    3. Procedures com parâmetro OUT;
    4. Procedures com parâmetro INOUT.

#### **Procedures sem parâmetros**

Normalmente é utilizada para realizar queries mais simples. Exemplo:

~~~SQL
USE sakila;
DELIMITER $$

CREATE PROCEDURE ShowAllActors()
BEGIN
  SELECT * FROM sakila.actor;
END $$

DELIMITER ;

-- Como usar:

CALL ShowAllActors();
~~~

Neste exemplo a `Query` retorna todos os atores da tabela `actor`.

#### **Procedure com parâmetros de entrada (IN)**

Para criar procedures com funcionalidades mais elaboradas, podemos passar parâmetros de entrada. Ao definir um parâmetro do tipo IN , podemos usá-lo e modificá-lo dentro da nossa procedure.

~~~SQL
USE sakila;
DELIMITER $$

CREATE PROCEDURE ShowActorsWithSyllable(IN syllable VARCHAR(50))
BEGIN
  SELECT *
    FROM sakila.actor
    WHERE first_name LIKE CONCAT('%', syllable, '%');
END $$

DELIMITER ;

-- Como usar:

CALL ShowActorsWithSyllable('lope');
~~~

Neste exemplo a `Query` retorna todos os resultados de atores com a sílaba `lope` dentro da tabela `actor`.

#### **Procedure com parâmetros de saida (OUT)**

O parâmetro `OUT` é útil quando você precisa que algo seja avaliado ou encontrado dentro de uma query e te retorne esse valor para que algo adicional possa ser feito com ele.

~~~SQL
USE sakila;
DELIMITER $$

CREATE PROCEDURE ShowAverageRentalDurationOfMovie(
  IN film_name VARCHAR(300),
    OUT media_de_aluguel_em_dias DOUBLE
)
BEGIN
  SELECT AVG(rental_duration) INTO media_de_aluguel_em_dias
    FROM sakila.film
    WHERE title = film_name;
END $$

DELIMITER ;

-- Como usar:

CALL ShowAverageRentalDurationOfMovie('ACADEMY DINOSAUR', @media_de_dias);
SELECT @media_de_dias;

~~~

Neste caso a `Query` está retornando o número em média de dias de aluguel de um filme, o nome desse filme é passado como primeiro parâmetro para a `Procedure` e o resultado é inserido na variável passada como segundo parâmetro para a `Procedure`.

#### **Procedure com parâmetros de entrada-saida (IN-OUT)**

O `IN-OUT` deve ser usado quando é necessário que um parâmetro possa ser modificado tanto antes como durante a execução de um `Procedure`.

~~~SQL
USE sakila;
DELIMITER $$

CREATE PROCEDURE NameGenerator(INOUT film_name VARCHAR(300))
BEGIN
  SELECT CONCAT('ULTRA ', film_name, ' THE BEST MOVIE OF THE CENTURY')
    INTO film_name;
END $$

DELIMITER ;

-- Como usar:

SELECT 'ACE GOLDFINGER' INTO @movie_title;
CALL NameGenerator(@movie_title);
SELECT @movie_title;
~~~

Neste caso a variável `movie_title` está recebendo o nome do filme e depois sendo passada como parâmetro para a `Procedure` `NameGenerator`, onde a variável está sendo modificada e recebendo um novo valor, valor esse que é exibido no final da `Query`.

---

## Stored Functions

Na área de programação, existe uma boa prática chamada DRY (Don't Repeat Yourself) que, em resumo, sugere que você não se repita ou reescreva o mesmo código várias vezes.

Nesse ponto, existe uma das principais ferramentas para combater esse problema no SQL: as `stored functions` .
Através delas, é possível encapsular as queries usadas mais frequentemente dentro de um bloco de código nomeado e parametrizável.

`Stored Functions` podem ser executadas com o comando `SELECT`. Ao criá-las, é necessário definir o tipo de retorno que sua função possui.

### Tipos de retorno comuns

- `DETERMINISTIC` - Sempre retorna o mesmo valor ao receber os mesmos dados de entrada;
- `READS SQL DATA` - Indica para o MySQL que sua função somente lerá dados.

### Estrutura padrão de uma Stored Function

~~~SQL
USE banco_de_dados; -- Obrigatório  para criar a função no banco correto
DELIMITER $$

CREATE FUNCTION nome_da_function(parametro1, parametro2, ..., parametroN)
RETURNS tipo_de_dado tipo_de_retorno
BEGIN
  query_sql
    RETURN resultado_a_ser_retornado;
END $$

DELIMITER ;
~~~

Exemplo de uma `Stored Function` que exibe a quantidade de filmes em que um determinado ator ou atriz atuou:

~~~SQL
USE sakila;
DELIMITER $$

CREATE FUNCTION MoviesWithActor(actor_id INT)
RETURNS INT READS SQL DATA
BEGIN
  DECLARE movie_total INT;
    SELECT COUNT(*)
    FROM sakila.film_actor
    WHERE sakila.film_actor.actor_id = actor_id INTO movie_total;
    RETURN movie_total;
END $$

DELIMITER ;

-- Como usar:

SELECT MoviesWithActor(1);
~~~

Exemplo de uma `Stored Function` que exibe o nome completo de um ator ou de uma atriz, dado seu id como parâmetro:

~~~SQL
USE sakila;
DELIMITER $$

CREATE FUNCTION GetFullName (id INT)
RETURNS VARCHAR(200) READS SQL DATA
BEGIN
  DECLARE full_name VARCHAR(200);
    SELECT CONCAT(first_name, ' ', last_name)
    FROM sakila.actor
    WHERE actor_id = id
    LIMIT 1
    INTO full_name;
    RETURN full_name;
END $$

DELIMITER ;

SELECT GetFullName(51);
~~~

---

## Triggers

`Triggers` são blocos de código SQL que são disparados em reação a alguma atividade que ocorre no banco de daos. Eles podem ser disparados em dois momentos distintos, e é possível definir condições para esse disparo.

### Momentos em que um Trigger pode ser disparado

- `BEFORE` - antes que alguma ação seja executada;
- `AFTER` -  depois que alguma ação seja executada;

### O que pode ativar um Trigger

- `INSERT`;
- `UPDATE`;
- `DELETE`.

### O que pode ser acessado dentro de um Trigger

- O valor `OLD` de uma coluna: valor presente em uma coluna antes de uma operação;
- O valor `NEW` de uma coluna: valor presente em uma coluna após uma operação.

### Em quais operações os valores OLD e NEW estão disponíveis?

![Demonstração de disponibilidade de OLD e NEW][O&N]

[O&N]: ../imagens/old_and_new_trigger_use.png

### Sintaxe

~~~SQL
DELIMITER $$

CREATE TRIGGER nome_do_trigger
[BEFORE | AFTER] [INSERT | UPDATE | DELETE] ON tabela
FOR EACH ROW
BEGIN
  -- o código SQL entra aqui
END $$

DELIMITER ;
~~~

---

## Modelando um banco de dados

    Para facilitar no entendimento e explicação do conteúdo, será feita uma abstração usando um **Catálogo de Álbuns Musicais**, que iremos tratar como sendo um banco de dados e nesse banco de dados teremos o que chamamos de **tabelas**. Uma tabela será chamada de *albuns_musicais*, onde as informações de cada álbum a serem armazenadas são:

    - Título;
    - Preço;
    - Estilo Musical;
    - Canções.

    Teremos também uma tabela para os dados de cada artistas e criaremos um relacionamento entre tabelas.

Um banco de dados pode ser modelado e criado a partir do 0, para realizar esses processos existem alguns passos que devem ser seguidos, é mais um fluxo criativo, esse fluxo é:

    1. Identificar as entidades , atributos e relacionamentos com base na descrição do problema;

    2. Construir um diagrama entidade-relacionamento para representar as entidades encontradas no passo 1;

    3. Criar um banco de dados para conter suas tabelas;

    4. Criar e modelar tabelas tendo o diagrama do passo 2 como base.

### Identificando entidades, atributos e relacionamentos

Antes de começar a identificar, precisamos saber o que são:

- `Entidades` - São uma representação de algo do mundo real dentro do banco de dados. Elas normalmente englobam toda uma ideia e são armazenadas em formato de tabelas em um banco de dados. Exemplo:

  - **Entidade 1**: `Álbum`;
  - **Entidade 2**: `Artista`;
  - **Entidade 3**: `Estilo Musical`;
  - **Entidade 4**: `Canção`.
  ---
- `Atributos` - Os atributos são tudo aquilo que pode ser usado para descrever algo. Por exemplo, uma entidade pessoa pode ter nome, altura, peso e idade.

  - **Álbum**: `album_id`, `titulo`, `preco`, `estilo_id` e `artista_id`;
  - **Artista**: `artista_id` e `nome`;
  - **Estilo Musical**: `estilo_id` e `nome`;
  - **Canção**: `cancao_id`, `nome` e `album_id`.
  ---
- `Relacionamentos` - Os relacionamentos servem para representar como uma entidade deve estar ligada com outra(s) no banco de dados. Há três tipos de relacionamentos possíveis em um banco de dados, que são:

  - **Relacionamento Um para Um (1..1)**: Nesse tipo de relacionamento, uma linha da `Tabela A` deve possuir apenas uma linha correspondente na `Tabela B` e vice-versa. Apesar de ser possível inserir essas informações em apenas uma tabela, esse tipo de relacionamento é usado normalmente quando se quer dividir as informações de uma tabela maior em tabelas menores, evitando que as tabelas tenham dezenas de colunas. Veja o exemplo abaixo:
  
    ![Exemplo de relacionamento 1 pra 1][1P1]

  - **Relacionamento Um para Muitos ou Muitos para Um (1..N)**: Esse é um dos tipos mais comuns de relacionamento. Em cenários assim, uma linha na `Tabela A` pode ter várias linhas correspondentes na `Tabela B` , mas uma linha da `Tabela B` só pode possuir uma linha correspondente na `Tabela A` . Veja o exemplo abaixo:

    ![Exemplo de relacionamento 1 pra muitos][1PN]

  - **Relacionamento Um para Muitos ou Muitos para Um (1..N)**: O relacionamento muitos para muitos acontece quando uma linha na Tabela A pode possuir muitas linhas correspondentes na Tabela B e vice-versa.
  Esse tipo de relacionamento pode ser visto também como dois relacionamentos um para muitos ligados por uma tabela intermediária, como é o caso da tabela filme_ator . Pode-se chamar essa tabela intermediária de tabela de junção . Ela é usada para guardar informações de como as tabelas se relacionam entre si. Desta maneira, quando se quer demonstrar que um filme pode contar com vários atores e também que os atores podem atuar em vários filmes, surge a necessidade de um relacionamento muitos para muitos. Veja o exemplo abaixo:
  
    ![Exemplo de relacionamento 1 pra muitos][NPN]

  ---
  
[1P1]: ../imagens/relacionamento_1P1.png
[1PN]: ../imagens/relacionamento_1PN.png
[NPN]: ../imagens/relacionamento_NPN.png

### Construindo um diagrama entidade-relacionamento

No segundo passo, será construído um diagrama entidade-relacionamento para representar as entidades encontradas no passo 1. É preciso montar um diagrama de relacionamento básico que demonstra como uma entidade é relacionada com a outra, usando o modelo `EntidadeA` + verbo + `EntidadeB` .

---

## Normalização de tabelas

---

## Clonando tabelas

Ao trabalhar com tabelas, as vezes é necessário criar algumas tabelas com estruturas bem parecidas, o que torna o trabalho bem repetitivo. Entretanto, existe um comando bem simples e tranquilo para resolver tal problema, que é o `CREATE TABLE nome_para_nova_tabela LIKE tabela_a_ser_clonada;`, ao usar esse comando, uma tabela com a estrutura exatamente igual a original será criada, chave primária, chave estrangeira, tipos, restições etc... Tudo usando somente 1 linha de código.

**OBSERVAÇÃO:** Esse comando não copia os dados, somente a estrutura e caso não seja especificado qual banco de dados utilizar, a nova tabela será inserida no banco de dados que estiver ativo no momento da execução, sendo assim, sempre especifique o banco de dados antes. Exemplo:

~~~SQL
-- Sintaxe:
USE nome_do_banco_de_dados;
CREATE TABLE nome_para_nova_tabela LIKE tabela_a_ser_clonada;

-- Exemplo prático:
USE sakila;
CREATE TABLE actor_clone LIKE sakila.actor;
~~~

---

## VIEW

Uma `VIEW` nada mais é do que uma tabela temporária no banco de dados, que pode ser consultada como qualquer outra. Porém, por ser uma tabela temporária, ela é criada a partir de uma `Query`. Uma `VIEW` permite:

- Ter uma tabela que pode ser usada em relatórios;
- Ter uma tabela para usar como base para montar novas queries;
- Reduzir a necessidade de recriar queries utilizadas com frequência.

~~~SQL
-- Sintaxe:
USE nome_do_banco_de_dados;
CREATE VIEW nome_da_view AS query;

-- Exemplo prático:
USE sakila;
CREATE VIEW top_10_customers AS
  SELECT c.customer_id, c.first_name, SUM(p.amount) AS total_amount_spent
  FROM sakila.payment p
  INNER JOIN sakila.customer c ON p.customer_id = c.customer_id
  GROUP BY customer_id
  ORDER BY total_amount_spent DESC
  LIMIT 10;
~~~

Nesse exemplo é uma query para exibir os top 10 clientes que mais compram com a empresa. Para acessar a informação é só fazer uma query de consulta, sem precisa montar a query acima de novo. Exemplo:

~~~SQL
SELECT * FROM top_10_customers;
~~~

Para excluir uma `VIEW` é só usar esse comando:

~~~SQL
DROP VIEW nome_da_view;
~~~

---

## Alterando Tabelas

Algo extremamente comum durante o ciclo de desenvolvimento de software é a necessidade constante de fazer melhorias na estrutura do banco de dados. As tabelas são uma dessas estruturas que podem sofrer alterações.

Para isso existem comandos para adicionar novas colunas (`ADD COLUMN`), mdificar propriedades de uma coluna (`MODIFY`), alterar o tipo e o nome das colunas (`CHANGE`) e excluir colunas (`DROP`).

Uma `Query` para alteração de coluna começa com `ALTER TABLE` seguida do nome da tabela, o tipo de alteração que será feita, o nome da coluna altera e a alteração que será feita. Exemplo:

~~~SQL
ALTER TABLE noticia ADD COLUMN data_postagem date NOT NULL;
~~~

Neste caso a coluna `data_postagem` está sendo adicionada na tabela `noticia` e essa coluna está recebendo a constrain `NOT NULL`;

Outros usos do `ALTER TABLE`:

~~~SQL
-- Modificar o tipo e propriedades de uma coluna
ALTER TABLE noticia MODIFY noticia_id BIGINT;

-- Adicionar incremento automático a uma coluna
-- (especifique o tipo da coluna + auto_increment)
ALTER TABLE noticia MODIFY noticia_id BIGINT auto_increment;

-- Alterar o tipo e nome de uma coluna
ALTER TABLE noticia CHANGE historia conteudo_postagem VARCHAR(1000) NOT NULL;

-- Dropar/Excluir uma coluna
ALTER TABLE noticia DROP COLUMN data_postagem;

-- Adicionar uma nova coluna após outra
ALTER TABLE noticia ADD COLUMN data_postagem DATETIME NOT NULL AFTER titulo;
~~~

---

## DROPando uma tabela

Dropar ou excluir uma tabelaé fácil, é só usar o comando `DROP TABLE`. Exemplo:

~~~SQL
DROP TABLE nome_da_tabela;
~~~

Entretanto, não possível dropar uma tabela que é referenciada por uma restrição de chave estrangeira. A chave estrangeira ou a tabela que a contém deve ser excluída antes. Ao tentar dropar uma tabela que é referenciada por outra, a seguinte mensagem de erro aparecerá:

~~~SQL
Error Code: 3730. Cannot drop table 'table' referenced by a foreign key constraint 'fk_key' on table 'table2'
~~~

Onde `table`, `fk_key` e `table2` serão substituídos pela tabela que foi tentada apagar, a chave estrangeira a qual a tabela está ligada e a tabela onde a chave estrangeira se encontra, respectivamente.

O impedimento da exclusão de um tabela dessa forma acontece por conta da **Integridade referencial**, que é uma propriedade que afirma que todas as referências de chaves estrangeiras devem ser válidas.

## Comandos em SQL

### Filtros

- `CONCAT` - Concatena os resultados de uma Query;
- `DISTINCT` - Filtra resultados iguais de uma Query, exibindo somente 1 representante das repetições, quanto mais colunas adicionar, mais específico fica esse filtro, ele vai comparar todas as colunas e mostrar somente os resultados que não sejam iguais em todas essas colunas;
- `LIMIT` - Limita o número de resultados de uma Query, é bom para Queries em tabelas com muitas linhas;
- `OFFSET` - Determina um salto na quantidade de linhas de uma Query, caso queira pular para o 5 resultado é só usar `OFFSET` 4, o `OFFSET` vai pular os 4 primeiros resultados e exibir do 5 pra frente. Normalmente é usado com o `LIMIT`. Ex: `SELECT * FROM sakila.rental LIMIT 10 OFFSET 5;`. A Query vai até a tabela `sakila.rental` e vai trazer os 10 resultados após o 5 resultado, ou seja, do 6 ao 15.
- `ORDER BY` - Ordena os resultados de uma Query em ordem crescente ou decrescente. Assim como o `DISTINCT` é cumulativo por colunas. Ex: `SELECT * FROM sakila.adress ORDER BY district ASC, address DESC;`.
- `WHERE` - Ordena os resultados de uma Query por ***onde*** é atendida as requisições dos filtros
- `LIKE` - Cria um filtro dinâmico, onde só é preciso passar uma parte do conteúdo a ser buscado, para isso é necessário o uso de um coringa, o `%`. Exemplo: `SELECT * FROM sakila.film WHERE title LIKE '%don';`. Dessa forma todos os filmes com títulos terminados em don aparecerão como resultado. O `%` pode ser usado tanto antes, quanto depois, quanto antes e depois do trecho a ser pesquisado. Alem disso existe outro coringa, o `_` (underscore) que representa um caractere. Ex: `SELECT * FROM sakila.film WHERE title LIKE E_%;`. Assim todos os títulos começados com E e com no mínimo 3 caracteres serão exibidos como resultado.
- `IN` - Procura um resultado dentro da coluna. Exemplo: `SELECT * FROM film WHERE first_name LIKE ('PENELOPE', 'NICK', 'ED');` ou `SELECT * FROM sakila.customer WHERE customer_id in (1, 2, 3, 4, 5);`.
- `BETWEEN` - Usado para encontrar valores em uma faixa de valores, sejam strings ou números. O `BETWEEN` não traz somente os valores entre os dois parâmetros, ele trás os que forem iguais aos 2 parâmetros também. Exemplo:

~~~SQL
SELECT * FROM sakila.language
WHERE name BETWEEN 'Italian' AND 'Mandarin'
ORDER BY name;
~~~

Para usar o BETWEEN com datas, basta que seja digitado o valor no formato padrão da data, que é YYYY-MM-DD HH:MM:SS , sendo os valores de horas, minutos e segundos opcionais. Exemplo:

~~~SQL
SELECT rental_id, rental_date FROM sakila.rental
WHERE rental_date
BETWEEN '2005-05-27' AND '2005-07-17';
~~~

- `GROUP BY` - Agrupa registros pelo valor de uma coluna, exibindo apenas um registro de cada valor.
- `HAVING` - Usado para filtrar os resultados agrupados, como um tipo de condição. Exemplo:

~~~SQL
SELECT first_name, COUNT(*)
FROM sakila.actor
GROUP BY first_name
HAVING COUNT(*) > 2;
~~~

### Manipuladores de string

- `UCASE()` - Muda o case da string para maiúsculo. Exemplo: `SELECT UCASE('Oi, eu sou uma string');`.
- `LCASE()` - Muda o case da string para minúsculo. Exemplo: `SELECT LCASE('Oi, eu sou uma string');`.
- `REPLACE()` - Muda uma ou mais palavras de uma string, recebe 3 parâmetros, 1. A string original, 2. Qual parte da string será mudada, 3. Pelo que a string será mudada. Exemplo: `SELECT REPLACE('Oi, eu sou uma string', 'string', 'cadeia de caracteres');`.
- `LEFT()` - Seleciona os caracteres da string a partir da esqueda, recebe como segundo parâmetro o caractere limite. Exemplo: `SELECT LEFT('Oi, eu sou uma string', 3);`.
- `RIGHT()` - Seleciona os caracteres da string a partir da direita, recebe como segundo parâmetro o caractere limite. Exemplo: `SELECT RIGHT('Oi, eu sou uma string', 6);`.
- `LENGTH()` - Conta quantos caracteres tem na string. Exemplo: `SELECT LENGTH('Oi, eu sou uma string');`.
- `SUBSTRING()` - Extrai parte de uma string de acordo com o índice de um caractere inicial e a quantidade de caracteres a extrair. Exemplo: `SELECT SUBSTRING('Oi, eu sou uma string', 5, 2);`. Entretanto se a quantidade de caracteres a extrair não for definida, então a string será extraída do índice inicial definido, até o seu final. Exemplo: `SELECT SUBSTRING('Oi, eu sou uma string', 5);`

### Condicionais

- `IF()` - Usado para uma condição binária simples, 0 ou 1. Exemplo:

~~~SQL
SELECT IF(idade >= 18, 'Maior de idade', 'Menor de Idade')
FROM PESSOAS;`
~~~

- `CASE()` - Usado para condições mais complexas, onde existem muitas opções e não só verdadeiro ou falso. Exemplo:

~~~SQL
SELECT
    nome,
    nivel_acesso,
    CASE
        WHEN nivel_acesso = 1 THEN 'Nível de acesso 1'
        WHEN nivel_acesso = 2 THEN 'Nível de acesso 2'
        WHEN nivel_acesso = 3 THEN 'Nível de acesso 3'
        ELSE 'Usuário sem acesso'
    END AS nivel_acesso
FROM permissoes_usuario;
~~~

O `WHEN` diz quando a condição é atendida então, `THEN`, algo é executado, se nenhuma das condições for atendida, `ELSE` e o `END` diz que deve terminar a condição ali e que a coluna dever ter o nome que foi escrito após o `AS`, o `FROM` diz de onde virão os dados iniciais para a comparação.

### Funções matemáticas

- `DIV` - Retorna o resultado inteiro de uma divisão, ignorando as casas decimais de um número. Exemplo: `SELECT 10 DIV 3;`. Nesse caso o retorno é igual a 3.
- `MOD` - Retorna o resto deuma divisão como resultado. Exemplo: `SELECT 10 MOD 3`. Nesse caso o retorno é igual a 1.
- `ROUND()` - Retorna o valor arredondado. Exemplo: `SELECT ROUND(10.4925);`. Neste caso retorna 10.
- `CEIL()` - Retorna o valor arredondado pra cima. Exemplo: `SELECT CEIL(10.49);`. Neste caso retorna 11.
- `FLOOR()` - Retorna o valor arredondado pra cima. Exemplo: `SELECT FLOOR(10.51);`. Neste caso retorna 10.
- `POW()` - Retorna o valor do primeiro parâmetro elevado pelo segundo. Exemplo: `SELECT POWER(2, 4)`. Neste caso retorna 16.
- `SQRT()` - Retorna a raiz quadrada. Exemplo: `SELECT SQRT(9)`. Neste caso retorna 3.
- `RAND()` - Retorna um valor aletório.

### Trabalhando com datas

- `DATE` - Possui apenas data, no formato YYYY-MM-DD na faixa de 1001-01-01 até 9999-12-31. Exemplo:`SELECT * FROM sakila.payment WHERE DATE(payment_date) = '2005-07-31';`
- `DATETIME` - Possui data e tempo, no formato YYYY-MM-DD HH:MM:SS com a faixa de 1000-01-01 00:00:00 até 9999-12-31 23:59:59. Exemplo: `SELECT * FROM sakila.payment WHERE DATE(payment_date) = '2005-07-31 00:00:00';`. É possivel combiar operadores com essas funções.
- `YEAR` - Possui o ano.
- `MONTH` - Possui o mês.
- `DAY` - Possui o dia.
- `HOUR` - Possui a hora.
- `MINUTE` - Possui o minuto.
- `SECOND` - Possui o segundo.

### Funções de agregação

- `AVG()` - Retorna a média dos valores entres os registros. Exemplo: `SELECT AVG(replacement_cost) FROM sakila.film;`.
- `MIN()` - Retorna o menor valor encontrado. Exemplo: `SELECT MIN(replacement_cost) FROM sakila.film;`.
- `MAX()` - Retorna o maior valor encontrado. Exemplo: `SELECT MAX(replacement_cost) FROM sakila.film;`.
- `SUM()` - Retorna a soma de todos os registros. Exemplo: `SELECT SUM(replacement_cost) FROM sakila.film;`.
- `COUNT()` - Retorna todos os registros encontrados. Exemplo: `SELECT COUNT(replacement_cost) FROM sakila.film;`.

### Junções

- `INNER JOIN` - Retorna todos os resultados em que a condição da cláusula `ON` for satisfeita. É a interseção entre 2 tabelas. Exemplo:

~~~SQL
SELECT t1.coluna, t2.coluna
FROM tabela1 AS t1
INNER JOIN tabela2 AS t2
ON t1.coluna_em_comum = t2.coluna_em_comum;
~~~

- `LEFT JOIN` - Retorna todos os resultados da tabela da esquerda e valores correspondentes da tabela da direita, caso existam . Valores que não possuem correspondentes são exibidos como nulos. Exemplo:

~~~SQL
USE sakila;
SELECT
  c.customer_id,
  c.first_name,
  a.actor_id,
  a.first_name
FROM customer AS c
LEFT JOIN actor AS a
ON c.last_name = a.last_name
ORDER BY c.last_name;
~~~

- `RIGHT JOIN` - Retorna todos os resultados da tabela da direita e valores correspondentes da tabela da esquerda, caso existam . Valores que não possuem correspondentes são exibidos como nulos. Exemplo:

~~~SQL
USE sakila;
SELECT
  c.customer_id,
  c.first_name,
  a.actor_id,
  a.first_name
FROM customer AS c
RIGHT JOIN actor AS a
ON c.last_name = a.last_name
ORDER BY c.last_name;
~~~

- `SELF JOIN` - Há certos cenários onde é necessário fazer comparações dentro de uma mesma tabela, para isso usamos o SELF JOIN, esse tipo de JOIN junta uma tabela nela mesma por meio de comparação entre 2 clones da mesma tabela. A forma de montar a Query é a mesma, só mudando a forma da comparação. Exemplo:

~~~SQL
SELECT
  t1.title,
  t1.replacement_cost,
  t2.title,
  t2.replacement_cost
FROM sakila.film AS t1, sakila.film AS t2
WHERE t1.length = t2.length;
~~~

- `UNION` - Faz a união de duas tabelas e no processo remove os dados duplicados. Para que funcione da forma correta, é necessário que o número de colunas de cada tabela sejam iguais. Para garantir que todos os filtros e ordenações aconteçam de forma certa, cada uma das Querys das tabelas são envolvidades por parênteses. Exemplo:

~~~SQL
(SELECT first_name, last_name, '-' AS 'customer_id' FROM sakila.actor)
UNION
(SELECT first_name, last_name, customer_id FROM sakila.customer)
ORDER BY first_name;
~~~

- `UNION ALL` - Faz a união de duas tabelas, mas não remove os dados duplicados. Para que funcione da forma correta, é necessário que o número de colunas de cada tabela sejam iguais. Para garantir que todos os filtros e ordenações aconteçam de forma certa, cada uma das Querys das tabelas são envolvidades por parênteses. Exemplo:

~~~SQL
(SELECT first_name, last_name FROM sakila.actor)
UNION ALL
(SELECT first_name, last_name FROM sakila.staff)
ORDER BY first_name;
~~~

- `EXISTS` - Retornar os registros da tabela A que possuem um relacionamento com os registros da tabela B.

### Alterar Tabelas

- `ADD COLUMN` - Adiciona uma nova coluna. Exemplo: `ALTER TABLE noticia ADD COLUMN data_postagem date NOT NULL`
- `MODIFY` - Modifica o tipo e prorpriedade de uma coluna. Exemplo:

~~~SQL
-- Modificar o tipo e propriedades de uma coluna
ALTER TABLE noticia MODIFY noticia_id BIGINT;

-- Adicionar incremento automático a uma coluna
-- (especifique o tipo da coluna + auto_increment)
ALTER TABLE noticia MODIFY noticia_id BIGINT auto_increment;
~~~

- `CHANGE` - Altera o tipo e o nome de uma coluna. Exemplo: `ALTER TABLE noticia CHANGE historia conteudo_postagem VARCHAR(1000) NOT NULL;`
- `DROP COLUMN` - Exclui uma coluna de uma tabela. Exemplo: `ALTER TABLE noticia DROP COLUMN data_postagem;`
- `SHOW COLUMNS` - Mostra as colunas de uma tabela. Exemplo: `SHOW COLUMNS FROM sakila.noticia;`
- `DROP TABLE` - Exclui uma tabela existe, desde que essa tabela não tenha uma chave estrangeira, se tiver, é necessário excluir a tabela origem da chave estrangeira para depois excluir a tabela que você quer, ou caso não queira perder a tabela origem da chave estrangeira, é necessário excluir a coluna da chave estrangeira antes de apagar a tabela.
