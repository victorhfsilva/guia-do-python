# Collections em Python

A biblioteca `collections` em Python fornece tipos de dados especializados, que são extensões dos tipos de dados embutidos no Python. Esses tipos de dados oferecem funcionalidades adicionais e são altamente eficientes para certas operações.

## 1. Named Tuples (`namedtuple`)

`namedtuple` é uma fábrica de classes para criar subclasses de tuplas com nome. Ele permite que você acesse os elementos da tupla usando nomes em vez de índices, o que torna o código mais legível e autodescritivo.

### Exemplo

```python
from collections import namedtuple

# Definindo uma namedtuple
Pessoa = namedtuple('Pessoa', 'nome idade cidade')

# Criando uma instância de Pessoa
joao = Pessoa(nome='João', idade=30, cidade='São Paulo')

# Acessando os elementos
print(joao.nome)   # Saída: João
print(joao.idade)  # Saída: 30
print(joao.cidade) # Saída: São Paulo
```

## 2. Deques (`deque`)

`deque` (double-ended queue) é uma fila que permite a inserção e remoção de elementos em ambas as extremidades com complexidade O(1). É ideal para implementações de filas e pilhas.

### Exemplo

```python
from collections import deque

# Criando um deque
fila = deque(['A', 'B', 'C'])

# Adicionando elementos
fila.append('D')        # Adiciona ao final
fila.appendleft('Z')    # Adiciona ao início

print(fila)  # Saída: deque(['Z', 'A', 'B', 'C', 'D'])

# Removendo elementos
fila.pop()            # Remove do final
fila.popleft()        # Remove do início

print(fila)  # Saída: deque(['A', 'B', 'C'])
```

## 3. Contadores (`Counter`)

`Counter` é uma subclasse de dicionário que é usada para contar elementos hasháveis. Ele facilita a contagem de elementos em uma coleção.

### Exemplo

```python
from collections import Counter

# Criando um contador
contador = Counter(['a', 'b', 'c', 'a', 'b', 'a'])

print(contador)  # Saída: Counter({'a': 3, 'b': 2, 'c': 1})

# Operações comuns
print(contador.most_common(2))  # Saída: [('a', 3), ('b', 2)]
```

## 4. Dicionários Ordenados (`OrderedDict`)

`OrderedDict` é uma subclasse de dicionário que preserva a ordem de inserção dos elementos. Ele é útil quando a ordem dos itens é importante.

### Exemplo

```python
from collections import OrderedDict

# Criando um OrderedDict
ord_dict = OrderedDict()

ord_dict['um'] = 1
ord_dict['dois'] = 2
ord_dict['três'] = 3

print(ord_dict)  # Saída: OrderedDict([('um', 1), ('dois', 2), ('três', 3)])
```

## 5. Dicionários com Valor Padrão (`defaultdict`)

`defaultdict` é uma subclasse de dicionário que retorna um valor padrão se a chave não existir. Isso evita exceções ao acessar chaves inexistentes.

### Exemplo

```python
from collections import defaultdict

# Criando um defaultdict
def_dict = defaultdict(int)

def_dict['a'] += 1
def_dict['b'] += 2

print(def_dict)  # Saída: defaultdict(<class 'int'>, {'a': 1, 'b': 2})
```

## 6. Mapas em Cadeia (`ChainMap`)

`ChainMap` agrupa múltiplos dicionários em uma única unidade. Ele é útil para gerenciar múltiplos contextos (como variáveis locais, globais e builtins).

### Exemplo

```python
from collections import ChainMap

# Criando dicionários
dict1 = {'um': 1, 'dois': 2}
dict2 = {'três': 3, 'quatro': 4}

# Criando um ChainMap
chain_map = ChainMap(dict1, dict2)

print(chain_map)  # Saída: ChainMap({'um': 1, 'dois': 2}, {'três': 3, 'quatro': 4})
print(chain_map['um'])  # Saída: 1
print(chain_map['três']) # Saída: 3
```
