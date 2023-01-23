# SQL Database

## USE

- O `USE` serve especificar o banco de dados(quando há mais de um) antes de realizar uma query:

``` SQL
USE [database-name];
```

- Exemplo:

``` SQL
USE Sakila;
```

## SELECT

- No trabalho com banco de dados e SQL, a tarefa mais comum é solicitar dados de uma ou mais tabelas e exibi-los. A instrução SELECT faz isso.
No entanto, SELECT pode fazer muito mais que simplesmente recuperar e exibir dados.

### Recuperando dados

- O `SELECT` serve para listarmos dados dos campos(colunas) especificados(ou todos com o `*` - *placeholder* que especifica todas as colunas) de uma determinada tabela:

``` SQL
USE [database-name];

SELECT * FROM [table-name];
-- OR
SELECT [column-name/columns-name] FROM [table-name];
```

- Exemplos:

``` SQL
USE Sakila;

SELECT * FROM actor; -- trás todos os campos
```

``` SQL
USE Sakila;

SELECT actor_id, first_name, last_name FROM actor; -- trás somente os campos especificados(actor_id, first_name, last_name)
```

### Expressões em instruções SELECT

- A instrução SELECT pode fazer muito mais que apenas selecionar colunas. Podemos efetuar `cálculos` em uma ou mais colunas e incluí-los no resultado da consulta. Exemplo:

``` SQL
USE Sakila;

SELECT payment_id, customer_id, amount, amount * 1.07 AS taxed_price 
FROM payment;
```

**Obs.:** A coluna `taxed_price` foi calculada dinamicamente na consulta. Essa coluna não é armazenada na tabela; em vez disso, é calculada e exibida sempre que executamos a consulta.
Demos um nome ao valor calculado usando uma instrução `AS`(conhecido como *alias*).

- Podemos também fixar uma arredondamento em `taxed_price` de duas casas deimais com a função `round()` - que aceita dois argumentos separados por vírgula: o valor a ser arredondado e o número de casas decimais do arredondamento -. Exemplo:

``` SQL
USE Sakila;

SELECT payment_id, customer_id, amount, round(amount * 1.07, 2) AS taxed_price 
FROM payment;
```

## ORDER BY

- O `ORDER BY` serve para ordenarmos os dados dos campos especificados(ou todos com o `*`.) de uma determinada tabela por um determinado campo(coluna) de forma decrescente(`DESC`) e crescente(`ASC` - padrão):

``` SQL
USE [database-name];

SELECT * FROM [table-name]
ORDER BY [column-name];
-- OR
SELECT [column-name/columns-name] FROM [table-name]
ORDER BY [column-name];
```

- Exemplos:

``` SQL
USE Sakila;

SELECT * FROM actor -- trás todos os campos
ORDER BY first_name; -- ordenado pelo campo first_name de forma crescente(ASC - padrão)
```

``` SQL
USE Sakila;

SELECT actor_id, first_name, last_name FROM actor -- trás somente os campos especificados(actor_id, first_name, last_name)
ORDER BY first_name DESC; -- ordenado pelo campo first_name de forma decrescente(DESC)
```

## WHERE

- No trabalho com dados, uma tarefa muito comum é a filtragem de registros de acordo com critérios, o que pode ser feito com uma instrução WHERE.

### Filtrando registros

- O `WHERE` serve para adicionarmos uma condição na busca dados especificando um campo ou mais(coluna ou colunas) e realizando uma comparação:

``` SQL
USE [database-name];

SELECT * FROM [table-name]
WHERE [column-name] = [value] -- podemos usar =, <, >, <=, >=
-- OR
SELECT [column-name/columns-name] FROM [table-name]
WHERE [column-name] = [value] 
```

- Exemplos:

``` SQL
USE Sakila;

SELECT * FROM actor -- trás todos os campos
WHERE actor_id = 100; -- trás o registro que contém id igual a 100
```

``` SQL
USE Sakila;

SELECT actor_id, first_name, last_name FROM actor -- trás somente os campos especificados(actor_id, first_name, last_name)
WHERE actor_id = 100; -- trás o registro que contém id igual a 100
```

- Inversamente, podemos usar o `!=` ou `<>` para obter todos exceto os atores com id igual a 100: 

``` SQL
USE Sakila;

SELECT actor_id, first_name, last_name FROM actor -- trás somente os campos especificados(actor_id, first_name, last_name)
WHERE actor_id <> 100; -- trás todos os registros que contém id diferente que 100
```

- Também podemos usar os operadores de comparação `<`, `>`, `<=`, `>=`. Exemplo:

``` SQL
USE Sakila;

SELECT actor_id, first_name, last_name FROM actor -- trás somente os campos especificados(actor_id, first_name, last_name)
WHERE actor_id <= 10; -- trás todos os registros que contém id menor ou igual que 10
```

- Também podemos qualificar intervalos inclusivos("inclusivo" significa que os valores especificados estão incluídos no resultado) usando uma instrução `BETWEEN`. Exemplo:

