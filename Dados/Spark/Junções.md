
No Apache Spark, junções de **DataFrames** são operações fundamentais para combinar dados de diferentes fontes com base em uma ou mais colunas. O Spark oferece várias opções de junção para atender a diferentes cenários analíticos.

### **Introdução às Junções**

Uma **junção** combina duas tabelas ou DataFrames com base em uma condição de correspondência. No Spark, isso é feito com o método **`join`**.

#### **Sintaxe Básica**

```python
df_result = df1.join(df2, join_condition, join_type)
```

- **`df1`** e **`df2`**: DataFrames a serem combinados.
- **`join_condition`**: Condição de junção, geralmente baseada em colunas.
- **`join_type`**: Tipo de junção (veja a seção 2).

### **Tipos de Junções**

#### **`inner` (Padrão)**

Mantém apenas as linhas com correspondências em ambos os DataFrames.

```python
df_result = df1.join(df2, df1["id"] == df2["id"], "inner")
```

#### **`left` ou `left_outer`**

Mantém todas as linhas do DataFrame esquerdo (`df1`) e adiciona os dados do DataFrame direito (`df2`) quando há correspondência. Preenche com **nulo** onde não há correspondência.

```python
df_result = df1.join(df2, df1["id"] == df2["id"], "left")
```

#### **`right` ou `right_outer`**

Mantém todas as linhas do DataFrame direito (`df2`) e adiciona os dados do DataFrame esquerdo (`df1`) quando há correspondência. Preenche com **nulo** onde não há correspondência.

```python
df_result = df1.join(df2, df1["id"] == df2["id"], "right")
```

#### **`full` ou `full_outer`**

Mantém todas as linhas de ambos os DataFrames. Onde não há correspondência, preenche com **nulo**.

```python
df_result = df1.join(df2, df1["id"] == df2["id"], "full")
```

#### **`cross`**

Realiza um produto cartesiano entre os DataFrames (todas as combinações possíveis).

```python
df_result = df1.join(df2, how="cross")
```

#### **`semi`**

Mantém apenas as linhas do DataFrame esquerdo (`df1`) que possuem correspondência no DataFrame direito (`df2`).

```python
df_result = df1.join(df2, df1["id"] == df2["id"], "semi")
```

#### **`anti`**

Mantém apenas as linhas do DataFrame esquerdo (`df1`) que **não** possuem correspondência no DataFrame direito (`df2`).

```python
df_result = df1.join(df2, df1["id"] == df2["id"], "anti")
```


### **Exemplo Prático**

#### **Criando DataFrames de Exemplo**

```python
from pyspark.sql import SparkSession

# Criando a SparkSession
spark = SparkSession.builder.appName("Join Example").getOrCreate()

# DataFrame 1
data1 = [
    (1, "Alice", 28),
    (2, "Bob", 35),
    (3, "Cathy", 30)
]
columns1 = ["id", "name", "age"]
df1 = spark.createDataFrame(data1, columns1)

# DataFrame 2
data2 = [
    (1, "Sales"),
    (2, "Marketing"),
    (4, "IT")
]
columns2 = ["id", "department"]
df2 = spark.createDataFrame(data2, columns2)

df1.show()
df2.show()
```
#### **Realizando Junções**

```python
# Inner Join
inner_join = df1.join(df2, df1["id"] == df2["id"], "inner")
inner_join.show()

# Left Outer Join
left_join = df1.join(df2, df1["id"] == df2["id"], "left")
left_join.show()

# Right Outer Join
right_join = df1.join(df2, df1["id"] == df2["id"], "right")
right_join.show()

# Full Outer Join
full_join = df1.join(df2, df1["id"] == df2["id"], "full")
full_join.show()

# Semi Join
semi_join = df1.join(df2, df1["id"] == df2["id"], "semi")
semi_join.show()

# Anti Join
anti_join = df1.join(df2, df1["id"] == df2["id"], "anti")
anti_join.show()
```

### **Junções com Múltiplas Colunas**

Você pode usar várias colunas para a condição de junção:

```python
df_result = df1.join(df2, (df1["id"] == df2["id"]) & (df1["name"] == df2["name"]), "inner")
```


### **Evitando Ambiguidade em Colunas**

Quando ambos os DataFrames têm colunas com o mesmo nome, renomeie ou use alias para evitar conflitos:

```python
from pyspark.sql.functions import col

df1 = df1.alias("df1")
df2 = df2.alias("df2")

result = df1.join(df2, col("df1.id") == col("df2.id"), "inner")
result.select("df1.id", "df1.name", "df2.department").show()
```

### **Lidando com Dados Nulos**

Valores **nulos** em colunas de junção podem causar resultados inesperados. Certifique-se de tratar os nulos:

```python
df1 = df1.na.fill({"id": -1})
df2 = df2.na.fill({"id": -1})
```


### **Boas Práticas**

1. **Prefira Especificar Colunas Explicitamente**: Sempre use condições explícitas em junções para evitar ambiguidade.
2. **Otimize o Reparticionamento**: Use `.repartition()` ou `.broadcast()` para melhorar o desempenho em junções de grandes DataFrames.
    
    ```python
    from pyspark.sql.functions import broadcast
    
    result = df1.join(broadcast(df2), "id", "inner")
    ```
    
3. **Evite Produtos Cartesianos**: Use junções `cross` apenas quando necessário, pois elas geram combinações de todas as linhas.

### **Resumo dos Tipos de Junções**

| **Tipo de Junção** | **Descrição**                                                                     |
| ------------------ | --------------------------------------------------------------------------------- |
| **`inner`**        | Retém apenas linhas com correspondência em ambos os DataFrames.                   |
| **`left`**         | Retém todas as linhas do DataFrame esquerdo, adicionando nulos quando necessário. |
| **`right`**        | Retém todas as linhas do DataFrame direito, adicionando nulos quando necessário.  |
| **`full`**         | Retém todas as linhas de ambos os DataFrames.                                     |
| **`semi`**         | Retém apenas as linhas do DataFrame esquerdo com correspondência.                 |
| **`anti`**         | Retém apenas as linhas do DataFrame esquerdo sem correspondência.                 |
| **`cross`**        | Produto cartesiano de ambos os DataFrames.                                        |
