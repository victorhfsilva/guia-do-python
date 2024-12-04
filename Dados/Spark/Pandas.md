
O módulo **`pyspark.pandas`** é uma integração poderosa que permite usar APIs do Pandas com grandes conjuntos de dados, aproveitando a escalabilidade do Spark. Ele fornece uma interface semelhante ao Pandas, mas funciona em um ambiente distribuído, facilitando a transição para quem já está familiarizado com o Pandas.


### **O Que é `pyspark.pandas`?**

O **`pyspark.pandas`** (ou **Koalas** em versões anteriores) combina a simplicidade do Pandas com a escalabilidade do Spark. Ele suporta a maioria das operações padrão do Pandas e permite trabalhar com grandes conjuntos de dados.


### **Configurando o Ambiente**

#### **Importar `pyspark.pandas`**

O módulo está disponível no PySpark a partir da versão 3.2.0. Para usá-lo:

```python
import pyspark.pandas as ps
```


### **Criando DataFrames com `pyspark.pandas`**

#### **Criar um DataFrame a Partir de um Dicionário**

```python
import pyspark.pandas as ps

data = {"id": [1, 2, 3], "name": ["Alice", "Bob", "Cathy"], "age": [25, 30, 35]}
df = ps.DataFrame(data)
print(df)
```

#### **Criar a Partir de um Arquivo CSV**

```python
df = ps.read_csv("dbfs:/mnt/my-bucket/data.csv")
print(df)
```

#### **Converter de um DataFrame Spark**

Se você já tem um DataFrame Spark:

```python
spark_df = spark.read.csv("dbfs:/mnt/my-bucket/data.csv", header=True, inferSchema=True)
ps_df = spark_df.to_pandas()
print(ps_df)
```

#### **Converter para DataFrame Spark**

```python
spark_df = ps_df.to_spark()
spark_df.show()
```

### **Operações Básicas com `pyspark.pandas`**

#### **Seleção de Colunas**

```python
# Selecionar uma única coluna
print(df["name"])

# Selecionar múltiplas colunas
print(df[["name", "age"]])
```

#### **Filtragem de Dados**

```python
# Filtrar linhas
filtered_df = df[df["age"] > 30]
print(filtered_df)
```

#### **Adicionar Colunas**

```python
# Adicionar uma nova coluna
df["age_in_5_years"] = df["age"] + 5
print(df)
```

#### **Operações de Agrupamento**

```python
# Agrupar e calcular a média
grouped = df.groupby("name").mean()
print(grouped)
```

### **Leitura e Escrita de Arquivos**

#### **Leitura de CSV**

```python
df = ps.read_csv("dbfs:/mnt/my-bucket/data.csv")
print(df)
```

#### **Leitura de Parquet**

```python
df = ps.read_parquet("dbfs:/mnt/my-bucket/data.parquet")
print(df)
```

#### **Escrita de Arquivos**

```python
# Salvar como CSV
df.to_csv("dbfs:/mnt/my-bucket/output.csv", index=False)

# Salvar como Parquet
df.to_parquet("dbfs:/mnt/my-bucket/output.parquet")
```

### **Operações Avançadas**

#### **Ordenação**

```python
df_sorted = df.sort_values(by="age", ascending=False)
print(df_sorted)
```

#### **Operações com Índices**

```python
# Definir uma coluna como índice
df = df.set_index("id")
print(df)

# Resetar o índice
df = df.reset_index()
print(df)
```

#### **Operações com Dados Faltantes**

```python
# Substituir valores nulos
df = df.fillna({"age": 0})
print(df)

# Remover linhas com valores nulos
df = df.dropna()
print(df)
```

### **Integração com SQL**

Você pode registrar um DataFrame `pyspark.pandas` como uma tabela Spark e usar SQL:

```python
# Registrar o DataFrame como uma tabela temporária
df.to_spark().createOrReplaceTempView("pandas_table")

# Executar uma consulta SQL
result = spark.sql("SELECT * FROM pandas_table WHERE age > 30")
result.show()
```


### **Desempenho e Boas Práticas**

1. **Evite Arquivos Pequenos**:
    
    - Use **`repartition`** no DataFrame Spark antes de convertê-lo para `pyspark.pandas`:
    
    ```python
    spark_df = spark_df.repartition(10)
    ps_df = spark_df.pandas_api()
    ```
    
2. **Limite o Tamanho de Dados**:
    
    - Para operações que não requerem paralelismo, converta para Pandas:
    
    ```python
    pandas_df = ps_df.to_pandas()
    ```
    
3. **Prefira Operações em Spark**:
    
    - Sempre que possível, realize operações complexas diretamente no Spark antes de usar `pyspark.pandas`.


