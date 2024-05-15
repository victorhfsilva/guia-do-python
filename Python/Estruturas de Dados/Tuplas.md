# Tuplas em Python

Tuplas são uma estrutura de dados fundamental em Python, usadas para armazenar coleções ordenadas de itens. Ao contrário das listas, as tuplas são imutáveis, o que significa que seus elementos não podem ser alterados após a criação. 

## Criando Tuplas

Você pode criar uma tupla usando parênteses `()` ou a função `tuple()`.

### Sintaxe

```python
minha_tupla = (elemento1, elemento2, elemento3)
ou
minha_tupla = tuple([elemento1, elemento2, elemento3])
```

### Exemplos

```python
numeros = (1, 2, 3, 4, 5)
frutas = ('maçã', 'banana', 'laranja')
mista = (1, 'maçã', 3.5, True)
```

### Tuplas Vazias e de um Elemento

```python
tupla_vazia = ()
tupla_um_elemento = (1,)  # Note a vírgula
```

## Acessando Elementos

Você pode acessar elementos de uma tupla usando índices. O índice em Python começa em 0.

### Sintaxe

```python
elemento = minha_tupla[indice]
```

### Exemplos

```python
frutas = ('maçã', 'banana', 'laranja')
print(frutas[0])  # Saída: maçã
print(frutas[1])  # Saída: banana
print(frutas[-1]) # Saída: laranja (índice negativo)
```

## Desempacotamento de Tuplas

Você pode desempacotar tuplas em variáveis individuais.

### Exemplo

```python
tupla = (1, 2, 3)
a, b, c = tupla
print(a)  # Saída: 1
print(b)  # Saída: 2
print(c)  # Saída: 3
```

### Desempacotamento com * (Asterisco)

Você pode usar o operador * para capturar múltiplos valores.

```python
tupla = (1, 2, 3, 4, 5)
a, *b, c = tupla
print(a)  # Saída: 1
print(b)  # Saída: [2, 3, 4]
print(c)  # Saída: 5
```

## Imutabilidade das Tuplas

Uma vez criada, você não pode alterar, adicionar ou remover elementos de uma tupla. Qualquer tentativa de fazê-lo resultará em um erro.

### Exemplo

```python
tupla = (1, 2, 3)
# tupla[1] = 4  # Isto resultará em um erro: TypeError: 'tuple' object does not support item assignment
```

## Operações com Tuplas

### Comprimento da Tupla

Use `len` para obter o número de elementos em uma tupla.

```python
numeros = (1, 2, 3, 4, 5)
print(len(numeros))  # Saída: 5
```

### Concatenando Tuplas

Use o operador `+` para concatenar duas tuplas.

```python
tupla1 = (1, 2, 3)
tupla2 = (4, 5, 6)
tupla3 = tupla1 + tupla2
print(tupla3)  # Saída: (1, 2, 3, 4, 5, 6)
```

### Repetindo Tuplas

Use o operador `*` para repetir uma tupla.

```python
tupla = (1, 2, 3)
tupla_repetida = tupla * 3
print(tupla_repetida)  # Saída: (1, 2, 3, 1, 2, 3, 1, 2, 3)
```

### Verificando a Presença de um Elemento

Use o operador `in` para verificar se um elemento está em uma tupla.

```python
frutas = ('maçã', 'banana', 'laranja')
print('maçã' in frutas)  # Saída: True
print('uva' in frutas)   # Saída: False
```

## Fatiamento de Tuplas

Você pode obter uma subseção (ou "fatia") de uma tupla usando a notação de fatiamento.

### Sintaxe

```python
sub_tupla = tupla[inicio:fim:passo]
```

### Exemplos

```python
numeros = (0, 1, 2, 3, 4, 5, 6, 7, 8, 9)
print(numeros[2:5])    # Saída: (2, 3, 4)
print(numeros[:5])     # Saída: (0, 1, 2, 3, 4)
print(numeros[5:])     # Saída: (5, 6, 7, 8, 9)
print(numeros[::2])    # Saída: (0, 2, 4, 6, 8)
print(numeros[::-1])   # Saída: (9, 8, 7, 6, 5, 4, 3, 2, 1, 0)
```

## Métodos Úteis de Tuplas

### `index`

Retorna o índice da primeira ocorrência de um elemento.

```python
frutas = ('maçã', 'banana', 'laranja')
print(frutas.index('banana'))  # Saída: 1
```

### `count`

Retorna o número de ocorrências de um elemento.

```python
numeros = (1, 2, 2, 3, 2, 4, 2)
print(numeros.count(2))  # Saída: 4
```

## Comparação de Tuplas

Tuplas podem ser comparadas. Python compara tuplas elemento por elemento.

### Exemplo

```python
tupla1 = (1, 2, 3)
tupla2 = (1, 2, 4)
print(tupla1 < tupla2)  # Saída: True
```

## Usos Comuns de Tuplas

### Tuplas como Chaves em Dicionários

Tuplas podem ser usadas como chaves em dicionários porque são imutáveis.

```python
dicionario = {(1, 2): 'a', (3, 4): 'b'}
print(dicionario[(1, 2)])  # Saída: 'a'
```

### Funções que Retornam Vários Valores

Funções podem retornar múltiplos valores usando tuplas.

```python
def operacoes(a, b):
    soma = a + b
    diferenca = a - b
    produto = a * b
    quociente = a / b
    return soma, diferenca, produto, quociente

resultado = operacoes(10, 2)
print(resultado)  # Saída: (12, 8, 20, 5.0)
```
