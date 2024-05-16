# Banco de Dados em Python

## SQLite

SQLite é um banco de dados leve e embutido, ideal para desenvolvimento e aplicações pequenas.

### Instalando a Biblioteca SQLite

A biblioteca `sqlite3` vem incluída na biblioteca padrão do Python.

### Conectando ao Banco de Dados

```python
import sqlite3

conexao = sqlite3.connect('meu_banco_de_dados.db')
cursor = conexao.cursor()
```

### Criando Tabelas

```python
cursor.execute('''
    CREATE TABLE IF NOT EXISTS usuarios (
        id INTEGER PRIMARY KEY,
        nome TEXT,
        idade INTEGER
    )
''')
```

### Inserindo Dados

```python
cursor.execute('''
    INSERT INTO usuarios (nome, idade)
    VALUES (?, ?)
''', ('João', 30))
conexao.commit()
```

### Consultando Dados

```python
cursor.execute('SELECT * FROM usuarios')
usuarios = cursor.fetchall()
for usuario in usuarios:
    print(usuario)
```

### Atualizando e Deletando Dados

```python
# Atualizando
cursor.execute('''
    UPDATE usuarios
    SET idade = ?
    WHERE nome = ?
''', (31, 'João'))
conexao.commit()

# Deletando
cursor.execute('''
    DELETE FROM usuarios
    WHERE nome = ?
''', ('João',))
conexao.commit()
```

### Fechando a Conexão

```python
conexao.close()
```

## MySQL

Para trabalhar com MySQL, a biblioteca `mysql-connector-python` é uma das opções populares.

### Instalando a Biblioteca MySQL

```bash
pip install mysql-connector-python
```

### Conectando ao Banco de Dados

```python
import mysql.connector

conexao = mysql.connector.connect(
    host='localhost',
    user='seu_usuario',
    password='sua_senha',
    database='meu_banco_de_dados'
)
cursor = conexao.cursor()
```

### Criando Tabelas, Inserindo, Consultando, Atualizando e Deletando Dados

Os comandos SQL são semelhantes aos do SQLite, mas com pequenas diferenças na sintaxe de conexão e execução de comandos.

### Fechando a Conexão

```python
conexao.close()
```

## PostgreSQL

Para trabalhar com PostgreSQL, a biblioteca `psycopg2` é uma das opções populares.

### Instalando a Biblioteca PostgreSQL

```bash
pip install psycopg2-binary
```

### Conectando ao Banco de Dados

```python
import psycopg2

conexao = psycopg2.connect(
    host='localhost',
    database='meu_banco_de_dados',
    user='seu_usuario',
    password='sua_senha'
)
cursor = conexao.cursor()
```

### Criando Tabelas, Inserindo, Consultando, Atualizando e Deletando Dados

Os comandos SQL são semelhantes aos do SQLite e MySQL.

### Fechando a Conexão

```python
conexao.close()
```

## MongoDB

Para trabalhar com MongoDB, a biblioteca `pymongo` é a opção mais comum.

### Instalando a Biblioteca MongoDB

```bash
pip install pymongo
```

### Conectando ao Banco de Dados

```python
from pymongo import MongoClient

cliente = MongoClient('localhost', 27017)
db = cliente.meu_banco_de_dados
colecao = db.usuarios
```

### Inserindo Dados

```python
usuario = {'nome': 'João', 'idade': 30}
colecao.insert_one(usuario)
```

### Consultando Dados

```python
usuarios = colecao.find()
for usuario in usuarios:
    print(usuario)
```

### Atualizando e Deletando Dados

```python
# Atualizando
colecao.update_one({'nome': 'João'}, {'$set': {'idade': 31}})

# Deletando
colecao.delete_one({'nome': 'João'})
```

### Fechando a Conexão

```python
cliente.close()
```

## SQL Server

SQL Server é um sistema de gerenciamento de banco de dados relacional (RDBMS) desenvolvido pela Microsoft.

### Instalando a Biblioteca SQL Server

A biblioteca `pyodbc` é uma das opções populares para conectar-se ao SQL Server.

```bash
pip install pyodbc
```

### Conectando ao Banco de Dados

