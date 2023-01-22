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

- A instrução SELECT pode fazer muito mais que apenas selecionar colunas. Podemos efetuar cálculos em uma ou mais colunas e incluí-los no resultado da consulta. Exemplo:

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

### Concatenação de texto

- As expressões não precisa ser usadas somente com números. Podemos usar expressões com texto e outros tipos de dados. O operador de concatenação é especificado por um pipe duplo (∣∣); os valores de dados a serem concatenados devem ser colocados nos dois lados do pipe duplo. 