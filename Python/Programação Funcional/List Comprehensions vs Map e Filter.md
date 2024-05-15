# List Comprehensions vs Map e Filter

## Compreensões de Listas (List Comprehensions)

Compreensões de listas são uma maneira concisa de criar listas. Elas são geralmente mais legíveis e fáceis de entender do que as funções `map` e `filter`.

### Sintaxe

```python
[expressão for item in iterável if condição]
```

### Exemplo de Uso

#### Criar uma lista de quadrados de números

```python
numeros = [1, 2, 3, 4, 5]
quadrados = [x ** 2 for x in numeros]
print(quadrados)  # Saída: [1, 4, 9, 16, 25]
```

#### Filtrar números pares

```python
numeros = [1, 2, 3, 4, 5, 6]
pares = [x for x in numeros if x % 2 == 0]
print(pares)  # Saída: [2, 4, 6]
```

### Vantagens

- **Legibilidade**: A sintaxe é mais clara e direta, tornando o código mais fácil de entender.
- **Flexibilidade**: Pode combinar filtragem e mapeamento em uma única expressão.

### Desvantagens

- **Complexidade**: Para operações muito complexas, compreensões de listas podem se tornar difíceis de ler e manter.
- **Desempenho**: Embora geralmente eficiente, pode não ser tão rápido quanto funções especializadas em alguns casos específicos.

## Funções `map` e `filter`

As funções `map` e `filter` são funções embutidas que aplicam uma função a todos os itens de um iterável (map) ou filtram os itens de acordo com uma função de teste (filter).

### Função `map`

A função `map` aplica uma função a todos os itens de um iterável e retorna um iterador.

#### Sintaxe

```python
map(função, iterável)
```

#### Exemplo de Uso

```python
def quadrado(x):
    return x ** 2

numeros = [1, 2, 3, 4, 5]
quadrados = map(quadrado, numeros)
print(list(quadrados))  # Saída: [1, 4, 9, 16, 25]
```

### Função `filter`

A função `filter` cria um iterador contendo apenas os itens do iterável para os quais a função de teste retorna `True`.

#### Sintaxe

```python
filter(função, iterável)
```

#### Exemplo de Uso

```python
def par(x):
    return x % 2 == 0

numeros = [1, 2, 3, 4, 5, 6]
pares = filter(par, numeros)
print(list(pares))  # Saída: [2, 4, 6]
```

### Vantagens

- **Especialização**: `map` e `filter` são bem otimizados para suas respectivas tarefas.
- **Composição**: Podem ser facilmente compostos para realizar operações complexas.

### Desvantagens

- **Legibilidade**: A combinação de `map` e `filter` pode ser menos legível do que compreensões de listas, especialmente para quem não está familiarizado com a programação funcional.
- **Flexibilidade**: Separar a lógica de mapeamento e filtragem pode exigir mais linhas de código e resultar em maior verbosidade.

### Exemplo Combinado

#### Usando List Comprehensions

```python
numeros = [1, 2, 3, 4, 5, 6]
resultado = [x ** 2 for x in numeros if x % 2 == 0]
print(resultado)  # Saída: [4, 16, 36]
```

#### Usando `map` e `filter`

```python
numeros = [1, 2, 3, 4, 5, 6]

def par(x):
    return x % 2 == 0

def quadrado(x):
    return x ** 2

pares = filter(par, numeros)
quadrados = map(quadrado, pares)
resultado = list(quadrados)
print(resultado)  # Saída: [4, 16, 36]
```

## Comparação Direta

### Legibilidade

- **List Comprehensions**: Geralmente mais legíveis e intuitivas para operações simples.
- **Map/Filter**: Pode ser menos legível, especialmente para quem não está familiarizado com a programação funcional.

### Desempenho

- **List Comprehensions**: Tende a ser eficiente e é muitas vezes mais rápida para operações simples. Em alguns casos, a diferença de desempenho pode ser insignificante.
- **Map/Filter**: Pode ser mais eficiente para operações complexas ou em grandes conjuntos de dados, pois são otimizadas para suas tarefas específicas.

### Flexibilidade

- **List Comprehensions**: Mais flexíveis, permitindo combinar mapeamento e filtragem em uma única expressão.
- **Map/Filter**: Cada função tem um propósito específico, o que pode exigir o uso de ambas para alcançar o mesmo resultado.