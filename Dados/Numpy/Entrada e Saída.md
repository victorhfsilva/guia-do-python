# Entrada e Saída de Arrays no NumPy

NumPy oferece funcionalidades convenientes para carregar e salvar arrays a partir de arquivos de texto, utilizando as funções `loadtxt` e `savetxt`. Essas funções são úteis para armazenar dados e recuperá-los posteriormente em formato de texto, como arquivos CSV ou TSV.

## Função `numpy.loadtxt`

A função `numpy.loadtxt` é usada para carregar dados de um arquivo de texto e retorná-los como um array NumPy. Esta função é flexível e permite a leitura de arquivos com diferentes delimitadores e tipos de dados.

### Sintaxe Básica

```python
numpy.loadtxt(fname, dtype=float, delimiter=' ', skiprows=0, usecols=None, unpack=False)
```

### Parâmetros Comuns

- `fname`: Nome do arquivo a ser lido.
- `dtype`: Tipo de dados dos elementos do array (padrão é `float`).
- `delimiter`: Caractere que separa os valores (padrão é espaço `' '`).
- `skiprows`: Número de linhas a serem puladas no início do arquivo (padrão é `0`).
- `usecols`: Índices das colunas a serem lidas (padrão é `None`, todas as colunas).
- `unpack`: Se `True`, retorna as colunas como arrays separados (padrão é `False`).

### Exemplo de Uso

#### Arquivo de Texto (dados.txt)

```
1.0 2.0 3.0
4.0 5.0 6.0
7.0 8.0 9.0
```

#### Carregando o Arquivo

```python
import numpy as np

# Carregar dados de um arquivo de texto
dados = np.loadtxt('dados.txt')
print(dados)
# Saída:
# [[1. 2. 3.]
#  [4. 5. 6.]
#  [7. 8. 9.]]
```

### Carregando com Diferentes Delimitadores

#### Arquivo de Texto (dados.csv)

```csv
1.0,2.0,3.0
4.0,5.0,6.0
7.0,8.0,9.0
```

#### Carregando o Arquivo

```python
import numpy as np

# Carregar dados de um arquivo CSV
dados = np.loadtxt('dados.csv', delimiter=',')
print(dados)
# Saída:
# [[1. 2. 3.]
#  [4. 5. 6.]
#  [7. 8. 9.]]
```

### Carregando Colunas Específicas

```python
import numpy as np

# Carregar apenas as colunas 0 e 2
dados = np.loadtxt('dados.txt', usecols=(0, 2))
print(dados)
# Saída:
# [[1. 3.]
#  [4. 6.]
#  [7. 9.]]
```

## Função `numpy.savetxt`

A função `numpy.savetxt` é usada para salvar arrays NumPy em arquivos de texto. Esta função permite especificar o delimitador, o formato dos dados e outras opções de salvamento.

### Sintaxe Básica

```python
numpy.savetxt(fname, X, fmt='%.18e', delimiter=' ', newline='\n', header='', footer='', comments='# ')
```

### Parâmetros Comuns

- `fname`: Nome do arquivo onde os dados serão salvos.
- `X`: Array a ser salvo.
- `fmt`: Formato das linhas do arquivo (padrão é `'%.18e'`).
- `delimiter`: Caractere que separa os valores (padrão é espaço `' '`).
- `newline`: String que separa as linhas (padrão é `'\n'`).
- `header`: String que será escrita no topo do arquivo (padrão é vazio).
- `footer`: String que será escrita no final do arquivo (padrão é vazio).
- `comments`: String que será colocada antes dos comentários (padrão é `'# '`).

### Exemplo de Uso

#### Salvando um Array em um Arquivo de Texto

```python
import numpy as np

# Criar um array
dados = np.array([[1.0, 2.0, 3.0], [4.0, 5.0, 6.0], [7.0, 8.0, 9.0]])

# Salvar o array em um arquivo de texto
np.savetxt('saida.txt', dados)
```

#### Arquivo de Saída (saida.txt)

```
1.000000000000000000e+00 2.000000000000000000e+00 3.000000000000000000e+00
4.000000000000000000e+00 5.000000000000000000e+00 6.000000000000000000e+00
7.000000000000000000e+00 8.000000000000000000e+00 9.000000000000000000e+00
```

### Especificando o Formato e o Delimitador

```python
import numpy as np

# Criar um array
dados = np.array([[1.0, 2.0, 3.0], [4.0, 5.0, 6.0], [7.0, 8.0, 9.0]])

# Salvar o array em um arquivo CSV com 2 casas decimais
np.savetxt('saida.csv', dados, delimiter=',', fmt='%.2f')
```

#### Arquivo de Saída (saida.csv)

```csv
1.00,2.00,3.00
4.00,5.00,6.00
7.00,8.00,9.00
```

### Adicionando Cabeçalhos e Rodapés

```python
import numpy as np

# Criar um array
dados = np.array([[1.0, 2.0, 3.0], [4.0, 5.0, 6.0], [7.0, 8.0, 9.0]])

# Salvar o array em um arquivo de texto com cabeçalho e rodapé
np.savetxt('saida_com_header_footer.txt', dados, header='Cabeçalho: valores', footer='Rodapé: fim dos valores', comments='# ')
```

#### Arquivo de Saída (saida_com_header_footer.txt)

```
# Cabeçalho: valores
1.000000000000000000e+00 2.000000000000000000e+00 3.000000000000000000e+00
4.000000000000000000e+00 5.000000000000000000e+00 6.000000000000000000e+00
7.000000000000000000e+00 8.000000000000000000e+00 9.000000000000000000e+00
# Rodapé: fim dos valores
```
