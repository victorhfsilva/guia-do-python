
O método **`map`** no Pandas é usado para aplicar funções ou mapeamentos em colunas de **Series** ou DataFrames. É uma ferramenta poderosa para transformar dados em colunas individuais de maneira eficiente.

### **O Que é `map`?**

O método **`map`** é usado para:

1. **Aplicar uma função personalizada** a cada elemento de uma coluna.
2. **Substituir valores** com base em um dicionário de mapeamento.
3. **Aplicar uma função built-in** (como `str.lower`, `abs`, etc.).

#### **Sintaxe**

```python
Series.map(arg, na_action=None)
```

|**Parâmetro**|**Descrição**|
|---|---|
|`arg`|Função, dicionário ou objeto Series para aplicar o mapeamento.|
|`na_action`|Se definido como `'ignore'`, ignora valores `NaN` ao aplicar a função.|


### **Criando um DataFrame de Exemplo**

Vamos criar um DataFrame para ilustrar o uso de **`map`**:

```python
import pandas as pd

data = {
    "name": ["Alice", "Bob", "Cathy", "David"],
    "age": [25, 30, 35, 40],
    "department": ["HR", "IT", "Finance", "HR"]
}

df = pd.DataFrame(data)
print(df)
```

|name|age|department|
|---|---|---|
|Alice|25|HR|
|Bob|30|IT|
|Cathy|35|Finance|
|David|40|HR|


### **Usando `map` para Transformações**

#### **Aplicar Função em uma Coluna**

Converta todos os nomes para letras maiúsculas:

```python
df["name"] = df["name"].map(str.upper)
print(df)
```

#### **Modificar os Valores**

Adicione 5 anos à coluna de idade:

```python
df["age"] = df["age"].map(lambda x: x + 5)
print(df)
```

#### **Substituir Valores com um Dicionário**

Mapeie os departamentos para novos nomes:

```python
department_map = {"HR": "Human Resources", "IT": "Information Technology", "Finance": "Financial Services"}
df["department"] = df["department"].map(department_map)
print(df)
```


### **Lidando com Valores Faltantes (`NaN`)**

Por padrão, o **`map`** aplica a função a todos os valores, incluindo os `NaN`. Para ignorar `NaN`, use o parâmetro **`na_action='ignore'`**.

```python
df["age"] = df["age"].map(lambda x: x * 2, na_action="ignore")
print(df)
```


### **Usando `map` com Objetos Series**

Você também pode usar **`map`** para criar relações entre colunas usando outro **Series**.

#### **Criar uma Série para Mapeamento**

```python
salary_data = pd.Series(
    [50000, 60000, 70000],
    index=["Human Resources", "Information Technology", "Financial Services"]
)
```

#### **Mapear Valores Entre Séries**

Adicione uma nova coluna de salários baseada no departamento:

```python
df["salary"] = df["department"].map(salary_data)
print(df)
```


### **Casos de Uso Comuns**

#### **Conversão de Formatos**

Converta valores numéricos em strings formatadas:

```python
df["age"] = df["age"].map(lambda x: f"{x} years old")
print(df)
```

#### **Marcar Categorias**

Crie uma nova coluna para identificar se o departamento é técnico:

```python
technical_departments = {"Information Technology": "Yes", "Human Resources": "No", "Financial Services": "No"}
df["is_technical"] = df["department"].map(technical_departments)
print(df)
```

#### **Normalizar Dados**

Divida cada idade pelo valor máximo da coluna:

```python
max_age = df["age"].map(lambda x: int(x.split()[0])).max()
df["normalized_age"] = df["age"].map(lambda x: int(x.split()[0]) / max_age)
print(df)
```


### **Diferença entre `map`, `apply` e `applymap`**

|**Método**|**Aplicação**|**Escopo**|
|---|---|---|
|`map`|Aplica função a **uma Série**|Apenas em colunas individuais.|
|`apply`|Aplica função a **linhas ou colunas**|Em DataFrames e Series.|
|`applymap`|Aplica função a **cada elemento**|Apenas em DataFrames.|


### **Exemplo Completo**

#### **Cenário**

Você deseja:

1. Converter os nomes para minúsculas.
2. Mapear departamentos para códigos curtos.
3. Adicionar uma coluna que categoriza os funcionários como "Jovem" ou "Idoso" com base na idade.

#### **Código**

```python
import pandas as pd

data = {
    "name": ["Alice", "Bob", "Cathy", "David"],
    "age": [25, 30, 35, 40],
    "department": ["HR", "IT", "Finance", "HR"]
}

df = pd.DataFrame(data)

# 1. Converter nomes para minúsculas
df["name"] = df["name"].map(str.lower)

# 2. Mapear departamentos para códigos
department_map = {"HR": "HR", "IT": "IT", "Finance": "FIN"}
df["department_code"] = df["department"].map(department_map)

# 3. Categorizar idade
df["age_group"] = df["age"].map(lambda x: "Young" if x < 35 else "Senior")

print(df)
```

Resultado:

|name|age|department|department_code|age_group|
|---|---|---|---|---|
|alice|25|HR|HR|Young|
|bob|30|IT|IT|Young|
|cathy|35|Finance|FIN|Senior|
|david|40|HR|HR|Senior|
