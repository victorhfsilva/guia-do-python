
O Apache Spark permite manipular arquivos **TXT** de maneira eficiente, mesmo para grandes volumes de dados. Com Spark, você pode ler, transformar, e salvar arquivos de texto de maneira otimizada.


### **Lendo Arquivos TXT**

#### **Ler um Arquivo TXT como DataFrame**

Use o método **`spark.read.text`** para carregar um arquivo de texto. Cada linha será lida como uma string:

```python
df = spark.read.text("dbfs:/mnt/my-bucket/data.txt")
df.show()
```

#### **Exibir Esquema do DataFrame**

```python
df.printSchema()
```

#### **Ler Múltiplos Arquivos**

Se você tiver vários arquivos no mesmo diretório, use curingas para carregar todos:

```python
df = spark.read.text("dbfs:/mnt/my-bucket/data_folder/*.txt")
df.show()
```


### **Manipulando Dados de Arquivos TXT**

#### **Renomear a Coluna Padrão**

Por padrão, o Spark lê os dados em uma única coluna chamada **`value`**. Renomeie a coluna para facilitar a manipulação:

```python
df = df.withColumnRenamed("value", "line")
df.show()
```

#### **Filtrar Linhas**

Use o método **`filter`** para selecionar linhas que contenham palavras ou padrões específicos:

```python
df_filtered = df.filter(df.line.contains("error"))
df_filtered.show()
```

#### **Dividir Linhas em Colunas**

Se o arquivo TXT contiver linhas delimitadas (como CSV), divida os valores usando **`split`**:

```python
from pyspark.sql.functions import split

df_split = df.withColumn("columns", split(df.line, "\t"))  # Delimitador é tabulação
df_split.show()
```

### **Escrevendo Arquivos TXT**

#### **Salvamento Simples**

Para salvar os dados em formato TXT, use o método **`write.text`**:

```python
df.write.text("dbfs:/mnt/my-bucket/output.txt")
```

#### **Salvar Compactado**

Adicione compactação ao salvar o arquivo:

```python
df.write.option("compression", "gzip").text("dbfs:/mnt/my-bucket/compressed_output.txt")
```

#### **Salvar em Partições**

Particione os dados ao salvar:

```python
df.write.partitionBy("column_name").text("dbfs:/mnt/my-bucket/partitioned_output")
```

#### **Salvar como Um Único Arquivo**

Para evitar que o Spark salve os dados como múltiplos arquivos:

```python
df.coalesce(1).write.text("dbfs:/mnt/my-bucket/single_file_output.txt")
```


### **Trabalhando com Arquivos TXT Estruturados**

Se o arquivo TXT tiver uma estrutura tabular, como colunas separadas por delimitadores, trate-o como um **CSV** sem cabeçalho.

#### **Ler TXT Estruturado**

Use **`spark.read.csv`** com o delimitador correto:

```python
df = spark.read.option("delimiter", "\t") \
               .option("header", "false") \
               .csv("dbfs:/mnt/my-bucket/structured_data.txt")
df.show()
```

#### **Definir um Esquema para TXT Estruturado**

Melhore o desempenho definindo um esquema explícito:

```python
from pyspark.sql.types import StructType, StructField, StringType, IntegerType

schema = StructType([
    StructField("id", IntegerType(), True),
    StructField("name", StringType(), True),
    StructField("age", IntegerType(), True)
])

df = spark.read.option("delimiter", "\t") \
               .schema(schema) \
               .csv("dbfs:/mnt/my-bucket/structured_data.txt")
df.printSchema()
df.show()
```


### **Trabalhando com RDDs para Arquivos TXT**

Se você preferir trabalhar com **RDDs** (Resilient Distributed Datasets), use o método **`sparkContext.textFile`**.

#### **Ler TXT como RDD**

```python
rdd = spark.sparkContext.textFile("dbfs:/mnt/my-bucket/data.txt")
rdd.collect()
```

#### **Filtrar e Transformar Linhas**

```python
rdd_filtered = rdd.filter(lambda line: "error" in line)
rdd_upper = rdd_filtered.map(lambda line: line.upper())
print(rdd_upper.collect())
```

#### **Converter RDD para DataFrame**

```python
df = rdd.map(lambda line: (line, )).toDF(["line"])
df.show()
```

### **Exemplo Prático Completo**

#### **Arquivo TXT de Exemplo**

Salve o seguinte conteúdo em `dbfs:/mnt/my-bucket/employees.txt`:

```
1,Alice,30,Sales
2,Bob,35,Marketing
3,Cathy,28,IT
```

#### **Código para Manipular o TXT**

```python
from pyspark.sql import SparkSession
from pyspark.sql.types import StructType, StructField, StringType, IntegerType

# Criar a SparkSession
spark = SparkSession.builder.appName("TXT Example").getOrCreate()

# Definir o esquema
schema = StructType([
    StructField("id", IntegerType(), True),
    StructField("name", StringType(), True),
    StructField("age", IntegerType(), True),
    StructField("department", StringType(), True)
])

# Ler o arquivo TXT como CSV sem cabeçalho
df = spark.read.option("delimiter", ",") \
               .schema(schema) \
               .csv("dbfs:/mnt/my-bucket/employees.txt")

# Exibir os dados
df.show()

# Filtrar por idade maior que 30
df_filtered = df.filter(df.age > 30)

# Salvar os dados filtrados como TXT
df_filtered.write.option("header", "true").text("dbfs:/mnt/my-bucket/filtered_employees.txt")
```


### **Dicas Úteis**

1. **Para Arquivos TXT Delimitados**:
    - Use `spark.read.csv` com o delimitador apropriado.

2. **Compacte Arquivos ao Salvar**:
    - Use opções de compressão como **gzip** para economizar espaço.

3. **Combine com SQL**:
    - Registre o DataFrame como uma tabela temporária e use Spark SQL para consultas complexas:
        
        ```python
        df.createOrReplaceTempView("employees")
        spark.sql("SELECT * FROM employees WHERE age > 30").show()
        ```
        
4. **Evite Arquivos Pequenos**:
    - Combine múltiplos arquivos em um único usando **`coalesce`**.

