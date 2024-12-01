
O método **`where`** no Apache Spark é uma alternativa ao **`filter`**, amplamente utilizado para aplicar condições lógicas em **DataFrames** ou **RDDs**. Ambos os métodos possuem funcionalidade idêntica, mas `where` é mais comum em cenários SQL-like devido à sua semântica.


### **Introdução ao `where`**

O `where` retorna um novo DataFrame contendo apenas as linhas que satisfazem a condição fornecida. Sua sintaxe é idêntica à do `filter`.

#### **Sintaxe Básica**

```python
df_filtered = df.where(condition)
```


### **Usos Comuns do `where`**

#### **Condições Simples**

Filtre linhas com base em uma única condição:

```python
df_filtered = df.where(df["column_name"] > 100)
df_filtered.show()
```

Ou usando a função `col`:

```python
from pyspark.sql.functions import col

df_filtered = df.where(col("column_name") == "value")
df_filtered.show()
```

#### **Múltiplas Condições**

Combine várias condições usando operadores lógicos:

- **AND** (`&`):

```python
df_filtered = df.where((col("column1") > 50) & (col("column2") < 100))
df_filtered.show()
```

- **OR** (`|`):

```python
df_filtered = df.where((col("column1") == "value1") | (col("column2") == "value2"))
df_filtered.show()
```

- **NOT** (`~`):

```python
df_filtered = df.where(~(col("column_name") < 0))
df_filtered.show()
```


### **Filtragem de Strings**

#### **Igualdade e Diferença**

Filtre linhas onde o valor da coluna de texto corresponda ou seja diferente:

```python
df_filtered = df.where(col("string_column") == "desired_value")
df_filtered.show()
```

#### **Expressões Regulares**

Use expressões regulares para selecionar valores baseados em padrões:

```python
df_filtered = df.where(col("string_column").rlike("regex_pattern"))
df_filtered.show()
```


### **Trabalhando com Valores Nulos**

#### **Selecionar Linhas com Valores Nulos**

```python
df_filtered = df.where(col("column_name").isNull())
df_filtered.show()
```

#### **Selecionar Linhas sem Valores Nulos**

```python
df_filtered = df.where(col("column_name").isNotNull())
df_filtered.show()
```


### **Usando Listas com `where`**

#### **Selecionar Valores Específicos**

Filtre valores que estão em uma lista:

```python
df_filtered = df.where(col("column_name").isin("value1", "value2", "value3"))
df_filtered.show()
```

#### **Excluir Valores Específicos**

```python
df_filtered = df.where(~col("column_name").isin("value1", "value2"))
df_filtered.show()
```


### **Trabalhando com Datas**

#### **Comparação de Datas**

```python
from pyspark.sql.functions import to_date

# Converter string para data
df = df.withColumn("date_column", to_date(col("date_column"), "yyyy-MM-dd"))

# Filtrar linhas com base em uma data
df_filtered = df.where(col("date_column") > "2023-01-01")
df_filtered.show()
```

#### **Intervalo de Datas**

```python
df_filtered = df.where((col("date_column") >= "2023-01-01") & (col("date_column") <= "2023-12-31"))
df_filtered.show()
```


### **Usando Expressões SQL com `where`**

O método `where` aceita expressões SQL-like como strings, tornando-o muito útil para usuários que preferem uma sintaxe mais próxima do SQL:

```python
df_filtered = df.where("column_name > 100 AND column2 = 'value'")
df_filtered.show()
```


### **Exemplo Prático**

#### **DataFrame de Exemplo**

```python
from pyspark.sql import SparkSession

# Criando uma SparkSession
spark = SparkSession.builder.appName("Where Example").getOrCreate()

# Criando um DataFrame de exemplo
data = [
    ("Alice", 28, 5000, "2023-01-01"),
    ("Bob", 35, 6000, "2023-02-15"),
    ("Cathy", 30, 7500, None)
]
columns = ["Name", "Age", "Salary", "JoinDate"]

df = spark.createDataFrame(data, columns)
df.show()
```

#### **Aplicando `where`**

```python
from pyspark.sql.functions import col

# Filtrar por idade maior que 30
df_filtered = df.where(col("Age") > 30)
df_filtered.show()

# Filtrar por salário maior que 5000 e idade menor que 35
df_filtered = df.where((col("Salary") > 5000) & (col("Age") < 35))
df_filtered.show()

# Filtrar valores nulos na coluna JoinDate
df_filtered = df.where(col("JoinDate").isNull())
df_filtered.show()

# Filtrar usando uma lista de valores
df_filtered = df.where(col("Name").isin("Alice", "Cathy"))
df_filtered.show()
```

### **Diferenças entre `where` e `filter`**

|**Aspecto**|**`where`**|**`filter`**|
|---|---|---|
|**Semântica**|Mais usado em contextos SQL-like.|Semântica mais genérica.|
|**Funcionalidade**|Idêntica ao `filter`.|Idêntica ao `where`.|
|**Preferência**|SQL-like workflows.|Programação orientada a objetos.|