``` SQL
USE Sakila;

SELECT actor_id, first_name, last_name FROM actor -- trás somente os campos especificados(actor_id, first_name, last_name)
WHERE actor_id BETWEEN 10 and 20; -- traś todos os registros que contém id's de 10 até 20
```

### Instruções AND, OR e IN

- Uma expressão `BETWEEN` pode ser expressa alternativamente com o uso das expressões maior ou igual a(>=) e menor ou igual a(<=) e uma instrução `AND`. É um pouco mais verboso, mas demostra que podemos usar duas condições com a instrução `AND`. Exemplo:

``` SQL
USE Sakila;

SELECT actor_id, first_name, last_name FROM actor -- trás somente os campos especificados(actor_id, first_name, last_name)
WHERE actor_id >= 10 AND actor_id <= 20; -- traś todos os registros que contém id's de 10 até 20
```

- Também temos a opção de usar `OR`. Uma instrução `OR`, pelo menos um dos critérios deve ser atendido para o registro se qualificar. Exemplo:

``` SQL
USE Sakila;

SELECT actor_id, first_name, last_name FROM actor -- trás somente os campos especificados(actor_id, first_name, last_name)
WHERE actor_id = 10 OR actor_id = 20; -- traś o registro que contém id igual a 10 ou id igual a 20
```

- Uma maneira mais eficiente de fazer isso é usando uma instrução `IN` que fornece uma lista de valores. Exemplo:

``` SQL
USE Sakila;

SELECT actor_id, first_name, last_name FROM actor -- trás somente os campos especificados(actor_id, first_name, last_name)
WHERE actor_id IN (10, 20); -- traś o registro que contém id igual a 10 ou id igual a 20
```

- Se quiséssemos todos os dados exceto os relativos aos id's 10 e 20, poderíamos usar o `NOT IN`. Exemplo:

``` SQL
USE Sakila;

SELECT actor_id, first_name, last_name FROM actor -- trás somente os campos especificados(actor_id, first_name, last_name)
WHERE actor_id NOT IN (10, 20); -- traś o registro que contém id igual a 10 ou id igual a 20
```

### Usando WHERE com texto

- As regras para qualificação de campos de texto seguem a mesma estrutura, embora haja diferenças sutis. Podemos usar instruções `=`, `AND`, `OR` e `IN` com texto. No entanto, ao usar texto(string), é preciso inserir *literais* em aspas simples. Exemplo:

``` SQL
USE Sakila;

SELECT actor_id, first_name, last_name FROM actor -- trás somente os campos especificados(actor_id, first_name, last_name)
WHERE first_name = 'NICK'; -- traś os registros que contém o primeiro nome igual a NICK
```

- Há outras operações e funções de texto úteis que podemos usar em instruções WHERE e SELECT. Por exemplo, a função `length()` conta o número de caracteres de um valor específico. Exemplo:

``` SQL
USE Sakila;

SELECT actor_id, first_name, last_name FROM actor -- trás somente os campos especificados(actor_id, first_name, last_name)
WHERE length(first_name) >= 6; -- traś os registros que contém o primeiro nome com seis ou mais caracteres
```

- Outra operação comum é o uso de curingas em uma expressão `LIKE`, onde `%` significa qualquer número de caracteres e `_` um único caractere. Exemplo:

``` SQL
USE Sakila;

SELECT actor_id, first_name, last_name FROM actor -- trás somente os campos especificados(actor_id, first_name, last_name)
WHERE first_name LIKE 'A%'; -- traś os registros que contém o primeiro nome que inicia com a letra A
```

### Usando WHERE com booleanos

- No universo de dados, normalmente falso é expresso como 0 e verdadeiro como 1. Exemplo:

``` SQL
USE Sakila;

SELECT * FROM customer -- trás todos os campos
WHERE active = 1; -- traś os registros que ativo é igual a 1(true)
```

- Como estamos buscando somente valores verdadeiros, não é necessário usar a expressçao `= 1`. Exemplo:

``` SQL
USE Sakila;

SELECT * FROM customer -- trás todos os campos
WHERE active; -- traś os registros que ativo é igual a 1(true)
```

- Porém, a qualificação de condições falsas precisa ser explícita. Exemplo:

``` SQL
USE Sakila;

SELECT * FROM customer -- trás todos os campos
WHERE active = 0; -- traś os registros que ativo é igual a 0(false)
```

- Podemos usar a palavra-chave `NOT` para qualificar como falso. Exemplo:

``` SQL
USE Sakila;

SELECT * FROM customer -- trás todos os campos
WHERE NOT active; -- traś os registros que ativo é igual a 0(false)
```

### Manipulando NULL

- Valor nulo é aquele que não apresenta valor. É ausência completa de qualquer conteúdo. Os valores nulos não pode ser determinados com `=`. Precisamos usar as instruções `IS NULL` ou `IS NOT NULL` para identificar valores nulos. Exemplo:

``` SQL
USE Sakila;

SELECT * FROM address -- trás todos os campos
WHERE address2 IS NULL; -- traś os registros que endereço2 é nulo
```

``` SQL
USE Sakila;

SELECT * FROM address -- trás todos os campos
WHERE address2 IS NOT NULL; -- traś os registros que endereço2 NÃO é nulo
```