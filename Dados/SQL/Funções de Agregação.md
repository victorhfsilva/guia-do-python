# Funções de Agregação no SQL

As funções de agregação no SQL são usadas para realizar cálculos em um conjunto de valores e retornar um único valor resumido. As funções de agregação mais comuns incluem `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`, entre outras.

## COUNT

A função `COUNT` retorna o número de registros em um conjunto de resultados.

### Contar Todos os Registros

```sql
SELECT COUNT(*)
FROM clientes;
```

### Contar Registros Não Nulos em uma Coluna

```sql
SELECT COUNT(email)
FROM clientes;
```

### Contar Registros Únicos

```sql
SELECT COUNT(DISTINCT cidade)
FROM clientes;
```

## SUM

A função `SUM` retorna a soma de um conjunto de valores numéricos.

### Soma Simples

```sql
SELECT SUM(preco)
FROM produtos;
```

### Soma com Condição

```sql
SELECT SUM(preco)
FROM produtos
WHERE categoria = 'Eletrônicos';
```

## AVG

A função `AVG` retorna a média de um conjunto de valores numéricos.

### Média Simples

```sql
SELECT AVG(preco)
FROM produtos;
```

### Média com Condição

```sql
SELECT AVG(preco)
FROM produtos
WHERE categoria = 'Eletrônicos';
```

## MIN

A função `MIN` retorna o menor valor em um conjunto de valores.

### Menor Valor Simples

```sql
SELECT MIN(preco)
FROM produtos;
```

### Menor Valor com Condição

```sql
SELECT MIN(preco)
FROM produtos
WHERE categoria = 'Eletrônicos';
```

## MAX

A função `MAX` retorna o maior valor em um conjunto de valores.

### Maior Valor Simples

```sql
SELECT MAX(preco)
FROM produtos;
```

### Maior Valor com Condição

```sql
SELECT MAX(preco)
FROM produtos
WHERE categoria = 'Eletrônicos';
```

## Conclusão

As funções de agregação no SQL são ferramentas poderosas para resumir e analisar dados. Compreender e utilizar essas funções de maneira eficaz é essencial para extrair insights valiosos dos dados.