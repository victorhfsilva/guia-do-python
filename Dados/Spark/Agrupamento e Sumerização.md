
Agrupamento e sumarização são operações fundamentais para análise de dados em larga escala. No Apache Spark, essas operações são realizadas principalmente com os métodos **`groupBy`** e **`agg`**, permitindo cálculos como soma, média, contagem, entre outros, agrupados por uma ou mais colunas.

### **Introdução ao Agrupamento e Sumarização**

#### ** Métodos Principais**

- **`groupBy`**: Agrupa os dados com base em uma ou mais colunas.
- **`agg`**: Aplica funções de agregação (como `sum`, `avg`, `count`, etc.) nos grupos.

#### **Estrutura Geral**

```python
df.groupBy("column_name").agg(aggregation_functions)
```


### **Funções de Agregação Disponíveis**

#### Funções Comuns:

- **`sum`**: Soma dos valores.
- **`avg`**: Média dos valores.
- **`count`**: Contagem de linhas no grupo.
- **`min`**: Valor mínimo.
- **`max`**: Valor máximo.
- **`countDistinct`**: Contagem de valores distintos.

Exemplo de uso:

```python
from pyspark.sql.functions import sum, avg, count, min, max
```


### **Agrupando e Sumarizando Dados**

#### **Agrupamento Simples**

Agrupe por uma coluna e aplique uma função de agregação:

```python
df.groupBy("group_column").sum("numeric_column").show()
```

#### **Agrupamento com Múltiplas Agregações**

Aplique múltiplas funções de agregação com o método `agg`:

```python
from pyspark.sql.functions import sum, avg

df.groupBy("group_column").agg(
    sum("numeric_column").alias("total"),
    avg("numeric_column").alias("average")
).show()
```

### **Agrupando por Múltiplas Colunas**

É possível agrupar por mais de uma coluna:

```python
df.groupBy("column1", "column2").agg(
    sum("numeric_column").alias("total")
).show()
```

### **Sumarização com Agregação Direta**

Se não houver necessidade de agrupar, você pode usar `agg` diretamente para sumarizar todo o DataFrame:

```python
df.agg(
    sum("numeric_column").alias("total"),
    avg("numeric_column").alias("average")
).show()
```

### **Contagem de Valores**

#### **Contagem Total**

Conte todas as linhas:

```python
df.groupBy("group_column").count().show()
```

#### **Contagem de Valores Distintos**

Conte os valores únicos:

```python
from pyspark.sql.functions import countDistinct

df.groupBy("group_column").agg(
    countDistinct("column_name").alias("distinct_count")
).show()
```

### **Exemplo Prático**

#### **DataFrame de Exemplo**

```python
from pyspark.sql import SparkSession

# Criando uma SparkSession
spark = SparkSession.builder.appName("GroupBy Example").getOrCreate()

# Criando um DataFrame de exemplo
data = [
    ("Alice", "Sales", 5000),
    ("Bob", "Sales", 6000),
    ("Cathy", "IT", 7500),
    ("David", "IT", 8000),
    ("Eva", "Sales", 7000)
]
columns = ["Name", "Department", "Salary"]

df = spark.createDataFrame(data, columns)
df.show()
```

#### **Agrupando e Sumarizando**

```python
from pyspark.sql.functions import sum, avg, count

# Soma dos salários por departamento
df.groupBy("Department").sum("Salary").show()

# Média e contagem de salários por departamento
df.groupBy("Department").agg(
    avg("Salary").alias("Average Salary"),
    count("Name").alias("Employee Count")
).show()

# Soma total de salários
df.agg(sum("Salary").alias("Total Salary")).show()

# Contagem de valores distintos no departamento
df.groupBy("Department").agg(countDistinct("Name").alias("Distinct Employees")).show()
```


### **Agrupamento com Ordenação**

Após o agrupamento, você pode ordenar os resultados:

```python
df.groupBy("Department").sum("Salary").orderBy("sum(Salary)", ascending=False).show()
```


### **Trabalhando com Dados Nulos**

#### **Ignorar Dados Nulos**

Certifique-se de lidar com valores nulos antes de agregar:

```python
df = df.na.fill({"Salary": 0})
df.groupBy("Department").sum("Salary").show()
```

#### **Excluir Linhas com Nulos**

```python
df = df.dropna(subset=["Salary"])
df.groupBy("Department").sum("Salary").show()
```


### **Considerações de Desempenho**

1. **Particionamento:** Operações de agrupamento podem ser custosas em termos de computação. Use `repartition()` para redistribuir dados uniformemente antes do agrupamento:
    
    ```python
    df.repartition("group_column")
    ```
    
2. **Funções Personalizadas:** Crie funções agregadoras personalizadas para cálculos mais complexos usando `pyspark.sql.expressions`.

### **Resumo**

| Operação             | Código                                                |
| -------------------- | ----------------------------------------------------- |
| Soma                 | `df.groupBy("col").sum("numeric_col").show()`         |
| Média                | `df.groupBy("col").avg("numeric_col").show()`         |
| Contagem             | `df.groupBy("col").count().show()`                    |
| Contagem Distinta    | `df.groupBy("col").agg(countDistinct("col2")).show()` |
| Agregação Direta     | `df.agg(sum("numeric_col")).show()`                   |
| Agrupamento Múltiplo | `df.groupBy("col1", "col2").agg(sum("col3")).show()`  |

Com essas técnicas, você pode realizar agrupamentos e sumarizações poderosas e escaláveis para análise de dados em Spark.