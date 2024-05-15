# Listas em Python

Listas são uma estrutura de dados fundamental em Python, usadas para armazenar coleções ordenadas de itens. Elas são mutáveis, o que significa que seus elementos podem ser alterados após a criação. 

## Criando Listas

Você pode criar uma lista usando colchetes `[]` ou a função `list()`.

### Sintaxe

```python
minha_lista = [elemento1, elemento2, elemento3]
ou
minha_lista = list([elemento1, elemento2, elemento3])
```

### Exemplos

```python
numeros = [1, 2, 3, 4, 5]
frutas = ['maçã', 'banana', 'laranja']
mista = [1, 'maçã', 3.5, True]
```

## Acessando Elementos

Você pode acessar elementos de uma lista usando índices. O índice em Python começa em 0.

### Sintaxe

```python
elemento = minha_lista[indice]
```

### Exemplos

```python
frutas = ['maçã', 'banana', 'laranja']
print(frutas[0])  # Saída: maçã
print(frutas[1])  # Saída: banana
print(frutas[-1]) # Saída: laranja (índice negativo)
```

## Modificando Listas

Listas são mutáveis, o que significa que você pode alterar seus elementos, adicionar novos elementos ou remover elementos existentes.

### Alterando Elementos

```python
frutas = ['maçã', 'banana', 'laranja']
frutas[1] = 'uva'
print(frutas)  # Saída: ['maçã', 'uva', 'laranja']
```

### Adicionando Elementos

#### Usando `append`

Adiciona um elemento ao final da lista.

```python
frutas = ['maçã', 'banana']
frutas.append('laranja')
print(frutas)  # Saída: ['maçã', 'banana', 'laranja']
```

#### Usando `insert`

Adiciona um elemento em uma posição específica.

```python
frutas = ['maçã', 'banana']
frutas.insert(1, 'laranja')
print(frutas)  # Saída: ['maçã', 'laranja', 'banana']
```

### Removendo Elementos

#### Usando `remove`

Remove a primeira ocorrência de um elemento.

```python
frutas = ['maçã', 'banana', 'laranja']
frutas.remove('banana')
print(frutas)  # Saída: ['maçã', 'laranja']
```

#### Usando `pop`

Remove e retorna o elemento na posição especificada. Se nenhum índice for especificado, remove e retorna o último elemento.

```python
frutas = ['maçã', 'banana', 'laranja']
fruta = frutas.pop(1)
print(fruta)   # Saída: banana
print(frutas)  # Saída: ['maçã', 'laranja']
```

### Usando `del`

Remove o elemento em uma posição específica ou a lista inteira.

```python
frutas = ['maçã', 'banana', 'laranja']
del frutas[1]
print(frutas)  # Saída: ['maçã', 'laranja']

del frutas
```

### Usando `clear`

Remove todos os elementos da lista.

```python
frutas = ['maçã', 'banana', 'laranja']
frutas.clear()
print(frutas)  # Saída: []
```

## Operações com Listas

### Comprimento da Lista

Use `len` para obter o número de elementos em uma lista.

```python
numeros = [1, 2, 3, 4, 5]
print(len(numeros))  # Saída: 5
```

### Concatenando Listas

Use o operador `+` para concatenar duas listas.

```python
lista1 = [1, 2, 3]
lista2 = [4, 5, 6]
lista3 = lista1 + lista2
print(lista3)  # Saída: [1, 2, 3, 4, 5, 6]
```

### Repetindo Listas

Use o operador `*` para repetir uma lista.

```python
lista = [1, 2, 3]
lista_repetida = lista * 3
print(lista_repetida)  # Saída: [1, 2, 3, 1, 2, 3, 1, 2, 3]
```

### Verificando a Presença de um Elemento

Use o operador `in` para verificar se um elemento está em uma lista.

```python
frutas = ['maçã', 'banana', 'laranja']
print('maçã' in frutas)  # Saída: True
print('uva' in frutas)   # Saída: False
```

## Fatiamento de Listas

Você pode obter uma subseção (ou "fatia") de uma lista usando a notação de fatiamento.

### Sintaxe

```python
sub_lista = lista[inicio:fim:passo]
```

### Exemplos

```python
numeros = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
print(numeros[2:5])    # Saída: [2, 3, 4]
print(numeros[:5])     # Saída: [0, 1, 2, 3, 4]
print(numeros[5:])     # Saída: [5, 6, 7, 8, 9]
print(numeros[::2])    # Saída: [0, 2, 4, 6, 8]
print(numeros[::-1])   # Saída: [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

## Métodos Úteis de Listas

### `index`

Retorna o índice da primeira ocorrência de um elemento.

```python
frutas = ['maçã', 'banana', 'laranja']
print(frutas.index('banana'))  # Saída: 1
```

### `count`

Retorna o número de ocorrências de um elemento.

```python
numeros = [1, 2, 2, 3, 2, 4, 2]
print(numeros.count(2))  # Saída: 4
```

### `sort`

Ordena a lista em ordem crescente.

```python
numeros = [3, 1, 4, 1, 5, 9, 2, 6, 5]
numeros.sort()
print(numeros)  # Saída: [1, 1, 2, 3, 4, 5, 5, 6, 9]
```

### `reverse`

Inverte a ordem dos elementos na lista.

```python
numeros = [1, 2, 3, 4, 5]
numeros.reverse()
print(numeros)  # Saída: [5, 4, 3, 2, 1]
```

### `copy`

Retorna uma cópia superficial da lista.

```python
numeros = [1, 2, 3]
copiados = numeros.copy()
print(copiados)  # Saída: [1, 2, 3]
```

## List Comprehensions

List Comprehensions é uma maneira concisa de criar listas.

### Sintaxe

```python
nova_lista = [expressão for item in iterável]
```

Ou,

```python
[expressão for item in sequência if condição]
```

### Exemplos

```python
numeros = [1, 2, 3, 4, 5]
quadrados = [x**2 for x in numeros]
print(quadrados)  # Saída: [1, 4, 9, 16, 25]
```

```python
quadrados = [x**2 for x in range(10) if x % 2 == 0]
print(quadrados)  # Saída: [0, 4, 16, 36, 64]
```