# DML (Data Manipulation Language) no SQL

A Data Manipulation Language (DML) no SQL é usada para inserir, atualizar, deletar e consultar dados em um banco de dados. Este guia abordará os principais comandos DML: `SELECT`, `INSERT`, `UPDATE`, `DELETE`, além de outras operações importantes como `MERGE` e `UPSERT`.

## SELECT

### Básico
O comando `SELECT` é usado para consultar dados de uma tabela.

```sql
SELECT coluna1, coluna2, ...
FROM nome_da_tabela;
```

#### Exemplo:
```sql
SELECT id, nome, email
FROM clientes;
```

### WHERE
Filtra registros com base em uma condição.

```sql
SELECT coluna1, coluna2, ...
FROM nome_da_tabela
WHERE condição;
```

#### Exemplo:
```sql
SELECT id, nome, email
FROM clientes
WHERE idade > 30;
```

### JOIN
Combina registros de duas ou mais tabelas com base em uma condição relacionada.

#### INNER JOIN
```sql
SELECT t1.coluna1, t2.coluna2, ...
FROM tabela1 t1
INNER JOIN tabela2 t2 ON t1.coluna = t2.coluna;
```

#### Exemplo:
```sql
SELECT c.nome, p.nome_produto
FROM clientes c
INNER JOIN pedidos p ON c.id = p.cliente_id;
```

#### LEFT JOIN
```sql
SELECT t1.coluna1, t2.coluna2, ...
FROM tabela1 t1
LEFT JOIN tabela2 t2 ON t1.coluna = t2.coluna;
```

### ORDER BY
Ordena os resultados da consulta.

```sql
SELECT coluna1, coluna2, ...
FROM nome_da_tabela
ORDER BY coluna1 [ASC|DESC], coluna2 [ASC|DESC], ...;
```

#### Exemplo:
```sql
SELECT nome, idade
FROM clientes
ORDER BY idade DESC;
```

### GROUP BY
Agrupa registros que têm valores iguais em colunas especificadas e permite executar funções agregadas.

```sql
SELECT coluna1, função_agregada(coluna2), ...
FROM nome_da_tabela
GROUP BY coluna1;
```

#### Exemplo:
```sql
SELECT cidade, COUNT(*)
FROM clientes
GROUP BY cidade;
```

### HAVING
Filtra grupos de registros com base em uma condição.

```sql
SELECT coluna1, função_agregada(coluna2), ...
FROM nome_da_tabela
GROUP BY coluna1
HAVING condição;
```

#### Exemplo:
```sql
SELECT cidade, COUNT(*)
FROM clientes
GROUP BY cidade
HAVING COUNT(*) > 10;
```

## INSERT

### Básico
Insere novos registros em uma tabela.

```sql
INSERT INTO nome_da_tabela (coluna1, coluna2, ...)
VALUES (valor1, valor2, ...);
```

#### Exemplo:
```sql
INSERT INTO clientes (nome, email, data_nascimento)
VALUES ('João Silva', 'joao.silva@example.com', '1990-05-15');
```

### Inserção Múltipla
Insere vários registros em uma única instrução.

```sql
INSERT INTO nome_da_tabela (coluna1, coluna2, ...)
VALUES 
    (valor1a, valor2a, ...),
    (valor1b, valor2b, ...),
    ...;
```

#### Exemplo:
```sql
INSERT INTO clientes (nome, email, data_nascimento)
VALUES 
    ('Maria Souza', 'maria.souza@example.com', '1985-07-20'),
    ('Pedro Oliveira', 'pedro.oliveira@example.com', '1978-02-25');
```

## UPDATE

### Básico
Atualiza registros existentes em uma tabela.

```sql
UPDATE nome_da_tabela
SET coluna1 = valor1, coluna2 = valor2, ...
WHERE condição;
```

#### Exemplo:
```sql
UPDATE clientes
SET email = 'novo.email@example.com'
WHERE id = 1;
```

## DELETE

### Básico
Remove registros de uma tabela.

```sql
DELETE FROM nome_da_tabela
WHERE condição;
```

#### Exemplo:
```sql
DELETE FROM clientes
WHERE id = 1;
```

## UPSERT

### Básico
Realiza uma inserção ou atualização dependendo da existência de um registro.

```sql
INSERT INTO nome_da_tabela (coluna1, coluna2, ...)
VALUES (valor1, valor2, ...)
ON DUPLICATE KEY UPDATE coluna1 = valor1, coluna2 = valor2, ...;
```

#### Exemplo:
```sql
INSERT INTO clientes (id, nome, email)
VALUES (1, 'João Silva', 'joao.silva@example.com')
ON DUPLICATE KEY UPDATE nome = 'João Silva', email = 'joao.silva@example.com';
```

## Conclusão

Os comandos DML são essenciais para manipular dados em um banco de dados SQL. Eles permitem consultar, inserir, atualizar e deletar dados de maneira eficiente. Este guia fornece uma visão geral dos principais comandos e casos de uso comuns para ajudar a entender e aplicar DML no SQL.