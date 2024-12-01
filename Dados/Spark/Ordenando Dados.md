
Ordenar dados é uma operação essencial em análise de dados. No Apache Spark, isso é feito usando os métodos **`orderBy`** e **`sort`**, que oferecem flexibilidade para ordenar **DataFrames** de forma ascendente ou descendente, com base em uma ou mais colunas.

### **Métodos para Ordenação**

- **`orderBy`**: Ordena as linhas com base nos valores das colunas especificadas.
- **`sort`**: Sinônimo de `orderBy`, com funcionalidade idêntica.


### **Ordenando por Uma Coluna**

#### **Ordem Ascendente (Padrão)**

Por padrão, os dados são ordenados em ordem ascendente:

```python
df_sorted = df.orderBy("column_name")
df_sorted.show()
```

#### **Ordem Descendente**

Para ordenar de forma descendente, use `desc()`:

```python
from pyspark.sql.functions import col

df_sorted = df.orderBy(col("column_name").desc())
df_sorted.show()
```

### **Ordenando por Múltiplas Colunas**

#### **Ordem Mista**

Você pode combinar colunas com diferentes direções de ordenação:

```python
df_sorted = df.orderBy(
    col("column1").asc(),
    col("column2").desc()
)
df_sorted.show()
```


### **Usando `sort`**

O método `sort` funciona de forma idêntica ao `orderBy`:

```python
df_sorted = df.sort("column_name")
df_sorted.show()
```

Para ordenar múltiplas colunas:

```python
df_sorted = df.sort(col("column1").asc(), col("column2").desc())
df_sorted.show()
```

### **Ordenando com Nulos**

Por padrão, o Spark posiciona valores **nulos** no início (ordem ascendente) ou no final (ordem descendente). Você pode controlar explicitamente o comportamento com `nullsFirst()` e `nullsLast()`:

```python
df_sorted = df.orderBy(col("column_name").asc_nulls_last())
df_sorted.show()
```


### **Ordenação com Expressões SQL**

Se você estiver trabalhando com Spark SQL, pode usar consultas SQL diretamente:

```python
df.createOrReplaceTempView("table_name")

df_sorted = spark.sql("""
    SELECT * 
    FROM table_name 
    ORDER BY column1 ASC, column2 DESC
""")
df_sorted.show()
```


### **Exemplo Prático**

#### **DataFrame de Exemplo**

```python
from pyspark.sql import SparkSession

# Criando uma SparkSession
spark = SparkSession.builder.appName("OrderBy Example").getOrCreate()

# Criando um DataFrame de exemplo
data = [
    ("Alice", 28, 5000),
    ("Bob", 35, 6000),
    ("Cathy", 30, 7500),
    ("David", 45, None)
]
columns = ["Name", "Age", "Salary"]

df = spark.createDataFrame(data, columns)
df.show()
```

#### **Ordenações**

```python
from pyspark.sql.functions import col

# Ordenar por uma coluna em ordem ascendente
df_sorted = df.orderBy("Age")
df_sorted.show()

# Ordenar por uma coluna em ordem descendente
df_sorted = df.orderBy(col("Salary").desc())
df_sorted.show()

# Ordenar por múltiplas colunas (idade ascendente, salário descendente)
df_sorted = df.orderBy(col("Age").asc(), col("Salary").desc())
df_sorted.show()

# Ordenar tratando nulos (nulos no final)
df_sorted = df.orderBy(col("Salary").asc_nulls_last())
df_sorted.show()
```


### **Considerações de Desempenho**

1. **Cuidado com Dados Grandes**: A ordenação é uma operação custosa em termos de tempo e memória, especialmente para grandes conjuntos de dados.
2. **Particionamento**: Ordenar um DataFrame particionado exige a reorganização dos dados entre nós. Se necessário, considere o uso de `repartition()` antes de ordenar.
3. **Uso com Agregações**: Combine ordenação com agregações para análises como encontrar os "Top N" valores:
    
    ```python
    df.orderBy(col("column_name").desc()).limit(10).show()
    ```
    

