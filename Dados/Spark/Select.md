
O método `select` no Apache Spark é usado para selecionar colunas específicas de um **DataFrame**. É uma das operações mais comuns no Spark e permite manipular, renomear ou criar novas colunas durante a seleção.

### **Selecionando Colunas**

#### ** Seleção Simples**

Você pode selecionar uma ou mais colunas usando `select`:

```python
# Selecionar uma coluna
df.select("column_name").show()

# Selecionar múltiplas colunas
df.select("column1", "column2").show()
```

### **Renomeando Colunas Durante a Seleção**

Use a função `alias` para renomear colunas diretamente na operação de seleção:

```python
from pyspark.sql.functions import col

# Renomeando uma coluna
df.select(col("column_name").alias("new_column_name")).show()

# Renomeando múltiplas colunas
df.select(
    col("column1").alias("new_column1"),
    col("column2").alias("new_column2")
).show()
```

### **Criando Colunas Derivadas**

Você pode criar colunas calculadas ou derivadas diretamente dentro do `select`:

```python
from pyspark.sql.functions import col

# Criando uma coluna derivada
df.select(col("column1"), (col("column2") * 2).alias("double_column2")).show()

# Combinação de valores em colunas
df.select(
    col("column1"),
    (col("column2") + col("column3")).alias("sum_column")
).show()
```


### **Aplicando Funções em Colunas**

O Spark suporta diversas funções nativas que podem ser aplicadas dentro do `select`:

```python
from pyspark.sql.functions import upper, length

# Convertendo texto para maiúsculas
df.select(upper(col("column_name")).alias("uppercase_column")).show()

# Calculando o tamanho de strings
df.select(length(col("column_name")).alias("string_length")).show()
```

### **Selecionando com Expressões SQL**

O método `expr` permite usar expressões SQL dentro do `select`:

```python
from pyspark.sql.functions import expr

# Usando uma expressão SQL para criar uma nova coluna
df.select(expr("column1 + column2 AS total")).show()

# Aplicando funções SQL
df.select(expr("UPPER(column_name) AS uppercase_column")).show()
```

### **Filtrando Dados Durante a Seleção**

Embora o método `filter` ou `where` seja mais comum para filtrar dados, você também pode aplicar filtros no `select` combinando com funções como `when`:

```python
from pyspark.sql.functions import when

# Criando uma coluna condicional
df.select(
    col("column1"),
    when(col("column2") > 100, "High").otherwise("Low").alias("category")
).show()
```

### **Selecionando Todas as Colunas com Ajustes**

Você pode selecionar todas as colunas do DataFrame e aplicar alterações em apenas algumas delas:

```python
# Selecionando todas as colunas e ajustando uma
df.select(
    "*",  # Todas as colunas
    (col("column2") * 2).alias("double_column2")
).show()
```


### **Exemplo Prático**

#### **DataFrame de Exemplo**

```python
from pyspark.sql import SparkSession

# Criando a SparkSession
spark = SparkSession.builder.appName("Select Example").getOrCreate()

# Criando um DataFrame de exemplo
data = [
    ("Alice", 28, 5000),
    ("Bob", 35, 6000),
    ("Cathy", 30, 7500)
]
columns = ["Name", "Age", "Salary"]

df = spark.createDataFrame(data, columns)

df.show()
```

#### **Seleções**

```python
from pyspark.sql.functions import col, upper, when

# Selecionar Nome e Salário
df.select("Name", "Salary").show()

# Renomear colunas
df.select(
    col("Name").alias("Employee_Name"),
    col("Salary").alias("Employee_Salary")
).show()

# Criar uma nova coluna derivada
df.select(
    col("Name"),
    col("Salary"),
    (col("Salary") * 1.1).alias("Salary_with_Bonus")
).show()

# Aplicar funções em colunas
df.select(
    upper(col("Name")).alias("Uppercase_Name"),
    when(col("Salary") > 6000, "High").otherwise("Low").alias("Salary_Category")
).show()
```

