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

- O `SELECT` serve para listarmos dados dos campos(colunas) especificados(ou todos com o `*`.) de uma determinada tabela:

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

``` SQL
USE Sakila;

SELECT actor_id, first_name, last_name FROM actor -- trás somente os campos especificados(actor_id, first_name, last_name)
WHERE actor_id <= 10; -- trás todos os registros que contém id menor ou igual que 10
```
