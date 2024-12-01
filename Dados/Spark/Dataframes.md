
Os **DataFrames** são uma abstração de dados estruturados no Apache Spark, permitindo manipulação eficiente e escalável de grandes volumes de dados.

## **Criando DataFrames no Spark**

Você pode criar DataFrames no Spark a partir de dados estruturados, como listas, RDDs, ou arquivos.

#### **Criando DataFrames a partir de listas**

```python
from pyspark.sql import SparkSession

# Iniciando uma SparkSession
spark = SparkSession.builder \
    .appName("Criando DataFrames") \
    .getOrCreate()

# Dados e colunas
data = [("Alice", 28), ("Bob", 35), ("Cathy", 30)]
columns = ["Name", "Age"]

# Criando o DataFrame
df = spark.createDataFrame(data, columns)

# Exibindo o DataFrame
df.show()
```

#### **Criando DataFrames a partir de RDDs**

```python
# Criando um RDD
rdd = spark.sparkContext.parallelize([("David", 40), ("Eva", 25)])

# Criando DataFrame a partir do RDD
df_from_rdd = rdd.toDF(["Name", "Age"])

df_from_rdd.show()
```


### **Carregando DataFrames a partir de arquivos**

O Spark suporta diversos formatos de arquivo como **CSV**, **JSON**, **Parquet**, e **Avro**.

#### **Carregando arquivos CSV**

```python
# Carregando arquivo CSV
df_csv = spark.read.csv("path/to/file.csv", header=True, inferSchema=True, sep=';')

# Exibindo o DataFrame
df_csv.show()
```

#### **Carregando arquivos JSON**

```python
# Carregando arquivo JSON
df_json = spark.read.json("path/to/file.json")

df_json.show()
```

#### **Carregando arquivos Parquet**

```python
# Carregando arquivo Parquet
df_parquet = spark.read.parquet("path/to/file.parquet")

df_parquet.show()
```

#### **Especificando opções ao carregar**

Você pode definir opções como separador, esquema de dados, e modo de leitura:

```python
df_csv = spark.read.option("delimiter", ";").csv("path/to/file.csv", header=True, inferSchema=True)
```


## **Salvando DataFrames no Spark**

Você pode salvar DataFrames em diferentes formatos para armazenamento persistente.

#### **Salvando em CSV**

```python
df.write.csv("path/to/save", header=True)
```

#### **Salvando em Parquet**

```python
df.write.parquet("path/to/save")
```

#### **Salvando em JSON**

```python
df.write.json("path/to/save")
```



## **Convertendo DataFrames do Spark em pandas**

O Spark permite converter DataFrames para **pandas** para operações que exigem análise local.

#### **Convertendo DataFrame Spark para pandas**

```python
# Convertendo DataFrame do Spark para pandas
df_pandas = df.toPandas()

# Exibindo o DataFrame pandas
print(df_pandas)
```

#### **Convertendo pandas para DataFrame Spark**

```python
import pandas as pd

# Criando um DataFrame pandas
data_pandas = pd.DataFrame({"Name": ["John", "Doe"], "Age": [45, 33]})

# Convertendo pandas para DataFrame Spark
df_spark = spark.createDataFrame(data_pandas)

df_spark.show()
```



### **Exemplos Práticos**

#### **Carregando um CSV e realizando operações**

```python
df = spark.read.csv("path/to/people.csv", header=True, inferSchema=True)

# Exibindo as primeiras linhas
df.show(5)

# Filtrando dados
df.filter(df.Age > 30).show()

# Selecionando colunas específicas
df.select("Name").show()
```

#### **Conversão e Análise Local**

```python
# Converter para pandas
df_pandas = df.toPandas()

# Realizar análise local
print(df_pandas.describe())
```


### **Dicas Úteis**

1. **Inferência de Schema:** Use `inferSchema=True` para detectar automaticamente os tipos de dados no arquivo.
2. **Particionamento:** Para grandes volumes, particione os dados antes de salvar:
    
    ```python
    df.write.partitionBy("column_name").csv("path/to/save")
    ```
    
3. **Spark UI:** Monitore o progresso dos jobs no Spark usando a interface web do Spark.

Com essas técnicas, você pode criar, manipular e converter DataFrames no Spark para trabalhar de forma eficiente com dados estruturados!