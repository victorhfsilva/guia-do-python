# Biblioteca `requests` em Python

A biblioteca `requests` é uma das bibliotecas mais populares em Python para fazer requisições HTTP. Ela é conhecida por sua simplicidade e facilidade de uso, permitindo que você interaja com serviços web de maneira eficiente. Neste guia, vamos explorar como instalar a biblioteca, fazer requisições básicas, lidar com diferentes tipos de dados, e usar recursos avançados como autenticação, sessões e tratamento de erros.

## Instalação

Para instalar a biblioteca `requests`, você pode usar `pip`:

```bash
pip install requests
```

## Fazendo Requisições Básicas

### Requisição GET

A requisição GET é usada para recuperar dados de um servidor.

```python
import requests

response = requests.get('https://api.github.com')
print(response.status_code)  # Saída: 200
print(response.text)         # Conteúdo da resposta
```

### Requisição POST

A requisição POST é usada para enviar dados ao servidor.

```python
import requests

url = 'https://httpbin.org/post'
data = {'chave': 'valor'}
response = requests.post(url, data=data)
print(response.status_code)  # Saída: 200
print(response.json())       # Conteúdo da resposta em JSON
```

### Outros Métodos HTTP

A biblioteca `requests` suporta outros métodos HTTP, como PUT, DELETE, HEAD, OPTIONS.

```python
# Requisição PUT
response = requests.put('https://httpbin.org/put', data={'chave': 'valor'})

# Requisição DELETE
response = requests.delete('https://httpbin.org/delete')

# Requisição HEAD
response = requests.head('https://httpbin.org/get')

# Requisição OPTIONS
response = requests.options('https://httpbin.org/get')
```

## Enviando Parâmetros em Requisições

### Parâmetros de URL

Para enviar parâmetros de URL em uma requisição GET, use o parâmetro `params`.

```python
import requests

url = 'https://httpbin.org/get'
params = {'param1': 'value1', 'param2': 'value2'}
response = requests.get(url, params=params)
print(response.url)  # Saída: https://httpbin.org/get?param1=value1&param2=value2
```

### Enviando Dados no Corpo da Requisição

Para enviar dados no corpo da requisição em formato JSON, use o parâmetro `json`.

```python
import requests

url = 'https://httpbin.org/post'
data = {'chave': 'valor'}
response = requests.post(url, json=data)
print(response.json())  # O servidor deve retornar os dados enviados em JSON
```

## Cabeçalhos de Requisição

Você pode adicionar cabeçalhos personalizados às suas requisições usando o parâmetro `headers`.

```python
import requests

url = 'https://httpbin.org/headers'
headers = {'User-Agent': 'my-app/0.0.1'}
response = requests.get(url, headers=headers)
print(response.json())
```

## Autenticação

A biblioteca `requests` suporta diversos métodos de autenticação, como autenticação básica, token e OAuth.

### Autenticação Básica

```python
from requests.auth import HTTPBasicAuth
import requests

url = 'https://httpbin.org/basic-auth/user/pass'
response = requests.get(url, auth=HTTPBasicAuth('user', 'pass'))
print(response.status_code)  # Saída: 200
```

### Autenticação com Token

```python
import requests

url = 'https://api.github.com/user'
token = 'seu_token_aqui'
headers = {'Authorization': f'token {token}'}
response = requests.get(url, headers=headers)
print(response.json())
```

## Sessões

Usar uma sessão permite que você persista certos parâmetros em várias requisições, como cabeçalhos e cookies.

```python
import requests

s = requests.Session()
s.headers.update({'User-Agent': 'my-app/0.0.1'})

response = s.get('https://httpbin.org/headers')
print(response.json())

response = s.get('https://httpbin.org/cookies/set/sessioncookie/123456789')
print(response.cookies)
```

## Tratamento de Erros

### Verificação de Status

Você pode verificar o status da resposta e levantar exceções para status de erro.

```python
import requests

url = 'https://httpbin.org/status/404'
response = requests.get(url)

if response.status_code != 200:
    print('Erro:', response.status_code)

# Ou use raise_for_status para levantar exceções automaticamente
try:
    response.raise_for_status()
except requests.exceptions.HTTPError as err:
    print('Erro HTTP:', err)
```

### Tratamento de Exceções

A biblioteca `requests` define várias exceções que você pode usar para capturar erros.

```python
import requests

url = 'https://httpbin.org/delay/5'

try:
    response = requests.get(url, timeout=2)
except requests.Timeout:
    print('A requisição demorou muito para completar')
except requests.RequestException as e:
    print('Erro na requisição:', e)
```

## Downloads de Arquivos

Você pode usar `requests` para baixar arquivos da internet.

```python
import requests

url = 'https://httpbin.org/image/png'
response = requests.get(url)

with open('image.png', 'wb') as f:
    f.write(response.content)
```

## Enviando Arquivos

Para enviar arquivos em uma requisição POST, use o parâmetro `files`.

```python
import requests

url = 'https://httpbin.org/post'
files = {'file': open('image.png', 'rb')}
response = requests.post(url, files=files)
print(response.json())
```
