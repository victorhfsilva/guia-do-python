# Manipulação de Datas e Horas em Python com `datetime`

Manipulação de datas e horas é uma tarefa comum em muitos aplicativos e scripts Python. A biblioteca `datetime` fornece classes para manipular datas e horas de maneira simples e eficiente. 

## Importando a Biblioteca `datetime`

Para usar a biblioteca `datetime`, você deve importá-la primeiro. A convenção comum é importar `datetime` diretamente ou importar classes específicas.

```python
import datetime

# Ou importe classes específicas
from datetime import datetime, date, time, timedelta
```

## Classes Principais

### `date`

A classe `date` representa uma data (ano, mês, dia) sem uma hora associada.

### `time`

A classe `time` representa uma hora (hora, minuto, segundo, microsegundo) sem uma data associada.

### `datetime`

A classe `datetime` combina uma data e uma hora em um único objeto.

### `timedelta`

A classe `timedelta` representa a diferença entre duas datas ou horas.

## Criação de Objetos `date`, `time` e `datetime`

### Criando um Objeto `date`

```python
from datetime import date

# Criar um objeto date
hoje = date.today()
print("Hoje:", hoje)

# Criar um objeto date especificando ano, mês e dia
data_especifica = date(2023, 5, 16)
print("Data específica:", data_especifica)
```

### Criando um Objeto `time`

```python
from datetime import time

# Criar um objeto time
hora_especifica = time(14, 30, 45)
print("Hora específica:", hora_especifica)
```

### Criando um Objeto `datetime`

```python
from datetime import datetime

# Criar um objeto datetime para a data e hora atuais
agora = datetime.now()
print("Agora:", agora)

# Criar um objeto datetime especificando ano, mês, dia, hora, minuto e segundo
data_hora_especifica = datetime(2023, 5, 16, 14, 30, 45)
print("Data e hora específica:", data_hora_especifica)
```

## Aritmética com Datas e Horas

### Usando `timedelta` para Aritmética

```python
from datetime import datetime, timedelta

# Obter a data e hora atuais
agora = datetime.now()

# Adicionar 10 dias
futuro = agora + timedelta(days=10)
print("10 dias no futuro:", futuro)

# Subtrair 5 horas
passado = agora - timedelta(hours=5)
print("5 horas no passado:", passado)
```

### Diferença entre Datas

```python
from datetime import date

# Criar duas datas
data1 = date(2023, 5, 16)
data2 = date(2023, 6, 16)

# Calcular a diferença entre as duas datas
diferenca = data2 - data1
print("Diferença em dias:", diferenca.days)
```

## Formatação de Datas e Horas

### Formatação usando `strftime`

```python
from datetime import datetime

# Obter a data e hora atuais
agora = datetime.now()

# Formatar a data e hora como string
data_formatada = agora.strftime("%d/%m/%Y %H:%M:%S")
print("Data formatada:", data_formatada)
```

### Parsing de Strings para Objetos `datetime` usando `strptime`

```python
from datetime import datetime

# Converter uma string para um objeto datetime
data_str = "16/05/2023 14:30:45"
data_obj = datetime.strptime(data_str, "%d/%m/%Y %H:%M:%S")
print("Objeto datetime:", data_obj)
```

## Trabalhando com Fusos Horários

Para trabalhar com fusos horários, você pode usar a biblioteca `pytz`.

### Instalando `pytz`

```bash
pip install pytz
```

### Usando `pytz` com `datetime`

```python
from datetime import datetime
import pytz

# Criar um objeto datetime para a data e hora atuais com fuso horário UTC
agora_utc = datetime.now(pytz.utc)
print("Agora (UTC):", agora_utc)

# Converter para outro fuso horário
fuso_horario = pytz.timezone('America/Sao_Paulo')
agora_sp = agora_utc.astimezone(fuso_horario)
print("Agora (São Paulo):", agora_sp)
```

## Outras Operações Úteis

### Obter Componentes de Datas e Horas

```python
from datetime import datetime

# Obter a data e hora atuais
agora = datetime.now()

# Extrair componentes individuais
ano = agora.year
mes = agora.month
dia = agora.day
hora = agora.hour
minuto = agora.minute
segundo = agora.second

print(f"Ano: {ano}, Mês: {mes}, Dia: {dia}, Hora: {hora}, Minuto: {minuto}, Segundo: {segundo}")
```

### Comparação de Datas e Horas

```python
from datetime import datetime

# Criar dois objetos datetime
data_hora1 = datetime(2023, 5, 16, 14, 30, 45)
data_hora2 = datetime(2023, 5, 17, 14, 30, 45)

# Comparar os objetos datetime
print("data_hora1 < data_hora2:", data_hora1 < data_hora2)
print("data_hora1 > data_hora2:", data_hora1 > data_hora2)
print("data_hora1 == data_hora2:", data_hora1 == data_hora2)
```