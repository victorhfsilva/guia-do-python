# Pilhas e Filas em Python

Pilhas e filas são estruturas de dados fundamentais que permitem o armazenamento e a manipulação de coleções de elementos de maneira ordenada. Em Python, essas estruturas podem ser implementadas de várias maneiras, incluindo listas e a biblioteca `collections`.

## Pilhas (Stacks)

Uma pilha é uma estrutura de dados que segue o princípio LIFO (Last In, First Out), ou seja, o último elemento adicionado é o primeiro a ser removido. A operação principal de uma pilha é `push` (adicionar um elemento) e `pop` (remover o elemento mais recente).

### Implementando Pilhas com Listas

Python não possui uma estrutura de pilha embutida, mas você pode usar listas para implementar uma pilha.

#### Exemplo

```python
pilha = []

# Adicionando elementos à pilha (push)
pilha.append(1)
pilha.append(2)
pilha.append(3)
print(pilha)  # Saída: [1, 2, 3]

# Removendo elementos da pilha (pop)
elemento = pilha.pop()
print(elemento)  # Saída: 3
print(pilha)    # Saída: [1, 2]
```

### Métodos de Pilhas com Listas

- `append(x)`: Adiciona o elemento `x` ao final da lista (push).
- `pop()`: Remove e retorna o último elemento da lista (pop).

### Verificando se a Pilha está Vazia

```python
if not pilha:
    print("A pilha está vazia")
```

## Filas (Queues)

Uma fila é uma estrutura de dados que segue o princípio FIFO (First In, First Out), ou seja, o primeiro elemento adicionado é o primeiro a ser removido. As operações principais de uma fila são `enqueue` (adicionar um elemento) e `dequeue` (remover o primeiro elemento).

### Implementando Filas com `collections.deque`

A biblioteca `collections` de Python fornece a classe `deque` que pode ser usada para implementar filas de forma eficiente.

#### Exemplo

```python
from collections import deque

fila = deque()

# Adicionando elementos à fila (enqueue)
fila.append(1)
fila.append(2)
fila.append(3)
print(fila)  # Saída: deque([1, 2, 3])

# Removendo elementos da fila (dequeue)
elemento = fila.popleft()
print(elemento)  # Saída: 1
print(fila)     # Saída: deque([2, 3])
```

### Métodos de Filas com `deque`

- `append(x)`: Adiciona o elemento `x` ao final da deque (enqueue).
- `popleft()`: Remove e retorna o primeiro elemento da deque (dequeue).

### Verificando se a Fila está Vazia

```python
if not fila:
    print("A fila está vazia")
```

## Filas de Prioridade

Uma fila de prioridade é uma estrutura de dados onde cada elemento possui uma prioridade. Elementos com maior prioridade são removidos antes dos elementos com menor prioridade. Python fornece a classe `PriorityQueue` no módulo `queue` para implementar filas de prioridade.

Em uma PriorityQueue, se dois itens tiverem a mesma prioridade, a ordem de desempate será baseada na ordem em que os itens foram inseridos na fila. Isso significa que, para itens com a mesma prioridade, o primeiro item inserido será o primeiro a ser removido, seguindo o princípio FIFO (First In, First Out) para itens de mesma prioridade.

### Exemplo de Fila de Prioridade

```python
from queue import PriorityQueue

fila_prioridade = PriorityQueue()

# Adicionando elementos à fila de prioridade
fila_prioridade.put((2, 'prioridade baixa'))
fila_prioridade.put((1, 'prioridade alta'))
fila_prioridade.put((3, 'prioridade muito baixa'))

# Removendo elementos da fila de prioridade
while not fila_prioridade.empty():
    item = fila_prioridade.get()
    print(item)
```

### Métodos de `PriorityQueue`

- `put(item)`: Adiciona um item à fila de prioridade.
- `get()`: Remove e retorna o item de maior prioridade na fila.
- `empty()`: Verifica se a fila está vazia.
