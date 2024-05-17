# Análise dos Dados no Pandas

A análise de dados é uma parte fundamental da ciência de dados e Pandas é uma das bibliotecas mais poderosas para realizar essa tarefa em Python.

## Exploração de Dados

### Visualizar as Primeiras e Últimas Linhas

Use `head` e `tail` para visualizar as primeiras e últimas linhas do DataFrame.

```python
# Mostrar as primeiras 5 linhas
print(df.head())

# Mostrar as últimas 5 linhas
print(df.tail())
```

### Informação sobre o DataFrame

Use `info` para obter uma visão geral do DataFrame, incluindo o número de entradas, colunas, tipos de dados e valores nulos.

```python
# Informações sobre o DataFrame
print(df.info())
```

### Estatísticas Descritivas

Use `describe` para obter estatísticas descritivas das colunas numéricas.

```python
# Estatísticas descritivas
print(df.describe())
```

### Contagem de Valores Únicos

Use `value_counts` para contar a frequência de valores únicos em uma coluna.

```python
# Contagem de valores únicos
print(df['coluna'].value_counts())
```

## Análise Estatística

### Média, Mediana, Moda

```python
# Média
media = df['coluna'].mean()

# Mediana
mediana = df['coluna'].median()

# Moda
moda = df['coluna'].mode()
```

### Variância e Desvio Padrão

```python
# Variância
variancia = df['coluna'].var()

# Desvio padrão
desvio_padrao = df['coluna'].std()
```

### Correlação

Calcule a correlação entre colunas para entender as relações entre diferentes variáveis.

```python
# Matriz de correlação
correlacao = df.corr()
print(correlacao)
```