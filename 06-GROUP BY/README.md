# SQL Database

## GROUP BY

- A agregação de dados é a criação de algum tipo de total a partir de vários registros. Soma, mínimo, máximo, contagem e média são operações comuns. Em SQL, podemos agrupar esses totais em qualquer coluna especificada, o que permite controlar facilmente o escopo das agregações.

### Agrupando registros

- Executaremos a operação de agregação mais simples: contar o número de registros de uma tabela. Exemplo:

``` SQL
USE Sakila;

SELECT COUNT(*) AS payment_count FROM payment; -- trás o campo payment_count com o total de registros
```

- `COUNT(*)` significa contar os registros. Também podemos usar essa função junto com outras operações SQL, como `WHERE`. Exemplo:

``` SQL
USE Sakila;

SELECT COUNT(*) AS payment_count FROM payment -- trás o campo payment_count com o total de registros...
WHERE customer_id = 1; -- onde customer_id é igual a 1
```

- E também podemos separar essa contagem de pagamentos(payment) pelo id do staff(staff_id). Exemplo:

``` SQL
USE Sakila;

SELECT staff_id, COUNT(*) AS payment_count FROM payment -- trás os campos staff_id e payment_count com o total de registros...
WHERE customer_id = 1 -- onde customer_id é igual a 1...
GROUP BY staff_id; -- agrupando pelo staff_id
```

- Podemos agrupar a contagem por mais de um campo. Exemplo:

``` SQL
USE Sakila;

SELECT customer_id, staff_id, COUNT(*) AS payment_count FROM payment -- trás os campos customer_id, staff_id e payment_count com o total de registros...
GROUP BY customer_id, staff_id; -- agrupando pelo customer_id e staff_id
```

### Ordenando registros 

- Podemos adicionar o operador `ORDER BY` no fim da instrução SQL para orderar essa lista de acordo com uma coluna especificada. Exemplo:

``` SQL
USE Sakila;

SELECT customer_id, staff_id, COUNT(*) AS payment_count FROM payment -- trás os campos customer_id, staff_id e payment_count com o total de registros...
GROUP BY customer_id, staff_id -- agrupando pelo customer_id e staff_id
ORDER BY customer_id; -- ordenando pelo id do cliente de forma crescente(ASC - padrão)
```

### Funções de agregação

- Primeiro examinaremos outra maneira de usar `COUNT()`. A função `COUNT()` pode ser usada para uma finalidade diferente da de simplesmente contar registros. Se especificarmos uma coluna em vez de um asterisco, ela contará quantos valores não nulos existem nessa coluna. Exemplo:

``` SQL
USE Sakila;

SELECT COUNT(amount) AS payment_amount_count FROM payment; -- trás o campo payment_amount_count com o total de valores não nulos na coluna amount
```

- Já usamos a função `COUNT(*)` para contar registros e contar valores não nulos de uma coluna. Porém, há outras funções de agregação, entre elas `SUM()`, `MIN()`, `MAX()` e `AVG()`. Podemos usar funções de agreção em uma coluna específica para executar algum tipo de cálculo nela. Exemplo:


``` SQL
USE Sakila;

SELECT customer_id, AVG(amount) AS amount_avg FROM payment -- trás os campos customer_id e amount_avg com a média do valores...
GROUP BY customer_id; -- agrupando pelo id do cliente
```

- Como sempre, podemos usar funções nos valores agregados e executar tarefas como a de arredondamento para melhorar a aparência do resultado. Exemplo:

``` SQL
USE Sakila;

SELECT customer_id, ROUND(AVG(amount), 2) AS amount_avg FROM payment -- trás os campos customer_id e amount_avg com a média do valores(arredondado em duas casas decimais)...
GROUP BY customer_id; -- agrupando pelo id do cliente
```

### Instrução HAVING

- A agregação funciona com o software processando registro a registro e encontrando os que ele deseja manter de acordo com a condição WHERE. Depois, ele  agrupa os registros em GROUP BY e executa as funções de agregação solicitadas, como AVG(). Se quiséssemos filtar pelo valor de `AVG()`, seria preciso que a filtragem ocorresse após o calculo. E aí que entra em cena `HAVING`:

``` SQL
USE Sakila;

SELECT customer_id, ROUND(AVG(amount), 2) AS amount_avg FROM payment -- trás os campos customer_id e amount_avg com a média do valores de amount(arredondado em duas casas decimais)...
GROUP BY customer_id -- agrupando pelo id do cliente...
HAVING AVG(amount) > 4.00; -- filtrando pela média do valores de amount maior que 4.00
```