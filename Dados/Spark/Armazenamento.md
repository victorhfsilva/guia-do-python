
### **Métodos de Salvamento**

Use o método **`write`** do DataFrame para salvar dados:

```python
df.write.format("format").options(options).save("path")
```

Ou diretamente com os métodos específicos:

- **Para CSV**: `df.write.csv("path")`
- **Para Parquet**: `df.write.parquet("path")`


### **Salvando em CSV**

#### **Configurações Comuns**

Ao salvar em CSV, as seguintes opções podem ser configuradas:

- **`header`**: Adiciona o cabeçalho ao arquivo.
- **`sep`**: Define o separador de colunas (ex.: `,`, `;`, ou outro).
- **`quote`**: Define o caractere para valores entre aspas.
- **`escape`**: Define o caractere de escape para valores entre aspas.

#### **Salvando Sem Particionamento**

```python
df.write.csv("path/to/csv", header=True, sep=",")
```

#### **Salvando com Particionamento**

Particionar organiza os dados em subdiretórios com base nos valores de uma coluna:

```python
df.write.partitionBy("column_name").csv("path/to/partitioned_csv", header=True)
```

#### **Exemplo Prático**

```python
from pyspark.sql import SparkSession

# Criando uma SparkSession
spark = SparkSession.builder.appName("Save CSV Example").getOrCreate()

# Criando um DataFrame de exemplo
data = [("Alice", 28, "Sales"), ("Bob", 35, "Marketing"), ("Cathy", 30, "IT")]
columns = ["Name", "Age", "Department"]

df = spark.createDataFrame(data, columns)

# Salvando como CSV com cabeçalho
df.write.csv("output/csv_no_partition", header=True)

# Salvando com particionamento
df.write.partitionBy("Department").csv("output/csv_partitioned", header=True)
```


### **alvando em Parquet**

**Parquet** é um formato binário otimizado para consultas rápidas, usado frequentemente em Big Data.

#### **Configurações Comuns**

Parquet não precisa de muitas opções adicionais, pois armazena metadados automaticamente:

- **`compression`**: Define o tipo de compressão (ex.: `snappy`, `gzip`).

#### **Salvando Sem Particionamento**

```python
df.write.parquet("path/to/parquet")
```

#### **Salvando com Particionamento**

Como no CSV, você pode particionar os dados:

```python
df.write.partitionBy("column_name").parquet("path/to/partitioned_parquet")
```

#### **Exemplo Prático**

```python
# Salvando como Parquet sem particionamento
df.write.parquet("output/parquet_no_partition")

# Salvando com particionamento
df.write.partitionBy("Department").parquet("output/parquet_partitioned")
```


### **Lidando com Dados Existentes**

Por padrão, o Spark não sobrescreve dados existentes. Você pode controlar isso com o modo:

- **`overwrite`**: Sobrescreve os dados existentes.
- **`append`**: Adiciona os dados ao conjunto existente.
- **`ignore`**: Ignora se o caminho já existir.
- **`error`** (padrão): Lança um erro se o caminho já existir.

#### **Exemplo de Sobrescrita**

```python
df.write.mode("overwrite").csv("path/to/csv")
df.write.mode("overwrite").parquet("path/to/parquet")
```

### **coalesce**

O método **`coalesce`** no Spark é usado para reduzir o número de partições de um DataFrame. Isso é especialmente útil quando você está salvando dados e deseja minimizar o número de arquivos gerados, especialmente em operações que criam muitas partições (como operações de `write.partitionBy`).

O **`coalesce`** combina partições adjacentes para reduzir o número de arquivos gerados. Ele é eficiente porque não realiza uma redistribuição completa dos dados, sendo adequado para operações que não precisam de balanceamento uniforme.

#### **Sintaxe**

```python
df.coalesce(num_partitions).write.format("format").save("path")
```

### **Usando `coalesce` em Exemplos**

#### **Salvando CSV em Um Único Arquivo**

Por padrão, o Spark cria múltiplos arquivos para salvar os dados. Para gerar um único arquivo:

```python
df.coalesce(1).write.csv("output/single_file_csv", header=True)
```

#### **Salvando Parquet em Um Único Arquivo**

```python
df.coalesce(1).write.parquet("output/single_file_parquet")
```

#### **Reduzindo Partições em Dados Particionados**

Mesmo quando você usa `partitionBy`, o Spark pode criar muitos arquivos em cada partição. Use `coalesce` para reduzir o número de arquivos dentro de cada partição:

```python
df.write.partitionBy("column").mode("overwrite").save("output/partitioned_data")
# Reduzindo para 2 arquivos em cada partição
df.coalesce(2).write.partitionBy("column").csv("output/coalesced_partitioned_csv", header=True)
```

#### **Quando Usar `coalesce`**

1. **Para Reduzir Arquivos Pequenos**:
    
    - Usado frequentemente para criar arquivos consolidados ao exportar dados.
    - Ideal para evitar overhead causado por muitos arquivos pequenos.

2. **Quando Você Não Precisa de Redistribuição Total**:
    
    - `coalesce` apenas combina partições existentes, sendo mais eficiente que **`repartition`**, que redistribui todos os dados.


##### **Comparação: `coalesce` vs. `repartition`**

|**Aspecto**|**`coalesce`**|**`repartition`**|
|---|---|---|
|**Objetivo**|Reduzir o número de partições|Alterar o número de partições|
|**Redistribuição**|Não realiza redistribuição completa|Redistribui uniformemente|
|**Performance**|Mais rápido, pois evita movimento de dados|Mais lento, devido à redistribuição|
|**Uso Típico**|Combinar partições para salvar arquivos|Balancear partições para processamento|


### **Lendo os Dados Salvos**

#### **Lendo CSV**

```python
df_csv = spark.read.csv("path/to/csv", header=True, inferSchema=True)
df_csv.show()
```

#### **Lendo Parquet**

```python
df_parquet = spark.read.parquet("path/to/parquet")
df_parquet.show()
```


### **Boas Práticas**

1. **Prefira Parquet para Análise**:
    
    - É mais eficiente e armazena os metadados automaticamente.
    - Recomendado para integração com ferramentas como Spark SQL, Hive e AWS Athena.

2. **Use Particionamento para Consultas Mais Rápidas**:
    
    - Para grandes volumes de dados, particione por colunas frequentemente usadas em filtros.

3. **Evite Arquivos Pequenos em Ambientes de Produção**:
    
    - Combine arquivos pequenos para evitar overhead de gerenciamento:
    
    ```python
    df.coalesce(1).write.csv("path/to/single_file_csv", header=True)
    ```
    
4. **Escolha o Tipo de Compressão Adequado**:
    
    - Para Parquet:
        
        ```python
        df.write.option("compression", "snappy").parquet("path/to/parquet")
        ```
        
    - Para CSV, a compressão pode ser feita após salvar, usando ferramentas externas.

