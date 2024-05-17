# SQLAlchemy

SQLAlchemy é uma biblioteca SQL toolkit e ORM (Object-Relational Mapping) para Python. Ele oferece uma abordagem completa para acessar e manipular bancos de dados, combinando uma interface SQL expressiva com a simplicidade do uso de objetos Python. 

## Instalação

Para instalar o SQLAlchemy, use `pip`:

```bash
pip install sqlalchemy
```

## Conceitos Básicos

SQLAlchemy consiste em dois componentes principais:

1. **SQLAlchemy Core**: Uma abordagem procedural para acessar bancos de dados, utilizando expressões SQL e operações de mapeamento.
2. **SQLAlchemy ORM**: Uma abordagem orientada a objetos para interagir com bancos de dados, mapeando classes Python para tabelas SQL.

## Conexão com o Banco de Dados

SQLAlchemy usa uma URL de conexão para se conectar ao banco de dados. Vamos demonstrar como se conectar a diferentes bancos de dados usando SQLAlchemy.

### Conexão com SQLite

```python
from sqlalchemy import create_engine

# Criar uma engine de conexão com o banco de dados SQLite
engine = create_engine('sqlite:///meu_banco_de_dados.db')
```

### Conexão com MySQL

```python
from sqlalchemy import create_engine

# Criar uma engine de conexão com o banco de dados MySQL
engine = create_engine('mysql+pymysql://usuario:senha@localhost/meu_banco_de_dados')
```

### Conexão com PostgreSQL

```python
from sqlalchemy import create_engine

# Criar uma engine de conexão com o banco de dados PostgreSQL
engine = create_engine('postgresql+psycopg2://usuario:senha@localhost/meu_banco_de_dados')
```

### Conexão com SQL Server

```python
from sqlalchemy import create_engine

# Definir os parâmetros de conexão
driver = 'ODBC Driver 17 for SQL Server'
server = 'seu_servidor'
database = 'seu_banco_de_dados'
username = 'seu_usuario'
password = 'sua_senha'

# Criar a URL de conexão
connection_string = f'mssql+pyodbc://{username}:{password}@{server}/{database}?driver={driver}'

# Criar a engine de conexão
engine = create_engine(connection_string)
```

## SQLAlchemy Core

SQLAlchemy Core fornece uma interface para construção e execução de consultas SQL de forma programática.

### Criando Tabelas

```python
from sqlalchemy import Table, Column, Integer, String, MetaData

metadata = MetaData()

usuarios = Table('usuarios', metadata,
    Column('id', Integer, primary_key=True),
    Column('nome', String),
    Column('idade', Integer),
    Column('cidade', String)
)

# Criar as tabelas no banco de dados
metadata.create_all(engine)
```

### Inserindo Dados

```python
from sqlalchemy import insert

# Inserir dados na tabela
inserir = usuarios.insert().values(nome='Ana', idade=28, cidade='São Paulo')
conn = engine.connect()
conn.execute(inserir)
conn.close()
```

### Consultando Dados

```python
from sqlalchemy import select

# Selecionar dados da tabela
selecao = select([usuarios])
conn = engine.connect()
result = conn.execute(selecao)

for row in result:
    print(row)

conn.close()
```

### Atualizando Dados

```python
from sqlalchemy import update

# Atualizar dados na tabela
atualizar = usuarios.update().where(usuarios.c.nome == 'Ana').values(idade=30)
conn = engine.connect()
conn.execute(atualizar)
conn.close()
```

### Deletando Dados

```python
from sqlalchemy import delete

# Deletar dados da tabela
deletar = usuarios.delete().where(usuarios.c.nome == 'Ana')
conn = engine.connect()
conn.execute(deletar)
conn.close()
```
