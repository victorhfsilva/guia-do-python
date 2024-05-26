## PyMongo

### Introdução

PyMongo é a biblioteca oficial do MongoDB para Python. Ela permite interagir com o MongoDB diretamente a partir de aplicativos Python, facilitando operações CRUD, agregações e outras funcionalidades avançadas. Este guia cobre a instalação, configuração e operações básicas utilizando PyMongo.

### Instalação

Para instalar o PyMongo, use o pip:

```bash
pip install pymongo
```

### Conectando ao MongoDB

Para se conectar ao MongoDB, você precisa criar um cliente MongoDB usando a classe `MongoClient`.

#### Exemplo de Conexão Básica

```python
from pymongo import MongoClient

# Conectando ao MongoDB na máquina local (localhost) na porta padrão (27017)
client = MongoClient('localhost', 27017)

# Selecionando o banco de dados
db = client['nome_do_banco']

# Selecionando a coleção
colecao = db['nome_da_colecao']
```

#### Conexão com Autenticação

Se o MongoDB requer autenticação, forneça o nome de usuário e senha na URI de conexão.

```python
client = MongoClient('mongodb://usuario:senha@localhost:27017/nome_do_banco')
db = client['nome_do_banco']
```

### Operações CRUD com PyMongo

#### Criar (Create)

Para inserir documentos em uma coleção, você pode usar os métodos `insert_one` e `insert_many`.

**Inserir um único documento:**

```python
documento = {"nome": "João", "idade": 30, "cidade": "São Paulo"}
resultado = colecao.insert_one(documento)
print(f"Documento inserido com o ID: {resultado.inserted_id}")
```

**Inserir múltiplos documentos:**

```python
documentos = [
    {"nome": "Maria", "idade": 25, "cidade": "Rio de Janeiro"},
    {"nome": "Pedro", "idade": 35, "cidade": "Belo Horizonte"}
]
resultado = colecao.insert_many(documentos)
print(f"Documentos inseridos com os IDs: {resultado.inserted_ids}")
```

#### Ler (Read)

Para buscar documentos, você pode usar os métodos `find` e `find_one`.

**Buscar um único documento:**

```python
documento = colecao.find_one({"nome": "João"})
print(documento)
```

**Buscar múltiplos documentos:**

```python
for documento in colecao.find({"cidade": "São Paulo"}):
    print(documento)
```

**Projeção de campos:**

```python
for documento in colecao.find({"cidade": "São Paulo"}, {"nome": 1, "idade": 1, "_id": 0}):
    print(documento)
```

#### Atualizar (Update)

Para atualizar documentos, use os métodos `update_one` e `update_many`.

**Atualizar um único documento:**

```python
resultado = colecao.update_one({"nome": "João"}, {"$set": {"idade": 31}})
print(f"Documentos correspondentes: {resultado.matched_count}")
print(f"Documentos modificados: {resultado.modified_count}")
```

**Atualizar múltiplos documentos:**

```python
resultado = colecao.update_many({"cidade": "São Paulo"}, {"$set": {"cidade": "SP"}})
print(f"Documentos correspondentes: {resultado.matched_count}")
print(f"Documentos modificados: {resultado.modified_count}")
```

#### Deletar (Delete)

Para deletar documentos, use os métodos `delete_one` e `delete_many`.

**Deletar um único documento:**

```python
resultado = colecao.delete_one({"nome": "João"})
print(f"Documentos deletados: {resultado.deleted_count}")
```

**Deletar múltiplos documentos:**

```python
resultado = colecao.delete_many({"cidade": "SP"})
print(f"Documentos deletados: {resultado.deleted_count}")
```

### Agregações

PyMongo suporta operações de agregação usando o método `aggregate`.

**Exemplo de agregação:**

```python
pipeline = [
    {"$match": {"cidade": "São Paulo"}},
    {"$group": {"_id": "$cidade", "media_idade": {"$avg": "$idade"}}}
]
resultado = colecao.aggregate(pipeline)
for doc in resultado:
    print(doc)
```

### Índices

Você pode criar, listar e remover índices usando PyMongo.

**Criar um índice:**

```python
indice = colecao.create_index([("nome", pymongo.ASCENDING)])
print(f"Índice criado: {indice}")
```

**Listar índices:**

```python
indices = colecao.list_indexes()
for idx in indices:
    print(idx)
```

**Remover um índice:**

```python
resultado = colecao.drop_index("nome_1")
print(f"Índice removido: {resultado}")
```
