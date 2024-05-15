# Encapsulamento em Python

Encapsulamento é um dos princípios fundamentais da programação orientada a objetos (POO). Ele se refere à restrição do acesso direto a alguns dos componentes de um objeto, o que pode ajudar a prevenir a modificação acidental ou intencional de dados. Em Python, o encapsulamento é implementado principalmente através de atributos e métodos privados e protegidos.

## Conceitos de Encapsulamento

### Atributos Públicos

Atributos públicos são acessíveis de qualquer lugar, dentro e fora da classe.

### Atributos Protegidos

Atributos protegidos são indicados por um sublinhado simples `_`. Eles podem ser acessados dentro da classe e nas subclasses, mas a convenção é que não sejam acessados fora dessas classes.

### Atributos Privados

Atributos privados são indicados por dois sublinhados `__`. Eles não podem ser acessados diretamente fora da classe que os define. Isso ajuda a esconder detalhes internos da classe.

## Exemplo de Atributos Públicos, Protegidos e Privados

### Definindo Atributos

```python
class MinhaClasse:
    def __init__(self, publico, protegido, privado):
        self.publico = publico            # Atributo público
        self._protegido = protegido       # Atributo protegido
        self.__privado = privado          # Atributo privado

    def metodo_publico(self):
        print("Método público")
        self.__metodo_privado()

    def _metodo_protegido(self):
        print("Método protegido")

    def __metodo_privado(self):
        print("Método privado")

# Criando uma instância da classe
obj = MinhaClasse("publico", "protegido", "privado")

# Acessando o atributo público
print(obj.publico)  # Saída: publico

# Acessando o atributo protegido (não recomendado)
print(obj._protegido)  # Saída: protegido

# Tentando acessar o atributo privado (causará erro)
# print(obj.__privado)  # AttributeError

# Acessando o método público
obj.metodo_publico()  # Saída: Método público

# Acessando o método protegido (não recomendado)
obj._metodo_protegido()  # Saída: Método protegido

# Tentando acessar o método privado (causará erro)
# obj.__metodo_privado()  # AttributeError
```

### Acessando Atributos Privados (Name Mangling)

Os atributos privados podem ser acessados indiretamente usando name mangling, que Python aplica a atributos privados para torná-los únicos para cada classe.

```python
# Acessando o atributo privado usando name mangling
print(obj._MinhaClasse__privado)  # Saída: privado

# Acessando o método privado usando name mangling
obj._MinhaClasse__metodo_privado()  # Saída: Método privado
```

## Encapsulamento com Propriedades

Em Python, você pode usar propriedades para controlar o acesso a atributos de uma classe. Isso permite a encapsulação e a definição de getter, setter e deleter methods.

O decorador @property em Python é uma maneira de usar métodos de uma classe como se fossem atributos. Ele permite definir métodos que podem ser acessados como atributos, facilitando o encapsulamento e a implementação de getters, setters e deleters.

### Exemplo de Propriedades

```python
class MinhaClasse:
    def __init__(self, valor):
        self.__valor = valor

    @property
    def valor(self):
        return self.__valor

    @valor.setter
    def valor(self, novo_valor):
        if novo_valor > 0:
            self.__valor = novo_valor
        else:
            raise ValueError("O valor deve ser positivo.")

    @valor.deleter
    def valor(self):
        del self.__valor

# Criando uma instância da classe
obj = MinhaClasse(10)

# Usando o getter
print(obj.valor)  # Saída: 10

# Usando o setter
obj.valor = 20
print(obj.valor)  # Saída: 20

# Tentando definir um valor inválido
# obj.valor = -10  # ValueError: O valor deve ser positivo.

# Usando o deleter
del obj.valor
# print(obj.valor)  # AttributeError: 'MinhaClasse' object has no attribute '_MinhaClasse__valor'
```

## Encapsulamento e Herança

### Atributos e Métodos Protegidos

Atributos e métodos protegidos podem ser acessados em subclasses, mas a convenção é que eles não sejam usados diretamente fora da classe ou suas subclasses.

```python
class Base:
    def __init__(self):
        self._protegido = "protegido"

class Subclasse(Base):
    def mostrar(self):
        print(self._protegido)

obj = Subclasse()
obj.mostrar()  # Saída: protegido
```

### Atributos e Métodos Privados

Atributos e métodos privados não podem ser acessados diretamente nas subclasses, mas podem ser acessados indiretamente usando métodos públicos ou protegidos.

```python
class Base:
    def __init__(self):
        self.__privado = "privado"

    def get_privado(self):
        return self.__privado

class Subclasse(Base):
    def mostrar_privado(self):
        return self.get_privado()

obj = Subclasse()
print(obj.mostrar_privado())  # Saída: privado
```