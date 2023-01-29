# SQL Database

## UPDATE

- Para atualizarmos registros de uma tabela podemos usar o comando `UPDATE`. Exemplo:

``` SQL
USE sakila;

UPDATE payment
SET amount = 15.99
WHERE payment_id = 1;
```