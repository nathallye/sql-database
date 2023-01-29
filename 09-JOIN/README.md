# SQL Database

## JOIN

### INNER JOIN

- Até o momento usamos o SELECT para filtrar campos/colunas de uma tabela. Agora, para filtrarmos campos de multiplas tabelas e gerar um resultado, vamos usar o `INNER JOIN`(ou só `JOIN`, que implicitamente é INNER JOIN):

``` SQL
USE [database-name];

SELECT * FROM [table-1]
JOIN [table-2] ON [table-1].[common-field] = [table-2].[common-field];
```

- Exemplo:

``` SQL
USE Sakila;

SELECT * FROM customer -- trás todos os campos de customer
JOIN payment ON customer.customer_id = payment.customer_id; -- trás todos os campos de payment, colocando os registros que contém a propriedade em comum(customer_id) na mesma linha 
```

- Podemos atribuir apelidos(*alias*) para as tabelas diminuindo o código. Exemplo:

``` SQL
USE Sakila;

SELECT * FROM customer AS c -- trás todos os campos de customer
JOIN payment p ON c.customer_id = p.customer_id; -- trás todos os campos de payment, colocando os registros que contém a propriedade em comum(customer_id) na mesma linha 
```

- Também podemos selecionar os campos/colunas de cada tabela que queremos retornar, ao invés de retornar todas(*). Exemplo:

``` SQL
USE Sakila;

SELECT 
    c.customer_id, c.first_name, c.email, -- trás os campos selecionados de customer
    p.payment_id, p.staff_id, p.amount -- trás os campos selecionados de payment
FROM customer AS c
JOIN payment p ON c.customer_id = p.customer_id;
```

- Mesmo funciona para multiplas tabelas. Exemplo:

``` SQL
USE Sakila;

SELECT 
    c.customer_id, c.first_name, c.email,
    p.payment_id, p.staff_id, p.amount,
    r.rental_date, r.inventory_id, r.return_date
FROM customer AS c
INNER JOIN payment p ON c.customer_id = p.customer_id
INNER JOIN rental r ON c.customer_id = r.customer_id;
```

### OUTER JOIN

- Dentro do OUTER JOIN temos o `LEFT JOIN` e o `RIGHT JOIN`. Basicamente, o INNER JOIN trás todos os registros que na comparação os dois lados não são nulos. Já o `LEFT JOIN` olha para o lado esquerdo da comparação, ou seja, que ele não seja nulo(e o da direita pode ser) e o `RIGHT JOIN` olha para o lado direito da comparação, ou seja, que ele não seja nulo(e o da esquerda pode ser).

### UNION

- O operador `UNION` combina os resultados de duas ou mais queries em um único result set, retornando todas as linhas pertencentes a todas as queries envolvidas na execução. Para utilizar o UNION, o número e a ordem das colunas precisam ser idênticos em todas as queries e os data types precisam ser compatíveis.

- O operador UNION, por default, executa o equivalente a um SELECT DISTINCT no result set final. Em outras palavras, ele combina o resultado de execução das duas queries e então executa um `SELECT DISTINCT` a fim de eliminar as linhas duplicadas. Este processo é executado mesmo que não hajam registros duplicados. Exemplo:

``` SQL
USE Sakila;

SELECT 
    c.customer_id, c.first_name, c.email, -- trás os campos selecionados de customer
    p.payment_id, p.staff_id, p.amount, -- trás os campos selecionados de payment
    'VIP' AS customer_status -- cria uma nova coluna com o status
FROM customer AS c
JOIN payment p ON c.customer_id = p.customer_id
WHERE p.amount >= 10.99 -- onde o valor do pagamento é maior ou igual 10.99

UNION

SELECT 
    c.customer_id, c.first_name, c.email, -- trás os campos selecionados de customer
    p.payment_id, p.staff_id, p.amount, -- trás os campos selecionados de payment
    'NON VIP' AS customer_status -- cria uma nova coluna com o status
FROM customer AS c
JOIN payment p ON c.customer_id = p.customer_id
WHERE p.amount < 10.99; -- onde o valor do pagamento é menor 10.99
```