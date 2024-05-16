# JSON em Python

JSON (JavaScript Object Notation) é um formato leve de intercâmbio de dados, fácil de ler e escrever tanto para humanos quanto para máquinas. Python oferece suporte robusto para manipulação de JSON através do módulo `json`. 

## Importando o Módulo JSON

O módulo `json` é parte da biblioteca padrão do Python, então você pode usá-lo diretamente sem necessidade de instalação.

```python
import json
```

## Convertendo Entre JSON e Objetos Python

### Convertendo um Objeto Python para JSON

Para converter um objeto Python (como um dicionário) para uma string JSON, use a função `json.dumps`.

```python
import json

dados = {
    "nome": "João",
    "idade": 30,
    "cidade": "São Paulo"
}

json_string = json.dumps(dados)
print(json_string)  # Saída: {"nome": "João", "idade": 30, "cidade": "São Paulo"}
```

### Convertendo JSON para um Objeto Python

Para converter uma string JSON para um objeto Python, use a função `json.loads`.

```python
import json

json_string = '{"nome": "João", "idade": 30, "cidade": "São Paulo"}'

dados = json.loads(json_string)
print(dados)  # Saída: {'nome': 'João', 'idade': 30, 'cidade': 'São Paulo'}
```

## Lendo e Escrevendo Arquivos JSON

### Escrevendo Dados para um Arquivo JSON

Para escrever dados em um arquivo JSON, use a função `json.dump`.

```python
import json

dados = {
    "nome": "João",
    "idade": 30,
    "cidade": "São Paulo"
}

with open('dados.json', 'w') as arquivo:
    json.dump(dados, arquivo)
```

### Lendo Dados de um Arquivo JSON

Para ler dados de um arquivo JSON, use a função `json.load`.

```python
import json

with open('dados.json', 'r') as arquivo:
    dados = json.load(arquivo)

print(dados)  # Saída: {'nome': 'João', 'idade': 30, 'cidade': 'São Paulo'}
```

## Trabalhando com Estruturas de Dados JSON Complexas

JSON pode representar dados complexos como listas aninhadas e dicionários.

### Exemplo de JSON Complexo

```json
{
    "pessoas": [
        {
            "nome": "João",
            "idade": 30,
            "cidades": ["São Paulo", "Rio de Janeiro"]
        },
        {
            "nome": "Maria",
            "idade": 25,
            "cidades": ["Belo Horizonte", "Curitiba"]
        }
    ]
}
```

### Manipulando JSON Complexo em Python

```python
import json

json_string = '''
{
    "pessoas": [
        {
            "nome": "João",
            "idade": 30,
            "cidades": ["São Paulo", "Rio de Janeiro"]
        },
        {
            "nome": "Maria",
            "idade": 25,
            "cidades": ["Belo Horizonte", "Curitiba"]
        }
    ]
}
'''

dados = json.loads(json_string)

# Acessando dados
for pessoa in dados['pessoas']:
    print(f"Nome: {pessoa['nome']}, Idade: {pessoa['idade']}")
    for cidade in pessoa['cidades']:
        print(f" - Cidade: {cidade}")
```

## Personalizando a Serialização JSON

### Usando a Opção `indent`

Para melhorar a legibilidade do JSON, você pode usar a opção `indent` para adicionar espaçamento.

```python
import json

dados = {
    "nome": "João",
    "idade": 30,
    "cidade": "São Paulo"
}

json_string = json.dumps(dados, indent=4)
print(json_string)
```

### Ordenando as Chaves

Para garantir que as chaves estejam em uma ordem específica no JSON, use a opção `sort_keys`.

```python
import json

dados = {
    "nome": "João",
    "idade": 30,
    "cidade": "São Paulo"
}

json_string = json.dumps(dados, sort_keys=True, indent=4)
print(json_string)
```

### Serializando Objetos Personalizados

Para serializar objetos personalizados, você precisa fornecer uma função de serialização personalizada.

#### Exemplo

```python
import json
from datetime import datetime

class Pessoa:
    def __init__(self, nome, idade):
        self.nome = nome
        self.idade = idade
        self.aniversario = datetime.now()

def serializar_pessoa(obj):
    if isinstance(obj, Pessoa):
        return {
            "nome": obj.nome,
            "idade": obj.idade,
            "aniversario": obj.aniversario.isoformat()
        }
    raise TypeError("Tipo não serializável")

pessoa = Pessoa("João", 30)
json_string = json.dumps(pessoa, default=serializar_pessoa, indent=4)
print(json_string)
```

### Desserializando Objetos Personalizados

Para desserializar objetos personalizados, você precisa fornecer uma função de desserialização personalizada.

#### Exemplo

```python
import json
from datetime import datetime

class Pessoa:
    def __init__(self, nome, idade, aniversario):
        self.nome = nome
        self.idade = idade
        self.aniversario = datetime.fromisoformat(aniversario)

def desserializar_pessoa(dct):
    if "nome" in dct and "idade" in dct and "aniversario" in dct:
        return Pessoa(dct["nome"], dct["idade"], dct["aniversario"])
    return dct

json_string = '''
{
    "nome": "João",
    "idade": 30,
    "aniversario": "2022-03-01T12:00:00"
}
'''

pessoa = json.loads(json_string, object_hook=desserializar_pessoa)
print(f"Nome: {pessoa.nome}, Idade: {pessoa.idade}, Aniversário: {pessoa.aniversario}")
```

## Tratamento de Exceções

Ao trabalhar com JSON, você deve estar preparado para lidar com exceções, como JSON malformado.

```python
import json

json_string = '{"nome": "João", "idade": 30, "cidade": "São Paulo"'

try:
    dados = json.loads(json_string)
except json.JSONDecodeError as e:
    print(f"Erro ao decodificar JSON: {e}")
```

## Conclusão

A manipulação de JSON em Python é uma tarefa comum e essencial, facilitada pelo módulo `json` da biblioteca padrão. Com este guia, você aprendeu a converter entre JSON e objetos Python, ler e escrever arquivos JSON, lidar com estruturas de dados complexas, personalizar a serialização e desserialização, e tratar exceções relacionadas a JSON. Com essas habilidades, você está bem equipado para trabalhar com dados JSON em suas aplicações Python. Boa programação!