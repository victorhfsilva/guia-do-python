
O método **`filter`** no Apache Spark é uma ferramenta essencial para realizar filtragens de dados em **DataFrames** ou **RDDs**. Ele permite aplicar condições lógicas para selecionar apenas os dados que atendem a critérios específicos.


### **Como Funciona o `filter`**

O `filter` cria um novo DataFrame contendo apenas as linhas que satisfazem a condição fornecida.

Sintaxe básica:

```python
df_filtered = df.filter(condition)
```

### **Filtragem em DataFrames**

#### **Filtrando com Condições Simples**

Use expressões de comparação diretamente nas colunas:

```python
df_filtered = df.filter(df["column_name"] > 100)
df_filtered.show()
```

Você também pode usar o método `col` para referenciar colunas:

```python
from pyspark.sql.functions import col

df_filtered = df.filter(col("column_name") == "value")
df_filtered.show()
```

#### **Filtragem com Condições Múltiplas**

Combine múltiplas condições com operadores lógicos:

- **AND** (`&`):

```python
df_filtered = df.filter((col("column1") > 50) & (col("column2") < 100))
df_filtered.show()
```

- **OR** (`|`):

```python
df_filtered = df.filter((col("column1") == "value1") | (col("column2") == "value2"))
df_filtered.show()
```

- **NOT** (`~`):

```python
df_filtered = df.filter(~(col("column_name") < 0))
df_filtered.show()
```

#### **Filtragem com Strings**

- **Igualdade e Diferença:**

```python
df_filtered = df.filter(col("string_column") == "desired_value")
```

- **Expressões Regulares:**

```python
df_filtered = df.filter(col("string_column").rlike("regex_pattern"))
```


### **Filtragem com Valores Nulos**

#### **Selecionar Linhas com Valores Nulos**

Use a função `isNull()`:

```python
df_filtered = df.filter(col("column_name").isNull())
df_filtered.show()
```

#### **Selecionar Linhas sem Valores Nulos**

Use a função `isNotNull()`:

```python
df_filtered = df.filter(col("column_name").isNotNull())
df_filtered.show()
```


### **Filtragem com Listas**

Filtre colunas com valores em uma lista específica usando a função `isin()`:

```python
df_filtered = df.filter(col("column_name").isin("value1", "value2", "value3"))
df_filtered.show()
```

Para excluir os valores da lista:

```python
df_filtered = df.filter(~col("column_name").isin("value1", "value2"))
df_filtered.show()
```


### **Filtragem por Data e Hora**

#### **Comparação Simples**

```python
from pyspark.sql.functions import to_date

# Converter string para data, se necessário
df = df.withColumn("date_column", to_date(col("date_column"), "yyyy-MM-dd"))

# Filtrar por data
df_filtered = df.filter(col("date_column") > "2023-01-01")
df_filtered.show()
```

#### **Intervalo de Datas**

```python
df_filtered = df.filter((col("date_column") >= "2023-01-01") & (col("date_column") <= "2023-12-31"))
df_filtered.show()
```


### **Filtragem com SQL Expressions**

O método `filter` também aceita strings como expressões SQL:

```python
df_filtered = df.filter("column_name > 100 AND column2 = 'value'")
df_filtered.show()
```


### **Exemplo Completo**

#### **DataFrame de Exemplo**

```python
from pyspark.sql import SparkSession

# Criando uma SparkSession
spark = SparkSession.builder.appName("Filter Example").getOrCreate()

# Criando um DataFrame de exemplo
data = [
    ("Alice", 28, 5000, "2023-01-01"),
    ("Bob", 35, 6000, "2023-02-15"),
    ("Cathy", 30, 7500, None)
]
columns = ["Name", "Age", "Salary", "JoinDate"]

df = spark.createDataFrame(data, columns)
df.show()
```

#### **Filtragens**

```python
from pyspark.sql.functions import col

# Filtrar por idade maior que 30
df_filtered = df.filter(col("Age") > 30)
df_filtered.show()

# Filtrar por salário maior que 5000 e idade menor que 35
df_filtered = df.filter((col("Salary") > 5000) & (col("Age") < 35))
df_filtered.show()

# Filtrar por valores nulos na coluna JoinDate
df_filtered = df.filter(col("JoinDate").isNull())
df_filtered.show()

# Filtrar usando uma lista de valores
df_filtered = df.filter(col("Name").isin("Alice", "Cathy"))
df_filtered.show()
```

### **Boas Práticas**

1. **Combine Condições para Melhorar a Legibilidade:**  
    Agrupe expressões lógicas com parênteses para evitar ambiguidades.
2. **Filtre Antes de Processar:**  
    Reduza o tamanho dos dados aplicando filtros antes de outras transformações ou operações.
3. **Use Funções SQL para Complexidade:**  
    Se as condições forem muito detalhadas, considere usar expressões SQL para maior clareza.

Com o método `filter`, você pode realizar filtragens avançadas e altamente específicas em seus dados, maximizando a eficiência e clareza no tratamento de grandes volumes de informação!