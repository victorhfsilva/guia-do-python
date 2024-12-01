# Configurando Apache Spark no Windows e Google Colab


### **Configurando o Apache Spark no Windows**

#### **Passo 1: Instalar o Java**

1. O Apache Spark requer o Java Development Kit (JDK) 8 ou superior.
2. Verifique se o Java está corretamente instalado:

```bash
java -version
```

#### **Passo 2: Instalar o Python**

1. Baixe e instale o Python na versão 3.6 ou superior [aqui](https://www.python.org/downloads/windows/).
2. Certifique-se de adicionar o Python ao PATH durante a instalação.
3. Verifique a instalação:

```bash
python --version
```

#### **Passo 3: Baixar e Configurar o Apache Spark**

1. Faça o download do Apache Spark [aqui](https://spark.apache.org/downloads.html).  
	    Escolha uma versão estável, como **Spark 3.1.2**, com o tipo de pacote **Pre-built for Apache Hadoop 2.7** ou outra versão disponível.
1. Extraia os arquivos em uma pasta, por exemplo: `C:\spark\spark-3.1.2-bin-hadoop2.7`.
2. Crie variáveis de ambiente no Windows:
    - **SPARK_HOME**: Apontando para a pasta onde o Spark foi extraído (exemplo: `C:\spark\spark-3.1.2-bin-hadoop2.7`).
    - **HADOOP_HOME**: Aponte para `%SPARK_HOME%\hadoop`.
    - **JAVA_HOME**: Aponte para `C:\Program Files\Java\jdk-17` ou a pasta referente a sua versão java.
    - **PYSPARK_PYTHON**: Aponte para `python`
#### **Passo 4: Instalar o `winutils`**

1. Faça o download do `winutils.exe` correspondente à versão Hadoop usada pelo Spark. Por exemplo, para Hadoop 2.7, baixe [aqui](https://github.com/steveloughran/winutils/tree/master/hadoop-2.7.1/bin).
2. Crie a pasta `C:\spark\spark-3.1.2-bin-hadoop2.7\hadoop\bin` e mova o arquivo `winutils.exe` para essa pasta.

#### **Passo 5: Instalar Bibliotecas Python**

1. Instale o `findspark`:
    
    ```bash
    pip install findspark
    ```
    
2. Teste o funcionamento do Spark executando:
    
    ```bash
    cd C:\spark\spark-3.1.2-bin-hadoop2.7
    bin\pyspark
    ```
    

### **Configurando o Apache Spark no Google Colab**

O Google Colab é uma excelente opção para usar o Spark sem precisar configurar ambientes locais complexos.

#### **Configuração do PySpark no Colab**

1. Execute o seguinte código em uma célula do notebook para instalar e configurar o Spark:
    
    ```bash
    # Instalar Java
    !apt-get update -qq
    !apt-get install openjdk-8-jdk-headless -qq > /dev/null
    
    # Baixar o Apache Spark
    !wget -q https://archive.apache.org/dist/spark/spark-3.1.2/spark-3.1.2-bin-hadoop2.7.tgz
    !tar xf spark-3.1.2-bin-hadoop2.7.tgz
    
    # Instalar o findspark
    !pip install -q findspark
    ```
    
2. Configure variáveis de ambiente no Python:
    
    ```python
    import os
    os.environ["JAVA_HOME"] = "/usr/lib/jvm/java-8-openjdk-amd64"
    os.environ["SPARK_HOME"] = "/content/spark-3.1.2-bin-hadoop2.7"
    ```
    


### **Iniciando uma SparkSession**

A **SparkSession** é o ponto de entrada para usar o Spark no modo DataFrame ou Dataset.

#### **Criando uma SparkSession**

Use o código abaixo para iniciar uma SparkSession no Python:

```python
import findspark
findspark.init()

from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .master("local[*]") \  # Utiliza todos os núcleos disponíveis
    .appName("MinhaPrimeiraApp") \
    .getOrCreate()
```

#### **Verificando a SparkSession**

Após criar a SparkSession, você pode verificar se ela está funcionando executando:

```python
spark
```

#### **Exemplo Prático: Criando e Exibindo um DataFrame**

```python
data = [("Alice", 28), ("Bob", 35), ("Cathy", 30)]
columns = ["Name", "Age"]

df = spark.createDataFrame(data, columns)
df.show()
```

