
O formato **AVRO** é amplamente utilizado em pipelines de dados por ser eficiente, compacto e suportar esquemas embutidos. O Apache Spark oferece suporte nativo para leitura, manipulação e gravação de arquivos AVRO. 

### **O Que é AVRO?**

**AVRO** é um formato de serialização de dados binário projetado para ser compacto, rápido e de fácil integração com esquemas. Ele é ideal para pipelines distribuídos, como os do Spark.


### **Lendo Arquivos AVRO**

#### **Leitura Simples**

Use o método **`spark.read.format("avro")`** para carregar um arquivo AVRO:

```python
df = spark.read.format("avro").load("dbfs:/mnt/my-bucket/data.avro")
df.show()
```

#### **Verificar o Esquema**

Exiba o esquema do DataFrame:

```python
df.printSchema()
```

#### **Lendo Múltiplos Arquivos**

Carregue todos os arquivos AVRO de um diretório:

```python
df = spark.read.format("avro").load("dbfs:/mnt/my-bucket/avro_folder/")
df.show()
```


### **Esquemas com AVRO**

#### **Inferência Automática de Esquema**

Por padrão, o Spark infere o esquema dos arquivos AVRO.

#### **Especificar um Esquema**

Definir um esquema manualmente pode melhorar o desempenho e evitar problemas com dados inconsistentes:

```python
from pyspark.sql.types import StructType, StructField, StringType, IntegerType

schema = StructType([
    StructField("id", IntegerType(), True),
    StructField("name", StringType(), True),
    StructField("age", IntegerType(), True)
])

df = spark.read.format("avro") \
               .schema(schema) \
               .load("dbfs:/mnt/my-bucket/data.avro")
df.printSchema()
```


### **Manipulando Dados de Arquivos AVRO**

#### **Selecionar e Filtrar Dados**

- **Selecionar Colunas Específicas**:

```python
df.select("name", "age").show()
```

- **Filtrar Linhas**:

```python
df.filter(df.age > 30).show()
```

#### **Criar Novas Colunas**

Adicione uma coluna calculada:

```python
from pyspark.sql.functions import col

df = df.withColumn("age_in_5_years", col("age") + 5)
df.show()
```


### **Escrevendo Arquivos AVRO**

#### **Gravação Simples**

Grave um DataFrame no formato AVRO:

```python
df.write.format("avro").save("dbfs:/mnt/my-bucket/output_data.avro")
```

#### **Gravar com Particionamento**

Particione os dados por uma coluna:

```python
df.write.format("avro") \
       .partitionBy("department") \
       .save("dbfs:/mnt/my-bucket/partitioned_data.avro")
```

#### **Gravar com Compactação**

Adicione compactação ao gravar arquivos AVRO:

```python
df.write.format("avro") \
       .option("compression", "snappy") \
       .save("dbfs:/mnt/my-bucket/compressed_data.avro")
```

Algoritmos suportados para compactação:

- **snappy** (padrão)
- **deflate**
- **bzip2**
- **xz**



### **Trabalhando com AVRO e Spark SQL**

#### **Registrar Tabela Temporária**

Você pode registrar um DataFrame AVRO como uma tabela temporária e executar consultas SQL:

```python
df.createOrReplaceTempView("avro_table")

spark.sql("SELECT * FROM avro_table WHERE age > 30").show()
```

#### **Criar Tabela Permanente no Catálogo**

```python
df.write.format("avro").saveAsTable("permanent_avro_table")
```


### **Exemplo Prático Completo**

#### **Cenário**

Você tem um arquivo AVRO chamado `employees.avro` com o seguinte esquema:

```json
{
  "type": "record",
  "name": "Employee",
  "fields": [
    {"name": "id", "type": "int"},
    {"name": "name", "type": "string"},
    {"name": "age", "type": "int"},
    {"name": "department", "type": "string"}
  ]
}
```

#### **Código de Exemplo**

```python
from pyspark.sql import SparkSession

# Criar a SparkSession
spark = SparkSession.builder.appName("AVRO Example").getOrCreate()

# Ler o arquivo AVRO
df = spark.read.format("avro").load("dbfs:/mnt/my-bucket/employees.avro")

# Exibir os dados
df.show()

# Filtrar por idade maior que 30
df_filtered = df.filter(df.age > 30)

# Adicionar uma coluna com a idade em 5 anos
df_transformed = df_filtered.withColumn("age_in_5_years", df_filtered.age + 5)

# Salvar como AVRO particionado por departamento
df_transformed.write.format("avro") \
                    .partitionBy("department") \
                    .save("dbfs:/mnt/my-bucket/output_employees.avro")
```


### **Dicas Úteis**

1. **Prefira Definir Esquemas Manualmente**:
    
    - Isso reduz o tempo de leitura e evita problemas com inferência de esquema.

2. **Compacte Arquivos Sempre Que Possível**:
    
    - Use **snappy** para compactação rápida e eficiente.

3. **Combine com Particionamento**:
    
    - Organize grandes conjuntos de dados para consultas eficientes.

4. **Integre com Tabelas SQL**:
    
    - Registre arquivos AVRO no catálogo do Spark para facilitar análises com SQL.

