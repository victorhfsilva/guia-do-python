
O **Databricks SQL** é uma interface poderosa para manipulação e consulta de dados em um ambiente distribuído. Ele permite criar tabelas, particioná-las, realizar consultas e gerenciar esquemas de banco de dados. 

### **Introdução ao SQL no Databricks**

O Databricks suporta comandos SQL diretamente em notebooks ou no editor de SQL, permitindo integração com a interface do Apache Spark.

#### **Alternar para SQL**

Para executar comandos SQL em um notebook:

- Inicie a célula com **`%sql`**:

```sql
%sql
SELECT * FROM my_table
```


### **Criando Tabelas no Databricks**

#### **Criar Tabelas Temporárias**

As tabelas temporárias são criadas em memória e válidas apenas para a sessão atual.

##### **Criando Tabela Temporária de um DataFrame**

```python
# Criar um DataFrame
data = [("Alice", 28), ("Bob", 35), ("Cathy", 30)]
columns = ["Name", "Age"]
df = spark.createDataFrame(data, columns)

# Registrar o DataFrame como tabela temporária
df.createOrReplaceTempView("temp_table")

# Executar SQL sobre a tabela temporária
%sql
SELECT * FROM temp_table
```

#### **Criar Tabelas Permanentes**

Tabelas permanentes são armazenadas no sistema de arquivos e disponíveis para diferentes sessões.

##### **Criar Tabela a partir de um DataFrame**

```python
# Criar DataFrame
data = [("Alice", "Sales", 5000), ("Bob", "Marketing", 6000), ("Cathy", "IT", 7500)]
columns = ["Name", "Department", "Salary"]
df = spark.createDataFrame(data, columns)

# Salvar como tabela permanente
df.write.format("parquet").saveAsTable("permanent_table")

# Consultar a tabela criada
%sql
SELECT * FROM permanent_table
```

##### **Criar Tabela Usando SQL**

```sql
%sql
CREATE TABLE employees (
    id INT,
    name STRING,
    department STRING,
    salary DOUBLE
)
USING parquet
LOCATION 'dbfs:/mnt/my-bucket/employees';
```

Ou carregado dados de um arquivo csv sem especificar o schema:

```sql
%sql
CREATE TABLE employees_csv_semicolon
USING csv
OPTIONS (
    path 'dbfs:/mnt/my-bucket/employees_semicolon.csv',
    header 'true',
    delimiter ';',
    inferSchema 'true'
);
```

### **Carregar Dados em Tabelas**

#### **Inserir Dados Manualmente**

```sql
%sql
INSERT INTO employees VALUES (1, 'Alice', 'Sales', 5000.0);
INSERT INTO employees VALUES (2, 'Bob', 'Marketing', 6000.0);
```

#### **Carregar Dados de Arquivos**

```sql
%sql
COPY INTO employees
FROM 'dbfs:/mnt/my-bucket/employees.csv'
FILEFORMAT = CSV
FORMAT_OPTIONS ('header' = 'true');
```


### **Particionamento de Tabelas**

O particionamento organiza os dados em subdiretórios com base em valores de uma ou mais colunas. Isso melhora o desempenho de consultas ao acessar apenas as partições relevantes.

#### **Criar Tabela Particionada**

```sql
%sql
CREATE TABLE employees_partitioned (
    id INT,
    name STRING,
    salary DOUBLE
)
USING parquet
PARTITIONED BY (department STRING)
LOCATION 'dbfs:/mnt/my-bucket/partitioned_employees';
```

#### **Inserir Dados em Partições**

```sql
%sql
INSERT INTO employees_partitioned PARTITION (department = 'Sales')
VALUES (1, 'Alice', 5000.0);

INSERT INTO employees_partitioned PARTITION (department = 'Marketing')
VALUES (2, 'Bob', 6000.0);
```

#### **Consultar Partições**

Visualize as partições existentes:

```sql
%sql
SHOW PARTITIONS employees_partitioned;
```

Execute consultas filtrando por partições:

```sql
%sql
SELECT * FROM employees_partitioned WHERE department = 'Sales';
```


### **Gerenciando Tabelas**

#### **Listar Tabelas**

```sql
%sql
SHOW TABLES;
```

#### **Descrever Tabelas**

Visualize o esquema e as informações de uma tabela:

```sql
%sql
DESCRIBE TABLE employees_partitioned;
```

#### **Excluir Tabelas**

```sql
%sql
DROP TABLE employees_partitioned;
```


### **Otimização com Delta Lake**

O Databricks integra-se ao **Delta Lake**, que oferece recursos avançados, como versionamento e compactação de arquivos.

#### **Criar Tabela Delta**

```sql
%sql
CREATE TABLE employees_delta (
    id INT,
    name STRING,
    department STRING,
    salary DOUBLE
)
USING delta
LOCATION 'dbfs:/mnt/my-bucket/employees_delta';
```

#### **Otimizar Tabela**

Compacta arquivos pequenos:

```sql
%sql
OPTIMIZE employees_delta;
```

#### **Executar Vacuum**

Remove arquivos obsoletos:

```sql
%sql
VACUUM employees_delta;
```


### **Consultas Avançadas**

#### **Consultas Agregadas**

```sql
%sql
SELECT department, AVG(salary) AS avg_salary
FROM employees_partitioned
GROUP BY department;
```

#### **Ordenação**

```sql
%sql
SELECT * FROM employees ORDER BY salary DESC;
```

#### **Joins**

```sql
%sql
SELECT e1.name, e1.department, e2.salary
FROM employees e1
INNER JOIN employees_partitioned e2
ON e1.name = e2.name;
```


### **Dicas Úteis**

1. **Use Particionamento para Grandes Conjuntos de Dados**:
    
    - Melhora o desempenho ao acessar apenas os dados necessários.

2. **Prefira Delta Lake**:
    
    - Oferece recursos avançados como transações ACID, compactação e controle de versões.

3. **Combine SQL com Spark**:
    
    - Crie tabelas com SQL e use DataFrames Spark para manipulação mais avançada.

4. **Gerencie Esquemas**:

	
    - Utilize comandos como `SHOW DATABASES` e `CREATE DATABASE` para organizar dados em esquemas.


