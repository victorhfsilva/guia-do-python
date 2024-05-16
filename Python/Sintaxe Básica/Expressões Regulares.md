# Expressões Regulares em Python

Expressões regulares (regex) são uma ferramenta poderosa para a manipulação e análise de strings. Elas permitem definir padrões complexos de pesquisa e substituição de texto. Em Python, o módulo `re` oferece suporte completo para o uso de expressões regulares.

## Introdução

Uma expressão regular é uma sequência de caracteres que define um padrão de pesquisa. Você pode usar expressões regulares para encontrar, extrair e substituir partes de uma string.

### Importando o Módulo `re`

Para usar expressões regulares em Python, importe o módulo `re`:

```python
import re
```

## Sintaxe Básica

### Metacaracteres

Os metacaracteres são caracteres especiais que têm um significado específico em expressões regulares:

- `.`: Qualquer caractere, exceto nova linha.
- `^`: Início da string.
- `$`: Fim da string.
- `*`: Zero ou mais ocorrências.
- `+`: Uma ou mais ocorrências.
- `?`: Zero ou uma ocorrência.
- `{n}`: Exatamente n ocorrências.
- `{n,}`: Pelo menos n ocorrências.
- `{n,m}`: De n a m ocorrências.
- `[]`: Conjunto de caracteres.
- `|`: Ou (alternativa).
- `()`: Agrupamento.

### Classes de Caracteres

- `\d`: Qualquer dígito (equivalente a `[0-9]`).
- `\D`: Qualquer caractere que não seja um dígito.
- `\w`: Qualquer caractere alfanumérico (equivalente a `[a-zA-Z0-9_]`).
- `\W`: Qualquer caractere que não seja alfanumérico.
- `\s`: Qualquer espaço em branco (espaço, tabulação, nova linha).
- `\S`: Qualquer caractere que não seja espaço em branco.

## Operações Básicas

### `re.match`

Verifica se o padrão corresponde ao início da string.

```python
import re

string = "Python é incrível!"
padrao = r"Python"

resultado = re.match(padrao, string)
if resultado:
    print("Correspondência encontrada!")
else:
    print("Nenhuma correspondência encontrada.")
```

### `re.search`

Pesquisa pela primeira ocorrência do padrão em qualquer parte da string.

```python
import re

string = "O número de telefone é 123-456-7890"
padrao = r"\d{3}-\d{3}-\d{4}"

resultado = re.search(padrao, string)
if resultado:
    print("Número encontrado:", resultado.group())
else:
    print("Nenhuma correspondência encontrada.")
```

### `re.findall`

Encontra todas as ocorrências do padrão na string.

```python
import re

string = "Aqui estão os números: 123-456-7890, 987-654-3210"
padrao = r"\d{3}-\d{3}-\d{4}"

resultados = re.findall(padrao, string)
print("Números encontrados:", resultados)
```

### `re.finditer`

Encontra todas as ocorrências do padrão na string, retornando um iterador com os objetos de correspondência.

```python
import re

string = "Aqui estão os números: 123-456-7890, 987-654-3210"
padrao = r"\d{3}-\d{3}-\d{4}"

resultados = re.finditer(padrao, string)
for resultado in resultados:
    print("Número encontrado:", resultado.group())
```

### `re.sub`

Substitui todas as ocorrências do padrão por uma string de substituição.

```python
import re

string = "O número de telefone é 123-456-7890"
padrao = r"\d{3}-\d{3}-\d{4}"

nova_string = re.sub(padrao, "XXX-XXX-XXXX", string)
print("String modificada:", nova_string)
```

## Grupos e Captura

### Usando Parênteses para Agrupamento

Parênteses `()` são usados para agrupar partes da expressão regular e capturar os resultados correspondentes.

```python
import re

string = "O número de telefone é 123-456-7890"
padrao = r"(\d{3})-(\d{3})-(\d{4})"

resultado = re.search(padrao, string)
if resultado:
    print("Código de área:", resultado.group(1))
    print("Prefixo:", resultado.group(2))
    print("Número:", resultado.group(3))
```

### Referências a Grupos

Você pode referenciar grupos capturados em substituições usando `\1`, `\2`, etc.

```python
import re

string = "O número de telefone é 123-456-7890"
padrao = r"(\d{3})-(\d{3})-(\d{4})"

nova_string = re.sub(padrao, r"(\1) \2-\3", string)
print("String modificada:", nova_string)
```

## Flags de Expressões Regulares

Flags modificam o comportamento das expressões regulares. Eles são passados como um segundo argumento para as funções `re`.

### Exemplos de Flags

- `re.IGNORECASE` (`re.I`): Ignora a diferença entre maiúsculas e minúsculas.
- `re.MULTILINE` (`re.M`): Faz `^` e `$` corresponderem ao início e fim de cada linha.
- `re.DOTALL` (`re.S`): Faz `.` corresponder a qualquer caractere, incluindo nova linha.

```python
import re

string = "Python é incrível! python é poderoso!"
padrao = r"python"

resultados = re.findall(padrao, string, re.IGNORECASE)
print("Ocorrências encontradas:", resultados)
```

## Expressões Regulares Comuns

### Validar um Endereço de Email

```python
import re

email = "exemplo@dominio.com"
padrao = r"^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$"

if re.match(padrao, email):
    print("Endereço de email válido.")
else:
    print("Endereço de email inválido.")
```

### Validar um Número de Telefone

```python
import re

telefone = "123-456-7890"
padrao = r"^\d{3}-\d{3}-\d{4}$"

if re.match(padrao, telefone):
    print("Número de telefone válido.")
else:
    print("Número de telefone inválido.")
```

### Extrair URLs de um Texto

```python
import re

texto = "Visite o site https://www.exemplo.com e http://www.teste.com.br para mais informações."
padrao = r"https?://[a-zA-Z0-9./-]+"

urls = re.findall(padrao, texto)
print("URLs encontradas:", urls)
```