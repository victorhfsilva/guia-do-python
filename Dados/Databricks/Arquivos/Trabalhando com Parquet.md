
O formato **Parquet** é amplamente utilizado em pipelines de dados devido à sua eficiência, compactação nativa e suporte para colunas armazenadas individualmente. Ele é ideal para trabalhar com grandes volumes de dados, oferecendo excelente desempenho em leitura e escrita.

### **O Que é Parquet?**

O **Parquet** é um formato de armazenamento em colunas, otimizado para sistemas distribuídos como o Apache Spark. Ele oferece:

- **Compactação nativa**: Reduz o tamanho dos arquivos.
- **Esquema embutido**: Mantém metadados no próprio arquivo.
- **Otimização de leitura**: Leitura seletiva de colunas.


### **Lendo Arquivos Parquet**

#### **Ler um Arquivo Parquet**

Carregue um arquivo Parquet em um DataFrame:

```python
df = spark.read.parquet("dbfs:/mnt/my-bucket/data.parquet")
df.show()
```

#### **Verificar o Esquema**

Visualize o esquema do arquivo:

```python
df.printSchema()
```

#### **Ler Múltiplos Arquivos**

Carregue todos os arquivos Parquet de um diretório:

```python
df = spark.read.parquet("dbfs:/mnt/my-bucket/parquet_folder/")
df.show()
```


### **Esquemas com Parquet**

O Parquet embute o esquema nos arquivos, mas você pode definir manualmente um esquema para melhorar a performance em leituras de arquivos grandes.

#### **Esquema Inferido**

O Spark infere automaticamente o esquema ao carregar um arquivo Parquet:

```python
df = spark.read.parquet("dbfs:/mnt/my-bucket/data.parquet")
df.printSchema()
```

#### **Esquema Definido Manualmente**

Defina um esquema personalizado:

```python
from pyspark.sql.types import StructType, StructField, StringType, IntegerType

schema = StructType([
    StructField("id", IntegerType(), True),
    StructField("name", StringType(), True),
    StructField("age", IntegerType(), True)
])

df = spark.read.schema(schema).parquet("dbfs:/mnt/my-bucket/data.parquet")
df.printSchema()
```


### **Manipulando Dados de Arquivos Parquet**

#### **Selecionar e Filtrar Dados**

- **Selecionar Colunas**:

```python
df.select("name", "age").show()
```

- **Filtrar Linhas**:

```python
df.filter(df.age > 30).show()
```

#### **Adicionar ou Transformar Colunas**

Adicione uma nova coluna calculada:

```python
from pyspark.sql.functions import col

df = df.withColumn("age_in_5_years", col("age") + 5)
df.show()
```



### **Escrevendo Arquivos Parquet**

#### **Salvar um DataFrame como Parquet**

Grave os dados em um arquivo Parquet:

```python
df.write.parquet("dbfs:/mnt/my-bucket/output_data.parquet")
```

#### **Salvar com Compactação**

Adicione compactação ao salvar os dados:

```python
df.write.option("compression", "snappy").parquet("dbfs:/mnt/my-bucket/compressed_data.parquet")
```

Algoritmos de compactação suportados:

- **snappy** (padrão)
- **gzip**
- **lz4**
- **zstd**

#### **Salvar com Particionamento**

Particione os dados por uma ou mais colunas:

```python
df.write.partitionBy("department").parquet("dbfs:/mnt/my-bucket/partitioned_data.parquet")
```

#### **Salvar como Um Único Arquivo**

Para consolidar os dados em um único arquivo:

```python
df.coalesce(1).write.parquet("dbfs:/mnt/my-bucket/single_file_output.parquet")
```

### **Trabalhando com Parquet e Spark SQL**

#### **Registrar Tabela Temporária**

Carregue um arquivo Parquet como uma tabela temporária para consultas SQL:

```python
df.createOrReplaceTempView("parquet_table")

spark.sql("SELECT * FROM parquet_table WHERE age > 30").show()
```

#### **Criar Tabela Permanente**

Grave os dados como uma tabela permanente no catálogo:

```python
df.write.saveAsTable("permanent_parquet_table")
```


### **Integração com Delta Lake**

O Delta Lake estende o formato Parquet com funcionalidades adicionais, como transações ACID, versionamento e otimizações.

#### **Criar Tabela Delta a Partir de Parquet**

```python
df.write.format("delta").save("dbfs:/mnt/my-bucket/delta_table")
```

#### **Consultar Delta Table**

```python
df_delta = spark.read.format("delta").load("dbfs:/mnt/my-bucket/delta_table")
df_delta.show()
```


### **Exemplo Prático Completo**

#### **Cenário**

Você tem um arquivo Parquet chamado `employees.parquet` com o seguinte esquema:

- **id**: Identificador único.
- **name**: Nome do empregado.
- **age**: Idade.
- **department**: Departamento.

#### **Código**

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col

# Criar a SparkSession
spark = SparkSession.builder.appName("Parquet Example").getOrCreate()

# Ler o arquivo Parquet
df = spark.read.parquet("dbfs:/mnt/my-bucket/employees.parquet")

# Exibir os dados
df.show()

# Filtrar os empregados com idade maior que 30
df_filtered = df.filter(df.age > 30)

# Adicionar uma coluna com a idade em 5 anos
df_transformed = df_filtered.withColumn("age_in_5_years", col("age") + 5)

# Salvar como Parquet particionado por departamento
df_transformed.write.partitionBy("department").parquet("dbfs:/mnt/my-bucket/output_employees.parquet")
```


### **Dicas Úteis**

1. **Prefira Parquet para Pipelines Analíticos**:
    
    - É mais eficiente que CSV ou JSON para armazenar e consultar grandes volumes de dados.

2. **Use Compactação Adequada**:
    
    - Compacte os dados para economizar espaço sem comprometer o desempenho.

3. **Combine Particionamento com Compactação**:
    
    - Particionar dados por colunas frequentemente filtradas melhora o desempenho das consultas.

4. **Aproveite o Catálogo do Spark**:
    
    - Registre tabelas Parquet no catálogo para consultas SQL diretas.

