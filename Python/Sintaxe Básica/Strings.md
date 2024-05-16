# Manipulação de Strings em Python

A manipulação de strings é uma tarefa comum em Python, e a linguagem oferece uma vasta gama de métodos e funções para facilitar o trabalho com texto. Este guia cobre os conceitos e operações mais importantes para a manipulação de strings em Python, incluindo métodos básicos, formatação, operações avançadas, e muito mais.

## Conceitos Básicos

### Criando Strings

Strings em Python são sequências de caracteres. Você pode criar uma string usando aspas simples (`'`) ou duplas (`"`).

```python
string1 = 'Olá, mundo!'
string2 = "Python é incrível!"
```

### Strings Multilinha

Você pode criar strings multilinha usando aspas triplas (`'''` ou `"""`).

```python
multilinha = '''Esta é uma string
em múltiplas linhas.'''
```

### Acessando Caracteres

Você pode acessar caracteres individuais de uma string usando indexação. Lembre-se de que a indexação começa em 0.

```python
string = "Python"
print(string[0])  # Saída: P
print(string[-1]) # Saída: n
```

### Fatiamento (Slicing)

Você pode extrair substrings usando fatiamento.

```python
string = "Python"
print(string[0:2])  # Saída: Py
print(string[2:])   # Saída: thon
print(string[:4])   # Saída: Pyth
print(string[::2])  # Saída: Pto
```

## Métodos de String Comuns

### Alteração de Maiúsculas e Minúsculas

```python
string = "Python"
print(string.upper())    # Saída: PYTHON
print(string.lower())    # Saída: python
print(string.capitalize()) # Saída: Python
print(string.title())    # Saída: Python
print(string.swapcase()) # Saída: pYTHON
```

### Remoção de Espaços

```python
string = "   Olá, mundo!   "
print(string.strip())   # Saída: "Olá, mundo!"
print(string.lstrip())  # Saída: "Olá, mundo!   "
print(string.rstrip())  # Saída: "   Olá, mundo!"
```

### Substituição de Substrings

```python
string = "Olá, mundo!"
nova_string = string.replace("mundo", "Python")
print(nova_string)  # Saída: "Olá, Python!"
```

### Divisão e Junção de Strings

```python
string = "Olá, mundo!"
lista = string.split(", ")
print(lista)  # Saída: ['Olá', 'mundo!']

nova_string = ", ".join(lista)
print(nova_string)  # Saída: "Olá, mundo!"
```

### Verificação de Conteúdo

```python
string = "Python é incrível!"
print(string.startswith("Python"))  # Saída: True
print(string.endswith("!"))         # Saída: True
print(string.find("é"))             # Saída: 7 (posição do caractere)
print(string.count("i"))            # Saída: 2 (ocorrências de 'i')
```

## Formatação de Strings

### Formatação com `%`

```python
nome = "João"
idade = 30
mensagem = "Meu nome é %s e eu tenho %d anos." % (nome, idade)
print(mensagem)  # Saída: Meu nome é João e eu tenho 30 anos.
```

### Formatação com `str.format`

```python
nome = "Maria"
idade = 25
mensagem = "Meu nome é {} e eu tenho {} anos.".format(nome, idade)
print(mensagem)  # Saída: Meu nome é Maria e eu tenho 25 anos.
```

### Formatação com f-strings (Python 3.6+)

```python
nome = "Ana"
idade = 22
mensagem = f"Meu nome é {nome} e eu tenho {idade} anos."
print(mensagem)  # Saída: Meu nome é Ana e eu tenho 22 anos.
```

## Métodos Avançados

### Verificação de Conteúdo

```python
string = "Python123"
print(string.isalnum())  # Saída: True (se a string é alfanumérica)
print(string.isalpha())  # Saída: False (se a string contém apenas letras)
print(string.isdigit())  # Saída: False (se a string contém apenas dígitos)
print(string.islower())  # Saída: False (se todos os caracteres são minúsculos)
print(string.isupper())  # Saída: False (se todos os caracteres são maiúsculos)
print(string.isspace())  # Saída: False (se a string contém apenas espaços)
```

### Codificação e Decodificação

Você pode codificar e decodificar strings usando métodos de codificação, como UTF-8.

```python
string = "Olá, mundo!"
bytes_string = string.encode('utf-8')
print(bytes_string)  # Saída: b'Ol\xc3\xa1, mundo!'

decodificada = bytes_string.decode('utf-8')
print(decodificada)  # Saída: Olá, mundo!
```

## Trabalhando com Strings Multilinha

### Usando `splitlines`

O método `splitlines` divide uma string em uma lista de linhas.

```python
multilinha = """Primeira linha
Segunda linha
Terceira linha"""
linhas = multilinha.splitlines()
print(linhas)
# Saída: ['Primeira linha', 'Segunda linha', 'Terceira linha']
```

### Concatenando Strings

Você pode concatenar strings usando o operador `+` ou o método `join`.

```python
string1 = "Python"
string2 = "é incrível!"
concatenada = string1 + " " + string2
print(concatenada)  # Saída: Python é incrível!

partes = ["Python", "é", "incrível!"]
concatenada = " ".join(partes)
print(concatenada)  # Saída: Python é incrível!
```