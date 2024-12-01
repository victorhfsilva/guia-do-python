### **Renomeação de Colunas**

Você pode renomear colunas individualmente ou em lote.

#### **Renomear uma única coluna**

Use o método `.withColumnRenamed()` para renomear uma coluna:

```python
df_renamed = df.withColumnRenamed("old_column_name", "new_column_name")
df_renamed.show()
```

#### **Renomear várias colunas**

Para renomear várias colunas, itere sobre o esquema:

```python
# Mapeamento de novos nomes
new_column_names = {"old_name1": "new_name1", "old_name2": "new_name2"}

# Aplicando renomeação
for old_name, new_name in new_column_names.items():
    df = df.withColumnRenamed(old_name, new_name)

df.show()
```

### **Visualização do Esquema de Dados**

O Spark fornece métodos para verificar o esquema de colunas e seus tipos.

#### **Exibir o esquema completo**

Use o método `.printSchema()`:

```python
df.printSchema()
```

#### **Exibir o resumo estatístico**

Visualize as estatísticas básicas das colunas:

```python
df.describe().show()
```

### **Troca de Tipos de Dados**

O Spark permite converter tipos de dados usando o método `.cast()`.

#### **String para Double**

```python
from pyspark.sql.functions import col

df = df.withColumn("new_double_column", col("string_column").cast("double"))
df.show()
```

#### **String para Date**

```python
from pyspark.sql.functions import to_date

df = df.withColumn("new_date_column", to_date(col("string_column"), "yyyy-MM-dd"))
df.show()
```

#### **Outros exemplos de conversão**

```python
# String para Integer
df = df.withColumn("new_int_column", col("string_column").cast("int"))

# Double para String
df = df.withColumn("new_string_column", col("double_column").cast("string"))
```


### **Manipulação de Valores: Substituições**

#### **Substituir vírgulas por pontos**

Se você trabalha com dados numéricos armazenados como strings com separadores de vírgula, use `.regexp_replace()`:

```python
from pyspark.sql.functions import regexp_replace

df = df.withColumn("cleaned_column", regexp_replace(col("string_column"), ",", "."))
df.show()
```

#### **Substituir valores nulos ou específicos**

```python
# Substituir valores nulos por um padrão
df = df.fillna({"column_name": "default_value"})

# Substituir valores específicos
df = df.replace("old_value", "new_value", subset=["column_name"])
```


### **Manipulação Avançada de Colunas**

#### **Criar ou Modificar Colunas**

Adicione uma nova coluna ou modifique uma existente com `.withColumn()`:

```python
from pyspark.sql.functions import col

df = df.withColumn("new_column", col("existing_column") * 2)
df.show()
```

#### **Remover Colunas**

Use o método `.drop()` para remover colunas desnecessárias:

```python
df = df.drop("column_to_remove")
df.show()
```


### **Exemplo Completo: Preparação de Dados**

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col, regexp_replace, to_date

# Iniciando SparkSession
spark = SparkSession.builder.appName("Data Conversion Example").getOrCreate()

# Criando um DataFrame
data = [("Alice", "1,200.50", "2023-01-01"), ("Bob", "3,450.75", "2023-02-15")]
columns = ["Name", "Salary", "JoinDate"]
df = spark.createDataFrame(data, columns)

# Substituir vírgula por ponto
df = df.withColumn("Salary", regexp_replace(col("Salary"), ",", ""))

# Converter Salary para Double
df = df.withColumn("Salary", col("Salary").cast("double"))

# Converter JoinDate para Date
df = df.withColumn("JoinDate", to_date(col("JoinDate"), "yyyy-MM-dd"))

# Renomear colunas
df = df.withColumnRenamed("Name", "EmployeeName")

# Exibir DataFrame final
df.show()
df.printSchema()
```

