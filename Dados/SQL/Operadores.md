# Operadores no SQL

Os operadores no SQL são usados para realizar diversas operações em consultas, como comparação, lógica, aritmética, entre outras. Este guia abordará os principais operadores usados no SQL: operadores de comparação, lógicos, aritméticos, e de cadeia de caracteres.

## Operadores de Comparação

Os operadores de comparação são usados para comparar dois valores.

### Igualdade (`=`)

Verifica se dois valores são iguais.

```sql
SELECT * FROM clientes WHERE idade = 30;
```

### Diferente (`<>` ou `!=`)

Verifica se dois valores são diferentes.

```sql
SELECT * FROM clientes WHERE idade <> 30;
```

### Maior Que (`>`)

Verifica se um valor é maior que outro.

```sql
SELECT * FROM clientes WHERE idade > 30;
```

### Menor Que (`<`)

Verifica se um valor é menor que outro.

```sql
SELECT * FROM clientes WHERE idade < 30;
```

### Maior ou Igual a (`>=`)

Verifica se um valor é maior ou igual a outro.

```sql
SELECT * FROM clientes WHERE idade >= 30;
```

### Menor ou Igual a (`<=`)

Verifica se um valor é menor ou igual a outro.

```sql
SELECT * FROM clientes WHERE idade <= 30;
```

### BETWEEN

Verifica se um valor está dentro de um intervalo.

```sql
SELECT * FROM clientes WHERE idade BETWEEN 20 AND 30;
```

### IN

Verifica se um valor está em uma lista de valores.

```sql
SELECT * FROM clientes WHERE idade IN (20, 30, 40);
```

### LIKE

Verifica se um valor corresponde a um padrão.

```sql
SELECT * FROM clientes WHERE nome LIKE 'João%';
```

### IS NULL / IS NOT NULL

Verifica se um valor é `NULL` ou não é `NULL`.

```sql
SELECT * FROM clientes WHERE email IS NULL;
```

## Operadores Lógicos

Os operadores lógicos são usados para combinar condições booleanas.

### AND

Retorna `TRUE` se ambas as condições forem verdadeiras.

```sql
SELECT * FROM clientes WHERE idade > 20 AND idade < 30;
```

### OR

Retorna `TRUE` se pelo menos uma das condições for verdadeira.

```sql
SELECT * FROM clientes WHERE idade < 20 OR idade > 30;
```

### NOT

Inverte o valor booleano de uma condição.

```sql
SELECT * FROM clientes WHERE NOT idade = 30;
```

## Operadores Aritméticos

Os operadores aritméticos são usados para realizar operações matemáticas.

### Adição (`+`)

Adiciona dois valores.

```sql
SELECT preco + 10 FROM produtos;
```

### Subtração (`-`)

Subtrai um valor de outro.

```sql
SELECT preco - 10 FROM produtos;
```

### Multiplicação (`*`)

Multiplica dois valores.

```sql
SELECT preco * 1.1 FROM produtos;
```

### Divisão (`/`)

Divide um valor por outro.

```sql
SELECT preco / 2 FROM produtos;
```

### Módulo (`%`)

Retorna o restante da divisão de um valor por outro.

```sql
SELECT quantidade % 2 FROM estoque;
```

## Operadores de Cadeia de Caracteres

Os operadores de cadeia de caracteres são usados para manipular strings.

### Concatenação (`||` ou `+`)

Concatena duas strings.

#### Usando `||` (padrão SQL):

```sql
SELECT nome || ' ' || sobrenome AS nome_completo FROM clientes;
```

#### Usando `+` (em alguns sistemas, como SQL Server):

```sql
SELECT nome + ' ' + sobrenome AS nome_completo FROM clientes;
```

### LENGTH

Retorna o comprimento de uma string.

```sql
SELECT LENGTH(nome) FROM clientes;
```

### UPPER / LOWER

Converte uma string para maiúsculas ou minúsculas.

```sql
SELECT UPPER(nome) FROM clientes;
SELECT LOWER(nome) FROM clientes;
```

### SUBSTRING

Extrai uma parte de uma string.

```sql
SELECT SUBSTRING(nome FROM 1 FOR 3) FROM clientes;
```

### TRIM

Remove espaços em branco de ambos os lados de uma string.

```sql
SELECT TRIM(nome) FROM clientes;
```

## Conclusão

Os operadores no SQL são ferramentas poderosas para manipular e consultar dados. Compreender e utilizar esses operadores de maneira eficaz é essencial para escrever consultas SQL eficientes e precisas.