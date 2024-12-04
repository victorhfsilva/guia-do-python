
O **Pandas** oferece suporte integrado para criar gráficos de maneira simples e eficiente, usando **Matplotlib** como backend. Com o método **`.plot()`**, é possível gerar diversos tipos de gráficos diretamente de **DataFrames** e **Series**, facilitando a análise visual dos dados.

### **Configurando o Ambiente**

#### **Importar Bibliotecas Necessárias**

Antes de criar gráficos, importe o Pandas e, opcionalmente, Matplotlib para ajustar detalhes dos gráficos:

```python
import pandas as pd
import matplotlib.pyplot as plt
```

#### **Habilitar Exibição de Gráficos**

Certifique-se de que os gráficos sejam exibidos no ambiente Jupyter ou Databricks:

```python
%matplotlib inline
```



### **Criando um DataFrame de Exemplo**

Vamos criar um **DataFrame** para usar nos exemplos:

```python
data = {
    "Month": ["Jan", "Feb", "Mar", "Apr", "May"],
    "Sales": [250, 300, 350, 400, 450],
    "Expenses": [200, 250, 300, 350, 400]
}

df = pd.DataFrame(data)
print(df)
```

|Month|Sales|Expenses|
|---|---|---|
|Jan|250|200|
|Feb|300|250|
|Mar|350|300|
|Apr|400|350|
|May|450|400|


### **Criando Gráficos Simples**

#### **Gráfico de Linhas**

O gráfico de linhas é o padrão do **`.plot()`**:

```python
df.plot(x="Month", y="Sales", kind="line", title="Monthly Sales", marker="o")
plt.show()
```

#### **Gráfico de Barras**

Crie um gráfico de barras para comparar categorias:

```python
df.plot(x="Month", y="Sales", kind="bar", title="Sales per Month")
plt.show()
```

#### **Gráfico de Barras Empilhadas**

Empilhe os valores para mostrar a relação entre colunas:

```python
df.plot(x="Month", y=["Sales", "Expenses"], kind="bar", stacked=True, title="Sales vs Expenses")
plt.show()
```

#### **Gráfico de Dispersão**

Visualize a relação entre duas variáveis:

```python
df.plot(x="Sales", y="Expenses", kind="scatter", title="Sales vs Expenses")
plt.show()
```

#### **Gráfico de Pizza**

Visualize proporções usando o **`.plot.pie()`**:

```python
df.set_index("Month")["Sales"].plot.pie(title="Sales Distribution", autopct="%.1f%%", figsize=(6, 6))
plt.show()
```



### **Personalizando Gráficos**

#### **Adicionar Títulos e Rótulos**

Adicione títulos, rótulos nos eixos e uma grade ao gráfico:

```python
ax = df.plot(x="Month", y="Sales", kind="line", title="Monthly Sales")
ax.set_xlabel("Month")
ax.set_ylabel("Sales")
ax.grid(True)
plt.show()
```

#### **Ajustar o Tamanho do Gráfico**

Defina o tamanho do gráfico usando o parâmetro **`figsize`**:

```python
df.plot(x="Month", y="Sales", kind="line", figsize=(8, 5), title="Sales per Month")
plt.show()
```

#### **Alterar Estilos**

Escolha estilos de gráfico com **Matplotlib**:

```python
plt.style.use("ggplot")
df.plot(x="Month", y="Sales", kind="line", title="Styled Sales Graph")
plt.show()
```


### **Comparando Múltiplas Colunas**

#### **Gráfico de Linhas com Múltiplas Colunas**

Compare várias colunas no mesmo gráfico:

```python
df.plot(x="Month", y=["Sales", "Expenses"], kind="line", title="Sales vs Expenses")
plt.show()
```

#### **Gráfico de Área**

Visualize a composição total de dados:

```python
df.plot(x="Month", y=["Sales", "Expenses"], kind="area", title="Cumulative Sales and Expenses", alpha=0.7)
plt.show()
```

### **Salvando Gráficos**

Salve o gráfico como uma imagem:

```python
ax = df.plot(x="Month", y="Sales", kind="line", title="Monthly Sales")
plt.savefig("monthly_sales.png")
```


### **Exemplo Completo**

#### **Cenário**

Você deseja:

1. Comparar vendas e despesas mensais em um gráfico de barras.
2. Adicionar um título e rótulos nos eixos.
3. Salvar o gráfico como um arquivo de imagem.

#### **Código**

```python
import pandas as pd
import matplotlib.pyplot as plt

data = {
    "Month": ["Jan", "Feb", "Mar", "Apr", "May"],
    "Sales": [250, 300, 350, 400, 450],
    "Expenses": [200, 250, 300, 350, 400]
}

df = pd.DataFrame(data)

# Criar gráfico de barras
ax = df.plot(x="Month", y=["Sales", "Expenses"], kind="bar", title="Sales vs Expenses", figsize=(8, 5))
ax.set_xlabel("Month")
ax.set_ylabel("Amount")
ax.grid(True)

# Salvar o gráfico
plt.savefig("sales_vs_expenses.png")
plt.show()
```
