# Carregamento de Dados no Pandas

O Pandas é uma biblioteca poderosa e versátil para a manipulação e análise de dados em Python. Um dos seus recursos mais úteis é a capacidade de carregar dados de várias fontes de forma eficiente. Este guia abrange as principais formas de carregar dados usando Pandas, incluindo arquivos CSV, Excel, JSON, bancos de dados SQL, entre outros.

## Instalando Pandas

Para instalar Pandas, use `pip`:

```bash
pip install pandas
```

## Importando Pandas

Para usar Pandas, você deve importá-lo primeiro. A convenção comum é importar Pandas como `pd`:

```python
import pandas as pd
```

## Carregando Dados de Arquivos CSV

### `pd.read_csv`

A função `pd.read_csv` é usada para ler arquivos CSV e convertê-los em um DataFrame do Pandas.

```python
import pandas as pd

# Carregar dados de um arquivo CSV
df = pd.read_csv('dados.csv')

# Mostrar as primeiras linhas do DataFrame
print(df.head())
```

### Principais Parâmetros de `pd.read_csv`

- `filepath_or_buffer`: Caminho para o arquivo CSV.
- `sep`: Delimitador (padrão é `,`).
- `header`: Linha a ser usada como cabeçalho (padrão é a primeira linha).
- `names`: Lista de nomes das colunas (útil se `header` for `None`).
- `index_col`: Coluna(s) a ser(em) usada(s) como índice do DataFrame.
- `usecols`: Lista de colunas a serem lidas.
- `dtype`: Tipo de dados para as colunas.
- `parse_dates`: Colunas a serem analisadas como datas.

#### Exemplo com Parâmetros

```python
import pandas as pd

# Carregar dados de um arquivo CSV com parâmetros específicos
df = pd.read_csv('dados.csv', sep=';', header=0, index_col=0, usecols=['col1', 'col2', 'col3'], dtype={'col1': int, 'col2': float}, parse_dates=['col3'])

# Mostrar as primeiras linhas do DataFrame
print(df.head())
```

## Carregando Dados de Arquivos Excel

### `pd.read_excel`

A função `pd.read_excel` é usada para ler arquivos Excel (.xlsx, .xls) e convertê-los em um DataFrame do Pandas.

```python
import pandas as pd

# Carregar dados de um arquivo Excel
df = pd.read_excel('dados.xlsx')

# Mostrar as primeiras linhas do DataFrame
print(df.head())
```

### Principais Parâmetros de `pd.read_excel`

- `io`: Caminho para o arquivo Excel.
- `sheet_name`: Nome ou índice da planilha a ser lida (padrão é a primeira planilha).
- `header`: Linha a ser usada como cabeçalho (padrão é a primeira linha).
- `names`: Lista de nomes das colunas.
- `index_col`: Coluna(s) a ser(em) usada(s) como índice do DataFrame.
- `usecols`: Lista de colunas a serem lidas.
- `dtype`: Tipo de dados para as colunas.
- `parse_dates`: Colunas a serem analisadas como datas.

#### Exemplo com Parâmetros

```python
import pandas as pd

# Carregar dados de uma planilha específica de um arquivo Excel
df = pd.read_excel('dados.xlsx', sheet_name='Planilha1', header=0, index_col=0, usecols=['col1', 'col2', 'col3'], dtype={'col1': int, 'col2': float}, parse_dates=['col3'])

# Mostrar as primeiras linhas do DataFrame
print(df.head())
```

## Carregando Dados de Arquivos JSON

### `pd.read_json`

A função `pd.read_json` é usada para ler arquivos JSON e convertê-los em um DataFrame do Pandas.

```python
import pandas as pd

# Carregar dados de um arquivo JSON
df = pd.read_json('dados.json')

# Mostrar as primeiras linhas do DataFrame
print(df.head())
```

### Principais Parâmetros de `pd.read_json`

- `path_or_buf`: Caminho para o arquivo JSON.
- `orient`: Orientação do JSON (padrão é `columns`).
- `dtype`: Tipo de dados para as colunas.
- `convert_dates`: Colunas a serem analisadas como datas.

#### Exemplo com Parâmetros

```python
import pandas as pd

# Carregar dados de um arquivo JSON com parâmetros específicos
df = pd.read_json('dados.json', orient='columns', dtype={'col1': int, 'col2': float}, convert_dates=['col3'])

# Mostrar as primeiras linhas do DataFrame
print(df.head())
```

## Carregando Dados de Bancos de Dados SQL

### `pd.read_sql`

A função `pd.read_sql` é usada para executar consultas SQL e carregar os resultados em um DataFrame do Pandas.

#### Usando `sqlite3`

```python
import pandas as pd
import sqlite3

# Conectar ao banco de dados SQLite
conexao = sqlite3.connect('meu_banco_de_dados.db')

# Executar uma consulta SQL e carregar os dados em um DataFrame
df = pd.read_sql('SELECT * FROM minha_tabela', conexao)

# Mostrar as primeiras linhas do DataFrame
print(df.head())

# Fechar a conexão
conexao.close()
```

### Principais Parâmetros de `pd.read_sql`

- `sql`: Consulta SQL ou nome da tabela.
- `con`: Conexão com o banco de dados.
- `index_col`: Coluna(s) a ser(em) usada(s) como índice do DataFrame.
- `coerce_float`: Forçar a conversão de números em ponto flutuante (padrão é `True`).
- `params`: Parâmetros para a consulta SQL.

#### Exemplo com Parâmetros

```python
import pandas as pd
import sqlite3

# Conectar ao banco de dados SQLite
conexao = sqlite3.connect('meu_banco_de_dados.db')

# Executar uma consulta SQL com parâmetros específicos
df = pd.read_sql('SELECT col1, col2 FROM minha_tabela WHERE col3 > ?', conexao, params=(10,), index_col='col1', coerce_float=True)

# Mostrar as primeiras linhas do DataFrame
print(df.head())

# Fechar a conexão
conexao.close()
```

## Carregando Dados de Arquivos HTML

### `pd.read_html`

A função `pd.read_html` é usada para ler tabelas HTML e convertê-las em DataFrames do Pandas.

```python
import pandas as pd

# Carregar todas as tabelas de um arquivo HTML
tables = pd.read_html('dados.html')

# Mostrar a primeira tabela
df = tables[0]
print(df.head())
```

### Principais Parâmetros de `pd.read_html`

- `io`: Caminho ou URL para o arquivo HTML.
- `match`: Expressão regular para selecionar tabelas específicas.
- `header`: Linha a ser usada como cabeçalho (padrão é a primeira linha).
- `index_col`: Coluna(s) a ser(em) usada(s) como índice do DataFrame.
- `attrs`: Atributos HTML para identificar as tabelas.

#### Exemplo com Parâmetros

```python
import pandas as pd

# Carregar tabelas específicas de um arquivo HTML
tables = pd.read_html('dados.html', match='Nome da Tabela', header=0, index_col=0, attrs={'class': 'tabela'})

# Mostrar a primeira tabela
df = tables[0]
print(df.head())
```