```python
import pyodbc

conexao = pyodbc.connect(
    'DRIVER={ODBC Driver 17 for SQL Server};'
    'SERVER=seu_servidor;'
    'DATABASE=seu_banco_de_dados;'
    'UID=seu_usuario;'
    'PWD=sua_senha'
)
cursor = conexao.cursor()
```

### Criando Tabelas

```python
cursor.execute('''
    CREATE TABLE IF NOT EXISTS usuarios (
        id INT PRIMARY KEY IDENTITY,
        nome NVARCHAR(100),
        idade INT
    )
''')
conexao.commit()
```

### Inserindo Dados

```python
cursor.execute('''
    INSERT INTO usuarios (nome, idade)
    VALUES (?, ?)
''', ('João', 30))
conexao.commit()
```

### Consultando Dados

```python
cursor.execute('SELECT * FROM usuarios')
usuarios = cursor.fetchall()
for usuario in usuarios:
    print(usuario)
```

### Atualizando e Deletando Dados

```python
# Atualizando
cursor.execute('''
    UPDATE usuarios
    SET idade = ?
    WHERE nome = ?
''', (31, 'João'))
conexao.commit()

# Deletando
cursor.execute('''
    DELETE FROM usuarios
    WHERE nome = ?
''', ('João',))
conexao.commit()
```

### Fechando a Conexão

```python
conexao.close()
```

## InfluxDB

InfluxDB é um banco de dados de séries temporais (TSDB) altamente escalável e eficiente, ideal para armazenar e consultar grandes volumes de dados de séries temporais. Neste guia, vamos explorar como usar a biblioteca `influxdb` e especificamente `DataFrameClient` para interagir com o InfluxDB.

### Instalando a Biblioteca InfluxDB

A biblioteca `influxdb` pode ser instalada usando `pip`:

```bash
pip install influxdb
```

### Conectando ao Banco de Dados

#### Usando DataFrameClient

```python
from influxdb import DataFrameClient

df_client = DataFrameClient(host='localhost', port=8086, username='seu_usuario', password='sua_senha', database='meu_banco_de_dados')
```

### Escrevendo Dados

#### Escrevendo DataFrames

Para escrever dados no InfluxDB usando `DataFrameClient`, você pode converter seus dados em um Pandas DataFrame.

```python
import pandas as pd
from datetime import datetime

# Criando um DataFrame
data = {
    'valor': [23.5, 24.0, 25.3],
    'sensor': ['sensor1', 'sensor1', 'sensor1']
}
index = [datetime(2022, 1, 1, 10, 0), datetime(2022, 1, 1, 10, 10), datetime(2022, 1, 1, 10, 20)]
df = pd.DataFrame(data, index=index)

# Escrevendo o DataFrame no InfluxDB
df_client.write_points(df, 'medicao')
```

### Consultando Dados

#### Consultando com DataFrameClient

Você pode consultar dados do InfluxDB e obter os resultados como DataFrames.

```python
query = 'SELECT * FROM medicao WHERE time > now() - 1h'
df_result = df_client.query(query)

for measurement, df in df_result.items():
    print(f"Measurement: {measurement}")
    print(df)
```

### Fechando a Conexão

```python
df_client.close()
```

## Boas Práticas

1. **Segurança**: Use variáveis de ambiente para armazenar credenciais sensíveis.
2. **Conexão**: Sempre feche as conexões com o banco de dados após concluir as operações.
3. **Tratamento de Erros**: Use blocos try-except para tratar erros e garantir que a conexão seja fechada adequadamente em caso de falhas.

## Boas Práticas

1. **Segurança**: Nunca insira dados diretamente nas consultas SQL para evitar ataques de injeção SQL. Use parâmetros em consultas.
2. **Conexão**: Sempre feche as conexões com o banco de dados após concluir as operações.
3. **Transações**: Use transações para garantir a integridade dos dados.
4. **Tratamento de Erros**: Use blocos try-except para tratar erros e garantir que a conexão seja fechada adequadamente em caso de falhas.

### Exemplo de Tratamento de Erros

```python
import sqlite3

try:
    conexao = sqlite3.connect('meu_banco_de_dados.db')
    cursor = conexao.cursor()
    
    # Suas operações no banco de dados aqui
    
except sqlite3.Error as e:
    print(f"Erro ao acessar o banco de dados: {e}")
finally:
    if conexao:
        conexao.close()
```
