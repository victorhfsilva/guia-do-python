# Funções de Manipulação de Dados no SQL

Este guia abrange funções de manipulação de dados em SQL, focando em três principais categorias: datas, strings e números. Essas funções são fundamentais para processar e transformar dados em um banco de dados SQL.

## Funções de Manipulação de Datas

### CURRENT_DATE

Retorna a data atual.

```sql
SELECT CURRENT_DATE;
```

### CURRENT_TIMESTAMP

Retorna a data e hora atuais.

```sql
SELECT CURRENT_TIMESTAMP;
```

### DATEADD

Adiciona um intervalo de tempo a uma data.

```sql
SELECT DATEADD(day, 7, '2023-01-01');  -- Adiciona 7 dias
```

### DATEDIFF

Calcula a diferença entre duas datas.

```sql
SELECT DATEDIFF(day, '2023-01-01', '2023-01-10');  -- Retorna 9
```

### DATEPART

Extrai uma parte específica de uma data (ano, mês, dia, etc.).

```sql
SELECT DATEPART(year, '2023-01-01');  -- Retorna o ano
```

### FORMAT

Formata uma data em uma string.

```sql
SELECT FORMAT(CURRENT_TIMESTAMP, 'yyyy-MM-dd');
```

## Funções de Manipulação de Strings

### CONCAT

Concatena duas ou mais strings.

```sql
SELECT CONCAT('Hello', ' ', 'World');  -- Retorna 'Hello World'
```

### LENGTH

Retorna o comprimento de uma string.

```sql
SELECT LENGTH('Hello');  -- Retorna 5
```

### SUBSTRING

Extrai uma parte de uma string.

```sql
SELECT SUBSTRING('Hello World', 1, 5);  -- Retorna 'Hello'
```

### REPLACE

Substitui uma substring por outra.

```sql
SELECT REPLACE('Hello World', 'World', 'SQL');  -- Retorna 'Hello SQL'
```

### TRIM

Remove espaços em branco do início e do fim de uma string.

```sql
SELECT TRIM('   Hello World   ');  -- Retorna 'Hello World'
```

### UPPER / LOWER

Converte uma string para maiúsculas ou minúsculas.

```sql
SELECT UPPER('hello');  -- Retorna 'HELLO'
SELECT LOWER('HELLO');  -- Retorna 'hello'
```

### LEFT / RIGHT

Extrai um número especificado de caracteres do início ou do fim de uma string.

```sql
SELECT LEFT('Hello World', 5);  -- Retorna 'Hello'
SELECT RIGHT('Hello World', 5);  -- Retorna 'World'
```

## Funções de Manipulação de Números

### ABS

Retorna o valor absoluto de um número.

```sql
SELECT ABS(-123);  -- Retorna 123
```

### CEILING

Arredonda um número para o inteiro mais próximo maior ou igual a ele.

```sql
SELECT CEILING(4.2);  -- Retorna 5
```

### FLOOR

Arredonda um número para o inteiro mais próximo menor ou igual a ele.

```sql
SELECT FLOOR(4.8);  -- Retorna 4
```

### ROUND

Arredonda um número para um número especificado de casas decimais.

```sql
SELECT ROUND(123.4567, 2);  -- Retorna 123.46
```

### POWER

Retorna o valor de um número elevado a uma potência especificada.

```sql
SELECT POWER(2, 3);  -- Retorna 8
```

### SQRT

Retorna a raiz quadrada de um número.

```sql
SELECT SQRT(16);  -- Retorna 4
```

## Funções de Manipulação de Dados Diversos

### CASE

Retorna valores condicionais.

```sql
SELECT 
    nome,
    CASE 
        WHEN idade < 18 THEN 'Menor de idade'
        WHEN idade >= 18 AND idade < 65 THEN 'Adulto'
        ELSE 'Idoso'
    END AS categoria_idade
FROM clientes;
```

### COALESCE

Retorna o primeiro valor não nulo em uma lista de argumentos.

```sql
SELECT COALESCE(NULL, NULL, 'SQL', 'World');  -- Retorna 'SQL'
```

### CAST

Converte um valor de um tipo de dado para outro.

```sql
SELECT CAST(123 AS VARCHAR);  -- Converte o número 123 para uma string '123'
```

### CONVERT

Converte um valor de um tipo de dado para outro. Similar ao `CAST`, mas com uma sintaxe diferente.

```sql
SELECT CONVERT(VARCHAR, 123);  -- Converte o número 123 para uma string '123'
```

## Conclusão

As funções de manipulação de dados no SQL são essenciais para transformar e analisar dados de maneira eficaz. Compreender e utilizar essas funções de maneira eficiente é fundamental para a administração e análise de dados em um banco de dados SQL.