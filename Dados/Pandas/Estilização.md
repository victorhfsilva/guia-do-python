
O Pandas oferece suporte para estilizar tabelas geradas a partir de **DataFrames** e **Series**. A estilização permite adicionar formatos, cores e destaques, melhorando a legibilidade e a apresentação dos dados, especialmente em relatórios.

### **Introdução à Estilização no Pandas**

O método principal para estilização é **`DataFrame.style`**, que retorna um objeto **Styler**. Este objeto permite aplicar formatações personalizadas e interativas.


### **Criando um DataFrame de Exemplo**

Antes de começar, vamos criar um DataFrame para usar nos exemplos:

```python
import pandas as pd
import numpy as np

data = {
    "Name": ["Alice", "Bob", "Cathy", "David"],
    "Age": [25, 30, 35, 40],
    "Salary": [50000, 60000, 70000, 80000],
    "Bonus": [5000, 7000, 8000, 9000]
}

df = pd.DataFrame(data)
print(df)
```

|Name|Age|Salary|Bonus|
|---|---|---|---|
|Alice|25|50000|5000|
|Bob|30|60000|7000|
|Cathy|35|70000|8000|
|David|40|80000|9000|


### **Aplicando Estilos Básicos**

#### **Alterar o Formato Numérico**

Formate os valores de uma coluna como moeda:

```python
styled_df = df.style.format({
    "Salary": "${:,.2f}",
    "Bonus": "${:,.0f}"
})
styled_df
```

#### **Adicionar Cores com Destaques**

- **Destaque Valores Máximos**:

```python
styled_df = df.style.highlight_max(axis=0)
styled_df
```

- **Destaque Valores Mínimos**:

```python
styled_df = df.style.highlight_min(axis=0)
styled_df
```

#### **Aplicar Gradiente de Cor**

Use cores graduais para representar valores:

```python
styled_df = df.style.background_gradient(cmap="viridis")
styled_df
```


### **Formatações Personalizadas**

#### **Adicionar Bordas**

```python
styled_df = df.style.set_table_styles(
    [{"selector": "th", "props": [("border", "1px solid black")]}]
)
styled_df
```

#### **Aplicar Estilos em Linhas ou Colunas Específicas**

Aplique estilos em uma linha com base em uma condição:

```python
def highlight_age(age):
    return ["background-color: yellow" if a > 30 else "" for a in age]

styled_df = df.style.apply(highlight_age, subset=["Age"])
styled_df
```


### **Trabalhando com Condições**

#### **Destacar Valores Acima de um Limite**

```python
styled_df = df.style.applymap(lambda x: "color: red;" if x > 60000 else "", subset=["Salary"])
styled_df
```

#### **Formatar Multiplas Colunas**

```python
def style_ages_and_salaries(val):
    if val > 30:
        return "background-color: lightblue"
    elif val > 60000:
        return "background-color: lightgreen"
    return ""

styled_df = df.style.applymap(style_ages_and_salaries, subset=["Age", "Salary"])
styled_df
```


### **Exemplo de Relatório Completo**

Crie um relatório visualmente aprimorado combinando várias estilizações:

```python
styled_df = (
    df.style
    .format({"Salary": "${:,.2f}", "Bonus": "${:,.0f}"})
    .highlight_max(axis=0, color="lightgreen")
    .highlight_min(axis=0, color="lightcoral")
    .background_gradient(cmap="coolwarm", subset=["Salary", "Bonus"])
    .set_table_styles(
        [{"selector": "th", "props": [("background-color", "lightgray")]}]
    )
)
styled_df
```


### **Exportando Tabelas Estilizadas**

#### **Exportar para HTML**

Salve a tabela estilizada como um arquivo HTML:

```python
styled_df.to_html("styled_table.html")
```

#### **Exibir em Notebooks**

No **Jupyter Notebook**, tabelas estilizadas são renderizadas automaticamente. Apenas retorne o objeto **Styler**:

```python
styled_df
```
