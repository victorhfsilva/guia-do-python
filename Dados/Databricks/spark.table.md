
A função **`spark.table`** no Apache Spark é uma forma eficiente de carregar e manipular tabelas registradas no catálogo do Spark. Ela é usada principalmente para trabalhar com tabelas criadas em Hive, Delta Lake, ou outros formatos suportados pelo Spark.

#### **Sintaxe**

```python
df = spark.table("table_name")
```

### **Exemplos de Uso**

#### **Carregar uma Tabela como DataFrame**

Se você já possui uma tabela criada no catálogo, carregue-a como um DataFrame:

```python
# Carregar a tabela "employees"
df = spark.table("employees")

# Exibir os dados
df.show()
```

#### **Realizar Transformações**

Depois de carregar a tabela, você pode aplicar operações Spark:

```python
# Filtrar e calcular média de salários
avg_salary = spark.table("employees") \
    .filter("department = 'Sales'") \
    .groupBy("department") \
    .avg("salary")

avg_salary.show()
```

#### **Usar com Outras Tabelas**

Combine tabelas carregadas com `spark.table` em operações como joins:

```python
# Carregar tabelas
df_employees = spark.table("employees")
df_departments = spark.table("departments")

# Realizar um join
df_joined = df_employees.join(df_departments, "department_id") \
    .select("employees.name", "departments.department_name", "employees.salary")

df_joined.show()
```

### **Usando `spark.table` com SQL**

`spark.table` também é útil para integrar consultas SQL diretamente em seu pipeline de manipulação:

```python
# Criar uma tabela temporária a partir de um DataFrame
data = [("Alice", "Sales", 5000), ("Bob", "Marketing", 6000)]
columns = ["name", "department", "salary"]
df = spark.createDataFrame(data, columns)
df.createOrReplaceTempView("temp_table")

# Consultar usando SQL
df_sql = spark.sql("SELECT * FROM temp_table WHERE salary > 5500")
df_sql.show()
```


### **Trabalhando com Delta Tables**

Se a tabela no catálogo for uma **Delta Table**, você pode carregar dados otimizados:

```python
# Carregar uma Delta Table
df_delta = spark.table("employees_delta")

# Exibir as alterações em uma tabela Delta
df_delta.select("*").show()
```


### **Verificando Metadados da Tabela**

Você pode verificar o esquema e a estrutura da tabela carregada:

```python
df = spark.table("employees")

# Exibir o esquema
df.printSchema()

# Contar o número de linhas
print(f"Number of rows: {df.count()}")
```


### **Dicas Úteis**

1. **Confirme o Nome da Tabela**: Use o comando SQL `SHOW TABLES` para verificar o nome exato das tabelas.
    
    ```sql
    %sql
    SHOW TABLES;
    ```
    
2. **Combine com Outras APIs do Spark**: Após carregar uma tabela com `spark.table`, você pode usar todas as funcionalidades do Spark, como filtros, agregações, e joins.
    
3. **Evite Carregamentos Desnecessários**: Use `spark.table` apenas quando precisar de acesso total à tabela como um DataFrame. Para consultas rápidas, prefira SQL direto.
    

### **Exemplo Prático Completo**

#### **Cenário**

Você tem uma tabela chamada `sales` no catálogo e deseja calcular as vendas totais por produto.

```python
# Carregar a tabela "sales"
df_sales = spark.table("sales")

# Calcular as vendas totais por produto
sales_summary = df_sales.groupBy("product_id") \
    .agg({"sales_amount": "sum"}) \
    .withColumnRenamed("sum(sales_amount)", "total_sales")

# Exibir o resumo
sales_summary.show()
```
