
O **Pandas** é uma biblioteca poderosa para manipulação e análise de dados em Python. Ele permite realizar consultas complexas em **DataFrames** com o método **`query`**, que oferece uma sintaxe simplificada e legível para filtrar e manipular dados.


### **O Que é o Método `query`?**

O método **`query`** do Pandas permite realizar consultas em um **DataFrame** usando uma string com uma sintaxe semelhante a SQL. Ele é útil para simplificar filtros e operações que seriam mais verbosas usando **`[]`** ou **`loc`**.  

#### **Sintaxe**

```python
df.query('condição', inplace=False)
```

- **`condição`**: Uma string contendo a condição lógica da consulta.
- **`inplace`**: Se **`True`**, a operação é realizada no próprio DataFrame.


### **Criando um DataFrame de Exemplo**

Antes de realizar consultas, vamos criar um DataFrame para usar nos exemplos:

```python
import pandas as pd

data = {
    "id": [1, 2, 3, 4, 5],
    "name": ["Alice", "Bob", "Cathy", "David", "Eve"],
    "age": [25, 30, 35, 40, 45],
    "department": ["Sales", "Marketing", "IT", "HR", "Finance"],
    "salary": [50000, 60000, 70000, 80000, 90000]
}

df = pd.DataFrame(data)
print(df)
```

|id|name|age|department|salary|
|---|---|---|---|---|
|1|Alice|25|Sales|50000|
|2|Bob|30|Marketing|60000|
|3|Cathy|35|IT|70000|
|4|David|40|HR|80000|
|5|Eve|45|Finance|90000|


### **Realizando Queries no Pandas**

#### **Filtros Simples**

Filtrar linhas onde a coluna **`age`** é maior que 30:

```python
result = df.query('age > 30')
print(result)
```

#### **Filtros com Operadores Lógicos**

Filtrar onde **`age`** é maior que 30 **e** **`salary`** é menor que 80000:

```python
result = df.query('age > 30 and salary < 80000')
print(result)
```

Filtrar onde **`department`** é "IT" **ou** **`salary`** é maior que 80000:

```python
result = df.query('department == "IT" or salary > 80000')
print(result)
```

#### **Filtros com Expressões Complexas**

Filtrar linhas onde o **`salary`** está entre 60000 e 80000:

```python
result = df.query('60000 <= salary <= 80000')
print(result)
```

#### **Filtros com Strings**

Filtrar linhas onde a coluna **`name`** começa com "A":

```python
result = df.query('name.str.startswith("A")', engine='python')
print(result)
```

#### **Usar Variáveis em Queries**

Se uma variável contém um valor usado na consulta:

```python
threshold = 70000
result = df.query('salary > @threshold')
print(result)
```

#### **Filtro por Intervalo de Valores**

Filtrar linhas onde **`age`** está entre 30 e 40:

```python
result = df.query('30 <= age <= 40')
print(result)
```

#### **Verificar Valores em uma Lista**

Filtrar linhas onde o **`department`** está em uma lista específica:

```python
departments = ["IT", "Finance"]
result = df.query('department in @departments')
print(result)
```

#### **Excluir Valores Específicos**

Filtrar linhas onde o **`department`** **não** está em uma lista:

```python
excluded_departments = ["HR", "Sales"]
result = df.query('department not in @excluded_departments')
print(result)
```

### **Modificar Dados In-Place**

Filtrar e atualizar o próprio DataFrame:

```python
df.query('age > 30', inplace=True)
print(df)
```


### **Combinar `query` com Outras Operações**

#### **Agrupar e Filtrar**

Filtrar dados e calcular a média de salários:

```python
result = df.query('age > 30').groupby('department')['salary'].mean()
print(result)
```

#### **Ordenar Após Filtrar**

Ordenar os resultados por **`salary`** em ordem decrescente:

```python
result = df.query('age > 30').sort_values(by='salary', ascending=False)
print(result)
```



### **7. Limitações e Considerações**

1. **Strings e Operadores**:
    
    - Para strings, use `.str` com **`engine='python'`**:
        
        ```python
        df.query('name.str.contains("A")', engine='python')
        ```
        
2. **Desempenho**:
    
    - Para consultas simples, `query` é eficiente. Em operações mais complexas, `loc` pode ser mais rápido.
    
3. **Colunas com Espaços ou Caracteres Especiais**:
    
    - Se uma coluna tiver caracteres especiais, use crase para referenciá-la:
        
        ```python
        df.query('`column with spaces` > 100')
        ```
        