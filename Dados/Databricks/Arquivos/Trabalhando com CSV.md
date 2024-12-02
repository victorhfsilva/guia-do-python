
Os arquivos **CSV** (Comma-Separated Values) são amplamente utilizados para armazenar dados estruturados. Com o **Databricks** e o **Apache Spark**, você pode ler, manipular, salvar e transformar arquivos CSV de maneira eficiente, mesmo em grandes volumes de dados.

### **Lendo Arquivos CSV**

#### **Leitura Simples**

Carregue um arquivo CSV como um DataFrame:

```python
df = spark.read.csv("dbfs:/mnt/my-bucket/data.csv")
df.show()
```

#### **Leitura com Cabeçalho e Inferência de Esquema**

Adicione opções para ler o cabeçalho e inferir automaticamente os tipos de dados:

```python
df = spark.read.option("header", "true") \
               .option("inferSchema", "true") \
               .csv("dbfs:/mnt/my-bucket/data.csv")
df.printSchema()
```

#### **Definir um Esquema Personalizado**

Para arquivos grandes ou onde o esquema é conhecido, definir manualmente o esquema melhora o desempenho:

```python
from pyspark.sql.types import StructType, StructField, StringType, IntegerType

schema = StructType([
    StructField("id", IntegerType(), True),
    StructField("name", StringType(), True),
    StructField("age", IntegerType(), True)
])

df = spark.read.option("header", "true").schema(schema).csv("dbfs:/mnt/my-bucket/data.csv")
df.printSchema()
```

#### **Leitura de Arquivos CSV com Delimitadores Diferentes**

Se o arquivo usar outro delimitador, como `;` ou `|`, especifique-o:

```python
df = spark.read.option("header", "true") \
               .option("delimiter", ";") \
               .csv("dbfs:/mnt/my-bucket/data.csv")
```

#### **Leitura de Múltiplos Arquivos**

Você pode carregar vários arquivos de um diretório:

```python
df = spark.read.option("header", "true") \
               .csv("dbfs:/mnt/my-bucket/data_folder/")
```

### **Manipulando Dados Lidos de CSV**

#### **Exibir Dados**

- **Exibir as Primeiras Linhas**:

```python
df.show(5)
```

- **Exibir o Esquema**:

```python
df.printSchema()
```

#### **Selecionar e Filtrar Dados**

- **Selecionar Colunas Específicas**:

```python
df.select("name", "age").show()
```

- **Filtrar Linhas**:

```python
df.filter(df.age > 30).show()
```

#### **Transformar Dados**

- **Adicionar uma Nova Coluna**:

```python
from pyspark.sql.functions import col

df = df.withColumn("age_in_5_years", col("age") + 5)
df.show()
```

- **Remover Nulos**:

```python
df = df.dropna()
```


### **Salvando Arquivos CSV**

#### **Salvamento Simples**

Salve o DataFrame como um arquivo CSV:

```python
df.write.csv("dbfs:/mnt/my-bucket/output_data.csv")
```

#### **Salvar com Cabeçalho**

Inclua o cabeçalho no arquivo CSV:

```python
df.write.option("header", "true").csv("dbfs:/mnt/my-bucket/output_data_with_header.csv")
```

#### **Salvamento Compactado**

Salve o CSV compactado com **gzip**:

```python
df.write.option("header", "true") \
        .option("compression", "gzip") \
        .csv("dbfs:/mnt/my-bucket/compressed_output_data.csv")
```

#### **Salvar com Particionamento**

Particione os dados por uma coluna:

```python
df.write.option("header", "true") \
        .partitionBy("state") \
        .csv("dbfs:/mnt/my-bucket/partitioned_data.csv")
```

#### **Salvar como Um Único Arquivo**

Por padrão, o Spark cria vários arquivos em um diretório. Use **`coalesce(1)`** para salvar como um único arquivo:

```python
df.coalesce(1).write.option("header", "true").csv("dbfs:/mnt/my-bucket/single_file_output.csv")
```


### **Tratando Erros Comuns com CSV**

#### **Arquivos com Formato Inconsistente**

Adicione a opção para ignorar linhas malformadas:

```python
df = spark.read.option("header", "true") \
               .option("mode", "DROPMALFORMED") \
               .csv("dbfs:/mnt/my-bucket/malformed_data.csv")
```

#### **Valores Nulos ou Vazios**

Substitua valores nulos ou vazios por padrões:

```python
df = df.fillna({"age": 0, "name": "Unknown"})
```


### **Exemplo Completo**

#### **Arquivo CSV de Exemplo**

Salve o seguinte arquivo em `dbfs:/mnt/my-bucket/employees.csv`:

```csv
id,name,age,department
1,Alice,30,Sales
2,Bob,35,Marketing
3,Cathy,28,IT
4,,40,HR
```

#### **Código para Manipular o CSV**

```python
from pyspark.sql import SparkSession

# Criar a SparkSession
spark = SparkSession.builder.appName("CSV Example").getOrCreate()

# Ler o CSV com cabeçalho e esquema inferido
df = spark.read.option("header", "true").option("inferSchema", "true").csv("dbfs:/mnt/my-bucket/employees.csv")

# Exibir os dados
df.show()

# Tratar valores nulos
df = df.fillna({"name": "Unknown"})

# Adicionar uma coluna calculada
from pyspark.sql.functions import col
df = df.withColumn("age_in_10_years", col("age") + 10)

# Salvar os dados tratados como CSV
df.write.option("header", "true").csv("dbfs:/mnt/my-bucket/employees_output.csv")
```


### **6. Dicas Úteis**

1. **Defina o Esquema Sempre Que Possível**:
    
    - Evite a inferência automática para melhorar o desempenho.

2. **Use Compactação para Arquivos Grandes**:
    
    - Compacte os dados com **gzip** ou **bzip2** para economizar espaço.

3. **Combine com SQL**:
    
    - Crie uma tabela temporária para consultas SQL:
        
        ```python
        df.createOrReplaceTempView("employees")
        spark.sql("SELECT * FROM employees WHERE age > 30").show()
        ```
        
4. **Evite Pequenos Arquivos**:
    
    - Use **`coalesce`** ou **`repartition`** para consolidar arquivos.
