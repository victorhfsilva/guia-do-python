#  Dicionários em Python

Dicionários são uma estrutura de dados fundamental em Python, usados para armazenar coleções de pares chave-valor. Eles são mutáveis e não ordenados (antes do Python 3.7, a ordem de inserção não era garantida; a partir do Python 3.7, a ordem de inserção é preservada).

## Criando Dicionários

Você pode criar um dicionário usando chaves `{}` ou a função `dict()`.

### Sintaxe

```python
meu_dicionario = {
    'chave1': 'valor1',
    'chave2': 'valor2',
    'chave3': 'valor3'
}

ou

meu_dicionario = dict(chave1='valor1', chave2='valor2', chave3='valor3')
```

### Exemplos

```python
dados_pessoais = {
    'nome': 'João',
    'idade': 30,
    'cidade': 'São Paulo'
}
vazio = {}
```

## Acessando Valores

Você pode acessar os valores em um dicionário usando suas chaves.

### Sintaxe

```python
valor = meu_dicionario[chave]
```

### Exemplos

```python
dados_pessoais = {
    'nome': 'João',
    'idade': 30,
    'cidade': 'São Paulo'
}

print(dados_pessoais['nome'])  # Saída: João
print(dados_pessoais['idade']) # Saída: 30
```

## Modificando Dicionários

### Adicionando ou Atualizando Valores

Você pode adicionar novos pares chave-valor ou atualizar valores existentes atribuindo um valor a uma chave.

```python
dados_pessoais = {
    'nome': 'João',
    'idade': 30,
    'cidade': 'São Paulo'
}

dados_pessoais['idade'] = 31  # Atualiza o valor existente
dados_pessoais['profissao'] = 'Engenheiro'  # Adiciona um novo par chave-valor
print(dados_pessoais)
```

### Removendo Itens

Você pode remover itens de um dicionário usando `del`, `pop`, ou `popitem`.

#### Usando `del`

```python
del dados_pessoais['cidade']
print(dados_pessoais)
```

#### Usando `pop`

```python
idade = dados_pessoais.pop('idade')
print(idade)  # Saída: 31
print(dados_pessoais)
```

#### Usando `popitem`

Remove e retorna o último par chave-valor adicionado (em versões do Python a partir do 3.7).

```python
par = dados_pessoais.popitem()
print(par)  # Saída: ('profissao', 'Engenheiro')
print(dados_pessoais)
```

### Limpando o Dicionário

Você pode remover todos os itens de um dicionário usando `clear`.

```python
dados_pessoais.clear()
print(dados_pessoais)  # Saída: {}
```

## Métodos Úteis de Dicionários

### `keys`

Retorna uma visão das chaves no dicionário.

```python
chaves = dados_pessoais.keys()
print(chaves)
```

### `values`

Retorna uma visão dos valores no dicionário.

```python
valores = dados_pessoais.values()
print(valores)
```

### `items`

Retorna uma visão dos pares chave-valor no dicionário.

```python
itens = dados_pessoais.items()
print(itens)
```

### `get`

Retorna o valor de uma chave, se a chave existir, caso contrário, retorna `None` ou um valor padrão fornecido.

```python
idade = dados_pessoais.get('idade')
print(idade)  # Saída: 31

estado = dados_pessoais.get('estado', 'Desconhecido')
print(estado)  # Saída: Desconhecido
```

### `update`

Atualiza o dicionário com os pares chave-valor de outro dicionário ou de um iterável de pares chave-valor.

```python
dados_pessoais.update({'cidade': 'Rio de Janeiro', 'idade': 32})
print(dados_pessoais)
```

## Iterando sobre Dicionários

Você pode iterar sobre as chaves, valores ou pares chave-valor de um dicionário usando loops `for`.

### Iterando sobre Chaves

```python
for chave in dados_pessoais:
    print(chave)
```

### Iterando sobre Valores

```python
for valor in dados_pessoais.values():
    print(valor)
```

### Iterando sobre Pares Chave-Valor

```python
for chave, valor in dados_pessoais.items():
    print(f'{chave}: {valor}')
```

## Dicionários Aninhados

Dicionários podem conter outros dicionários, permitindo estruturas de dados complexas.

### Exemplo

```python
alunos = {
    'aluno1': {
        'nome': 'João',
        'idade': 20,
        'notas': [7.5, 8.0, 9.0]
    },
    'aluno2': {
        'nome': 'Maria',
        'idade': 22,
        'notas': [8.5, 9.0, 10.0]
    }
}

print(alunos['aluno1']['nome'])  # Saída: João
print(alunos['aluno2']['notas']) # Saída: [8.5, 9.0, 10.0]
```
