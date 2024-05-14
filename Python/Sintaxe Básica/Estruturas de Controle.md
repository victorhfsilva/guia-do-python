# Estruturas de Controle em Python

## Estruturas Condicionais

### `if`, `elif`, `else`

A estrutura condicional `if` avalia uma expressão e executa um bloco de código se a expressão for verdadeira. Você pode usar `elif` para verificar múltiplas condições e `else` para executar um bloco de código se todas as condições anteriores falharem.

#### Sintaxe

```python
if condição:
    # bloco de código se a condição for verdadeira
elif outra_condição:
    # bloco de código se a outra condição for verdadeira
else:
    # bloco de código se nenhuma das condições for verdadeira
```

#### Exemplo

```python
idade = 18

if idade < 18:
    print("Menor de idade")
elif idade == 18:
    print("Tem 18 anos")
else:
    print("Maior de idade")
```

## Estruturas de Repetição (Loops)

### `for`

O loop `for` itera sobre uma sequência (como uma lista, tupla, dicionário, conjunto ou string) ou qualquer objeto iterável.

#### Sintaxe

```python
for item in sequencia:
    # bloco de código para cada item na sequência
```

#### Exemplo

```python
numeros = [1, 2, 3, 4, 5]

for numero in numeros:
    print(numero)
```

### `while`

O loop `while` repete um bloco de código enquanto uma condição for verdadeira.

#### Sintaxe

```python
while condição:
    # bloco de código enquanto a condição for verdadeira
```

#### Exemplo

```python
contador = 0

while contador < 5:
    print(contador)
    contador += 1
```

## Estruturas de Controle Adicionais

### `break` e `continue`

- **`break`**: Interrompe o loop imediatamente.
- **`continue`**: Pula a iteração atual e vai para a próxima iteração do loop.

#### Exemplo com `break`

```python
for numero in range(10):
    if numero == 5:
        break
    print(numero)
```

#### Exemplo com `continue`

```python
for numero in range(10):
    if numero % 2 == 0:
        continue
    print(numero)
```

### `else` em Loops

Você pode usar `else` com loops `for` e `while`. O bloco `else` é executado quando o loop termina normalmente (sem interrupção por `break`).

#### Exemplo

```python
for numero in range(5):
    print(numero)
else:
    print("Loop concluído sem interrupção")
```

## List Comprehensions

List comprehensions são uma maneira concisa de criar listas.

#### Sintaxe

```python
[expressão for item in sequência if condição]
```

#### Exemplo

```python
quadrados = [x**2 for x in range(10) if x % 2 == 0]
print(quadrados)  # Saída: [0, 4, 16, 36, 64]
```

## Dict Comprehensions

Assim como list comprehensions, você pode criar dicionários de maneira concisa.

#### Exemplo

```python
quadrados = {x: x**2 for x in range(10) if x % 2 == 0}
print(quadrados)  # Saída: {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}
```
