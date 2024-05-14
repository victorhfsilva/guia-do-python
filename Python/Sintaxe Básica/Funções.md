# Funções em Python

## Definindo Funções

Para definir uma função em Python, usamos a palavra-chave `def`, seguida pelo nome da função, parênteses e dois pontos. O corpo da função contém o código que será executado quando a função for chamada.

### Sintaxe

```python
def nome_da_funcao(argumentos):
    # corpo da função
    return valor_de_retorno
```

### Exemplo Básico

```python
def saudacao():
    print("Olá, Mundo!")

saudacao()  # Chama a função saudacao
```

## Argumentos de Função

Funções podem receber valores chamados argumentos, que são passados para a função quando ela é chamada. Existem diferentes tipos de argumentos que podem ser usados em Python.

### Argumentos Posicionais

Argumentos posicionais são os mais comuns e são passados para a função na ordem em que são definidos.

#### Exemplo

```python
def saudacao(nome):
    print(f"Olá, {nome}!")

saudacao("João")  # Saída: Olá, João!
```

### Argumentos Padrão

Argumentos padrão são usados quando você quer que a função tenha um valor padrão caso nenhum argumento seja fornecido.

#### Exemplo

```python
def saudacao(nome="Mundo"):
    print(f"Olá, {nome}!")

saudacao()         # Saída: Olá, Mundo!
saudacao("João")   # Saída: Olá, João!
```

### Argumentos Nomeados (Keyword Arguments)

Argumentos nomeados são passados para a função por nome, permitindo que a ordem dos argumentos seja diferente da definição da função.

#### Exemplo

```python
def saudacao(nome, mensagem):
    print(f"{mensagem}, {nome}!")

saudacao(mensagem="Bom dia", nome="João")  # Saída: Bom dia, João!
```

### Argumentos Arbitrários

Você pode usar `*args` e `**kwargs` para passar um número variável de argumentos para a função.

#### `*args`

Permite passar uma lista de argumentos posicionais.

```python
def lista_nomes(*nomes):
    for nome in nomes:
        print(nome)

lista_nomes("João", "Maria", "Pedro")  # Saída: João, Maria, Pedro
```

#### `**kwargs`

Permite passar um dicionário de argumentos nomeados.

```python
def dados_pessoais(**dados):
    for chave, valor in dados.items():
        print(f"{chave}: {valor}")

dados_pessoais(nome="João", idade=30, cidade="São Paulo")
# Saída:
# nome: João
# idade: 30
# cidade: São Paulo
```

## Retorno de Valores

Funções podem retornar valores usando a palavra-chave `return`. Quando uma função atinge uma instrução `return`, ela encerra a execução e retorna o valor especificado.

### Exemplo

```python
def soma(a, b):
    return a + b

resultado = soma(5, 3)
print(resultado)  # Saída: 8
```

### Retornando Múltiplos Valores

Uma função pode retornar múltiplos valores como uma tupla.

#### Exemplo

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

## Funções Aninhadas e Closures

Funções podem ser definidas dentro de outras funções. Funções aninhadas têm acesso às variáveis da função externa.

### Exemplo de Função Aninhada

```python
def externa(mensagem):
    def interna():
        print(mensagem)
    interna()

externa("Olá, Mundo!")  # Saída: Olá, Mundo!
```

### Closures

Closures ocorrem quando uma função aninhada captura o estado da função externa.

#### Exemplo

```python
def criar_mensagem(mensagem):
    def imprimir_mensagem():
        print(mensagem)
    return imprimir_mensagem

saudacao = criar_mensagem("Olá, Mundo!")
saudacao()  # Saída: Olá, Mundo!
```

## Funções Lambda

Funções lambda são pequenas funções anônimas definidas com a palavra-chave `lambda`. Elas são úteis para operações simples e de curta duração.

### Sintaxe

```python
lambda argumentos: expressão
```

### Exemplo

```python
soma = lambda a, b: a + b
print(soma(5, 3))  # Saída: 8
```
