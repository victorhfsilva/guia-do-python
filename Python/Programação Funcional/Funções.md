# Funções em Python

Em Python, funções são consideradas "cidadãs de primeira classe" ou "funções de primeira classe". Isso significa que as funções em Python são tratadas como objetos de primeira classe. Elas podem ser atribuídas a variáveis, passadas como argumentos para outras funções, retornadas de outras funções e armazenadas em estruturas de dados. Este conceito é fundamental para muitos paradigmas de programação, incluindo programação funcional.

## Características das Funções de Primeira Classe

### 1. Atribuição de Funções a Variáveis

Você pode atribuir uma função a uma variável, o que permite chamá-la através dessa variável.

#### Exemplo

```python
def saudacao(nome):
    return f"Olá, {nome}!"

saudar = saudacao
print(saudar("João"))  # Saída: Olá, João!
```

### 2. Passagem de Funções como Argumentos

Funções podem ser passadas como argumentos para outras funções.

#### Exemplo

```python
def aplicar_funcao(func, valor):
    return func(valor)

def quadrado(x):
    return x ** 2

resultado = aplicar_funcao(quadrado, 5)
print(resultado)  # Saída: 25
```

### 3. Retorno de Funções de Outras Funções

Funções podem retornar outras funções.

#### Exemplo

```python
def saudacao(prefixo):
    def adicionar_nome(nome):
        return f"{prefixo}, {nome}!"
    return adicionar_nome

saudar_ola = saudacao("Olá")
print(saudar_ola("João"))  # Saída: Olá, João!

saudar_bom_dia = saudacao("Bom dia")
print(saudar_bom_dia("Maria"))  # Saída: Bom dia, Maria!
```

### 4. Armazenamento de Funções em Estruturas de Dados

Funções podem ser armazenadas em listas, dicionários ou outras estruturas de dados.

#### Exemplo

```python
def somar(a, b):
    return a + b

def subtrair(a, b):
    return a - b

operacoes = {
    'soma': somar,
    'subtracao': subtrair
}

print(operacoes['soma'](10, 5))       # Saída: 15
print(operacoes['subtracao'](10, 5))  # Saída: 5
```

## Funções de Ordem Superior

Funções que recebem outras funções como argumentos ou retornam funções como resultado são chamadas de funções de ordem superior.

### Exemplo com `map`

A função `map` aplica uma função a todos os itens de um iterável (como uma lista).

#### Exemplo

```python
def quadrado(x):
    return x ** 2

numeros = [1, 2, 3, 4, 5]
quadrados = map(quadrado, numeros)
print(list(quadrados))  # Saída: [1, 4, 9, 16, 25]
```

### Exemplo com `filter`

A função `filter` cria uma lista de elementos para os quais uma função retorna `True`.

#### Exemplo

```python
def par(x):
    return x % 2 == 0

numeros = [1, 2, 3, 4, 5, 6]
pares = filter(par, numeros)
print(list(pares))  # Saída: [2, 4, 6]
```

### Exemplo com `reduce`

A função `reduce` aplica uma função de duas entradas cumulativamente aos itens de um iterável, reduzindo-os a um único valor. `reduce` está disponível no módulo `functools`.

#### Exemplo

```python
from functools import reduce

def somar(x, y):
    return x + y

numeros = [1, 2, 3, 4, 5]
soma_total = reduce(somar, numeros)
print(soma_total)  # Saída: 15
```

## Funções Lambda

Funções lambda são funções anônimas definidas usando a palavra-chave `lambda`. Elas são úteis para criar pequenas funções de forma concisa.

### Exemplo

```python
quadrado = lambda x: x ** 2
print(quadrado(5))  # Saída: 25

numeros = [1, 2, 3, 4, 5]
quadrados = map(lambda x: x ** 2, numeros)
print(list(quadrados))  # Saída: [1, 4, 9, 16, 25]
```

## Funções Decoradoras

Decoradores são funções que modificam o comportamento de outras funções. Eles são usados para adicionar funcionalidades a uma função existente de forma concisa e reutilizável.

### Exemplo de Decorador

```python
def decorador(func):
    def wrapper(*args, **kwargs):
        print("Executando antes da função")
        resultado = func(*args, **kwargs)
        print("Executando depois da função")
        return resultado
    return wrapper

@decorador
def saudacao(nome):
    print(f"Olá, {nome}!")

saudacao("João")
# Saída:
# Executando antes da função
# Olá, João!
# Executando depois da função
```