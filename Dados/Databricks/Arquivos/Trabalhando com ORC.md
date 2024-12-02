
O **ORC** (Optimized Row Columnar) é um formato de arquivo projetado para armazenar grandes volumes de dados de maneira eficiente. Ele oferece compactação avançada, esquemas embutidos e otimizações para leitura e escrita, tornando-se ideal para pipelines de Big Data.

### **O Que é ORC?**

**ORC** é um formato de armazenamento em colunas, projetado para sistemas distribuídos. Ele é amplamente utilizado devido a:

- **Alta compactação**: Reduz o tamanho dos dados armazenados.
- **Suporte a esquemas embutidos**: Os metadados do esquema são armazenados no arquivo.
- **Otimizações para leitura seletiva de colunas**.


### **Lendo Arquivos ORC**

#### **Leitura Simples**

Carregue um arquivo ORC em um DataFrame Spark:

```python
df = spark.read.orc("dbfs:/mnt/my-bucket/data.orc")
df.show()
```

#### **Verificar o Esquema**

Exiba o esquema do arquivo:

```python
df.printSchema()
```

#### **Ler Múltiplos Arquivos**

Carregue todos os arquivos ORC de um diretório:

```python
df = spark.read.orc("dbfs:/mnt/my-bucket/orc_folder/")
df.show()
```

### **Esquemas com ORC**

O ORC embute o esquema no arquivo, mas você pode definir manualmente um esquema para otimizar a leitura.

#### **Esquema Inferido**

O Spark infere automaticamente o esquema:

```python
df = spark.read.orc("dbfs:/mnt/my-bucket/data.orc")
df.printSchema()
```

#### **Esquema Definido Manualmente**

Defina o esquema explicitamente:

```python
from pyspark.sql.types import StructType, StructField, StringType, IntegerType

schema = StructType([
    StructField("id", IntegerType(), True),
    StructField("name", StringType(), True),
    StructField("age", IntegerType(), True)
])

df = spark.read.schema(schema).orc("dbfs:/mnt/my-bucket/data.orc")
df.printSchema()
```


### **Manipulando Dados de Arquivos ORC**

#### **Selecionar e Filtrar Dados**

- **Selecionar Colunas**:

```python
df.select("name", "age").show()
```

- **Filtrar Linhas**:

```python
df.filter(df.age > 30).show()
```

#### **Adicionar Colunas**

Adicione uma nova coluna:

```python
from pyspark.sql.functions import col

df = df.withColumn("age_in_5_years", col("age") + 5)
df.show()
```


### **Escrevendo Arquivos ORC**

#### **Salvar um DataFrame como ORC**

Grave os dados no formato ORC:

```python
df.write.orc("dbfs:/mnt/my-bucket/output_data.orc")
```

#### **Salvar com Compactação**

Adicione compactação ao salvar os dados:

```python
df.write.option("compression", "snappy").orc("dbfs:/mnt/my-bucket/compressed_data.orc")
```

Compactações suportadas:

- **snappy** (padrão)
- **zlib**
- **none**

#### **Salvar com Particionamento**

Particione os dados para otimizar consultas:

```python
df.write.partitionBy("department").orc("dbfs:/mnt/my-bucket/partitioned_data.orc")
```

#### **Salvar como Um Único Arquivo**

Para consolidar os dados em um único arquivo:

```python
df.coalesce(1).write.orc("dbfs:/mnt/my-bucket/single_file_output.orc")
```


### **Trabalhando com ORC e Spark SQL**

#### **Registrar Tabela Temporária**

Registre um arquivo ORC como tabela temporária para consultas SQL:

```python
df.createOrReplaceTempView("orc_table")

spark.sql("SELECT * FROM orc_table WHERE age > 30").show()
```

#### **Criar Tabela Permanente**

Grave os dados como uma tabela no catálogo do Spark:

```python
df.write.saveAsTable("permanent_orc_table")
```


### **Integração com Delta Lake**

Você pode usar Delta Lake para aprimorar o formato ORC com funcionalidades adicionais, como transações ACID e versionamento.

#### **Criar Tabela Delta a Partir de ORC**

Converta arquivos ORC para Delta:

```python
df.write.format("delta").save("dbfs:/mnt/my-bucket/delta_table")
```

#### **Consultar Tabela Delta**

```python
df_delta = spark.read.format("delta").load("dbfs:/mnt/my-bucket/delta_table")
df_delta.show()
```



### **Exemplo Prático Completo**

#### **Cenário**

Você tem um arquivo ORC chamado `employees.orc` com o seguinte esquema:

- **id**: Identificador único.
- **name**: Nome do empregado.
- **age**: Idade.
- **department**: Departamento.

#### **Código**

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col

# Criar a SparkSession
spark = SparkSession.builder.appName("ORC Example").getOrCreate()

# Ler o arquivo ORC
df = spark.read.orc("dbfs:/mnt/my-bucket/employees.orc")

# Exibir os dados
df.show()

# Filtrar empregados com idade maior que 30
df_filtered = df.filter(df.age > 30)

# Adicionar uma coluna com a idade em 5 anos
df_transformed = df_filtered.withColumn("age_in_5_years", col("age") + 5)

# Salvar como ORC particionado por departamento
df_transformed.write.partitionBy("department").orc("dbfs:/mnt/my-bucket/output_employees.orc")
```


### **Dicas Úteis**

1. **Prefira ORC para Consultas Colunares**:
    
    - Ele é mais eficiente do que CSV e JSON para armazenar e consultar grandes volumes de dados.

2. **Use Compactação Sempre Que Possível**:
    
    - Compacte os dados para economizar espaço sem comprometer o desempenho.

3. **Combine Particionamento com Compactação**:
    
    - Particione dados por colunas frequentemente filtradas para otimizar consultas.

4. **Integre com o Catálogo do Spark**:
    
    - Registre arquivos ORC como tabelas permanentes para facilitar consultas com SQL.
