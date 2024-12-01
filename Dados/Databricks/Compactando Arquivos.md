
O Apache Spark oferece suporte para salvar **DataFrames** em diversos formatos e com várias opções de compressão. A compactação é útil para reduzir o espaço de armazenamento e melhorar o desempenho de transferência de arquivos, especialmente em sistemas distribuídos.


### **O Que é Compactação de Arquivos?**

A compactação de arquivos reduz o tamanho dos dados armazenados, aplicando algoritmos que eliminam redundâncias ou padrões repetidos. Spark suporta compactação nativa para formatos como **CSV**, **JSON**, **Parquet**, **ORC**, e outros.


### **Métodos de Compressão Disponíveis**

Spark suporta os seguintes algoritmos de compressão:

|**Algoritmo**|**Formatos Suportados**|**Descrição**|
|---|---|---|
|**gzip**|CSV, JSON, Parquet, ORC|Compactação eficiente, mas lenta.|
|**bzip2**|CSV, JSON|Mais compactado, mas mais lento.|
|**snappy**|Parquet, ORC|Rápido, mas menos eficiente.|
|**lz4**|Parquet|Compactação rápida.|
|**zstd**|Parquet|Compactação equilibrada.|
|**deflate**|CSV, JSON, Parquet, ORC|Equilíbrio entre compactação e velocidade.|

### **Como Configurar Compactação com `df.write`**

A compactação é configurada por meio da opção **`compression`** no método **`write`**.

#### **Sintaxe Geral**

```python
df.write \
    .option("compression", "algorithm") \
    .format("format") \
    .save("path")
```


### **Exemplos de Compactação**

#### **Compactação com CSV**

Salvando um DataFrame no formato CSV com compressão **gzip**:

```python
df.write \
    .option("header", "true") \
    .option("compression", "gzip") \
    .csv("dbfs:/mnt/my-bucket/compressed_csv")
```

#### **Compactação com JSON**

Compactação de arquivos JSON com **bzip2**:

```python
df.write \
    .option("compression", "bzip2") \
    .json("dbfs:/mnt/my-bucket/compressed_json")
```

#### **Compactação com Parquet**

Compactação de arquivos Parquet com **snappy** (padrão do Parquet):

```python
df.write \
    .option("compression", "snappy") \
    .parquet("dbfs:/mnt/my-bucket/compressed_parquet")
```

#### **Compactação com ORC**

Compactação de arquivos ORC com **zstd**:

```python
df.write \
    .option("compression", "zstd") \
    .orc("dbfs:/mnt/my-bucket/compressed_orc")
```


### **Usando Compactação com Particionamento**

Você pode combinar particionamento e compactação para organizar os dados em subdiretórios e compactar cada partição:

```python
df.write \
    .option("compression", "gzip") \
    .partitionBy("state") \
    .csv("dbfs:/mnt/my-bucket/partitioned_compressed_csv")
```

Neste exemplo, os dados serão particionados por estado e compactados com **gzip**.



### **Verificando a Compactação**

#### **Listar Arquivos Compactados**

Após salvar o DataFrame, você pode listar os arquivos no diretório:

```python
files = dbutils.fs.ls("dbfs:/mnt/my-bucket/compressed_csv")
for file in files:
    print(f"Name: {file.name}, Size: {file.size} bytes")
```

#### **Confirmar Compactação**

- **Arquivos `.gz`**: Verifique se os arquivos possuem a extensão `.gz`, `.bz2`, etc.
- **Parquet ou ORC**: A compactação está integrada ao formato, então a verificação pode ser feita pela redução no tamanho do arquivo.


### **Boas Práticas de Compactação**

1. **Escolha o Algoritmo Baseado na Necessidade**:
    
    - **gzip** ou **bzip2**: Para arquivos CSV/JSON que serão transferidos ou armazenados.
    - **snappy**: Para Parquet/ORC em pipelines analíticos que requerem rapidez.
    - **zstd**: Para um equilíbrio entre compactação e desempenho.

2. **Combine Compactação com Particionamento**:
    
    - Para dados grandes, particione por colunas frequentemente filtradas e compacte cada partição.

3. **Avalie a Performance**:
    
    - Teste diferentes algoritmos para encontrar o melhor equilíbrio entre compactação e velocidade para o seu caso de uso.


### **Exemplo Prático Completo**

#### **Código de Exemplo**

```python
from pyspark.sql import SparkSession

# Criar a SparkSession
spark = SparkSession.builder.appName("Compression Example").getOrCreate()

# Criar um DataFrame de exemplo
data = [("Alice", 28, "Sales"), ("Bob", 35, "Marketing"), ("Cathy", 30, "IT")]
columns = ["Name", "Age", "Department"]
df = spark.createDataFrame(data, columns)

# Salvar o DataFrame como CSV compactado com gzip
df.write \
    .option("header", "true") \
    .option("compression", "gzip") \
    .csv("dbfs:/mnt/my-bucket/compressed_csv")

# Salvar o DataFrame como Parquet compactado com snappy
df.write \
    .option("compression", "snappy") \
    .parquet("dbfs:/mnt/my-bucket/compressed_parquet")
```

#### **Verificar os Arquivos**

```python
files = dbutils.fs.ls("dbfs:/mnt/my-bucket/compressed_csv")
for file in files:
    print(f"Name: {file.name}, Size: {file.size} bytes")
```
