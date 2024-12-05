# Manipulação de Dados no Pandas

## Seleção de Dados

### Seleção de Colunas

Você pode selecionar uma ou mais colunas de um DataFrame.

```python
# Selecionar uma coluna
coluna = df['nome_coluna']

# Selecionar várias colunas
colunas = df[['nome_coluna1', 'nome_coluna2']]
```

### Seleção de Linhas

Você pode selecionar linhas usando rótulos ou índices.

```python
# Selecionar uma linha pelo índice
linha = df.loc[0]

# Selecionar várias linhas pelo índice
linhas = df.loc[0:3]

# Selecionar uma linha pela posição
linha = df.iloc[0]

# Selecionar várias linhas pela posição
linhas = df.iloc[0:3]
```

### Filtragem de Dados

Você pode filtrar dados com base em condições.

```python
# Filtrar linhas onde a idade é maior que 30
filtro = df[df['idade'] > 30]

# Filtrar com múltiplas condições
filtro = df[(df['idade'] > 30) & (df['cidade'] == 'São Paulo')]
```



## Limpeza de Dados

### Tratamento de Valores Nulos

Valores nulos são comuns em conjuntos de dados e precisam ser tratados adequadamente.

#### Verificar Valores Nulos

```python
# Verificar valores nulos
print(df.isnull().sum())
```

#### Remover Valores Nulos

```python
# Remover linhas com valores nulos
df_sem_nulos = df.dropna()

# Remover colunas com valores nulos
df_sem_nulos = df.dropna(axis=1)
```

#### Preencher Valores Nulos

```python
# Preencher valores nulos com um valor específico
df_preenchido = df.fillna(0)

# Preencher valores nulos com a média da coluna
df['idade'] = df['idade'].fillna(df['idade'].mean())
```

### Remoção de Duplicatas

```python
# Verificar duplicatas
print(df.duplicated().sum())

# Remover duplicatas
df_sem_duplicatas = df.drop_duplicates()
```

## Transformação de Dados

### Aplicação de Funções

Você pode aplicar funções a colunas ou linhas de um DataFrame.

```python
# Aplicar uma função a uma coluna
df['nova_coluna'] = df['idade'].apply(lambda x: x * 2)

# Aplicar uma função a várias colunas
df[['idade', 'nova_coluna']] = df[['idade', 'nova_coluna']].applymap(lambda x: x + 1)
```

### Renomeação de Colunas

```python
# Renomear uma coluna
df.rename(columns={'nome_coluna_antigo': 'nome_coluna_novo'}, inplace=True)

# Renomear várias colunas
df.rename(columns={'coluna1_antigo': 'coluna1_novo', 'coluna2_antigo': 'coluna2_novo'}, inplace=True)
```

### Alteração de Tipos de Dados

```python
# Alterar o tipo de dados de uma coluna
df['idade'] = df['idade'].astype(float)
```

### Criação de Novas Colunas

```python
# Criar uma nova coluna com base em outras colunas
df['nova_coluna'] = df['coluna1'] + df['coluna2']
```

## Substituição de Valores

### Substituição de Valores Específicos

```python
# Substituir valores específicos em uma coluna
df['cidade'] = df['cidade'].replace({'São Paulo': 'SP', 'Rio de Janeiro': 'RJ'})
```

### Substituição Condicional

```python
# Substituir valores condicionalmente
df.loc[df['idade'] > 30, 'categoria'] = 'Adulto'
df.loc[df['idade'] <= 30, 'categoria'] = 'Jovem'
```

## Manipulação de Strings

### Métodos de String

Você pode usar métodos de string para manipular dados textuais em colunas.

```python
# Converter strings para minúsculas
df['nome'] = df['nome'].str.lower()

# Remover espaços em branco
df['nome'] = df['nome'].str.strip()

# Dividir strings em colunas
df[['nome', 'sobrenome']] = df['nome_completo'].str.split(' ', expand=True)
```

## Agrupamento e Agregação

### Agrupamento de Dados

Você pode agrupar dados e realizar operações de agregação.

