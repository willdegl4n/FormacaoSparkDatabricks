- [Instalação Local do Spark](#pr-1-instalação-local-do-spark)
  - [Windows](#windows)
  - [macOS](#macos)
  - [Linux (Ubuntu/Debian)](#linux-ubuntudebian)
    
- [Primeiros Passos com o Spark-Shell](#pr-2-primeiros-passos-com-o-spark-shell)
  - [Iniciando o Spark Shell](#iniciando-o-spark-shell)
  - [Comandos básicos](#comandos-básicos)
  - [Exemplos de shell do PySpark](#exemplos-de-shell-do-pyspark)
  - [Trabalhando com dados do projeto](#trabalhando-com-dados-do-projeto)
    
- [Primeiros passos com Spark-Submit](#pr-3-primeiros-passos-com-spark-submit)
  - [O que é Spark-Submit?](#o-que-é-spark-submit)
  - [Etapa 1: Entendendo o aplicativo atualizado](#etapa-1-entendendo-o-aplicativo-atualizado)
  - [Etapa 2: Preparação para a execução](#etapa-2-preparação-para-a-execução)
  - [Etapa 3: Executando com Spark-Submit](#etapa-3-executando-com-spark-submit)
  - [Etapa 4: Explorando Spark-Submit --help](#etapa-4-explorando-spark-submit---help)
  - [Etapa 5: Exercício prático](#etapa-5-exercício-prático)

- [Primeiros passos com Spark e Docker ( *o meu laboratório começa aqui* )](#pr-4-primeiros-passos-com-spark-e-docker--o-meu-lab-começa-aqui-)
  - [Por que o Docker?](#por-que-o-docker)
  - [Etapa 1: Puxe a imagem do Docker](#etapa-1-puxe-a-imagem-do-docker)
  - [Etapa 2: Preparar seus arquivos](#etapa-2-prepare-seus-arquivos)
  - [Etapa 3: executar um contêiner persistente](#etapa-3-executar-um-contêiner-persistente)
  - [Etapa 4: executar Spark-Submit](#etapa-4-execute-spark-submit)
  - [Etapa 5: Personalização com Spark-Submit](#etapa-5-personalização-com-spark-submit)
  - [Etapa 6: Exercício prático](#etapa-6-exercício-prático)
  - [Etapa 7: Para o contêiner](#etapa-7-parar-o-contêiner)

- [Criando sua primeira imagem personalizada do Docker no Spark](#pr-5-criando-sua-primeira-imagem-personalizada-do-docker-no-spark)
  - [Por que criar uma imagem personalizada?](#por-que-criar-uma-imagem-personalizada)
  - [Etapa 1: configure seu Dockerfile](#etapa-1-configure-seu-dockerfile)
  - [Etapa 2: Crie uma imagem personalizada](#etapa-2-crie-a-imagem-personalizada)
  - [Etapa 3: execute sua imagem personalizada](#etapa-3-execute-sua-imagem-personalizada)
  - [Etapa 4: personalize com Spark-Submit](#etapa-3-execute-sua-imagem-personalizada)
  - [Etapa 5: Exercício prático](#etapa-5-exercício-prático-1)
  - [Etapa 6: Pare o contêiner](#etapa-6-pare-o-contêiner)

- [Cluster Spark com implantação do Docker](#pr-6-cluster-spark-com-implantação-do-docker)
  - [Configuração do ambiente](#configuração-do-ambiente)
    1. [Clonando o Repositório](#1-clonando-o-repositório)
    2. [Navegue até o diretório de construção Build](#2-navegue-até-o-diretório-de-construção-build)
    3. [Crie o arquivo .env](#3-crie-o-arquivo-env)
    4. [Crie os diretórios necessários](#4-crie-os-diretórios-necessários)
    5. [Chore imagens do Docker](#5-crie-imagens-do-docker)
    6. [Iniciie o Spark Cluster](#6-inicie-o-spark-cluster)
    7. [Verificar implantação](#7-verificar-implantação)
    8. [Pare o Spark Cluster](#8-pare-o-spark-cluster)
  - [Componentes do Cluster](#componentes-do-cluster)
  - [Acessando Serviços](#acessando-serviços)
  - [Tecnologias Incluídas](#tecnologias-incluídas)
  - [Solução de problemas](#troubleshooting-2)
  - [Arquivos de configuração](#configuration-files)
 
- [Executando seu primeiro aplicativo Spark distribuído com o Docker Compose](#pr-7-executando-seu-primeiro-aplicativo-spark-distribuído-com-o-docker-compose)
  - [Etapa 1: preparar o script do aplicativo](#etapa-1-preparar-o-script-do-aplicativo)
  - [Etapa 2: execute o aplicativo no cluster](#etapa-2-execute-o-aplicativo-no-cluster)
  - [Etapa 3: Monitore o trabalho](#etapa-3-monitore-o-trabalho)
  - [Etapa 4: Exercícios práticos](#etapa-4-exercícios-práticos)
  - [Troubleshooting](#troubleshooting-3)
    

# pr-1: Instalação Local do Spark 

Este guia cobre a instalação do Apache Spark localmente no **Windows**, **macOS** e **Linux**. Siga os passos para o seu sistema operacional para configurar o Spark.

---

## Pré-requisitos

- **Java 8 ou 11**: O Spark requer Java.
- **Python 3.6+**: Para compatibilidade com o PySpark.
- **Terminal**: Prompt de Comando (Windows), Terminal (macOS/Linux).

---

## Windows

### Passo 1: Instalar o Java
1. Baixe o OpenJDK 11 em [AdoptOpenJDK](https://adoptopenjdk.net/) (instalador `.msi`).
2. Execute o instalador.
3. Defina a variável `JAVA_HOME`:
   - Abra "Editar variáveis de ambiente do sistema" no menu Iniciar.
   - Adicione uma nova variável de sistema:
     - Nome: `JAVA_HOME`
     - Valor: `C:\Program Files\AdoptOpenJDK\jdk-11.0.11.9-hotspot` (ajuste o caminho conforme necessário).
   - Edite o `Path`, adicione: `%JAVA_HOME%\bin`.
4. Verifique: Em um novo Prompt de Comando, execute `java -version`.

### Passo 2: Instalar o Python
1. Baixe o Python 3.6+ em [python.org](https://www.python.org/downloads/).
2. Execute o instalador, marcando "Add Python to PATH".
3. Verifique: Em um novo Prompt de Comando, execute `python --version`.

### Passo 3: Instalar o Spark
1. Baixe o Spark 3.5.5 (Hadoop 3.x) em [spark.apache.org](https://spark.apache.org/downloads.html) (arquivo `.tgz`).
2. Extraia para `C:\spark-3.5.5-bin-hadoop3` usando o [7-Zip](https://www.7-zip.org/).
3. Defina a variável `SPARK_HOME`:
   - Adicione uma nova variável de sistema:
     - Nome: `SPARK_HOME`
     - Valor: `C:\spark-3.5.5-bin-hadoop3`.
   - Edite o `Path`, adicione: `%SPARK_HOME%\bin`.
4. Instale o `winutils`:
   - Baixe o `winutils.exe` para Hadoop 3.x deste [repositório no GitHub](https://github.com/cdarlint/winutils).
   - Coloque em `C:\hadoop\bin`.
   - Defina a variável:
     - Nome: `HADOOP_HOME`
     - Valor: `C:\hadoop`.
   - Adicione `%HADOOP_HOME%\bin` ao `Path`.

### Passo 4: Verificar
- Em um novo Prompt de Comando, execute `spark-shell`. Procure pelo logo do Spark. Saia com `:q`.

---

## macOS

### Passo 1: Instalar o Java
1. Instale o Homebrew: `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"` (se ainda não estiver instalado).
2. Execute `brew install openjdk@11`.
3. Defina o `JAVA_HOME`:
   - Adicione ao `~/.zshrc` ou `~/.bash_profile`:
     ```bash
     export JAVA_HOME=$(/usr/libexec/java_home -v 11)
     ```
   - Execute `source ~/.zshrc` (ou o arquivo apropriado).
4. Verifique: Execute `java -version`.

### Passo 2: Instalar o Python
1. Execute `brew install python`.
2. Verifique: Execute `python3 --version`.

### Passo 3: Instalar o Spark
1. Execute `brew install apache-spark` (instala a versão mais recente, por exemplo, 3.5.5).
2. Alternativamente, baixe manualmente:
   - Baixe o Spark 3.5.5 (Hadoop 3.x) em [spark.apache.org](https://spark.apache.org/downloads.html).
   - Extraia: `tar -xzf spark-3.5.5-bin-hadoop3.tgz`.
   - Mova para `/usr/local/spark-3.5.5-bin-hadoop3`.
   - Adicione ao `~/.zshrc`:
     ```bash
     export SPARK_HOME=/usr/local/spark-3.5.5-bin-hadoop3
     export PATH=$SPARK_HOME/bin:$PATH
     ```
   - Execute `source ~/.zshrc`.

### Passo 4: Verificar
- Execute `spark-shell`. Procure pelo logo do Spark. Saia com `:q`.

---

## Linux (Ubuntu/Debian)

### Passo 1: Instalar o Java
1. Atualize os pacotes: `sudo apt update`.
2. Instale: `sudo apt install openjdk-11-jdk`.
3. Defina o `JAVA_HOME`:
   - Adicione ao `~/.bashrc`:
     ```bash
     export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
     export PATH=$JAVA_HOME/bin:$PATH
     ```
   - Execute `source ~/.bashrc`.
4. Verifique: Execute `java -version`.

### Passo 2: Instalar o Python
1. Instale: `sudo apt install python3 python3-pip`.
2. Verifique: Execute `python3 --version`.

### Passo 3: Instalar o Spark
1. Baixe o Spark 3.5.5 (Hadoop 3.x) em [spark.apache.org](https://spark.apache.org/downloads.html):
   ```bash
   wget https://downloads.apache.org/spark/spark-3.5.5/spark-3.5.5-bin-hadoop3.tgz
   tar -xzf spark-3.5.5-bin-hadoop3.tgz
   sudo mv spark-3.5.5-bin-hadoop3 /opt/spark
   ````

2. Definir ambiente:
   - Adicionar à `~/.bashrc`:
     ```bash
     export SPARK_HOME=/opt/spark
     export PATH=$SPARK_HOME/bin:$PATH
     ```
   - Execute `source ~/.bashrc`.

### Etapa 4: Verificar
- Execute `spark-shell`. Procure o logotipo do Spark. Saia com `:q`.

# pr-2: Primeiros Passos com o Spark-Shell

Agora que você instalou o Apache Spark 3.5.5 (veja `pr-1.md`), vamos explorar o Spark Shell—uma poderosa ferramenta interativa para 
executar comandos Spark. Este guia apresenta o shell baseado em Scala (`spark-shell`) e o shell Python (`pyspark`).

---

## Pré-requisitos

- Spark 3.5.5 instalado localmente (Windows, macOS ou Linux).
- Acesso ao terminal: Prompt de Comando (Windows), Terminal (macOS/Linux).
- Opcional: O arquivo `src/spark/mod-1/data/users.json` do projeto para testes.

---

## Iniciando o Spark Shell

### Shell Scala (`spark-shell`)
1. Abra o seu terminal.
2. Execute:
   ```bash
   spark-shell
   ```
3. Você verá um prompt do Python ( `>>>`) com o Spark inicializado. Este é o shell do PySpark.

**Observação** : use `spark-shell` para Scala ou `pyspark` para Python, dependendo da sua preferência. O projeto  `pr-3-app.py` usa Python, então `pyspark` se alinha com isso.

---

## Comandos básicos

### Exemplos de Scala Shell
1. **Verifique a versão do Spark**:
   ```scala
   scala> spark.version
   ```
   Retorno: `"3.5.5"`

2. **Crie um dataset simples**:
   ```scala
   scala> val data = Seq((1, "Alice"), (2, "Bob"))
   scala> val df = spark.createDataFrame(data).toDF("id", "name")
   scala> df.show()
   ```
   Output:
   ```
   +---+-----+
   | id| name|
   +---+-----+
   |  1|Alice|
   |  2|  Bob|
   +---+-----+
   ```

3. **Sair**:
   ```scala
   scala> :q
   ```

### Exemplos de shell do PySpark
1. **Verifique a versão do Spark**:
   ```python
   >>> spark.version
   ```
   Output: `'3.5.5'`

2. **Crie um conjunto de dados simples**:
   ```python
   >>> data = [(1, "Alice"), (2, "Bob")]
   >>> df = spark.createDataFrame(data, ["id", "name"])
   >>> df.show()
   ```
   Output:
   ```
   +---+-----+
   | id| name|
   +---+-----+
   |  1|Alice|
   |  2|  Bob|
   +---+-----+
   ```

3. **Sair**:
   ```python
   >>> exit()
   ```

---

## Trabalhando com dados do projeto

Vamos carregar o `users.json` arquivo do projeto  (`src/spark/mod-1/data/users.json`) para ver o Spark em ação.

1. **Copie o arquivo**:
   - Coloque  `users.json` em um diretório acessível (por exemplo,`C:\spark-data` no Windows, e `/home/user/spark-data` no macOS/Linux).

2. **Carregar no Scala Shell**:
   ```scala
   scala> val df = spark.read.json("C:/spark-data/users.json")  // Windows path
   scala> val df = spark.read.json("/home/user/spark-data/users.json")  // macOS/Linux path
   scala> df.show(1)
   ```
   Output (parcial):
   ```
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   |    delivery_address|city|country|               email|         phone_number|                uuid|  user_id|    user_identifier| dt_current_timestamp|
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   |Sobrado 76 0225 V...|Palmas|   BR|ofelia.barbosa@bo...|(51) 4463-9821|94a1eff2-4dce-c26...|        1|    709.528.582-65|2025-02-05 21:50:...|
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   ```

3. **Carregar no PySpark Shell**:
   ```python
   >>> df = spark.read.json("C:/spark-data/users.json")  # Windows path
   >>> df = spark.read.json("/home/user/spark-data/users.json")  # macOS/Linux path
   >>> df.show(1)
   ```
   Output: Igual ao acima.

4. **Contagem de linhas**:
   - Scala: `df.count()`
   - Python: `df.count()`
   
    Output: `1` (já que `users.json` só tem um registro).

---

## Pontas
- **Caminhos**: use barras (`/`) em caminhos de arquivo, mesmo no Windows, ou escape com barras invertidas (por exemplo, `C:\\spark-data\\users.json`).
- **Erros**: Se você receber um `FileNotFoundException`,verifique novamente o caminho do arquivo.
- **Parar o Spark**: Após sair, o Spark para automaticamente no shell.

---

# pr-3: Primeiros passos com Spark-Submit

Bem-vindo ao terceiro módulo deste curso de treinamento! Depois de instalar o Spark (`pr-1.md`) e explorar o Spark Shell (`pr-2.md`), é hora de dominar `spark-submit` — 
a ferramenta para executar aplicativos Spark como um profissional. Usaremos o script do projeto `pr-3-app.py`,agora atualizado para carregar  `users.json` 
de `scripts/`diretório, e exploraremos as opções `spark-submit`, incluindo insights de `spark-submit --help`. Esta é a aula de Submissão do Spark (GOAT - O Maior de Todos os Tempos) — vamos começar!

---

## Pré-requisitos

- Spark 3.5.5 instalado localmente (veja `pr-1.md`).
- Acesso ao terminal: Prompt de Comando (Windows), Terminal (macOS/Linux).
- Os arquivos do projeto em `src/spark/mod-1/scripts/`:
  - `pr-3-app.py`
  - `users.json` (movido de `data/` para `scripts/`)

---

## O que é Spark-Submit?

`spark-submit`é a ferramenta de linha de comando do Spark para enviar aplicativos a um cluster Spark — ou executá-los localmente, como faremos aqui. É a ponte entre a exploração interativa (Spark Shell) e a execução com script, perfeita para workflow de produção.

---

## Etapa 1: Entendendo o aplicativo atualizado

Ja que `users.json`está em `scripts/`, aqui está a atualização do `pr-3-app.py`:

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .getOrCreate()

df_users = spark.read.json("users.json")  
count = df_users.count()
df_users.show(3)

spark.stop()
```

### Explicação
- **SparkSession**: Inicializa o Spark com o nome "pr-3-app".
- **Leitura de dados**: Carrega  `users.json` do mesmo diretório (`scripts/`) para um DataFrame (`df_users`).
- **Operações **:
  - `count()`: Conta linhas (1 no nosso caso).
  - `show(3)`: Exibe até 3 linhas (mas existe apenas 1).
- **Limpeza **: `spark.stop()` fecha a sessão.

O conteúdo de `users.json` permanece: 

```json
{"user_id":1,"country":"BR","city":"Palmas","phone_number":"(51) 4463-9821","email":"ofelia.barbosa@bol.com.br","uuid":"94a1eff2-4dce-c26e-cea4-3c55b1f8418b","delivery_address":"Sobrado 76 0225 Viela Pérola, Córrego do Bom Jesus, AL 13546-174","user_identifier":"709.528.582-65","dt_current_timestamp":"2025-02-05 21:50:45.932"}
```

---

## Etapa 2: Preparação para a execução

1. **Navegue até o Diretório**:
   - Abra seu terminal e vá para `src/spark/mod-1/scripts/`:
     ```bash
     cd path/to/src/spark/mod-1/scripts
     ```
     Substitua `path/to/` pela localização do seu repositório.

2. **Verificar arquivos**:
   - Confirme que `pr-3-app.py` e `users.json` então em `scripts/`.

3. **Verificar Spark**:
   - execute `spark-submit --version` para garantir que o Spark 3.5.5 esteja pronto.

---

## Etapa 3: Executando com Spark-Submit

### Comando Básico
Execute o script:

```bash
spark-submit pr-3-app.py
```

### O que acontece?
1. O Spark inicia um cluster local.
2. O script é executado:
   - Carrega  `users.json` from `scripts/`.
   - Gera a contagem de linhas (`1`).
   - Exibe o DataFrame.
3. O Spark desliga.

### Output esperada
Após os logs, você verá:

```
1
+--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
|    delivery_address|city|country|               email|         phone_number|                uuid|  user_id|    user_identifier| dt_current_timestamp|
+--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
|Sobrado 76 0225 V...|Palmas|   BR|ofelia.barbosa@bo...|(51) 4463-9821|94a1eff2-4dce-c26...|        1|    709.528.582-65|2025-02-05 21:50:...|
+--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
```

---

## Etapa 4: Explorando Spark-Submit --help

Execute `spark-submit --help` no seu terminal para ver todas as opções. Aqui estão algumas interessantes para discutir:

### Opções de Chaves
1. **`--master`**:
   - Especifica onde executar o aplicativo (por exemplo `local`, uma URL de cluster).
   - Exemplo:
     ```bash
     spark-submit --master local[2] pr-3-app.py
     ```
     - `local[2]`: Executa localmente com 2 núcleos. Teste `local[*]` com todos os núcleos disponíveis.

2. **`--deploy-mode`**:
   - Escolhe onde o driver é executado:  `client` (máquina local) ou `cluster` (em um cluster).
   - Examplo (o local default é `client`):
     ```bash
     spark-submit --deploy-mode client pr-3-app.py
     ```

3. **`--conf`**:
   - Define configurações personalizadas do Spark.
   - Exemplo: limitar a memória e habilitar o registro:
     ```bash
     spark-submit --conf spark.driver.memory=2g --conf spark.eventLog.enabled=true pr-3-app.py
     ```
     - `spark.driver.memory=2g`: Define a memória do driver para 2 GB.
     - `spark.eventLog.enabled=true`: Registra eventos (verifique se `SPARK_HOME/logs` está configurado).

4. **`--py-files`**:
   - Adiciona dependências do Python (por exemplo, `.py` ou arquivos `.zip`).
   - Exemplo: Se `pr-3-app.py` usar um modulo auxiliar `utils.py`:
     ```bash
     spark-submit --py-files utils.py pr-3-app.py
     ```

5. **`--files`**:
   - Carrega arquivos para o diretório de trabalho (útil para dados ou configurações).
   - Exemplo: Se `users.json` estivésse em outro lugar:
     ```bash
     spark-submit --files /path/to/users.json pr-3-app.py
     ```
     - Observação: nosso script que é local assume `users.json`, então isso não é necessário agora.

### Experimente!
Options combinadas:
```bash
spark-submit --master local[4] --name "GOATJob" --conf spark.driver.memory=4g pr-3-app.py
```
- Usa 4 núcleos, nomeia o trabalho "GOATJob" e aloca 4 GB para o driver.

---

## Etapa 5: Exercício prático

Vamos tornar esta aula lendária com uma tarefa prática!

1. **Modifique o script**:
   - Copie `pr-3-app.py` para `pr-3-exercise.py`.
   - Antes, adicione isso: `spark.stop()`:
     ```python
     df_users.select("email", "user_identifier").show()
     ```
   - Salve-o.

2. **Executar com opções**:
   ```bash
   spark-submit --master local[2] --name "UserExtract" pr-3-exercise.py
   ```

3. **Output esperado**:
   - Original `count` e exibe `show(3)`, então:
     ```
     +--------------------+--------------------+
     |               email|    user_identifier|
     +--------------------+--------------------+
     |ofelia.barbosa@bo...|    709.528.582-65|
     +--------------------+--------------------+
     ```

4. **Desafio **:
   - Atualize  `pr-3-exercise.py` para filtrar por `city == "Palmas"` e exibir `email` e `city`. Execute com `--verbose`:
     ```bash
     spark-submit --verbose pr-3-exercise.py
     ```
     - Dica: Use `df_users.filter(df_users.city == "Palmas").select("email", "city").show()`.

---

## Solução de problemas

- **FileNotFoundException**: Confirme se `users.json` está em `scripts/`. Use o caminho absoluto, se necessário (por exemplo: `/path/to/scripts/users.json`).
- **Opções de Erros**: verifique em `spark-submit --help`se a syntaxe está correta.
- **Problemas de recurso**: Se falhar, ajuste o `--driver-memory` (por exemplo: `4g`).

----

# pr-4: Primeiros passos com Spark e Docker ( _o meu lab começa aqui_ )

Bem-vindo ao quarto módulo deste curso de treinamento! Depois de dominar a instalação local do Spark (`pr-1.md`), o Spark Shell (`pr-2.md`), e `spark-submit` (`pr-3.md`),vamos executar o Spark em um contêiner Docker usando `bitnami/spark:latest`. Mapearemos nosso diretorio `src/spark/mod-1/scripts/` (contendo `pr-3-app.py` e `users.json`) para `/app`, definiremos o diretório de trabalho corretamente e manteremos o contêiner em execução para facilitar o acesso. Esta é uma aula de GOAT (Melhor de Todos os Tempos) — vamos acertar!

---

## Pré-requisitos

- **Docker**: instalado e em execução (Windows, macOS ou Linux).
  - Obtenha-o em [docker.com](https://www.docker.com/get-started).
- Acesso ao terminal: Prompt de Comando (Windows), Terminal (macOS/Linux).
- Os arquivos do projeto em `src/spark/mod-1/scripts/`:
  - `pr-3-app.py`
  - `users.json`
- Acesso à Internet para extrair a imagem.

---

## Por que o Docker?

O Docker oferece um ambiente Spark consistente e pré-configurado. Com ele `bitnami/spark:latest`, executaremos seu aplicativo sem complicações de configuração local, garantindo que os arquivos sejam mapeados e acessíveis.

---

## Etapa 1: Puxe a imagem do Docker

1. Abra seu terminal.
2. Baixe a imagem:
   ```bash
   docker pull bitnami/spark:latest
   ```
3. Verifique:
   ```bash
   docker images
   ```
   - Procure `bitnami/spark` com `latest`.

---

## Etapa 2: Prepare seus arquivos

O Script `pr-3-app.py` precisa do `users.json` no mesmo diretorio de trabalho:

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("pr-3-app") \
    .getOrCreate()

df_users = spark.read.json("users.json")  # Relative path
count = df_users.count()
df_users.show(3)

spark.stop()
```

- **Localização**: Certifique-se de que `pr-3-app.py` e `users.json` estão em `src/spark/mod-1/scripts/`.
- **Mapeamento**: Mapearemos isso em `/app` e o definiremos como o diretório de trabalho.

---

## Etapa 3: executar um contêiner persistente

Vamos executar o contêiner em segundo plano com o diretório de trabalho correto:

1. Inicie o contêiner::
   ```bash
   docker run -d --name spark-container --user root -v /absolute/path/to/src/spark/mod-1/scripts:/app -w /app -e HOME=/root bitnami/spark:latest tail -f /dev/null
   ```
   - `-d`: Modo Detached (em background).
   - `--name spark-container`: Nome do container.
   - `--user root`: Execulta como root
   - `-v`: Maps `scripts/` para `/app`.
   - `-w /app`: define `/app` como diretorio de trabalho.
   - `tail -f /dev/null`: mantem tudo funcionando (execultando).
   - Substitua `/absolute/path/to/` pelo seu caminho.

   **Meu comando específico**:
   ```bash
   docker run -d --name spark-container --user root -v /home/willdeglan/frm-spark-databricks-mec/src/spark/mod-1/scripts:/app -w /app -e HOME=/root bitnami/spark:latest tail -f /dev/null
   ```

2. Verifique se está em execução:
   ```bash
   docker ps
   ```
   - Localize `spark-container`.

3. Verifique os arquivos:
   ```bash
   docker exec spark-container ls -la /app
   ```
   - Confirme se o `pr-3-app.py` e `users.json` estão presente.

---

## Etapa 4: execute Spark-Submit

Execute o script no contêiner em execução:

1. Execute:
   ```bash
   docker exec spark-container spark-submit pr-3-app.py
   ```
   - Como o diretório de trabalho é `/app`, o `users.json` é encontrado automaticamente.

2. **Output esperada**:
   ```
   1
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   |    delivery_address|city|country|               email|         phone_number|                uuid|  user_id|    user_identifier| dt_current_timestamp|
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   |Sobrado 76 0225 V...|Palmas|   BR|ofelia.barbosa@bo...|(51) 4463-9821|94a1eff2-4dce-c26...|        1|    709.528.582-65|2025-02-05 21:50:...|
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   ```

---

## Etapa 5: Personalização com Spark-Submit

Adicione opções do contêiner em execução:

1. **definição do Master**:
   ```bash
   docker exec spark-container spark-submit --master local[2] pr-3-app.py
   ```

2. **Configurações adicionais**:
   ```bash
   docker exec spark-container spark-submit --conf spark.driver.memory=2g pr-3-app.py
   ```

3. **Modo Verbose**:
   ```bash
   docker exec spark-container spark-submit --verbose pr-3-app.py
   ```

---

## Etapa 6: Exercício prático

1. **Novo Script**:
   - Copiar `pr-3-app.py` para `pr-4-exercise.py` dentro de `scripts/`.
   - Adicionar antes `spark.stop()`:
     ```python
     df_users.select("city", "phone_number").show()
     ```

2. **Execute-o**:
   ```bash
   docker exec spark-container spark-submit pr-4-exercise.py
   ```

3. **Output esperado**:
   - Output original, então:
     ```
     +------+--------------------+
     |  city|        phone_number|
     +------+--------------------+
     |Palmas|    (51) 4463-9821|
     +------+--------------------+
     ```

4. **Desafio**:
   - Modifique `pr-4-exercise.py` para filtrar `country == "BR"` e exibir `email`. Execute:
     ```bash
     docker exec spark-container spark-submit --master local[4] pr-4-exercise.py
     ```
     - Hint: `df_users.filter(df_users.country == "BR").select("email").show()`.

---

## Etapa 7: Parar o contêiner

Quando terminar:
```bash
docker stop spark-container
docker rm spark-container
```
`stop`: para 
`rm`: apaga

---

## Troubleshooting

- **Erro de caminho não encontrado**:
  - **Verifique o mapeamento**:
    ```bash
    docker exec spark-container ls -la /app
    ```
    - Se vazio, verifique o caminho local:
      ```bash
      ls -la /home/willdeglan/frm-spark-databricks-mec/src/spark/mod-1/scripts
      ```
  - **Permissões do Docker (macOS)**:
    - Docker Desktop > Settings > Resources > File Sharing.
    - Adicione `/home/willdeglan/` e reinicie o Docker.
      
- **Container saiu**:
  - verifique com `docker ps -a`. Reinicie com:
    ```bash
    docker start spark-container
    ```
- **Diretório errado**: a flag `-w /app` garante que o `users.json` está no diretorio de trabalho.



# pr-5: Criando sua primeira imagem personalizada do Docker no Spark

Bem-vindo ao quinto módulo deste curso de treinamento! Após executar o Spark em um contêiner Docker (`pr-4.md`), vamos criar uma imagem Docker personalizada baseada em `bitnami/spark:latest`. Criamos um `Dockerfile` em `src/spark/mod-1/scripts/`,  adicionaremos camadas com nossos arquivos de aplicativo (`pr-3-app.py` e `users.json`), e o executaremos. Esta é uma aula simples e passo a passo sobre o GOAT (o Maior de Todos os Tempos) para prepará-lo para sistemas distribuídos!



---

## Pré-requisitos

- **Docker**: instalado e em execução (Windows, macOS ou Linux).
	- Obtenha-o em [docker.com](https://www.docker.com/get-started).
- Acesso ao terminal: Prompt de Comando (Windows), Terminal (macOS/Linux).
- Os arquivos do projeto estão em `src/spark/mod-1/scripts/`:
  - `pr-3-app.py`
  - `users.json`
- Acesso à Internet para baixar `bitnami/spark:latest`.

---

## Por que criar uma imagem personalizada?

Uma imagem personalizada empacota seu aplicativo com o Spark, garantindo portabilidade e consistência. Ao colocar o  `Dockerfile` em `scripts/`, simplificaremos a inclusão de arquivos e criaremos uma imagem reutilizável.

---

## Etapa 1: configure seu Dockerfile

1. **Navegue até Scripts**:
   - Vá para  `src/spark/mod-1/scripts/`:
     ```bash
     cd /home/willdeglan/frm-spark-databricks-mec/src/spark/mod-1/scripts/
     ```

2. **Verificar arquivos**:
   - Verifique o diretório:
     ```bash
     ls -la
     ```
   - Garantir que `pr-3-app.py` e `users.json` estão no diretorio.

3. **Crie o Dockerfile**:
   - Crie o `Dockerfile` com:
     ```Dockerfile
     # Base image
     FROM bitnami/spark:latest

     # Set working directory
     WORKDIR /app

     # Copy application files from current directory
     COPY pr-3-app.py /app/
     COPY users.json /app/

     # Install a simple dependency (optional)
     RUN pip install --no-cache-dir numpy

     # Keep container running
     CMD ["tail", "-f", "/dev/null"]
     ```
   - **Notas**:
     - `COPY pr-3-app.py /app/`: Copia de `scripts/` (contexto de constuçao (build)) para `/app`.
     - Não há caminhos complexos, pois os arquivos são locais no `Dockerfile`.

---

## Etapa 2: Crie a imagem personalizada

1. **Construir a imagem (Build)**:
   - De `src/spark/mod-1/scripts/`:
     ```bash
     docker build -t my-spark-app:latest .
     ```
   - `-t my-spark-app:latest`: nomeia a imagem.
   - `.`: usa `scripts/` como contexto de construção.

2. **Verify**:
   ```bash
   docker images
   ```
   - procurar por `my-spark-app:latest`.

---

## Etapa 3: execute sua imagem personalizada

1. **Inicie o contêiner**:
   ```bash
   docker run -d --name my-spark-container my-spark-app:latest
   ```

2. **Verificar arquivos**:
   ```bash
   docker exec my-spark-container ls -la /app
   ```
   - Confirme `pr-3-app.py` e `users.json`.

3. **Execute Spark-Submit**:
   ```bash
   docker exec my-spark-container spark-submit pr-3-app.py
   ```

4. **Output esperado**:
   ```
   1
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   |    delivery_address|city|country|               email|         phone_number|                uuid|  user_id|    user_identifier| dt_current_timestamp|
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   |Sobrado 76 0225 V...|Palmas|   BR|ofelia.barbosa@bo...|(51) 4463-9821|94a1eff2-4dce-c26...|        1|    709.528.582-65|2025-02-05 21:50:...|
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   ```

---

## Etapa 4: personalize com Spark-Submit

1. **Definir o Master**:
   ```bash
   docker exec my-spark-container spark-submit --master local[2] pr-3-app.py
   ```

2. **Modo Verbose**:
   ```bash
   docker exec my-spark-container spark-submit --verbose pr-3-app.py
   ```

---

## Etapa 5: Exercício prático

1. **Novo Script**:
   - em `scripts/`, crie `pr-5-exercise.py`:
     ```python
     from pyspark.sql import SparkSession

     spark = SparkSession.builder \
         .appName("pr-5-exercise") \
         .getOrCreate()

     df_users = spark.read.json("users.json")
     df_users.select("email", "city").show()

     spark.stop()
     ```

2. **Atualização do Dockerfile**:
   ```Dockerfile
   FROM bitnami/spark:latest
   WORKDIR /app
   COPY pr-3-app.py /app/
   COPY users.json /app/
   COPY pr-5-exercise.py /app/
   RUN pip install --no-cache-dir numpy
   CMD ["tail", "-f", "/dev/null"]
   ```

3. **Rebuild**:
   ```bash
   docker build -t my-spark-app:latest .
   ```

4. **Run It**:
   - Parar e remover:
     ```bash
     docker stop my-spark-container
     docker rm my-spark-container
     ```
   - Iniciar :
     ```bash
     docker run -d --name my-spark-container my-spark-app:latest
     ```
   - Executar:
     ```bash
     docker exec my-spark-container spark-submit pr-5-exercise.py
     ```

5. **Output esperado**:
   ```
   +--------------------+------+
   |               email|  city|
   +--------------------+------+
   |ofelia.barbosa@bo...|Palmas|
   +--------------------+------+
   ```

6. **Desafio**:
   - adicione `RUN pip install pandas` ao `Dockerfile`, rebuilda, e re-execute o `pr-5-exercise.py`.

---

## Etapa 6: Pare o contêiner

```bash
docker stop my-spark-container
docker rm my-spark-container
```

---

## Troubleshooting

- **Erro de CÓPIA**:
  - Verificar arquivos:
    ```bash
    ls -la /home/willdeglan/frm-spark-databricks-mec/src/spark/mod-1/scripts/
    ```
  - Garanta que `pr-3-app.py` e `users.json` esteja em `scripts/`.
    
- **Problemas de permissão (macOS)**:
  - Docker Desktop > Settings > Resources > File Sharing > Add `/Users/luanmorenomaciel/GitHub/`.
- **Falhas de Build**:
  - Adicione `--no-cache` se necessário:
    ```bash
    docker build -t my-spark-app:latest --no-cache .
    ```

----

# pr-6: Cluster Spark com implantação do Docker

## Pré-requisitos
- Docker
- Docker Compose
- Git

## Configuração do ambiente

### 1. Clonando o Repositório
```bash
git clone https://github.com/owshq-mec/frm-spark-databricks-mec.git
cd /home/willdeglan/github/frm-spark-databricks-mec/
```

### 2. Navegue até o diretório de construção Build 
```bash
cd build
```

### 3. Crie o arquivo .env
Crie um arquivo `.env` no diretório build com o seguinte conteúdo:
```bash
APP_SRC_PATH=/home/willdeglan/github/frm-spark-databricks-mec/src
APP_STORAGE_PATH=/home/willdeglan/github/frm-spark-databricks-mec/storage
APP_LOG_PATH=/home/willdeglan/github/frm-spark-databricks-mec/build/logs
APP_METRICS_PATH=/home/willdeglan/github/frm-spark-databricks-mec/build/metrics
```

**Nota:** Substitua `/home/willdeglan/github/frm-spark-databricks-mec/` pelo caminho completo para o diretório do seu projeto.

### 4. Crie os diretórios necessários
```bash
mkdir -p src storage logs metrics
```

### 5. Crie imagens do Docker
```bash
docker build -t owshq-spark:3.5 -f Dockerfile.spark .
docker build -t owshq-spark-history-server:3.5 -f Dockerfile.history .
```

### 6. Inicie o Spark Cluster
```bash
docker-compose up -d
```

### 7. Verificar implantação
```bash
docker ps

docker logs spark-master
docker logs spark-worker-1
docker logs spark-worker-2
docker logs spark-history-server
```

### 8. Pare o Spark Cluster
```bash
docker-compose down
```

## Componentes do Cluster
- **Spark Master**: roda na porta 8080
- **Spark Workers**: 3 workers configurado
- **Spark History Server**: executado na porta 18080

## Acessando Serviços
- Interface (UI) do Spark Master: http://localhost:8080
- Servidor de histórico do Spark: http://localhost:18080

## Tecnologias Incluídas
- Spark 3.5.0
- Python 3
- PySpark
- Pandas
- Delta Lake
- Apache Arrow

## Troubleshooting
- Ensure all paths in `.env` are absolute and correct
- Check Docker and Docker Compose versions
- Verify network ports are not in use by other services

## Configuration Files
- `docker-compose.yml`: Define o cluster Spark de multi-container
- `Dockerfile.spark`: Builda (cria) a imagem base do Spark
- `Dockerfile.history`: Builda (cria) a imagem do Spark History Server
- `config/spark/spark-defaults.conf`: Configuração do Spark
- `config/spark/log4j2.properties`: Configuração de registro

----

# pr-7: Executando seu primeiro aplicativo Spark distribuído com o Docker Compose

Em `pr-6.md`, você configura um cluster Spark distribuído com o Docker Compose. Agora, vamos aproveitar esse cluster para executar uma aplicação PySpark! Esta classe usa `get-users-json.py` em `src/app/` para processar `users.json` em `src/storage/`, executando-o no cluster de fora do Docker. Monitoraremos a tarefa e faremos exercícios práticos para dominar o Spark distribuído.

---

## Pré-requisitos

- **Docker e Docker Compose**: instalados e em execução (Windows, macOS ou Linux).
- **Spark Cluster**: Executando a partir de `pr-6.md`.  Inicie-o a partir de `/build/` se precisar:
  ```bash
  cd /home/willdeglan/github/frm-spark-databricks-mec/build/
  docker compose up -d
  ```
- **Arquivos**:
  - Applicação: `src/app/get-users-json.py`
  - Dados: `src/storage/users.json`
- **Acesso ao terminal**: Prompt de comando (Windows) ou Terminal (macOS/Linux).

---

## Etapa 1: preparar o script do aplicativo

Usaremos o script fornecido, garantindo que ele esteja pronto para o cluster.

1. **Criar o `get-users-json.py`**:
   - Navegue até `src/app/` (crie-o se não existir):
     ```bash
     mkdir -p /home/willdeglan/github/frm-spark-databricks-mec/src/app/
     cd /home/willdeglan/github/frm-spark-databricks-mec/src/app/
     ```
   - Criar `get-users-json.py`:
     ```python
     """
     docker exec -it spark-master /opt/bitnami/spark/bin/spark-submit \
       --master spark://spark-master:7077 \
       --deploy-mode client \
       /opt/bitnami/spark/jobs/app/get-users-json.py
     """

     from pyspark.sql import SparkSession

     spark = SparkSession.builder \
         .getOrCreate()

     df_users = spark.read.json("./storage/users.json")
     count = df_users.count()
     df_users.show(3)

     spark.stop()
     ```
   - **Observação**: O Master não é especificado aqui; `spark-submit` ele o manipulará. A docstring mostra o comando pretendido.

2. **Verificar dados**:
   - Certifique-se de que `users.json` está em `src/storage/`:
     ```bash
     ls -la /home/willdeglan/github/frm-spark-databricks-mec/src/storage/
     ```

---

## Etapa 2: execute o aplicativo no cluster

Executaremos o script de fora do contêiner, visando o mestre do cluster.

1. **Copiar script para cluster**:
   - Para simplificar, copie `get-users-json.py` para `/build/` (mapeado para `/app/` em `pr-6.md`):
     ```bash
     cp /home/willdeglan/github/frm-spark-databricks-mec/src/app/get-users-json.py /home/willdeglan/github/frm-spark-databricks-mec/build/
     ```

2. **Executar `spark-submit`**:
   - Use o comando especificado (ajustado para o caminho):
     ```bash
     docker exec -it spark-master /opt/bitnami/spark/bin/spark-submit \
       --master spark://spark-master:7077 \
       --deploy-mode client \
       /app/get-users-json.py
     ```
     
   - **explicação**:
     - `docker exec -it spark-master`: Executa dentro do container `spark-master`.
     - `/opt/bitnami/spark/bin/spark-submit`: caminho para o `spark-submit`.
     - `--master spark://spark-master:7077`: Conecta-se ao cluster.
     - `--deploy-mode client`: O driver é executado por meio da CLI do contêiner.
     - `/app/get-users-json.py`: Caminho do script no contêiner (mapeado de `/build/`).

3. **Output esperado**:
   - Depois dos logs:
     ```
     +--------------------+----+-----+--------------------+--------------------+--------------------+
     |    delivery_address|city|country|               email|         phone_number|                uuid|
     +--------------------+----+-----+--------------------+--------------------+--------------------+
     |Sobrado 76 0225 V...|Palmas|   BR|ofelia.barbosa@bo...|(51) 4463-9821|94a1eff2-4dce-c26...|
     +--------------------+----+-----+--------------------+--------------------+--------------------+
     ```

---

## Etapa 3: Monitore o trabalho

A interface do usuário da Web do Spark oferece uma janela para o desempenho do seu trabalho distribuído.

1. **Acesse a Interface (IU)**:
   - Abrir `http://localhost:8080` (mapeado de `spark-master:8080` em `pr-6.md`).
   - **Seções principais**:
     - **Workers**: lista os trabalhadores ativos (por exemplo, `spark-worker-1`). Verifique seu status, núcleos e uso de memória.
     - **Aplicativos em execução**: exibe o trabalho se ainda estiver ativo.
     - **Aplicativos concluídos**: Exibe `get-users-json` a pós-execução com um ID de aplicativo (por exemplo, `app-202304...`).

2. **Explorar detalhes**:
   - Clique no ID do aplicativo:
     - **Stages**: divide tarefas (por exemplo, leitura de JSON, contagem de linhas). Verifica a duração e o paralelismo das tarefas.
     - **Executors**: mostra quais trabalhadores executaram tarefas, com métricas como tamanho dos dados de entrada e atividade de embaralhamento.
     - **Environment**: lista as configurações do Spark (por exemplo, URL mestre, configurações de memória).
   - Confirme se as tarefas foram distribuídas (por exemplo, divididas entre os trabalhadores se houver vários ativos).

3. **Por que monitorar**:
   - Identifica gargalos (por exemplo, trabalhadores lentos), verifica a distribuição e auxilia na otimização.

---

## Etapa 4: Exercícios práticos

Vamos aprofundar suas habilidades distribuídas no Spark com três exercícios.

### Exercício 1: Filtrar por país
1. **Modificar o `get-users-json.py`**:
   - Atualizar para filtrar por país:
     ```python
     """
     docker exec -it spark-master /opt/bitnami/spark/bin/spark-submit \
       --master spark://spark-master:7077 \
       --deploy-mode client \
       /opt/bitnami/spark/jobs/app/get-users-json.py
     """

     from pyspark.sql import SparkSession

     spark = SparkSession.builder \
         .getOrCreate()

     df_users = spark.read.json("./storage/users.json")
     df_users.filter(df_users.country == "BR").show()

     spark.stop()
     ```
     
2. **Copiar e executar **:
   ```bash
   cp /home/willdeglan/github/frm-spark-databricks-mec/src/app/get-users-json.py /home/willdeglan/github/frm-spark-databricks-mec/build/
   docker exec -it spark-master /opt/bitnami/spark/bin/spark-submit \
     --master spark://spark-master:7077 \
     --deploy-mode client \
     /app/get-users-json.py
   ```
   
3. **Verificar saída**: mostra apenas linhas com `country = "BR"`.
4. **Monitor**: verifique a interface do usuário para o novo trabalho.

### Exercício 2: Agregar por Cidade
1. **Criar `get-users-by-city.py`**:
   - em `src/app/`:
     ```python
     """
     docker exec -it spark-master /opt/bitnami/spark/bin/spark-submit \
       --master spark://spark-master:7077 \
       --deploy-mode client \
       /opt/bitnami/spark/jobs/app/get-users-by-city.py
     """

     from pyspark.sql import SparkSession

     spark = SparkSession.builder \
         .getOrCreate()

     df_users = spark.read.json("./storage/users.json")
     df_users.groupBy("city").count().show()

     spark.stop()
     ```
2. **Copiar e executar**:
   ```bash
   cp /home/willdeglan/github/frm-spark-databricks-mec/src/app/get-users-by-city.py /home/willdeglan/github/frm-spark-databricks-mec/build/
   docker exec -it spark-master /opt/bitnami/spark/bin/spark-submit \
     --master spark://spark-master:7077 \
     --deploy-mode client \
     /app/get-users-by-city.py
   ```
   
3. **Output esperado**:
   ```
   +------+-----+
   |  city|count|
   +------+-----+
   |Palmas|    1|
   +------+-----+
   ```
   
4. **Monitor**: Verifique a distribuição de tarefas na interface do usuário (UI).

---

## Troubleshooting

- **"Conneção recusada"**:
  - Verifique o status do cluster:
    ```bash
    docker ps
    ```
    
  - Verificações dos logs:
    ```bash
    docker logs spark-master
    ```
    
- **"FileNotFoundException"**:
  - Verifique o `users.json` em `src/storage/` e o mapeamento do volume em `docker-compose.yml`.

- **No Distribution (Sem distribuição)**:
  - Garanta que vários trabalhadores estejam listados na interface do usuário (UI).
 

    # até a proxima


























  
