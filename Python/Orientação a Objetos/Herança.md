# Guia sobre Herança em Python

Herança é um conceito fundamental na programação orientada a objetos (POO) que permite criar novas classes a partir de classes existentes. Isso promove a reutilização de código e facilita a criação de hierarquias de classes. Em Python, a herança pode ser simples ou múltipla. 

## Herança Simples

Herança simples ocorre quando uma classe herda de uma única classe base. A classe derivada (ou filha) herda os atributos e métodos da classe base (ou pai).

### Exemplo de Herança Simples

```python
class Animal:
    def __init__(self, nome):
        self.nome = nome

    def falar(self):
        pass

class Cachorro(Animal):
    def falar(self):
        return f"{self.nome} diz Au Au"

class Gato(Animal):
    def falar(self):
        return f"{self.nome} diz Miau"

cachorro = Cachorro("Rex")
gato = Gato("Whiskers")

print(cachorro.falar())  # Saída: Rex diz Au Au
print(gato.falar())      # Saída: Whiskers diz Miau
```

## Herança Múltipla

Herança múltipla ocorre quando uma classe herda de mais de uma classe base. Isso permite que a classe derivada combine comportamentos de várias classes base.

### Exemplo de Herança Múltipla

```python
class Mamifero:
    def amamentar(self):
        return "Amamentando"

class Ave:
    def voar(self):
        return "Voando"

class Morcego(Mamifero, Ave):
    pass

morcego = Morcego()
print(morcego.amamentar())  # Saída: Amamentando
print(morcego.voar())       # Saída: Voando
```

### Ordem de Resolução de Método (MRO)

A ordem de resolução de método (MRO) define a ordem em que Python procura métodos em uma hierarquia de classes. Para visualizar a MRO de uma classe, você pode usar o método `mro()` ou o atributo `__mro__`.

```python
print(Morcego.mro())  # Saída: [<class '__main__.Morcego'>, <class '__main__.Mamifero'>, <class '__main__.Ave'>, <class 'object'>]
print(Morcego.__mro__)  # Saída: (<class '__main__.Morcego'>, <class '__main__.Mamifero'>, <class '__main__.Ave'>, <class 'object'>)
```

## Usando `super()`

A função `super()` é usada para chamar métodos da classe base a partir da classe derivada. Isso é particularmente útil para estender o comportamento de métodos na classe base sem sobrescrevê-los completamente.

### Exemplo com `super()`

```python
class Animal:
    def __init__(self, nome):
        self.nome = nome

    def falar(self):
        return "Som genérico de animal"

class Cachorro(Animal):
    def __init__(self, nome, raca):
        super().__init__(nome)
        self.raca = raca

    def falar(self):
        return super().falar() + " e Au Au"

cachorro = Cachorro("Rex", "Labrador")
print(cachorro.falar())  # Saída: Som genérico de animal e Au Au
```

## Classes Abstratas (ABC)

Classes abstratas são classes que não podem ser instanciadas e são usadas como classes base para outras classes. Elas podem conter métodos abstratos, que são métodos declarados mas que não têm implementação. Subclasses que herdam de uma classe abstrata devem implementar todos os métodos abstratos.

### Exemplo de Classe Abstrata

```python
from abc import ABC, abstractmethod

class Forma(ABC):
    @abstractmethod
    def area(self):
        pass

    @abstractmethod
    def perimetro(self):
        pass

class Retangulo(Forma):
    def __init__(self, largura, altura):
        self.largura = largura
        self.altura = altura

    def area(self):
        return self.largura * self.altura

    def perimetro(self):
        return 2 * (self.largura + self.altura)

class Circulo(Forma):
    def __init__(self, raio):
        self.raio = raio

    def area(self):
        import math
        return math.pi * self.raio ** 2

    def perimetro(self):
        import math
        return 2 * math.pi * self.raio

retangulo = Retangulo(3, 4)
circulo = Circulo(5)

print(f"Área do retângulo: {retangulo.area()}")       # Saída: Área do retângulo: 12
print(f"Perímetro do retângulo: {retangulo.perimetro()}") # Saída: Perímetro do retângulo: 14
print(f"Área do círculo: {circulo.area()}")           # Saída: Área do círculo: 78.53981633974483
print(f"Perímetro do círculo: {circulo.perimetro()}")     # Saída: Perímetro do círculo: 31.41592653589793
```

Neste exemplo, `Forma` é uma classe abstrata com métodos abstratos `area` e `perimetro`. As classes `Retangulo` e `Circulo` herdam de `Forma` e implementam esses métodos.
