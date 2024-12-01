# Joins no SQL

Joins no SQL são usados para combinar registros de duas ou mais tabelas com base em uma condição relacionada. Este guia abordará os principais tipos de joins: `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, e `FULL OUTER JOIN`.

## INNER JOIN

O `INNER JOIN` retorna registros que têm correspondências em ambas as tabelas.

### Exemplo

Suponha que temos duas tabelas:

**clientes**
| id | nome        |
|----|-------------|
| 1  | João Silva  |
| 2  | Maria Souza |
| 3  | Pedro Oliveira |

**pedidos**
| id | cliente_id | produto         |
|----|------------|-----------------|
| 1  | 1          | Notebook        |
| 2  | 1          | Mouse           |
| 3  | 2          | Teclado         |
| 4  | 4          | Monitor         |

### Consulta

```sql
SELECT c.id, c.nome, p.produto
FROM clientes c
INNER JOIN pedidos p ON c.id = p.cliente_id;
```

### Resultado

| id | nome        | produto  |
|----|-------------|----------|
| 1  | João Silva  | Notebook |
| 1  | João Silva  | Mouse    |
| 2  | Maria Souza | Teclado  |

## 2. LEFT JOIN

O `LEFT JOIN` retorna todos os registros da tabela à esquerda e os registros correspondentes da tabela à direita. Se não houver correspondência, os resultados da tabela à direita serão `NULL`.

### Exemplo

**clientes**
| id | nome        |
|----|-------------|
| 1  | João Silva  |
| 2  | Maria Souza |
| 3  | Pedro Oliveira |

**pedidos**
| id | cliente_id | produto         |
|----|------------|-----------------|
| 1  | 1          | Notebook        |
| 2  | 1          | Mouse           |
| 3  | 2          | Teclado         |
| 4  | 4          | Monitor         |

### Consulta

```sql
SELECT c.id, c.nome, p.produto
FROM clientes c
LEFT JOIN pedidos p ON c.id = p.cliente_id;
```

### Resultado

| id | nome         | produto  |
|----|--------------|----------|
| 1  | João Silva   | Notebook |
| 1  | João Silva   | Mouse    |
| 2  | Maria Souza  | Teclado  |
| 3  | Pedro Oliveira | NULL     |

## 3. RIGHT JOIN

O `RIGHT JOIN` retorna todos os registros da tabela à direita e os registros correspondentes da tabela à esquerda. Se não houver correspondência, os resultados da tabela à esquerda serão `NULL`.

### Exemplo

**clientes**
| id | nome        |
|----|-------------|
| 1  | João Silva  |
| 2  | Maria Souza |
| 3  | Pedro Oliveira |

**pedidos**
| id | cliente_id | produto         |
|----|------------|-----------------|
| 1  | 1          | Notebook        |
| 2  | 1          | Mouse           |
| 3  | 2          | Teclado         |
| 4  | 4          | Monitor         |

### Consulta

```sql
SELECT c.id, c.nome, p.produto
FROM clientes c
RIGHT JOIN pedidos p ON c.id = p.cliente_id;
```

### Resultado

| id  | nome         | produto  |
|-----|--------------|----------|
| 1   | João Silva   | Notebook |
| 1   | João Silva   | Mouse    |
| 2   | Maria Souza  | Teclado  |
| NULL | NULL        | Monitor  |

## 4. FULL OUTER JOIN

O `FULL OUTER JOIN` retorna todos os registros quando há uma correspondência em uma das tabelas. Os registros não correspondentes da tabela à esquerda e à direita serão `NULL`.

### Exemplo

**clientes**
| id | nome        |
|----|-------------|
| 1  | João Silva  |
| 2  | Maria Souza |
| 3  | Pedro Oliveira |

**pedidos**
| id | cliente_id | produto         |
|----|------------|-----------------|
| 1  | 1          | Notebook        |
| 2  | 1          | Mouse           |
| 3  | 2          | Teclado         |
| 4  | 4          | Monitor         |

### Consulta

```sql
SELECT c.id, c.nome, p.produto
FROM clientes c
FULL OUTER JOIN pedidos p ON c.id = p.cliente_id;
```

### Resultado

| id  | nome         | produto  |
|-----|--------------|----------|
| 1   | João Silva   | Notebook |
| 1   | João Silva   | Mouse    |
| 2   | Maria Souza  | Teclado  |
| 3   | Pedro Oliveira | NULL     |
| NULL | NULL        | Monitor  |

## Conclusão

Os diferentes tipos de joins no SQL permitem combinar registros de tabelas de várias maneiras, conforme a necessidade de análise dos dados. Cada join possui características específicas que são úteis em diferentes cenários. Este guia apresentou exemplos práticos para ajudar a entender e aplicar esses joins no SQL.