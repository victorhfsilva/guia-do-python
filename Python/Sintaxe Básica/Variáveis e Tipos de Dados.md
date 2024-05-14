# Variáveis e Tipos de Dados em Python

## Variáveis

Uma variável é um nome que aponta para um valor armazenado na memória. Em Python, você não precisa declarar o tipo da variável explicitamente; o tipo é inferido automaticamente pelo interpretador com base no valor atribuído.

### Como Declarar Variáveis

A sintaxe para declarar uma variável em Python é simples:

```python
nome_da_variavel = valor
```

### Exemplos de Declaração de Variáveis

```python
nome = "João"
idade = 25
altura = 1.75
tem_animal_de_estimacao = True
```

### Regras para Nomeação de Variáveis

1. **Deve começar com uma letra (a-z, A-Z) ou um sublinhado (_).**
2. **Pode conter letras, números (0-9) e sublinhados.**
3. **Não pode começar com um número.**
4. **Não pode conter espaços; use sublinhados (_) para separar palavras.**
5. **Não pode ser uma palavra reservada do Python (e.g., `if`, `for`, `while`).**

## Tipos de Dados

Python possui vários tipos de dados incorporados. Vamos explorar os mais comuns:

### 1. Inteiros (int)

Números inteiros, positivos ou negativos, sem ponto decimal.

```python
numero_inteiro = 10
```

### 2. Ponto Flutuante (float)

Números reais, que contêm um ponto decimal.

```python
numero_ponto_flutuante = 10.5
```

### 3. Cadeia de Caracteres (str)

Sequência de caracteres, usada para representar texto.

```python
texto = "Olá, Mundo!"
```

### 4. Booleanos (bool)

Representam valores de Verdadeiro (True) ou Falso (False).

```python
verdadeiro = True
falso = False
```

### 5. Listas (list)

Coleção ordenada de itens que podem ser de tipos diferentes.

```python
lista = [1, 2, 3, "quatro", 5.0]
```

### 6. Tuplas (tuple)

Semelhantes às listas, mas imutáveis (não podem ser alteradas após a criação).

```python
tupla = (1, 2, 3, "quatro", 5.0)
```

### 7. Conjuntos (set)

Coleção não ordenada de itens únicos.

```python
conjunto = {1, 2, 3, 4, 5}
```

### 8. Dicionários (dict)

Coleção de pares chave-valor.

```python
dicionario = {"nome": "João", "idade": 25, "altura": 1.75}
```

## Conversão de Tipos

Python permite a conversão entre diferentes tipos de dados usando funções de conversão de tipos.

### Exemplos de Conversão de Tipos

- **Inteiro para String**

```python
numero = 10
numero_str = str(numero)
```

- **String para Inteiro**

```python
numero_str = "10"
numero = int(numero_str)
```

- **String para Float**

```python
numero_str = "10.5"
numero_float = float(numero_str)
```

- **Lista para Tupla**

```python
lista = [1, 2, 3]
tupla = tuple(lista)
```

- **Tupla para Lista**

```python
tupla = (1, 2, 3)
lista = list(tupla)
```

## Verificação de Tipos

Para verificar o tipo de uma variável, use a função `type()`:

```python
tipo = type(numero)  # Retorna <class 'int'>
```
