# Plots com o Matplotlib em Python

Matplotlib é uma biblioteca poderosa para criação de gráficos e visualizações em Python. Ela oferece uma ampla gama de ferramentas para criar gráficos de linhas, dispersão, barras, histogramas, gráficos de pizza, entre outros. 

## Instalando Matplotlib

Para instalar o Matplotlib, use `pip`:

```bash
pip install matplotlib
```

## Importando Matplotlib

A convenção comum é importar o módulo `pyplot` como `plt`:

```python
import matplotlib.pyplot as plt
```

## Criando Gráficos Básicos

### Gráfico de Linhas

```python
import matplotlib.pyplot as plt

# Dados
x = [1, 2, 3, 4, 5]
y = [2, 3, 5, 7, 11]

# Criar o gráfico de linha
plt.plot(x, y)

# Adicionar título e rótulos
plt.title("Gráfico de Linha")
plt.xlabel("Eixo X")
plt.ylabel("Eixo Y")

# Mostrar o gráfico
plt.show()
```

### Gráfico de Dispersão

```python
import matplotlib.pyplot as plt

# Dados
x = [1, 2, 3, 4, 5]
y = [2, 3, 5, 7, 11]

# Criar o gráfico de dispersão
plt.scatter(x, y)

# Adicionar título e rótulos
plt.title("Gráfico de Dispersão")
plt.xlabel("Eixo X")
plt.ylabel("Eixo Y")

# Mostrar o gráfico
plt.show()
```

### Gráfico de Barras

```python
import matplotlib.pyplot as plt

# Dados
categorias = ['A', 'B', 'C', 'D', 'E']
valores = [5, 7, 3, 8, 6]

# Criar o gráfico de barras
plt.bar(categorias, valores)

# Adicionar título e rótulos
plt.title("Gráfico de Barras")
plt.xlabel("Categorias")
plt.ylabel("Valores")

# Mostrar o gráfico
plt.show()
```

### Histograma

```python
import matplotlib.pyplot as plt
import numpy as np

# Dados
dados = np.random.randn(1000)

# Criar o histograma
plt.hist(dados, bins=30, edgecolor='black')

# Adicionar título e rótulos
plt.title("Histograma")
plt.xlabel("Valor")
plt.ylabel("Frequência")

# Mostrar o gráfico
plt.show()
```

### Gráfico de Pizza

```python
import matplotlib.pyplot as plt

# Dados
labels = ['A', 'B', 'C', 'D']
sizes = [15, 30, 45, 10]

# Criar o gráfico de pizza
plt.pie(sizes, labels=labels, autopct='%1.1f%%', startangle=140)

# Adicionar título
plt.title("Gráfico de Pizza")

# Mostrar o gráfico
plt.show()
```

## Customização de Gráficos

### Tamanho e Resolução

```python
import matplotlib.pyplot as plt

# Dados
x = [1, 2, 3, 4, 5]
y = [2, 3, 5, 7, 11]

# Ajustar o tamanho da figura
plt.figure(figsize=(10, 5))

# Criar o gráfico de linha
plt.plot(x, y)

# Adicionar título e rótulos
plt.title("Gráfico de Linha")
plt.xlabel("Eixo X")
plt.ylabel("Eixo Y")

# Mostrar o gráfico
plt.show()
```

### Estilos de Linha e Marcadores

```python
import matplotlib.pyplot as plt

# Dados
x = [1, 2, 3, 4, 5]
y = [2, 3, 5, 7, 11]

# Criar o gráfico de linha com estilo
plt.plot(x, y, linestyle='--', marker='o', color='r')

# Adicionar título e rótulos
plt.title("Gráfico de Linha Customizado")
plt.xlabel("Eixo X")
plt.ylabel("Eixo Y")

# Mostrar o gráfico
plt.show()
```

### Adicionando Legendas

```python
import matplotlib.pyplot as plt

# Dados
x = [1, 2, 3, 4, 5]
y1 = [2, 3, 5, 7, 11]
y2 = [1, 4, 6, 8, 10]

# Criar os gráficos de linha
plt.plot(x, y1, label='Série 1')
plt.plot(x, y2, label='Série 2')

# Adicionar título, rótulos e legenda
plt.title("Gráfico com Legendas")
plt.xlabel("Eixo X")
plt.ylabel("Eixo Y")
plt.legend()

# Mostrar o gráfico
plt.show()
```

### Adicionando Anotações

```python
import matplotlib.pyplot as plt

# Dados
x = [1, 2, 3, 4, 5]
y = [2, 3, 5, 7, 11]

# Criar o gráfico de linha
plt.plot(x, y)

# Adicionar anotação
plt.annotate('Ponto Máximo', xy=(5, 11), xytext=(3, 10),
             arrowprops=dict(facecolor='black', shrink=0.05))

# Adicionar título e rótulos
plt.title("Gráfico com Anotações")
plt.xlabel("Eixo X")
plt.ylabel("Eixo Y")

# Mostrar o gráfico
plt.show()
```

## Subplots

### Criando Múltiplos Gráficos

```python
import matplotlib.pyplot as plt

# Dados
x = [1, 2, 3, 4, 5]
y1 = [2, 3, 5, 7, 11]
y2 = [1, 4, 6, 8, 10]

# Criar subplots
fig, axs = plt.subplots(2, 1, figsize=(8, 6))

# Primeiro gráfico
axs[0].plot(x, y1)
axs[0].set_title('Gráfico 1')

# Segundo gráfico
axs[1].plot(x, y2, color='r')
axs[1].set_title('Gráfico 2')

# Ajustar o layout
plt.tight_layout()

# Mostrar os gráficos
plt.show()
```

### Compartilhando Eixos

```python
import matplotlib.pyplot as plt

# Dados
x = [1, 2, 3, 4, 5]
y1 = [2, 3, 5, 7, 11]
y2 = [1, 4, 6, 8, 10]

# Criar subplots com eixos compartilhados
fig, (ax1, ax2) = plt.subplots(1, 2, sharey=True, figsize=(10, 4))

# Primeiro gráfico
ax1.plot(x, y1)
ax1.set_title('Gráfico 1')

# Segundo gráfico
ax2.plot(x, y2, color='r')
ax2.set_title('Gráfico 2')

# Ajustar o layout
plt.tight_layout()

# Mostrar os gráficos
plt.show()
```

## Salvando Gráficos

### Salvando em Arquivos de Imagem

```python
import matplotlib.pyplot as plt

# Dados
x = [1, 2, 3, 4, 5]
y = [2, 3, 5, 7, 11]

# Criar o gráfico de linha
plt.plot(x, y)

# Adicionar título e rótulos
plt.title("Gráfico para Salvar")
plt.xlabel("Eixo X")
plt.ylabel("Eixo Y")

# Salvar o gráfico em um arquivo PNG
plt.savefig('grafico.png')

# Mostrar o gráfico
plt.show()
```

### Salvando com Alta Resolução

```python
import matplotlib.pyplot as plt

# Dados
x = [1, 2, 3, 4, 5]
y = [2, 3, 5, 7, 11]

# Criar o gráfico de linha
plt.plot(x, y)

# Adicionar título e rótulos
plt.title("Gráfico de Alta Resolução")
plt.xlabel("Eixo X")
plt.ylabel("Eixo Y")

# Salvar o gráfico em um arquivo PNG com alta resolução
plt.savefig('grafico_alta_resolucao.png', dpi=300)

# Mostrar o gráfico
plt.show()
```
