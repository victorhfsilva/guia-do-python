# Classes e Objetos em Python

A programação orientada a objetos (POO) é um paradigma de programação que utiliza "objetos" e suas interações para projetar aplicações e programas. Python é uma linguagem orientada a objetos e oferece suporte completo para a criação de classes e objetos. 

## Definindo Classes e Objetos

### Definindo uma Classe

Você define uma classe em Python usando a palavra-chave `class`:

```python
class Pessoa:
    def __init__(self, nome, idade):
        self.nome = nome  # Atributo da instância
        self.idade = idade  # Atributo da instância

    def apresentar(self):
        print(f"Olá, meu nome é {self.nome} e eu tenho {self.idade} anos.")
```

### Criando um Objeto

Para criar um objeto, você chama a classe como se fosse uma função:

```python
joao = Pessoa('João', 30)
joao.apresentar()  # Saída: Olá, meu nome é João e eu tenho 30 anos.
```

## Atributos e Métodos

### Atributos de Instância

Atributos de instância são dados associados a uma instância específica de uma classe. Eles são definidos no método `__init__`, que é o inicializador (construtor) da classe.

### Métodos de Instância

Métodos de instância são funções definidas dentro de uma classe que operam nos atributos da instância. O primeiro parâmetro de um método de instância é sempre `self`, que referencia a própria instância.

### Exemplo

```python
class Carro:
    def __init__(self, marca, modelo):
        self.marca = marca
        self.modelo = modelo

    def descrever(self):
        print(f"Este carro é um {self.marca} {self.modelo}.")

meu_carro = Carro('Toyota', 'Corolla')
meu_carro.descrever()  # Saída: Este carro é um Toyota Corolla.
```

## Atributos e Métodos de Classe

### Atributos de Classe

Atributos de classe são atributos compartilhados por todas as instâncias de uma classe. Eles são definidos diretamente na classe e não no método `__init__`.

### Métodos de Classe

Métodos de classe são métodos que operam na classe em si, em vez de em uma instância. Eles são definidos usando o decorador `@classmethod`.

### Exemplo

```python
class Animal:
    reino = 'Animalia'  # Atributo de classe

    def __init__(self, nome):
        self.nome = nome  # Atributo de instância

    @classmethod
    def obter_reino(cls):
        return cls.reino

gato = Animal('Gato')
print(gato.obter_reino())  # Saída: Animalia
```

## Métodos Estáticos

Métodos estáticos são métodos que não operam nem na instância nem na classe. Eles são definidos usando o decorador `@staticmethod`.

### Exemplo

```python
class Calculadora:
    @staticmethod
    def somar(a, b):
        return a + b

print(Calculadora.somar(5, 3))  # Saída: 8
```

## Herança

Herança é um mecanismo que permite criar uma nova classe com base em uma classe existente. A classe nova herda os atributos e métodos da classe existente.

### Exemplo

```python
class Veiculo:
    def __init__(self, marca, modelo):
        self.marca = marca
        self.modelo = modelo

    def descrever(self):
        print(f"Este é um {self.marca} {self.modelo}.")

class Carro(Veiculo):
    def __init__(self, marca, modelo, portas):
        super().__init__(marca, modelo)
        self.portas = portas

    def descrever(self):
        super().descrever()
        print(f"Ele tem {self.portas} portas.")

meu_carro = Carro('Toyota', 'Corolla', 4)
meu_carro.descrever()
# Saída:
# Este é um Toyota Corolla.
# Ele tem 4 portas.
```

## Encapsulamento

Encapsulamento é o princípio de restringir o acesso a certos componentes de um objeto. Em Python, você pode definir atributos e métodos como privados usando um sublinhado duplo (`__`).

### Exemplo

```python
class ContaBancaria:
    def __init__(self, saldo):
        self.__saldo = saldo  # Atributo privado

    def depositar(self, quantia):
        self.__saldo += quantia

    def sacar(self, quantia):
        if quantia <= self.__saldo:
            self.__saldo -= quantia
        else:
            print("Saldo insuficiente.")

    def obter_saldo(self):
        return self.__saldo

conta = ContaBancaria(1000)
conta.depositar(500)
conta.sacar(300)
print(conta.obter_saldo())  # Saída: 1200
```

## Polimorfismo

Polimorfismo permite que diferentes classes tenham métodos com o mesmo nome, mas comportamentos diferentes. Isso é frequentemente usado junto com a herança.

### Exemplo

```python
class Forma:
    def area(self):
        pass

class Retangulo(Forma):
    def __init__(self, largura, altura):
        self.largura = largura
        self.altura = altura

    def area(self):
        return self.largura * self.altura

class Circulo(Forma):
    def __init__(self, raio):
        self.raio = raio

    def area(self):
        import math
        return math.pi * self.raio ** 2

formas = [Retangulo(3, 4), Circulo(5)]
for forma in formas:
    print(forma.area())
# Saída:
# 12
# 78.53981633974483
```
