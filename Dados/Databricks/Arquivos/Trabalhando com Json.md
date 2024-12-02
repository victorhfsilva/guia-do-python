
### **Lendo Arquivos JSON**

#### **Ler um Arquivo JSON Simples**

Use o método `spark.read.json` para carregar arquivos JSON em um DataFrame:

```python
df = spark.read.json("dbfs:/mnt/my-bucket/data.json")
df.show()
```

#### **Ler com Esquema Inferido**

Por padrão, o Spark infere o esquema dos arquivos JSON. No entanto, para conjuntos de dados grandes, isso pode ser custoso:

```python
df = spark.read.option("inferSchema", "true").json("dbfs:/mnt/my-bucket/data.json")
df.printSchema()
```

#### **Especificar um Esquema Manualmente**

Definir o esquema manualmente melhora a performance e evita erros com tipos inconsistentes:

```python
from pyspark.sql.types import StructType, StructField, StringType, IntegerType

schema = StructType([
    StructField("id", IntegerType(), True),
    StructField("name", StringType(), True),
    StructField("age", IntegerType(), True),
    StructField("address", StructType([
        StructField("city", StringType(), True),
        StructField("state", StringType(), True)
    ]), True)
])

df = spark.read.schema(schema).json("dbfs:/mnt/my-bucket/data.json")
df.printSchema()
```

#### **Ler Arquivos JSON Multilinha**

Se o JSON estiver armazenado em várias linhas (multilinha), especifique a opção:

```python
df = spark.read.option("multiline", "true").json("dbfs:/mnt/my-bucket/multiline_data.json")
df.show()
```

### **Manipulando Dados JSON**

#### **Explorar o Esquema**

```python
df.printSchema()
```

#### **Trabalhar com Campos Aninhados**

Use `col` para acessar campos dentro de objetos aninhados:

```python
from pyspark.sql.functions import col

# Selecionar campos aninhados
df.select(col("name"), col("address.city")).show()
```

#### **Explodir Arrays**

Se um campo contém uma lista, use `explode` para criar uma linha por elemento:

```python
from pyspark.sql.functions import explode

df_exploded = df.withColumn("individual_value", explode(col("array_field")))
df_exploded.show()
```


### **Salvando Arquivos JSON**

#### **Salvar como JSON Simples**

```python
df.write.json("dbfs:/mnt/my-bucket/output_data.json")
```

#### **Salvar em JSON Compactado**

Especifique o formato de compactação:

```python
df.write.option("compression", "gzip").json("dbfs:/mnt/my-bucket/compressed_output.json")
```

#### **Salvar com Particionamento**

Particione os dados para melhorar a organização e consultas futuras:

```python
df.write.partitionBy("state").json("dbfs:/mnt/my-bucket/partitioned_output.json")
```


### **Exemplo Prático Completo**

#### **Arquivo JSON de Exemplo**

Salve o seguinte JSON no caminho `dbfs:/mnt/my-bucket/employees.json`:

```json
[
  {"id": 1, "name": "Alice", "age": 30, "address": {"city": "New York", "state": "NY"}},
  {"id": 2, "name": "Bob", "age": 35, "address": {"city": "Los Angeles", "state": "CA"}},
  {"id": 3, "name": "Cathy", "age": 28, "address": {"city": "Chicago", "state": "IL"}}
]
```

#### **Código de Exemplo**

```python
from pyspark.sql.types import StructType, StructField, StringType, IntegerType

# Definir o esquema
schema = StructType([
    StructField("id", IntegerType(), True),
    StructField("name", StringType(), True),
    StructField("age", IntegerType(), True),
    StructField("address", StructType([
        StructField("city", StringType(), True),
        StructField("state", StringType(), True)
    ]), True)
])

# Ler o arquivo JSON
df = spark.read.schema(schema).json("dbfs:/mnt/my-bucket/employees.json")

# Exibir os dados
df.show()

# Selecionar campos específicos
df.select("name", "address.city", "address.state").show()

# Salvar como JSON compactado
df.write.option("compression", "gzip").json("dbfs:/mnt/my-bucket/employees_output.json")
```

### **Dicas Úteis**

1. **Defina o Esquema Sempre Que Possível**:
    
    - Evite a inferência automática para melhorar o desempenho.
2. **Use Particionamento para Dados Grandes**:
    
    - Divida os dados em diretórios baseados em colunas.
3. **Lide com JSON Multilinha com Cuidado**:
    
    - Use a opção `multiline` para arquivos com múltiplos objetos JSON por linha.
4. **Combine JSON com Spark SQL**:
    
    - Crie uma tabela temporária para consultar JSONs diretamente:
        
        ```python
        df.createOrReplaceTempView("employees")
        spark.sql("SELECT * FROM employees WHERE age > 30").show()
        ```
        
