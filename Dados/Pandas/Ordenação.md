
A ordenação é uma operação fundamental para organizar dados em um **DataFrame** no **Pandas**. O método **`sort_values`** é a ferramenta principal para ordenar linhas com base em uma ou mais colunas. O Pandas também oferece o método **`sort_index`** para ordenar pelo índice.


### **Métodos Principais para Ordenação**

#### **Ordenar Linhas com `sort_values`**

Usado para ordenar linhas com base nos valores de uma ou mais colunas:

```python
df.sort_values(by="coluna", ascending=True)
```

#### **Ordenar pelo Índice com `sort_index`**

Usado para ordenar linhas ou colunas com base no índice:

```python
df.sort_index(ascending=True)
```


### **Criando um DataFrame de Exemplo**

Antes de explorar os métodos, vamos criar um **DataFrame** para usar nos exemplos:

```python
import pandas as pd

data = {
    "id": [1, 2, 3, 4, 5],
    "name": ["Alice", "Bob", "Cathy", "David", "Eve"],
    "age": [25, 30, 35, 40, 45],
    "salary": [50000, 60000, 70000, 80000, 90000]
}

df = pd.DataFrame(data)
print(df)
```

|id|name|age|salary|
|---|---|---|---|
|1|Alice|25|50000|
|2|Bob|30|60000|
|3|Cathy|35|70000|
|4|David|40|80000|
|5|Eve|45|90000|


### **Ordenando Linhas com `sort_values`**

#### **Ordenar por uma Única Coluna**

Ordenar os dados pela coluna **`age`** em ordem crescente:

```python
df_sorted = df.sort_values(by="age")
print(df_sorted)
```

Ordenar pela coluna **`salary`** em ordem decrescente:

```python
df_sorted = df.sort_values(by="salary", ascending=False)
print(df_sorted)
```

#### **Ordenar por Múltiplas Colunas**

Ordenar pelos salários (**`salary`**) em ordem decrescente e, em caso de empate, pela idade (**`age`**) em ordem crescente:

```python
df_sorted = df.sort_values(by=["salary", "age"], ascending=[False, True])
print(df_sorted)
```

#### **Ordenar Coluna com Valores Ausentes**

Por padrão, valores ausentes (**NaN**) são colocados no final:

```python
df.loc[2, "age"] = None  # Introduzindo um NaN
df_sorted = df.sort_values(by="age")
print(df_sorted)
```

Para colocar os valores ausentes no início:

```python
df_sorted = df.sort_values(by="age", na_position="first")
print(df_sorted)
```

### **Ordenando pelo Índice com `sort_index`**

#### **Ordenar Linhas pelo Índice**

Por padrão, o DataFrame é ordenado pelo índice em ordem crescente:

```python
df_sorted = df.sort_index()
print(df_sorted)
```

Ordenar o índice em ordem decrescente:

```python
df_sorted = df.sort_index(ascending=False)
print(df_sorted)
```

#### **Ordenar Colunas pelo Nome**

Você também pode ordenar as colunas em ordem alfabética:

```python
df_sorted = df.sort_index(axis=1)
print(df_sorted)
```


### **Alterar o DataFrame Original**

Por padrão, os métodos de ordenação retornam uma cópia do DataFrame. Para alterar o DataFrame original, use o parâmetro **`inplace=True`**:

```python
df.sort_values(by="age", inplace=True)
print(df)
```

