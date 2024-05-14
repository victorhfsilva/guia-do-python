# Operadores em Python

## Operadores Aritméticos

Operadores aritméticos são usados para realizar operações matemáticas básicas.

| Operador | Descrição          | Exemplo     | Resultado |
|----------|--------------------|-------------|-----------|
| `+`      | Adição             | `5 + 3`     | `8`       |
| `-`      | Subtração          | `5 - 3`     | `2`       |
| `*`      | Multiplicação      | `5 * 3`     | `15`      |
| `/`      | Divisão            | `5 / 3`     | `1.6667`  |
| `//`     | Divisão inteira    | `5 // 3`    | `1`       |
| `%`      | Módulo (resto)     | `5 % 3`     | `2`       |
| `**`     | Exponenciação      | `5 ** 3`    | `125`     |

## Operadores Relacionais

Operadores relacionais são usados para comparar valores e retornar um valor booleano (True ou False).

| Operador | Descrição            | Exemplo      | Resultado |
|----------|----------------------|--------------|-----------|
| `==`     | Igual a              | `5 == 3`     | `False`   |
| `!=`     | Diferente de         | `5 != 3`     | `True`    |
| `>`      | Maior que            | `5 > 3`      | `True`    |
| `<`      | Menor que            | `5 < 3`      | `False`   |
| `>=`     | Maior ou igual a     | `5 >= 3`     | `True`    |
| `<=`     | Menor ou igual a     | `5 <= 3`     | `False`   |

## Operadores Lógicos

Operadores lógicos são usados para combinar expressões booleanas.

| Operador | Descrição   | Exemplo             | Resultado |
|----------|-------------|---------------------|-----------|
| `and`    | E lógico    | `True and False`    | `False`   |
| `or`     | Ou lógico   | `True or False`     | `True`    |
| `not`    | Não lógico  | `not True`          | `False`   |

## Operadores de Atribuição

Operadores de atribuição são usados para atribuir valores a variáveis.

| Operador | Descrição                   | Exemplo      | Equivalente a |
|----------|-----------------------------|--------------|---------------|
| `=`      | Atribuição simples          | `x = 5`      | `x = 5`       |
| `+=`     | Atribuição com adição       | `x += 5`     | `x = x + 5`   |
| `-=`     | Atribuição com subtração    | `x -= 5`     | `x = x - 5`   |
| `*=`     | Atribuição com multiplicação| `x *= 5`     | `x = x * 5`   |
| `/=`     | Atribuição com divisão      | `x /= 5`     | `x = x / 5`   |
| `//=`    | Atribuição com divisão inteira | `x //= 5` | `x = x // 5`  |
| `%=`     | Atribuição com módulo       | `x %= 5`     | `x = x % 5`   |
| `**=`    | Atribuição com exponenciação| `x **= 5`    | `x = x ** 5`  |

## Operadores Especiais

Python também possui alguns operadores especiais que são úteis em determinadas situações.

### Operador de Identidade

Verifica se duas variáveis apontam para o mesmo objeto.

| Operador | Descrição        | Exemplo           | Resultado |
|----------|------------------|-------------------|-----------|
| `is`     | É                | `x is y`          | `True`    |
| `is not` | Não é            | `x is not y`      | `False`   |

### Operador de Pertinência

Verifica se um valor está presente em uma sequência (como uma lista, tupla, ou string).

| Operador | Descrição        | Exemplo           | Resultado |
|----------|------------------|-------------------|-----------|
| `in`     | Pertence         | `5 in [1, 2, 3, 5]` | `True`  |
| `not in` | Não pertence     | `4 not in [1, 2, 3, 5]` | `True` |
