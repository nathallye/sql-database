# SQL Database

## DELETE

- Para removermos registros de uma tabela podemos usar o comando `DELETE`. Exemplo:

``` SQL
USE sakila;

DELETE FROM payment
WHERE payment_id = 1;
```