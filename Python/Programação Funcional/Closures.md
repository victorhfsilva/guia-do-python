# Closures em Python

Closures são uma característica poderosa e útil na programação em Python. Elas permitem que funções internas lembrem do ambiente em que foram criadas, mesmo depois que a função externa tiver terminado de executar.

## O Que é uma Closure?

Uma closure é uma função que lembra das variáveis do escopo onde foi criada, mesmo após esse escopo ter sido encerrado. Isso é possível porque as funções internas têm acesso às variáveis locais da função externa, mesmo depois que a função externa terminou sua execução.

### Exemplo Simples

```python
def externo():
    x = 10
    def interno():
        print(x)
    return interno

closure = externo()
closure()  # Saída: 10
```

Neste exemplo, a função `interno` é uma closure porque ela "lembra" da variável `x` definida na função `externo`, mesmo após `externo` ter terminado de executar.

## Como Closures Funcionam

Quando uma função é definida dentro de outra função, a função interna tem acesso às variáveis locais da função externa. Quando a função externa retorna a função interna, essa função interna mantém uma referência ao escopo em que foi criada, permitindo que ela acesse essas variáveis posteriormente.

### Exemplo com Parâmetros

```python
def criar_multiplicador(multiplicador):
    def multiplicar(numero):
        return numero * multiplicador
    return multiplicar

multiplicar_por_3 = criar_multiplicador(3)
print(multiplicar_por_3(10))  # Saída: 30

multiplicar_por_5 = criar_multiplicador(5)
print(multiplicar_por_5(10))  # Saída: 50
```

Neste exemplo, `multiplicar` é uma closure que lembra do valor de `multiplicador` passado para `criar_multiplicador`.

## Usos de Closures

Closures são frequentemente usadas para criar funções com comportamento configurável, manter estado entre chamadas de função, e em muitos outros cenários onde a retenção de contexto é útil.

### Exemplo: Contador

```python
def criar_contador():
    contador = 0
    def incrementar():
        nonlocal contador
        contador += 1
        return contador
    return incrementar

contador1 = criar_contador()
print(contador1())  # Saída: 1
print(contador1())  # Saída: 2

contador2 = criar_contador()
print(contador2())  # Saída: 1
```

Neste exemplo, `incrementar` é uma closure que mantém o estado de `contador` entre as chamadas. `nonlocal` é utilizado para modificar o estado de uma variável externa dentro da função interna.

## Limitações e Considerações

- **Uso de memória**: Closures podem aumentar o uso de memória, pois mantêm uma referência ao escopo onde foram criadas.
- **Complexidade**: O uso excessivo de closures pode tornar o código difícil de entender e manter.
- **Nonlocal**: Para modificar variáveis capturadas pelo escopo exterior, use a palavra-chave `nonlocal`.
