# Múltiplas Consultas no SQL

## Subconsultas

Subconsultas são consultas aninhadas dentro de outra consulta. Elas podem ser usadas em diferentes partes de uma instrução SQL, como no `SELECT`, `FROM`, `WHERE`, e `HAVING`.

### Subconsulta no SELECT

Uma subconsulta pode ser usada para calcular um valor a ser selecionado na consulta principal.

```sql
SELECT nome, 
    (SELECT COUNT(*)
     FROM pedidos
     WHERE pedidos.cliente_id = clientes.id) AS total_pedidos
FROM clientes;
```

### Subconsulta no FROM

Uma subconsulta pode ser usada como uma tabela derivada no `FROM`.

```sql
SELECT sub.nome, sub.total_pedidos
FROM (
    SELECT clientes.nome, COUNT(pedidos.id) AS total_pedidos
    FROM clientes
    LEFT JOIN pedidos ON clientes.id = pedidos.cliente_id
    GROUP BY clientes.nome
) AS sub;
```

### Subconsulta no WHERE

Uma subconsulta pode ser usada para filtrar resultados na cláusula `WHERE`.

```sql
SELECT nome
FROM clientes
WHERE idade > (SELECT AVG(idade) FROM clientes);
```

## Combinação de Resultados de Múltiplas Consultas

### UNION

O operador `UNION` combina os resultados de duas ou mais consultas, removendo duplicatas. Todas as consultas combinadas devem ter o mesmo número de colunas e os mesmos tipos de dados correspondentes.

```sql
SELECT nome FROM clientes_migrados
UNION
SELECT nome FROM clientes_ativos;
```

#### UNION ALL

Para incluir duplicatas, use `UNION ALL`.

```sql
SELECT nome FROM clientes_migrados
UNION ALL
SELECT nome FROM clientes_ativos;
```

### INTERSECT

O operador `INTERSECT` retorna apenas os registros que estão presentes em ambas as consultas. Assim como o `UNION`, as consultas devem ter o mesmo número de colunas e os mesmos tipos de dados.

```sql
SELECT nome FROM clientes_migrados
INTERSECT
SELECT nome FROM clientes_ativos;
```

### EXCEPT (ou MINUS)

O operador `EXCEPT` (ou `MINUS` em alguns SGBDs) retorna os registros que estão presentes na primeira consulta, mas não na segunda.

```sql
SELECT nome FROM clientes_migrados
EXCEPT
SELECT nome FROM clientes_ativos;
```