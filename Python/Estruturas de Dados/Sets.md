# Sets em Python

Sets (conjuntos) são uma estrutura de dados em Python que armazenam coleções não ordenadas de elementos únicos. Sets são mutáveis, o que significa que seus elementos podem ser alterados após a criação, mas todos os elementos devem ser únicos. 

## Criando Sets

Você pode criar um set usando chaves `{}` ou a função `set()`.

### Sintaxe

```python
meu_set = {elemento1, elemento2, elemento3}
ou
meu_set = set([elemento1, elemento2, elemento3])
```

### Exemplos

```python
numeros = {1, 2, 3, 4, 5}
frutas = {'maçã', 'banana', 'laranja'}
vazio = set()
```

## Características dos Sets

1. **Elementos Únicos**: Um set não permite elementos duplicados.
2. **Não Ordenado**: Os elementos não têm uma ordem específica.
3. **Mutável**: Você pode adicionar e remover elementos de um set.

### Exemplo de Duplicação

```python
numeros = {1, 2, 2, 3, 4, 5}
print(numeros)  # Saída: {1, 2, 3, 4, 5}
```

## Acessando Elementos

Você não pode acessar elementos diretamente pelo índice, pois sets são não ordenados. No entanto, você pode iterar sobre os elementos de um set.

### Exemplo

```python
frutas = {'maçã', 'banana', 'laranja'}
for fruta in frutas:
    print(fruta)
```

## Modificando Sets

### Adicionando Elementos

#### Usando `add`

Adiciona um único elemento ao set.

```python
frutas = {'maçã', 'banana'}
frutas.add('laranja')
print(frutas)  # Saída: {'maçã', 'banana', 'laranja'}
```

#### Usando `update`

Adiciona múltiplos elementos ao set.

```python
frutas = {'maçã', 'banana'}
frutas.update(['laranja', 'uva'])
print(frutas)  # Saída: {'maçã', 'banana', 'laranja', 'uva'}
```

### Removendo Elementos

#### Usando `remove`

Remove um elemento específico. Lança um erro se o elemento não existir.

```python
frutas = {'maçã', 'banana', 'laranja'}
frutas.remove('banana')
print(frutas)  # Saída: {'maçã', 'laranja'}
```

#### Usando `discard`

Remove um elemento específico. Não faz nada se o elemento não existir.

```python
frutas = {'maçã', 'banana', 'laranja'}
frutas.discard('banana')
print(frutas)  # Saída: {'maçã', 'laranja'}
```

#### Usando `pop`

Remove e retorna um elemento arbitrário do set.

```python
frutas = {'maçã', 'banana', 'laranja'}
elemento = frutas.pop()
print(elemento)
print(frutas)
```

#### Usando `clear`

Remove todos os elementos do set.

```python
frutas = {'maçã', 'banana', 'laranja'}
frutas.clear()
print(frutas)  # Saída: set()
```

## Operações com Sets

### União

Retorna um novo set contendo todos os elementos de ambos os sets.

```python
set1 = {1, 2, 3}
set2 = {3, 4, 5}
uniao = set1 | set2
print(uniao)  # Saída: {1, 2, 3, 4, 5}
```

### Interseção

Retorna um novo set contendo apenas os elementos que estão em ambos os sets.

```python
set1 = {1, 2, 3}
set2 = {3, 4, 5}
intersecao = set1 & set2
print(intersecao)  # Saída: {3}
```

### Diferença

Retorna um novo set contendo os elementos do primeiro set que não estão no segundo set.

```python
set1 = {1, 2, 3}
set2 = {3, 4, 5}
diferenca = set1 - set2
print(diferenca)  # Saída: {1, 2}
```

### Diferença Simétrica

Retorna um novo set contendo os elementos que estão em um dos sets, mas não em ambos.

```python
set1 = {1, 2, 3}
set2 = {3, 4, 5}
diferenca_simetrica = set1 ^ set2
print(diferenca_simetrica)  # Saída: {1, 2, 4, 5}
```

## Métodos Úteis de Sets

### `copy`

Retorna uma cópia superficial do set.

```python
frutas = {'maçã', 'banana', 'laranja'}
frutas_copia = frutas.copy()
print(frutas_copia)
```

### `issubset`

Verifica se todos os elementos do set estão em outro set.

```python
set1 = {1, 2, 3}
set2 = {1, 2, 3, 4, 5}
print(set1.issubset(set2))  # Saída: True
```

### `issuperset`

Verifica se todos os elementos de outro set estão no set atual.

```python
set1 = {1, 2, 3, 4, 5}
set2 = {1, 2, 3}
print(set1.issuperset(set2))  # Saída: True
```

### `isdisjoint`

Verifica se os sets não têm elementos em comum.

```python
set1 = {1, 2, 3}
set2 = {4, 5, 6}
print(set1.isdisjoint(set2))  # Saída: True
```