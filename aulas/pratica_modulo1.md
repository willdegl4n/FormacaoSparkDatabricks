`Parei a tradução na linha 890`

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

# pr-6: Spark Cluster with Docker Deployment

## Prerequisites
- Docker
- Docker Compose
- Git

## Environment Setup

### 1. Clone the Repository
```bash
git clone <repository-url>
cd <repository-directory>
```

### 2. Navigate to Build Directory
```bash
cd build
```

### 3. Create .env File
Create a `.env` file in the build directory with the following content:
```bash
APP_SRC_PATH=/absolute/path/to/repo/build/src
APP_STORAGE_PATH=/absolute/path/to/repo/build/storage
APP_LOG_PATH=/absolute/path/to/repo/build/logs
APP_METRICS_PATH=/absolute/path/to/repo/build/metrics
```

**Note:** Replace `/absolute/path/to/repo/` with the full path to your project directory.

### 4. Create Required Directories
```bash
mkdir -p src storage logs metrics
```

### 5. Build Docker Images
```bash
docker build -t owshq-spark:3.5 -f Dockerfile.spark .
docker build -t owshq-spark-history-server:3.5 -f Dockerfile.history .
```

### 6. Start Spark Cluster
```bash
docker-compose up -d
```

### 7. Verify Deployment
```bash
docker ps

docker logs spark-master
docker logs spark-worker-1
docker logs spark-worker-2
docker logs spark-history-server
```

### 8. Stop Spark Cluster
```bash
docker-compose down
```

## Cluster Components
- **Spark Master**: Runs on port 8080
- **Spark Workers**: 3 workers configured
- **Spark History Server**: Runs on port 18080

## Accessing Services
- Spark Master UI: http://localhost:8080
- Spark History Server: http://localhost:18080

## Included Technologies
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
- `docker-compose.yml`: Defines the multi-container Spark cluster
- `Dockerfile.spark`: Builds the base Spark image
- `Dockerfile.history`: Builds the Spark History Server image
- `config/spark/spark-defaults.conf`: Spark configuration
- `config/spark/log4j2.properties`: Logging configuration

  
# pr-7: Running Your First Distributed Spark Application with Docker Compose

In `pr-6.md`, you set up a distributed Spark cluster with Docker Compose. Now, let’s harness that cluster to run a PySpark application! This class uses `get-users-json.py` in `src/app/` to process `users.json` from `src/storage/`, executing it on the cluster from outside Docker. We’ll monitor the job and dive into hands-on exercises to master distributed Spark.

---

## Prerequisites

- **Docker and Docker Compose**: Installed and running (Windows, macOS, or Linux).
- **Spark Cluster**: Running from `pr-6.md`. Start it from `/build/` if needed:
  ```bash
  cd /Users/luanmorenomaciel/GitHub/frm-spark-databricks-mec/build/
  docker-compose up -d
  ```
- **Files**:
  - Application: `src/app/get-users-json.py`
  - Data: `src/storage/users.json`
- **Terminal Access**: Command Prompt (Windows) or Terminal (macOS/Linux).

---

## Step 1: Prepare the Application Script

We’ll use your provided script, ensuring it’s ready for the cluster.

1. **Create `get-users-json.py`**:
   - Navigate to `src/app/` (create it if it doesn’t exist):
     ```bash
     mkdir -p /Users/luanmorenomaciel/GitHub/frm-spark-databricks-mec/src/app/
     cd /Users/luanmorenomaciel/GitHub/frm-spark-databricks-mec/src/app/
     ```
   - Create `get-users-json.py`:
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
   - **Note**: The master isn’t specified here; `spark-submit` will handle it. The docstring shows the intended command.

2. **Verify Data**:
   - Ensure `users.json` is in `src/storage/`:
     ```bash
     ls -la /Users/luanmorenomaciel/GitHub/frm-spark-databricks-mec/src/storage/
     ```

---

## Step 2: Run the Application on the Cluster

We’ll execute the script from outside the container, targeting the cluster’s master.

1. **Copy Script to Cluster**:
   - For simplicity, copy `get-users-json.py` to `/build/` (mapped to `/app/` in `pr-6.md`):
     ```bash
     cp /Users/luanmorenomaciel/GitHub/frm-spark-databricks-mec/src/app/get-users-json.py /Users/luanmorenomaciel/GitHub/frm-spark-databricks-mec/build/
     ```

