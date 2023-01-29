# SQL Database

## SubQuery

- Podemos executar uma query dentro da outra. Para que o resultado de uma query seja usado dentro de outra(principa). Exemplo:

``` SQL
USE sakila;

SELECT * FROM payment
WHERE amount > ( -- verifica se amount é maior que o valor médio
  SELECT AVG(amount) -- retorna o valor médio de amount
  FROM payment
);
```