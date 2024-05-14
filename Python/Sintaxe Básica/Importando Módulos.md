# Importação de Módulos em Python

## Importando Módulos com `import`

A maneira mais simples de importar um módulo é usar a instrução `import`, que carrega o módulo completo.

### Sintaxe

```python
import nome_do_modulo
```

### Exemplo

```python
import math

print(math.sqrt(16))  # Saída: 4.0
```

Neste exemplo, o módulo `math` é importado, e a função `sqrt` é chamada usando a notação de ponto (`math.sqrt`).

## Importando Componentes Específicos com `from ... import`

Você pode importar componentes específicos de um módulo usando a instrução `from ... import`. Isso pode tornar seu código mais legível e evitar a necessidade de usar a notação de ponto.

### Sintaxe

```python
from nome_do_modulo import componente1, componente2
```

### Exemplo

```python
from math import sqrt, pi

print(sqrt(16))  # Saída: 4.0
print(pi)       # Saída: 3.141592653589793
```

Neste exemplo, apenas `sqrt` e `pi` são importados do módulo `math`, permitindo que sejam usados diretamente.

## Importando Todos os Componentes com `from ... import *`

Você pode importar todos os componentes de um módulo usando o asterisco (`*`). No entanto, essa prática não é recomendada, pois pode causar conflitos de nomes e reduzir a legibilidade do código.

### Sintaxe

```python
from nome_do_modulo import *
```

### Exemplo

```python
from math import *

print(sqrt(16))  # Saída: 4.0
print(pi)       # Saída: 3.141592653589793
```

## Renomeando Módulos e Componentes com `as`

Você pode renomear módulos e componentes durante a importação usando a instrução `as`. Isso pode ser útil para evitar conflitos de nomes ou para tornar o código mais curto e legível.

### Renomeando Módulos

```python
import nome_do_modulo as novo_nome
```

#### Exemplo

```python
import math as m

print(m.sqrt(16))  # Saída: 4.0
```

### Renomeando Componentes

```python
from nome_do_modulo import componente as novo_nome
```

#### Exemplo

```python
from math import sqrt as raiz_quadrada

print(raiz_quadrada(16))  # Saída: 4.0
```

## Importando Módulos Personalizados

Além dos módulos embutidos, você pode importar módulos personalizados que você criou. Suponha que você tenha um arquivo chamado `meu_modulo.py` com o seguinte conteúdo:

```python
# meu_modulo.py
def saudacao(nome):
    return f"Olá, {nome}!"
```

Você pode importar e usar esse módulo em outro arquivo:

```python
# outro_arquivo.py
import meu_modulo

print(meu_modulo.saudacao("João"))  # Saída: Olá, João!
```

## Organização de Pacotes

Módulos podem ser organizados em pacotes, que são diretórios contendo um arquivo especial `__init__.py` (pode estar vazio) e outros módulos. Por exemplo, a estrutura de diretório a seguir define um pacote:

```
meu_pacote/
    __init__.py
    modulo1.py
    modulo2.py
```

Você pode importar módulos de um pacote usando a notação de ponto:

```python
from meu_pacote import modulo1
import meu_pacote.modulo2 as m2
```
