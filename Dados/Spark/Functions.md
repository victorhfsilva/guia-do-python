
O módulo **`pyspark.sql.functions`** oferece um conjunto poderoso de funções integradas para manipulação e transformação de dados em **DataFrames** no PySpark. Este guia apresenta as funções mais úteis, categorizadas para facilitar o entendimento.


### **Introdução ao `pyspark.sql.functions`**

Para usar as funções, importe o módulo:

```python
from pyspark.sql.functions import *
```

Essas funções podem ser usadas com o método `.withColumn()`, `.select()`, `.filter()`, entre outros.


### **Funções de Manipulação de Colunas**

#### **Renomear Colunas**

Use `alias` para renomear colunas:

```python
df = df.withColumn("new_name", col("old_name").alias("new_name"))
```

#### **Criar ou Modificar Colunas**

- **Adicionar valores constantes:**

```python
df = df.withColumn("new_column", lit("default_value"))
```

- **Multiplicar ou somar valores de colunas:**

```python
df = df.withColumn("new_column", col("column1") * 2 + col("column2"))
```

#### **Remover Espaços**

- **Remover espaços à direita e à esquerda:**

```python
df = df.withColumn("trimmed_column", trim(col("column_name")))
```

- **Remover apenas espaços à esquerda:**

```python
df = df.withColumn("ltrimmed_column", ltrim(col("column_name")))
```

- **Remover apenas espaços à direita:**

```python
df = df.withColumn("rtrimmed_column", rtrim(col("column_name")))
```


### **Funções de Texto**

#### **Conversões**

- **Converter texto para maiúsculas ou minúsculas:**

```python
df = df.withColumn("uppercase", upper(col("text_column")))
df = df.withColumn("lowercase", lower(col("text_column")))
```

- **Concatenar colunas:**

```python
df = df.withColumn("full_name", concat(col("first_name"), lit(" "), col("last_name")))
```

#### **Substituições**

- **Substituir valores específicos:**

```python
df = df.withColumn("new_column", regexp_replace(col("column_name"), "old_value", "new_value"))
```

#### **Extração de Padrões**

- **Extração baseada em expressões regulares:**

```python
df = df.withColumn("extracted", regexp_extract(col("column_name"), r"\d+", 0))
```

### **Funções Numéricas**

#### **Operações Básicas**

- **Arredondar valores:**

```python
df = df.withColumn("rounded", round(col("numeric_column"), 2))
```

- **Truncar valores:**

```python
df = df.withColumn("truncated", bround(col("numeric_column"), 2))
```

#### **Funções Matemáticas Avançadas**

- **Calcular o logaritmo:**

```python
df = df.withColumn("log_value", log(col("numeric_column")))
```

- **Raiz quadrada:**

```python
df = df.withColumn("sqrt_value", sqrt(col("numeric_column")))
```


### **Funções de Data e Hora**

#### **Conversão de Tipos**

- **Converter string para data:**

```python
df = df.withColumn("date_column", to_date(col("string_column"), "yyyy-MM-dd"))
```

- **Obter timestamp atual:**

```python
df = df.withColumn("current_timestamp", current_timestamp())
```

#### **Operações com Datas**

- **Adicionar dias, meses ou anos:**

```python
df = df.withColumn("next_week", date_add(col("date_column"), 7))
df = df.withColumn("next_month", add_months(col("date_column"), 1))
```

- **Subtrair datas:**

```python
df = df.withColumn("days_diff", datediff(current_date(), col("date_column")))
```

#### **Extração de Componentes**

- **Extrair ano, mês e dia:**

```python
df = df.withColumn("year", year(col("date_column")))
df = df.withColumn("month", month(col("date_column")))
df = df.withColumn("day", dayofmonth(col("date_column")))
```

### **Funções de Agregação**

#### **Agregações Comuns**

- **Soma, média, mínimo e máximo:**

```python
from pyspark.sql.functions import sum, avg, min, max

df.groupBy("group_column").agg(
    sum("numeric_column").alias("total"),
    avg("numeric_column").alias("average"),
    min("numeric_column").alias("min_value"),
    max("numeric_column").alias("max_value")
).show()
```

#### **Contagem**

- **Contar valores não nulos:**

```python
df.groupBy("group_column").count().show()
```

- **Contar valores distintos:**

```python
df.groupBy("group_column").agg(countDistinct("column_name").alias("distinct_count")).show()
```


### **Funções de Condição**

#### **Condicionais com `when`**

- **Criar uma coluna condicional:**

```python
df = df.withColumn("category", when(col("numeric_column") > 100, "High").otherwise("Low"))
```

#### **Filtrar valores nulos**

- **Substituir valores nulos:**

```python
df = df.fillna({"column_name": "default_value"})
```


### **Funções de Ordenação e Classificação**

#### **Ordenar Dados**

- **Ordenar por uma ou mais colunas:**

```python
df = df.orderBy("column_name")
df = df.orderBy(col("column_name").desc())
```

#### **Criar uma Coluna de Ranking**

- **Adicionar um ranking baseado em uma coluna:**

```python
from pyspark.sql.window import Window

window_spec = Window.orderBy(col("numeric_column").desc())
df = df.withColumn("rank", rank().over(window_spec))
```


### **Exemplo Completo**

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col, to_date, when, avg

# Criando a SparkSession
spark = SparkSession.builder.appName("Functions Example").getOrCreate()

# Criando um DataFrame de exemplo
data = [
    ("Alice", "2023-01-01", 5000),
    ("Bob", "2023-02-15", 6000),
    ("Cathy", None, 7500)
]
columns = ["Name", "JoinDate", "Salary"]

df = spark.createDataFrame(data, columns)

# Transformações com pyspark.sql.functions
df = df.withColumn("JoinDate", to_date(col("JoinDate"), "yyyy-MM-dd"))
df = df.withColumn("SalaryCategory", when(col("Salary") > 5500, "High").otherwise("Low"))
df = df.fillna({"JoinDate": "2023-01-01"})

# Agregações
agg_df = df.groupBy("SalaryCategory").agg(avg("Salary").alias("AverageSalary"))

# Exibindo os resultados
df.show()
agg_df.show()
```
