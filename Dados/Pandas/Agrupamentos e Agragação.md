# grupamentos e Agregação no Pandas

Agrupamento e agregação são funcionalidades poderosas no Pandas que permitem resumir e analisar grandes conjuntos de dados de forma eficiente. 

## Carregar Dados

Para ilustrar as operações de agrupamento e agregação, vamos começar carregando um DataFrame de exemplo.

```python
import pandas as pd

# Exemplo de DataFrame
dados = {
    'Nome': ['Ana', 'João', 'Maria', 'Pedro', 'Ana', 'João'],
    'Idade': [28, 34, 29, 45, 28, 34],
    'Cidade': ['São Paulo', 'Rio de Janeiro', 'Curitiba', 'São Paulo', 'Curitiba', 'Rio de Janeiro'],
    'Salário': [3000, 4000, 3500, 5000, 3000, 4000]
}

df = pd.DataFrame(dados)

# Mostrar as primeiras linhas do DataFrame
print(df.head())
```

## Agrupamento Básico

### `groupby`

O método `groupby` permite agrupar dados com base em uma ou mais colunas. Após o agrupamento, você pode aplicar várias funções de agregação aos dados agrupados.

### Exemplo de Agrupamento Simples

Agrupar por uma coluna e calcular a média de outra coluna.

```python
# Agrupar por cidade e calcular a média dos salários
grupo_cidade = df.groupby('Cidade')['Salário'].mean()
print(grupo_cidade)
```

### Agrupamento por Múltiplas Colunas

Você pode agrupar dados por múltiplas colunas e aplicar funções de agregação.

```python
# Agrupar por cidade e idade e calcular a média dos salários
grupo_cidade_idade = df.groupby(['Cidade', 'Idade'])['Salário'].mean()
print(grupo_cidade_idade)
```

### Aplicando Várias Funções de Agregação

Você pode aplicar várias funções de agregação ao mesmo tempo usando o método `agg`.

```python
# Agrupar por cidade e aplicar várias funções de agregação
grupo_cidade_agg = df.groupby('Cidade')['Salário'].agg(['mean', 'sum', 'min', 'max'])
print(grupo_cidade_agg)
```

## Funções de Agregação Comuns

### `mean`

Calcula a média dos valores.

```python
# Média dos salários por cidade
media_salarios = df.groupby('Cidade')['Salário'].mean()
print(media_salarios)
```

### `sum`

Calcula a soma dos valores.

```python
# Soma dos salários por cidade
soma_salarios = df.groupby('Cidade')['Salário'].sum()
print(soma_salarios)
```

### `min` e `max`

Calcula o valor mínimo e máximo.

```python
# Salário mínimo e máximo por cidade
min_salarios = df.groupby('Cidade')['Salário'].min()
max_salarios = df.groupby('Cidade')['Salário'].max()
print(min_salarios)
print(max_salarios)
```

### `count`

Conta o número de ocorrências.

```python
# Contagem de pessoas por cidade
contagem_pessoas = df.groupby('Cidade')['Nome'].count()
print(contagem_pessoas)
```

### `std` e `var`

Calcula o desvio padrão e a variância dos valores.

```python
# Desvio padrão e variância dos salários por cidade
desvio_padrao_salarios = df.groupby('Cidade')['Salário'].std()
variancia_salarios = df.groupby('Cidade')['Salário'].var()
print(desvio_padrao_salarios)
print(variancia_salarios)
```

## Agrupamento e Transformação

### `transform`

O método `transform` permite aplicar uma função aos grupos e retornar um objeto do mesmo tamanho que o DataFrame original.

```python
# Normalizar os salários por cidade
df['Salário Normalizado'] = df.groupby('Cidade')['Salário'].transform(lambda x: (x - x.mean()) / x.std())
print(df)
```

## Agrupamento e Filtragem

### `filter`

O método `filter` permite filtrar grupos com base em uma condição.

```python
# Filtrar cidades com média salarial maior que 3500
cidades_filtradas = df.groupby('Cidade').filter(lambda x: x['Salário'].mean() > 3500)
print(cidades_filtradas)
```

## Agrupamento e Aplicação de Funções Customizadas

### `apply`

O método `apply` permite aplicar uma função customizada aos grupos.

```python
# Definir uma função customizada para calcular a faixa salarial (máximo - mínimo)
def faixa_salarial(grupo):
    return grupo['Salário'].max() - grupo['Salário'].min()

# Aplicar a função customizada aos grupos
faixa_salarios = df.groupby('Cidade').apply(faixa_salarial)
print(faixa_salarios)
```
