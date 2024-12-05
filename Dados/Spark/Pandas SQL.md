
No **Pandas on Spark**, o método **`ps.sql()`** permite executar consultas SQL diretamente em DataFrames, simplificando operações complexas como filtros, seleções e agregações. O método aceita uma string SQL e associa os DataFrames no contexto com identificadores nomeados.


#### **Criando um DataFrame**

```python
import pyspark.pandas as ps

# Criar o DataFrame de exemplo
data = {
    "nome_curso": ["Engenharia", "Direito", "Medicina", "Arquitetura"],
    "mensalidade": [2500, 3500, 5000, 3000]
}
df = ps.DataFrame(data)
```

O DataFrame criado:

|nome_curso|mensalidade|
|---|---|
|Engenharia|2500|
|Direito|3500|
|Medicina|5000|
|Arquitetura|3000|


#### **Realizando uma Consulta SQL**

Filtrar cursos com mensalidade maior que 3000 e que não sejam "Medicina":

```python
result = ps.sql(
    "SELECT nome_curso, mensalidade FROM {DF} WHERE mensalidade > 3000 AND nome_curso != 'Medicina'", 
    DF=df
)
print(result)
```

Resultado:

|nome_curso|mensalidade|
|---|---|
|Direito|3500|


### **Estrutura do `ps.sql()`**

A função **`ps.sql()`** aceita:

1. Uma string SQL contendo a consulta.
2. Identificadores para os DataFrames, passados como argumentos nomeados.

#### **Sintaxe**

```python
ps.sql("SQL Query", DataFrameName=df)
```

- **`SQL Query`**: Uma string contendo a consulta SQL.
- **`DataFrameName`**: Nome associado ao DataFrame que será usado na consulta.


### **Consultas Comuns com `ps.sql()`**

#### **Selecionar Todas as Colunas**

```python
result = ps.sql("SELECT * FROM {DF}", DF=df)
```

#### **Selecionar Colunas Específicas**

```python
result = ps.sql("SELECT nome_curso, mensalidade FROM {DF}", DF=df)
```

#### **Filtro com Condições**

Selecionar cursos com mensalidade menor que 4000:

```python
result = ps.sql("SELECT * FROM {DF} WHERE mensalidade < 4000", DF=df)
```

#### **Ordenação**

Ordenar os cursos por mensalidade em ordem decrescente:

```python
result = ps.sql("SELECT * FROM {DF} ORDER BY mensalidade DESC", DF=df)
```

#### **Agrupamento e Agregação**

Calcular a média de mensalidades por curso:

```python
result = ps.sql("SELECT AVG(mensalidade) AS media_mensalidade FROM {DF}", DF=df)
```

### **Trabalhando com Múltiplos DataFrames**

Você pode referenciar vários DataFrames em uma única consulta SQL.

#### **Criar Outro DataFrame**

```python
data_faculdades = {
    "faculdade": ["UFSP", "UFRJ", "USP", "UNESP"],
    "nome_curso": ["Engenharia", "Direito", "Medicina", "Arquitetura"]
}
df_faculdades = ps.DataFrame(data_faculdades)
```

#### **Realizar um Join**

Combinar os cursos com as faculdades:

```python
result = ps.sql("""
    SELECT DF.nome_curso, DF.mensalidade, DF2.faculdade
    FROM {DF} DF
    JOIN {DF2} DF2
    ON DF.nome_curso = DF2.nome_curso
""", DF=df, DF2=df_faculdades)
```


### **Exemplo Completo**

#### **Cenário**

Você deseja:

1. Selecionar cursos com mensalidade acima de 3000, excluindo "Medicina".
2. Ordenar os resultados pela mensalidade em ordem decrescente.
3. Combinar com informações de faculdades.

#### **Código**

```python
import pyspark.pandas as ps

# Criar DataFrames
data_cursos = {
    "nome_curso": ["Engenharia", "Direito", "Medicina", "Arquitetura"],
    "mensalidade": [2500, 3500, 5000, 3000]
}
df_cursos = ps.DataFrame(data_cursos)

data_faculdades = {
    "faculdade": ["UFSP", "UFRJ", "USP", "UNESP"],
    "nome_curso": ["Engenharia", "Direito", "Medicina", "Arquitetura"]
}
df_faculdades = ps.DataFrame(data_faculdades)

# Consulta SQL
query = """
    SELECT DF.nome_curso, DF.mensalidade, DF2.faculdade
    FROM {DF} DF
    JOIN {DF2} DF2
    ON DF.nome_curso = DF2.nome_curso
    WHERE DF.mensalidade > 3000 AND DF.nome_curso != 'Medicina'
    ORDER BY DF.mensalidade DESC
"""
result = ps.sql(query, DF=df_cursos, DF2=df_faculdades)
print(result)
```

Resultado:

|nome_curso|mensalidade|faculdade|
|---|---|---|
|Direito|3500|UFRJ|
