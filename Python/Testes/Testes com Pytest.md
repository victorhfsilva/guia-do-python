# Testes com `pytest` em Python

`pytest` é um framework de teste poderoso e fácil de usar para Python. Ele permite escrever testes de forma simples e possui recursos avançados para testar código de forma eficaz. 

## Instalação

### Usando `pip`

Você pode instalar o `pytest` usando o gerenciador de pacotes `pip`.

```bash
pip install pytest
```

## Estrutura Básica de Testes

### Escrevendo Seu Primeiro Teste

Os testes em `pytest` são funções normais que começam com `test_`. Para escrever um teste, crie um arquivo de teste, por exemplo `test_sample.py`, e adicione uma função de teste.

#### Exemplo: `test_sample.py`

```python
def test_soma():
    assert soma(1, 2) == 3
```

### Executando Testes

Para executar testes, use o comando `pytest` no diretório onde seus arquivos de teste estão localizados.

```bash
pytest
```

## Configuração do `pytest`

### Arquivo de Configuração

O `pytest` pode ser configurado usando um arquivo chamado `pytest.ini`, `tox.ini` ou `setup.cfg`. O arquivo de configuração permite personalizar o comportamento do `pytest`.

#### Exemplo: `pytest.ini`

```ini
[pytest]
minversion = 6.0
addopts = -ra -q
testpaths =
    tests
```

### Opções Comuns

- `minversion`: Define a versão mínima do `pytest` necessária.
- `addopts`: Adiciona opções de linha de comando por padrão.
- `testpaths`: Especifica os diretórios onde os testes estão localizados.

## Estrutura de Diretórios de Teste

É uma boa prática organizar seus testes em um diretório separado. Um exemplo comum é ter uma estrutura de diretórios como esta:

```
my_project/
├── my_module/
│   └── my_code.py
└── tests/
    ├── __init__.py
    └── test_my_code.py
```

## Fixtures

Fixtures são uma maneira poderosa de configurar e desmontar o estado necessário para os testes. Elas ajudam a evitar duplicação de código e a tornar os testes mais legíveis.

### Exemplo de Fixture

#### Definindo uma Fixture

```python
import pytest

@pytest.fixture
def dados_de_teste():
    return {"chave": "valor"}
```

#### Usando uma Fixture em um Teste

```python
def test_uso_fixture(dados_de_teste):
    assert dados_de_teste["chave"] == "valor"
```

## Marcadores

Marcadores são usados para categorizar testes e podem ser úteis para rodar subconjuntos de testes.

### Definindo Marcadores

Você pode definir marcadores no arquivo de configuração `pytest.ini`.

#### Exemplo: `pytest.ini`

```ini
[pytest]
markers =
    lento: marca testes como lentos
    rapido: marca testes como rápidos
```

### Usando Marcadores

#### Exemplo de Uso

```python
import pytest

@pytest.mark.lento
def test_lento():
    import time
    time.sleep(5)
    assert True

@pytest.mark.rapido
def test_rapido():
    assert True
```

### Executando Testes Marcados

Para rodar apenas os testes marcados como `lento`, use:

```bash
pytest -m lento
```

## Testes Parametrizados

Testes parametrizados permitem que você execute a mesma função de teste com diferentes entradas.

### Exemplo de Teste Parametrizado

```python
import pytest

@pytest.mark.parametrize("entrada,esperado", [(1, 2), (2, 3), (3, 4)])
def test_incrementar(entrada, esperado):
    assert entrada + 1 == esperado
```

## Plugins

`pytest` tem uma arquitetura de plugins rica e muitos plugins estão disponíveis para estender suas funcionalidades.

### Instalando Plugins

Plugins podem ser instalados usando `pip`. Por exemplo, para instalar o plugin `pytest-cov` (para cobertura de código), use:

```bash
pip install pytest-cov
```

### Usando Plugins

Para usar o plugin de cobertura de código, execute:

```bash
pytest --cov=my_module tests/
```

## Boas Práticas

- **Isolamento**: Certifique-se de que os testes são isolados e independentes uns dos outros.
- **Nomeação**: Nomeie arquivos de teste e funções de teste de maneira clara e consistente.
- **Cobertura**: Tente cobrir o máximo de código possível com testes, incluindo casos de borda.
- **Automação**: Integre `pytest` em pipelines de CI/CD para automação de testes.
