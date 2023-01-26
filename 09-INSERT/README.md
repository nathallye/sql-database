# SQL Database

## INSERT

- Para adicionarmos novos registros a uma tabela podemos usar o comando `INSERT`. Exemplo:

``` SQL
USE sakila;

INSERT INTO category
VALUES
	(default, 'Animation', '2023-01-15 04:46:27'); -- default, significa que ele vai usar o padrão auto incremento
```

- Também podemos adicionar mais de um registro a uma tabela ao mesmo tempo. Exemplo:

``` SQL
USE sakila;

INSERT INTO category
VALUES
	(default, 'Animation', '2023-01-15 04:46:27'),
  (default, 'Classics', '2023-01-15 04:46:50'),
  (default, 'Comedy', '2023-01-15 04:46:55');
```