2. **Run `spark-submit`**:
   - Use your specified command (adjusted for path):
     ```bash
     docker exec -it spark-master /opt/bitnami/spark/bin/spark-submit \
       --master spark://spark-master:7077 \
       --deploy-mode client \
       /app/get-users-json.py
     ```
   - **Breakdown**:
     - `docker exec -it spark-master`: Runs inside the `spark-master` container.
     - `/opt/bitnami/spark/bin/spark-submit`: Path to `spark-submit`.
     - `--master spark://spark-master:7077`: Connects to the cluster.
     - `--deploy-mode client`: Driver runs via the container’s CLI.
     - `/app/get-users-json.py`: Script path in the container (mapped from `/build/`).

3. **Expected Output**:
   - After logs:
     ```
     +--------------------+----+-----+--------------------+--------------------+--------------------+
     |    delivery_address|city|country|               email|         phone_number|                uuid|
     +--------------------+----+-----+--------------------+--------------------+--------------------+
     |Sobrado 76 0225 V...|Palmas|   BR|ofelia.barbosa@bo...|(51) 4463-9821|94a1eff2-4dce-c26...|
     +--------------------+----+-----+--------------------+--------------------+--------------------+
     ```

---

## Step 3: Monitor the Job

The Spark Web UI offers a window into your distributed job’s performance.

1. **Access the UI**:
   - Open `http://localhost:8080` (mapped from `spark-master:8080` in `pr-6.md`).
   - **Key Sections**:
     - **Workers**: Lists active workers (e.g., `spark-worker-1`). Check their status, cores, and memory usage.
     - **Running Applications**: Displays the job if still active.
     - **Completed Applications**: Shows `get-users-json` post-run with an Application ID (e.g., `app-202304...`).

2. **Explore Details**:
   - Click the Application ID:
     - **Stages**: Breaks down tasks (e.g., reading JSON, counting rows). Check task durations and parallelism.
     - **Executors**: Shows which workers executed tasks, with metrics like input data size and shuffle activity.
     - **Environment**: Lists Spark configs (e.g., master URL, memory settings).
   - Confirm tasks were distributed (e.g., split across workers if multiple are active).

3. **Why Monitor**:
   - Identifies bottlenecks (e.g., slow workers), verifies distribution, and aids optimization.

---

## Step 4: Hands-On Exercises

Let’s deepen your distributed Spark skills with three exercises.

### Exercise 1: Filter by Country
1. **Modify `get-users-json.py`**:
   - Update to filter by country:
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
2. **Copy and Run**:
   ```bash
   cp /Users/luanmorenomaciel/GitHub/frm-spark-databricks-mec/src/app/get-users-json.py /Users/luanmorenomaciel/GitHub/frm-spark-databricks-mec/build/
   docker exec -it spark-master /opt/bitnami/spark/bin/spark-submit \
     --master spark://spark-master:7077 \
     --deploy-mode client \
     /app/get-users-json.py
   ```
3. **Check Output**: Shows only rows with `country = "BR"`.
4. **Monitor**: Check the UI for the new job.

### Exercise 2: Aggregate by City
1. **Create `get-users-by-city.py`**:
   - In `src/app/`:
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
2. **Copy and Run**:
   ```bash
   cp /Users/luanmorenomaciel/GitHub/frm-spark-databricks-mec/src/app/get-users-by-city.py /Users/luanmorenomaciel/GitHub/frm-spark-databricks-mec/build/
   docker exec -it spark-master /opt/bitnami/spark/bin/spark-submit \
     --master spark://spark-master:7077 \
     --deploy-mode client \
     /app/get-users-by-city.py
   ```
3. **Expected Output**:
   ```
   +------+-----+
   |  city|count|
   +------+-----+
   |Palmas|    1|
   +------+-----+
   ```
4. **Monitor**: Verify task distribution in the UI.

---

## Troubleshooting

- **"Connection Refused"**:
  - Check cluster status:
    ```bash
    docker ps
    ```
  - View logs:
    ```bash
    docker logs spark-master
    ```
- **"FileNotFoundException"**:
  - Verify `users.json` in `src/storage/` and volume mapping in `docker-compose.yml`.
- **No Distribution**:
  - Ensure multiple workers are listed in the UI.


























  
