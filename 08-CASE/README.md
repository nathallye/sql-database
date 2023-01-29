# SQL Database

## CASE

- Uma instrução `CASE` permite mapear uma ou mais condições para um valor correspondente a cada condição. Ela deve ser iniciada com a palavra `CASE` e finalizada com `END`. Entre essas palavras-chave devemos especificar cada condição com a sintaxe `WHEN[condição]` `THEN[valor]`, em que a `[condição]` e o `[valor]` correspondente nós que fornecemos. Após especifica cada os pares condição-valor, podemos estabelecer um valor geral a ser usado como padrão se nenhuma condição for atendida, que deve ser definido em `ELSE`. Exemplo:

``` SQL
USE sakila;

SELECT payment_id, amount,
CASE 
	WHEN amount >= 10.99 THEN 'HIGH'
    WHEN amount >= 7.99 THEN 'MIDDLE'
    ELSE 'LOW'
END AS amount_range_price
FROM payment;
```

- Podemos fazer alguns truques interessantes com a instrução `CASE`. Um padrão simples, porém útil, é o truque da instrução *CASE "zero/null"*. Ele permite aplicar diferentes "filtros" a valores agregados distintos na mesma consulta SELECT. Exemplo:

``` SQL
USE sakila;

SELECT c.customer_id, c.first_name,

SUM(CASE WHEN c.active = 1 THEN p.amount ELSE 0 END) AS active_amount,
SUM(CASE WHEN c.active = 0 THEN p.amount ELSE 0 END) AS non_active_amount

FROM customer AS c
JOIN payment p ON c.customer_id = p.customer_id

GROUP BY c.customer_id, c.first_name;
```