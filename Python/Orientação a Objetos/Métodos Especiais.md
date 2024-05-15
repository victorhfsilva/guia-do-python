# Métodos Especiais em Python

Métodos especiais, também conhecidos como "métodos mágicos" ou "dunder methods" (de "double underscore"), são métodos que têm um significado especial em Python. Eles são precedidos e seguidos por dois sublinhados (`__`). Esses métodos permitem que você defina como os objetos de suas classes devem se comportar em várias situações, como inicialização, representação em string, comparação, entre outras. 

## Métodos Especiais Comuns

### `__init__`

O método `__init__` é o inicializador (construtor) de uma classe. Ele é chamado quando uma nova instância da classe é criada.

#### Exemplo

```python
class Pessoa:
    def __init__(self, nome, idade):
        self.nome = nome
        self.idade = idade

p = Pessoa('João', 30)
print(p.nome)  # Saída: João
print(p.idade) # Saída: 30
```

### `__str__`

O método `__str__` define a representação em string "amigável" de um objeto, usada principalmente para exibição ao usuário final. Ele é chamado pela função `print()` e pelas funções `str()` e `format()`.

#### Exemplo

```python
class Pessoa:
    def __init__(self, nome, idade):
        self.nome = nome
        self.idade = idade

    def __str__(self):
        return f'{self.nome}, {self.idade} anos'

p = Pessoa('João', 30)
print(p)  # Saída: João, 30 anos
```

### `__repr__`

O método `__repr__` define a representação "oficial" de um objeto, usada principalmente para depuração. Ele deve fornecer uma string que poderia, idealmente, ser usada para recriar o objeto. Ele é chamado pela função `repr()`.

#### Exemplo

```python
class Pessoa:
    def __init__(self, nome, idade):
        self.nome = nome
        self.idade = idade

    def __repr__(self):
        return f'Pessoa({self.nome!r}, {self.idade!r})'

p = Pessoa('João', 30)
print(repr(p))  # Saída: Pessoa('João', 30)
```

### `__eq__`, `__ne__`, `__lt__`, `__le__`, `__gt__`, `__ge__`

Esses métodos definem operadores de comparação: igual (`==`), diferente (`!=`), menor que (`<`), menor ou igual a (`<=`), maior que (`>`), maior ou igual a (`>=`).

#### Exemplo

```python
class Pessoa:
    def __init__(self, nome, idade):
        self.nome = nome
        self.idade = idade

    def __eq__(self, outro):
        return self.nome == outro.nome and self.idade == outro.idade

p1 = Pessoa('João', 30)
p2 = Pessoa('João', 30)
print(p1 == p2)  # Saída: True
```

### `__len__`

O método `__len__` deve retornar o comprimento (número de itens) de um objeto. Ele é chamado pela função `len()`.

#### Exemplo

```python
class MinhaLista:
    def __init__(self, itens):
        self.itens = itens

    def __len__(self):
        return len(self.itens)

ml = MinhaLista([1, 2, 3, 4])
print(len(ml))  # Saída: 4
```

### `__getitem__`, `__setitem__`, `__delitem__`

Esses métodos permitem definir o comportamento de acesso, modificação e deleção de itens usando a notação de índice (`obj[key]`).

#### Exemplo

```python
class MinhaLista:
    def __init__(self, itens):
        self.itens = itens

    def __getitem__(self, index):
        return self.itens[index]

    def __setitem__(self, index, value):
        self.itens[index] = value

    def __delitem__(self, index):
        del self.itens[index]

ml = MinhaLista([1, 2, 3, 4])
print(ml[1])  # Saída: 2
ml[1] = 20
print(ml[1])  # Saída: 20
del ml[1]
print(ml.itens)  # Saída: [1, 20, 4]
```

### `__iter__` e `__next__`

Esses métodos definem o comportamento de um objeto iterável. `__iter__` deve retornar o objeto iterador e `__next__` deve retornar o próximo item da sequência.

#### Exemplo

```python
class Contador:
    def __init__(self, limite):
        self.limite = limite
        self.atual = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.atual < self.limite:
            self.atual += 1
            return self.atual
        else:
            raise StopIteration

cont = Contador(5)
for numero in cont:
    print(numero)  # Saída: 1, 2, 3, 4, 5
```

### `__call__`

O método `__call__` permite que uma instância de uma classe seja chamada como uma função.

#### Exemplo

```python
class Saudacao:
    def __init__(self, mensagem):
        self.mensagem = mensagem

    def __call__(self, nome):
        return f'{self.mensagem}, {nome}!'

saudar = Saudacao('Olá')
print(saudar('João'))  # Saída: Olá, João!
```