```python
# Agrupar por uma coluna e calcular a média
grupo = df.groupby('cidade')['idade'].mean()
print(grupo)

# Agrupar por múltiplas colunas e calcular várias estatísticas
grupo = df.groupby(['cidade', 'sexo']).agg({'idade': ['mean', 'min', 'max']})
print(grupo)
```

## Mesclagem e Junção de Dados

### `pd.merge`

Você pode combinar múltiplos DataFrames usando `merge`.

```python
# Criar dois DataFrames
df1 = pd.DataFrame({'ID': [1, 2, 3], 'Nome': ['Ana', 'João', 'Maria']})
df2 = pd.DataFrame({'ID': [1, 2, 3], 'Idade': [28, 34, 29]})

# Fazer a junção dos DataFrames
df_merged = pd.merge(df1, df2, on='ID')
print(df_merged)
```

### `pd.concat`

Você pode concatenar DataFrames verticalmente ou horizontalmente usando `concat`.

```python
# Criar dois DataFrames
df1 = pd.DataFrame({'ID': [1, 2], 'Nome': ['Ana', 'João']})
df2 = pd.DataFrame({'ID': [3, 4], 'Nome': ['Maria', 'Carlos']})

# Concatenar os DataFrames verticalmente
df_concat = pd.concat([df1, df2])
print(df_concat)

# Concatenar os DataFrames horizontalmente
df_concat = pd.concat([df1, df2], axis=1)
print(df_concat)
```

## Salvando Dados

### Salvando em Arquivos CSV

```python
# Salvar o DataFrame em um arquivo CSV
df.to_csv('saida.csv', index=False)
```

### Salvando em Arquivos Excel

```python
# Salvar o DataFrame em um arquivo Excel
df.to_excel('saida.xlsx', index=False)
```
### Salvando em um Banco de Dados

Você pode salvar um DataFrame diretamente em um banco de dados SQL usando a função `to_sql` do Pandas. A função `to_sql` permite inserir dados de um DataFrame em uma tabela de um banco de dados.

#### Exemplo com SQLite

```python
import pandas as pd
from sqlalchemy import create_engine

# Criar uma conexão com o banco de dados SQLite
engine = create_engine('sqlite:///meu_banco_de_dados.db')

# Exemplo de DataFrame
dados = {
    'Nome': ['Ana', 'João', 'Maria'],
    'Idade': [28, 34, 29],
    'Cidade': ['São Paulo', 'Rio de Janeiro', 'Curitiba']
}
df = pd.DataFrame(dados)

# Salvar o DataFrame no banco de dados
df.to_sql('usuarios', con=engine, if_exists='replace', index=False)
```

#### Exemplo com MySQL

```python
import pandas as pd
from sqlalchemy import create_engine

# Criar uma conexão com o banco de dados MySQL
engine = create_engine('mysql+pymysql://usuario:senha@localhost/meu_banco_de_dados')

# Salvar o DataFrame no banco de dados
df.to_sql('usuarios', con=engine, if_exists='replace', index=False)
```

#### Exemplo com PostgreSQL

```python
import pandas as pd
from sqlalchemy import create_engine

# Criar uma conexão com o banco de dados PostgreSQL
engine = create_engine('postgresql+psycopg2://usuario:senha@localhost/meu_banco_de_dados')

# Salvar o DataFrame no banco de dados
df.to_sql('usuarios', con=engine, if_exists='replace', index=False)
```

### Parâmetros Importantes de `to_sql`

- `name`: Nome da tabela no banco de dados.
- `con`: Conexão com o banco de dados (usando SQLAlchemy).
- `if_exists`: Comportamento se a tabela já existir. Pode ser 'fail' (lança um erro), 'replace' (substitui a tabela) ou 'append' (adiciona novos dados à tabela existente).
- `index`: Se `True`, salva o índice do DataFrame no banco de dados. Se `False`, não salva o índice.
- `dtype`: Especifica o tipo de dados das colunas. Pode ser um dicionário {nome_da_coluna: tipo}.

Com essas abordagens, você pode facilmente salvar seus dados em diferentes formatos e garantir que eles estejam disponíveis para futuras análises e processamento. Boa manipulação de dados!