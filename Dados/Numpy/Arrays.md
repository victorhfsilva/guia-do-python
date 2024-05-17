# Arrays no NumPy

NumPy (Numerical Python) é uma biblioteca essencial para computação científica em Python. Ela fornece suporte para arrays multidimensionais e matrizes, além de uma vasta coleção de funções matemáticas para operar nesses arrays. 

## Instalando NumPy

Para instalar o NumPy, você pode usar o `pip`:

```bash
pip install numpy
```

## Importando NumPy

Para começar a usar NumPy, você precisa importá-lo. A convenção comum é importá-lo como `np`:

```python
import numpy as np
```

## Criando Arrays

### Usando `np.array`

Você pode criar um array a partir de uma lista ou tupla usando `np.array`.

```python
import numpy as np

# Criar um array a partir de uma lista
lista = [1, 2, 3, 4, 5]
array = np.array(lista)
print(array)  # Saída: [1 2 3 4 5]
```

### Arrays de Zeros e Uns

Você pode criar arrays de zeros e uns usando `np.zeros` e `np.ones`.

```python
# Criar um array de zeros
zeros = np.zeros((3, 4))
print(zeros)
# Saída:
# [[0. 0. 0. 0.]
#  [0. 0. 0. 0.]
#  [0. 0. 0. 0.]]

# Criar um array de uns
ones = np.ones((2, 3))
print(ones)
# Saída:
# [[1. 1. 1.]
#  [1. 1. 1.]]
```

### Arrays de Valores Aleatórios

Você pode criar arrays de valores aleatórios usando `np.random`.

```python
# Criar um array de valores aleatórios
random_array = np.random.random((3, 3))
print(random_array)
```

### Arrays com Valores Espaciais

Você pode criar arrays com valores espaçados uniformemente usando `np.linspace` e `np.arange`.

```python
# Criar um array de valores espaçados uniformemente
linspace_array = np.linspace(0, 10, 5)
print(linspace_array)  # Saída: [ 0.   2.5  5.   7.5 10. ]

# Criar um array de valores espaçados por intervalo
arange_array = np.arange(0, 10, 2)
print(arange_array)  # Saída: [0 2 4 6 8]
```

## Atributos dos Arrays

Os arrays do NumPy possuem vários atributos úteis.

```python
import numpy as np

array = np.array([[1, 2, 3], [4, 5, 6]])

print("Shape:", array.shape)  # Saída: Shape: (2, 3)
print("Size:", array.size)    # Saída: Size: 6
print("Ndim:", array.ndim)    # Saída: Ndim: 2
print("Dtype:", array.dtype)  # Saída: Dtype: int64 (ou int32 dependendo do sistema)
```

## Indexação e Fatiamento

### Indexação

Você pode acessar elementos individuais de um array usando a indexação.

```python
import numpy as np

array = np.array([1, 2, 3, 4, 5])
print(array[0])  # Saída: 1
print(array[-1]) # Saída: 5
```

### Fatiamento

Você pode acessar uma subseção de um array usando a fatiamento.

```python
import numpy as np

array = np.array([1, 2, 3, 4, 5])
print(array[1:4])  # Saída: [2 3 4]
print(array[:3])   # Saída: [1 2 3]
print(array[::2])  # Saída: [1 3 5]
```

### Indexação em Arrays Multidimensionais

```python
import numpy as np

array = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
print(array[0, 1])  # Saída: 2
print(array[1:, 1:])  # Saída: [[5 6]
                      #         [8 9]]
```

## Operações em Arrays

### Operações Element-wise

As operações aritméticas são aplicadas elemento por elemento.

```python
import numpy as np

a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

print(a + b)  # Saída: [5 7 9]
print(a - b)  # Saída: [-3 -3 -3]
print(a * b)  # Saída: [ 4 10 18]
print(a / b)  # Saída: [0.25 0.4  0.5 ]
```

### Funções Universais

NumPy fornece várias funções universais (`ufuncs`) que operam em arrays.

```python
import numpy as np

array = np.array([1, 2, 3, 4, 5])
print(np.sqrt(array))  # Saída: [1.         1.41421356 1.73205081 2.         2.23606798]
print(np.exp(array))   # Saída: [  2.71828183   7.3890561   20.08553692  54.59815003 148.4131591 ]
print(np.mean(array))  # Saída: 3.0
print(np.std(array))   # Saída: 1.4142135623730951
```

### Produto de Matrizes

NumPy fornece várias maneiras de realizar a multiplicação de matrizes.

```python
import numpy as np

A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

print(np.dot(A, B))  # Produto escalar
# Saída:
# [[19 22]
#  [43 50]]

print(A @ B)  # Usando o operador @
# Saída:
# [[19 22]
#  [43 50]]
```

## Manipulação de Arrays

### Redimensionando Arrays

Você pode alterar a forma de um array usando `reshape`.

```python
import numpy as np

array = np.array([1, 2, 3, 4, 5, 6])
reshaped_array = array.reshape((2, 3))
print(reshaped_array)
# Saída:
# [[1 2 3]
#  [4 5 6]]
```

### Concatenando Arrays

Você pode concatenar arrays ao longo de um eixo usando `np.concatenate`.

```python
import numpy as np

a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6]])

concatenated = np.concatenate((a, b), axis=0)
print(concatenated)
# Saída:
# [[1 2]
#  [3 4]
#  [5 6]]
```

### Dividindo Arrays

Você pode dividir arrays em sub-arrays usando `np.split`.

```python
import numpy as np

array = np.array([1, 2, 3, 4, 5, 6])
split_array = np.split(array, 3)
print(split_array)
# Saída:
# [array([1, 2]), array([3, 4]), array([5, 6])]
```
