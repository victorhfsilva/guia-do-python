# Dados Temporais no Pandas

## Criação de Objetos Datetime

Pandas fornece várias maneiras de criar objetos datetime a partir de strings, listas e outras fontes.

### Usando `pd.to_datetime`

```python
import pandas as pd

# Converter uma string para datetime
data = pd.to_datetime('2023-05-01')
print(data)

# Converter uma lista de strings para datetime
datas = pd.to_datetime(['2023-05-01', '2023-05-02', '2023-05-03'])
print(datas)
```

### Criar um Range de Datas com `pd.date_range`

```python
# Criar um range de datas
date_range = pd.date_range(start='2023-05-01', end='2023-05-10', freq='D')
print(date_range)
```

## Indexação Temporal

### Usar Datas como Índice

Você pode definir uma coluna de datas como índice do DataFrame para facilitar a manipulação de séries temporais.

```python
import pandas as pd

# Exemplo de DataFrame
dados = {
    'Data': ['2023-05-01', '2023-05-02', '2023-05-03'],
    'Valor': [10, 20, 30]
}

df = pd.DataFrame(dados)

# Converter a coluna 'Data' para datetime
df['Data'] = pd.to_datetime(df['Data'])

# Definir a coluna 'Data' como índice
df.set_index('Data', inplace=True)
print(df)
```

### Seleção de Dados Temporais

Você pode selecionar dados específicos com base em datas usando indexação.

```python
# Selecionar dados para uma data específica
print(df.loc['2023-05-01'])

# Selecionar dados para um range de datas
print(df.loc['2023-05-01':'2023-05-02'])
```

## Resampling e Agregação

### Resampling

O método `resample` permite alterar a frequência dos dados temporais, agregando os dados em novas frequências.

```python
# Exemplo de DataFrame com dados diários
date_range = pd.date_range(start='2023-05-01', periods=10, freq='D')
dados = {'Data': date_range, 'Valor': range(10)}
df = pd.DataFrame(dados)
df.set_index('Data', inplace=True)

# Resample para frequência semanal e calcular a soma
df_semanal = df.resample('W').sum()
print(df_semanal)
```

### Agregação

Você pode usar funções de agregação com `resample` para resumir os dados.

```python
# Calcular a média semanal
df_media_semanal = df.resample('W').mean()
print(df_media_semanal)

# Calcular a soma e o máximo semanal
df_agregado = df.resample('W').agg({'Valor': ['sum', 'max']})
print(df_agregado)
```

## Operações com Datas

### Extraindo Componentes de Datas

Você pode extrair componentes como ano, mês, dia, etc., de uma coluna datetime.

```python
# Adicionar colunas para ano, mês e dia
df['Ano'] = df.index.year
df['Mes'] = df.index.month
df['Dia'] = df.index.day
print(df)
```

### Operações com Timedeltas

Você pode realizar operações com diferenças de tempo usando `pd.Timedelta`.

```python
# Adicionar 7 dias a cada data
df['Data_Mais_7_Dias'] = df.index + pd.Timedelta(days=7)
print(df)
```

## Trabalhando com Time Zones

### Conversão de Time Zones

Pandas permite trabalhar com time zones, convertendo e localizando datas.

```python
# Definir o time zone para o índice datetime
df = df.tz_localize('UTC')
print(df)

# Converter para outro time zone
df = df.tz_convert('America/Sao_Paulo')
print(df)
```
