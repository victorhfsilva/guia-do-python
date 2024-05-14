# Tratamento de Erros e Exceções em Python

## O que são Exceções?

Exceções são eventos que interrompem o fluxo normal de execução de um programa. Elas ocorrem quando o Python encontra uma situação que não sabe como lidar. Por exemplo, tentar dividir por zero ou acessar um índice fora dos limites de uma lista gera uma exceção.

## Blocos `try` e `except`

A maneira mais básica de tratar exceções em Python é usar blocos `try` e `except`. O código que pode gerar uma exceção é colocado dentro do bloco `try`, e o código que lida com a exceção é colocado dentro do bloco `except`.

### Sintaxe

```python
try:
    # código que pode gerar uma exceção
except TipoDeExcecao:
    # código que lida com a exceção
```

### Exemplo

```python
try:
    resultado = 10 / 0
except ZeroDivisionError:
    print("Erro: Divisão por zero não é permitida.")
```

## Capturando Múltiplas Exceções

Você pode capturar diferentes tipos de exceções usando múltiplos blocos `except`.

### Sintaxe

```python
try:
    # código que pode gerar uma exceção
except TipoDeExcecao1:
    # código que lida com TipoDeExcecao1
except TipoDeExcecao2:
    # código que lida com TipoDeExcecao2
```

### Exemplo

```python
try:
    numero = int(input("Digite um número: "))
    resultado = 10 / numero
except ValueError:
    print("Erro: Valor inválido. Digite um número inteiro.")
except ZeroDivisionError:
    print("Erro: Divisão por zero não é permitida.")
```

## Usando `else` com `try`

O bloco `else` é opcional e pode ser usado para executar código que deve rodar apenas se o bloco `try` não gerar uma exceção.

### Sintaxe

```python
try:
    # código que pode gerar uma exceção
except TipoDeExcecao:
    # código que lida com a exceção
else:
    # código que é executado se não houver exceção
```

### Exemplo

```python
try:
    resultado = 10 / 2
except ZeroDivisionError:
    print("Erro: Divisão por zero não é permitida.")
else:
    print("Divisão bem-sucedida:", resultado)
```

## Usando `finally`

O bloco `finally` é executado independentemente de uma exceção ter sido gerada ou não. É geralmente usado para liberar recursos, como fechar arquivos ou conexões de rede.

### Sintaxe

```python
try:
    # código que pode gerar uma exceção
except TipoDeExcecao:
    # código que lida com a exceção
else:
    # código que é executado se não houver exceção
finally:
    # código que é sempre executado
```

### Exemplo

```python
try:
    arquivo = open('meu_arquivo.txt', 'r')
    conteudo = arquivo.read()
except FileNotFoundError:
    print("Erro: Arquivo não encontrado.")
else:
    print("Arquivo lido com sucesso.")
finally:
    arquivo.close()
    print("Arquivo fechado.")
```

## Levantando Exceções

Você pode levantar exceções manualmente usando a palavra-chave `raise`. Isso é útil para gerar erros personalizados ou para testar o comportamento do seu código com diferentes exceções.

### Sintaxe

```python
raise TipoDeExcecao("mensagem de erro")
```

### Exemplo

```python
def verifica_numero(numero):
    if numero < 0:
        raise ValueError("Número não pode ser negativo.")
    return numero

try:
    verifica_numero(-1)
except ValueError as e:
    print("Erro:", e)
```

## Criando Exceções Personalizadas

Você pode definir suas próprias classes de exceção para tratar casos específicos em seu código. As exceções personalizadas devem herdar de `Exception` ou de uma de suas subclasses.

### Sintaxe

```python
class MinhaExcecao(Exception):
    pass
```

### Exemplo

```python
class NumeroNegativoError(Exception):
    def __init__(self, numero, mensagem="Número não pode ser negativo."):
        self.numero = numero
        self.mensagem = mensagem
        super().__init__(self.mensagem)

def verifica_numero(numero):
    if numero < 0:
        raise NumeroNegativoError(numero)
    return numero

try:
    verifica_numero(-1)
except NumeroNegativoError as e:
    print(f"Erro: {e.mensagem} Número fornecido: {e.numero}")
```

## Conclusão

O tratamento de erros e exceções é uma parte crucial da programação em Python. Usar blocos `try`, `except`, `else`, `finally`, levantar exceções manualmente e criar exceções personalizadas ajuda a criar programas mais robustos e confiáveis. Este guia cobre os conceitos básicos, mas a prática e a aplicação em cenários reais ajudarão a aprofundar seu entendimento e habilidades. Boa programação!