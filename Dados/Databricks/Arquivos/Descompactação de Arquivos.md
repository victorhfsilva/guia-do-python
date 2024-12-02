
A descompactação de arquivos é uma etapa comum em pipelines de dados, especialmente quando trabalhamos com arquivos compactados para otimizar o armazenamento e a transferência. O **Databricks** e o **Apache Spark** permitem descompactar arquivos com suporte a diversos formatos, como **gzip**, **bzip2**, **zip**, e **tar**.


### **Suporte do Spark para Arquivos Compactados**

O Spark pode ler arquivos compactados de maneira nativa para formatos como **gzip**, **bzip2**, **xz**, e **snappy**. Para esses formatos, não é necessário descompactá-los manualmente; o Spark faz isso automaticamente ao carregar os dados.

#### **Leitura de Arquivos Compactados**

```python
df = spark.read.csv("dbfs:/mnt/my-bucket/compressed_file.csv.gz", header=True)
df.show()
```

### **Trabalhando com Arquivos ZIP**

O formato **ZIP** não é suportado nativamente pelo Spark. Para trabalhar com arquivos ZIP, você precisa descompactá-los manualmente antes de processá-los.

#### **Descompactando Arquivos ZIP no Databricks**

Use o comando **`dbutils.fs.cp`** e o módulo **`zipfile`** para extrair os arquivos.

##### **Exemplo**

```python
import zipfile

# Caminho do arquivo ZIP
zip_path = "/dbfs/mnt/my-bucket/data.zip"
extract_path = "/dbfs/mnt/my-bucket/extracted_data"

# Descompactar o arquivo ZIP
with zipfile.ZipFile(zip_path, 'r') as zip_ref:
    zip_ref.extractall(extract_path)

# Listar os arquivos extraídos
files = dbutils.fs.ls("dbfs:/mnt/my-bucket/extracted_data")
for file in files:
    print(f"Name: {file.name}, Size: {file.size}")
```

### **Trabalhando com Arquivos TAR**

O Spark também não suporta arquivos **TAR** diretamente. Use o módulo **`tarfile`** para descompactá-los.

#### **Descompactando Arquivos TAR**

```python
import tarfile

# Caminho do arquivo TAR
tar_path = "/dbfs/mnt/my-bucket/data.tar.gz"
extract_path = "/dbfs/mnt/my-bucket/extracted_data"

# Descompactar o arquivo TAR
with tarfile.open(tar_path, "r:gz") as tar_ref:
    tar_ref.extractall(extract_path)

# Listar os arquivos extraídos
files = dbutils.fs.ls("dbfs:/mnt/my-bucket/extracted_data")
for file in files:
    print(f"Name: {file.name}, Size: {file.size}")
```


### **Descompactando Arquivos em Batch**

Se você tiver vários arquivos compactados em um diretório, pode automatizar a descompactação para todos eles.

#### **Descompactar Vários Arquivos ZIP**

```python
import zipfile
from pyspark.sql import SparkSession

# Caminho do diretório com os arquivos ZIP
zip_dir = "/dbfs/mnt/my-bucket/zip_files/"
extract_dir = "/dbfs/mnt/my-bucket/extracted_files/"

# Listar os arquivos ZIP
files = dbutils.fs.ls(zip_dir)

# Descompactar cada arquivo ZIP
for file in files:
    if file.name.endswith(".zip"):
        with zipfile.ZipFile(file.path.replace("dbfs:", "/dbfs"), 'r') as zip_ref:
            zip_ref.extractall(extract_dir)

# Listar os arquivos extraídos
extracted_files = dbutils.fs.ls(extract_dir)
for file in extracted_files:
    print(file.name)
```

### **Dicas Úteis**

1. **Trabalhe Diretamente com Formatos Compactados Suportados pelo Spark**:
    
    - Para **gzip**, **bzip2**, **lz4**, e **snappy**, o Spark descompacta automaticamente ao carregar os arquivos.

2. **Evite Arquivos ZIP e TAR em Produção**:
    
    - Esses formatos requerem etapas extras para descompactação manual. Considere converter os dados para **Parquet** ou **AVRO**.

3. **Gerencie Espaço de Armazenamento**:
    
    - Após descompactar os arquivos, remova os originais se não forem mais necessários:
        
        ```python
        dbutils.fs.rm("/mnt/my-bucket/data.zip", recurse=True)
        ```
        
4. **Use `dbutils.fs` para Gerenciar Arquivos**:
    
    - Combine operações de descompactação com comandos como `dbutils.fs.cp`, `dbutils.fs.rm`, e `dbutils.fs.ls`.


### **Resumo de Comandos**

| **Formato** | **Comando de Descompactação**                             |
| ----------- | --------------------------------------------------------- |
| **gzip**    | `spark.read.option("header", "true").csv("file.csv.gz")`  |
| **zip**     | `zipfile.ZipFile(file).extractall(path)`                  |
| **tar.gz**  | `tarfile.open(file).extractall(path)`                     |
| **bzip2**   | `spark.read.option("header", "true").csv("file.csv.bz2")` |
| **xz**      | `spark.read.option("header", "true").csv("file.csv.xz")`  |

Com estas técnicas, você pode descompactar e processar arquivos em pipelines de dados no Databricks de maneira eficiente!