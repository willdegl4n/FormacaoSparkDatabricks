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

   2. Set environment:
   - Add to `~/.bashrc`:
     ```bash
     export SPARK_HOME=/opt/spark
     export PATH=$SPARK_HOME/bin:$PATH
     ```
   - Run `source ~/.bashrc`.

### Step 4: Verify
- Run `spark-shell`. Look for the Spark logo. Exit with `:q`.

# pr-2: Primeiros Passos com o Spark-Shell

Agora que você instalou o Apache Spark 3.5.5 (veja `pr-1.md`), vamos explorar o Spark Shell—uma poderosa ferramenta interativa para executar comandos Spark. Este guia apresenta o shell baseado em Scala (`spark-shell`) e o shell Python (`pyspark`).

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
2. You’ll see a Python prompt (`>>>`) with Spark initialized. This is the PySpark shell.

**Note**: Use `spark-shell` for Scala or `pyspark` for Python, depending on your preference. The project’s `pr-3-app.py` uses Python, so `pyspark` aligns with that.

---

## Basic Commands

### Scala Shell Examples
1. **Check Spark Version**:
   ```scala
   scala> spark.version
   ```
   Output: `"3.5.5"`

2. **Create a Simple Dataset**:
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

3. **Exit**:
   ```scala
   scala> :q
   ```

### PySpark Shell Examples
1. **Check Spark Version**:
   ```python
   >>> spark.version
   ```
   Output: `'3.5.5'`

2. **Create a Simple Dataset**:
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

3. **Exit**:
   ```python
   >>> exit()
   ```

---

## Working with Project Data

Let’s load the `users.json` file from the project (`src/spark/mod-1/data/users.json`) to see Spark in action.

1. **Copy the File**:
   - Place `users.json` in an accessible directory (e.g., `C:\spark-data` on Windows, `/home/user/spark-data` on macOS/Linux).

2. **Load in Scala Shell**:
   ```scala
   scala> val df = spark.read.json("C:/spark-data/users.json")  // Windows path
   scala> val df = spark.read.json("/home/user/spark-data/users.json")  // macOS/Linux path
   scala> df.show(1)
   ```
   Output (partial):
   ```
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   |    delivery_address|city|country|               email|         phone_number|                uuid|  user_id|    user_identifier| dt_current_timestamp|
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   |Sobrado 76 0225 V...|Palmas|   BR|ofelia.barbosa@bo...|(51) 4463-9821|94a1eff2-4dce-c26...|        1|    709.528.582-65|2025-02-05 21:50:...|
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   ```

3. **Load in PySpark Shell**:
   ```python
   >>> df = spark.read.json("C:/spark-data/users.json")  # Windows path
   >>> df = spark.read.json("/home/user/spark-data/users.json")  # macOS/Linux path
   >>> df.show(1)
   ```
   Output: Same as above.

4. **Count Rows**:
   - Scala: `df.count()`
   - Python: `df.count()`
   Output: `1` (since `users.json` has one record).

---

## Tips
- **Paths**: Use forward slashes (`/`) in file paths, even on Windows, or escape backslashes (e.g., `C:\\spark-data\\users.json`).
- **Errors**: If you get a `FileNotFoundException`, double-check the file path.
- **Stop Spark**: After exiting, Spark stops automatically in the shell.

# pr-3: First Steps with Spark-Submit

Welcome to the third module of this training course! After installing Spark (`pr-1.md`) and exploring the Spark Shell (`pr-2.md`), it’s time to master `spark-submit`—the tool for running Spark applications like a pro. We’ll use the project’s `pr-3-app.py` script, now updated to load `users.json` from the `scripts/` directory, and dive into `spark-submit` options, including insights from `spark-submit --help`. This is the GOAT (Greatest of All Time) Spark-Submit class—let’s get started!

---

## Prerequisites

- Spark 3.5.5 installed locally (see `pr-1.md`).
- Terminal access: Command Prompt (Windows), Terminal (macOS/Linux).
- The project files in `src/spark/mod-1/scripts/`:
  - `pr-3-app.py`
  - `users.json` (moved from `data/` to `scripts/`)

---

## What is Spark-Submit?

`spark-submit` is Spark’s command-line tool for submitting applications to a Spark cluster—or running them locally, as we’ll do here. It’s the bridge from interactive exploration (Spark Shell) to scripted execution, perfect for production workflows.

---

## Step 1: Understanding the Updated Application

Since `users.json` is now in `scripts/`, here’s the updated `pr-3-app.py`:

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .getOrCreate()

df_users = spark.read.json("users.json")  
count = df_users.count()
df_users.show(3)

spark.stop()
```

### Breakdown
- **SparkSession**: Initializes Spark with the name "pr-3-app".
- **Reading Data**: Loads `users.json` from the same directory (`scripts/`) into a DataFrame (`df_users`).
- **Operations**:
  - `count()`: Counts rows (1 in our case).
  - `show(3)`: Displays up to 3 rows (only 1 exists).
- **Cleanup**: `spark.stop()` closes the session.

The `users.json` content remains:

```json
{"user_id":1,"country":"BR","city":"Palmas","phone_number":"(51) 4463-9821","email":"ofelia.barbosa@bol.com.br","uuid":"94a1eff2-4dce-c26e-cea4-3c55b1f8418b","delivery_address":"Sobrado 76 0225 Viela Pérola, Córrego do Bom Jesus, AL 13546-174","user_identifier":"709.528.582-65","dt_current_timestamp":"2025-02-05 21:50:45.932"}
```

---

## Step 2: Preparing to Run

1. **Navigate to the Directory**:
   - Open your terminal and change to `src/spark/mod-1/scripts/`:
     ```bash
     cd path/to/src/spark/mod-1/scripts
     ```
     Replace `path/to/` with your repo’s location.

2. **Check Files**:
   - Confirm `pr-3-app.py` and `users.json` are both in `scripts/`.

3. **Verify Spark**:
   - Run `spark-submit --version` to ensure Spark 3.5.5 is ready.

---

## Step 3: Running with Spark-Submit

### Basic Command
Execute the script:

```bash
spark-submit pr-3-app.py
```

### What Happens?
1. Spark starts a local cluster.
2. The script runs:
   - Loads `users.json` from `scripts/`.
   - Outputs the row count (`1`).
   - Displays the DataFrame.
3. Spark shuts down.

### Expected Output
After logs, you’ll see:

```
1
+--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
|    delivery_address|city|country|               email|         phone_number|                uuid|  user_id|    user_identifier| dt_current_timestamp|
+--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
|Sobrado 76 0225 V...|Palmas|   BR|ofelia.barbosa@bo...|(51) 4463-9821|94a1eff2-4dce-c26...|        1|    709.528.582-65|2025-02-05 21:50:...|
+--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
```

---

## Step 4: Exploring Spark-Submit --help

Run `spark-submit --help` in your terminal to see all options. Here are some interesting ones to discuss:

### Key Options
1. **`--master`**:
   - Specifies where to run the app (e.g., `local`, a cluster URL).
   - Example:
     ```bash
     spark-submit --master local[2] pr-3-app.py
     ```
     - `local[2]`: Runs locally with 2 cores. Try `local[*]` for all available cores.

2. **`--deploy-mode`**:
   - Chooses where the driver runs: `client` (local machine) or `cluster` (on a cluster).
   - Example (local default is `client`):
     ```bash
     spark-submit --deploy-mode client pr-3-app.py
     ```

3. **`--conf`**:
   - Sets custom Spark configurations.
   - Example: Limit memory and enable logging:
     ```bash
     spark-submit --conf spark.driver.memory=2g --conf spark.eventLog.enabled=true pr-3-app.py
     ```
     - `spark.driver.memory=2g`: Sets driver memory to 2 GB.
     - `spark.eventLog.enabled=true`: Logs events (check `SPARK_HOME/logs` if configured).

4. **`--py-files`**:
   - Adds Python dependencies (e.g., `.py` or `.zip` files).
   - Example: If `pr-3-app.py` used a helper module `utils.py`:
     ```bash
     spark-submit --py-files utils.py pr-3-app.py
     ```

5. **`--files`**:
   - Uploads files to the working directory (useful for data or configs).
   - Example: If `users.json` were elsewhere:
     ```bash
     spark-submit --files /path/to/users.json pr-3-app.py
     ```
     - Note: Our script assumes `users.json` is local, so this isn’t needed now.

### Try It!
Combine options:
```bash
spark-submit --master local[4] --name "GOATJob" --conf spark.driver.memory=4g pr-3-app.py
```
- Uses 4 cores, names the job "GOATJob," and allocates 4 GB to the driver.

---

## Step 5: Hands-On Exercise

Let’s make this class legendary with a practical task!

1. **Modify the Script**:
   - Copy `pr-3-app.py` to `pr-3-exercise.py`.
   - Add this before `spark.stop()`:
     ```python
     df_users.select("email", "user_identifier").show()
     ```
   - Save it.

2. **Run with Options**:
   ```bash
   spark-submit --master local[2] --name "UserExtract" pr-3-exercise.py
   ```

3. **Expected Output**:
   - Original `count` and `show(3)` output, then:
     ```
     +--------------------+--------------------+
     |               email|    user_identifier|
     +--------------------+--------------------+
     |ofelia.barbosa@bo...|    709.528.582-65|
     +--------------------+--------------------+
     ```

4. **Challenge**:
   - Update `pr-3-exercise.py` to filter for `city == "Palmas"` and show `email` and `city`. Run it with `--verbose`:
     ```bash
     spark-submit --verbose pr-3-exercise.py
     ```
     - Hint: Use `df_users.filter(df_users.city == "Palmas").select("email", "city").show()`.

---

## Troubleshooting

- **FileNotFoundException**: Confirm `users.json` is in `scripts/`. Use an absolute path if needed (e.g., `/path/to/scripts/users.json`).
- **Option Errors**: Check `spark-submit --help` for correct syntax.
- **Resource Issues**: Adjust `--driver-memory` (e.g., `4g`) if it fails.


# pr-4: First Steps with Spark & Docker

Welcome to the fourth module of this training course! After mastering local Spark installation (`pr-1.md`), Spark Shell (`pr-2.md`), and `spark-submit` (`pr-3.md`), let’s run Spark in a Docker container using `bitnami/spark:latest`. We’ll map our `src/spark/mod-1/scripts/` directory (containing `pr-3-app.py` and `users.json`) to `/app`, set the working directory correctly, and keep the container running for easy access. This is a GOAT (Greatest of All Time) class—let’s get it right!

---

## Prerequisites

- **Docker**: Installed and running (Windows, macOS, or Linux).
  - Get it from [docker.com](https://www.docker.com/get-started).
- Terminal access: Command Prompt (Windows), Terminal (macOS/Linux).
- The project files in `src/spark/mod-1/scripts/`:
  - `pr-3-app.py`
  - `users.json`
- Internet access to pull the image.

---

## Why Docker?

Docker provides a consistent, pre-configured Spark environment. With `bitnami/spark:latest`, we’ll run your app without local setup hassles, ensuring files are mapped and accessible.

---

## Step 1: Pull the Docker Image

1. Open your terminal.
2. Pull the image:
   ```bash
   docker pull bitnami/spark:latest
   ```
3. Verify:
   ```bash
   docker images
   ```
   - Look for `bitnami/spark` with `latest`.

---

## Step 2: Prepare Your Files

The script `pr-3-app.py` expects `users.json` in its working directory:

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

- **Location**: Ensure `pr-3-app.py` and `users.json` are in `src/spark/mod-1/scripts/`.
- **Mapping**: We’ll map this to `/app` and set it as the working directory.

---

## Step 3: Run a Persistent Container

Let’s run the container in the background with the correct working directory:

1. Start the container:
   ```bash
   docker run -d --name spark-container -v /absolute/path/to/src/spark/mod-1/scripts:/app -w /app bitnami/spark:latest tail -f /dev/null
   ```
   - `-d`: Detached mode (background).
   - `--name spark-container`: Easy reference.
   - `-v`: Maps `scripts/` to `/app`.
   - `-w /app`: Sets `/app` as the working directory.
   - `tail -f /dev/null`: Keeps it running.
   - Replace `/absolute/path/to/` with your path.

   **Your Specific Command**:
   ```bash
   docker run -d --name spark-container -v /Users/luanmorenomaciel/GitHub/frm-spark-databricks-mec/src/spark/mod-1/scripts:/app -w /app bitnami/spark:latest tail -f /dev/null
   ```

2. Verify it’s running:
   ```bash
   docker ps
   ```
   - Look for `spark-container`.

3. Check the files:
   ```bash
   docker exec spark-container ls -la /app
   ```
   - Confirms `pr-3-app.py` and `users.json` are present.

---

## Step 4: Execute Spark-Submit

Run the script in the running container:

1. Execute:
   ```bash
   docker exec spark-container spark-submit pr-3-app.py
   ```
   - Since the working directory is `/app`, `users.json` is found automatically.

2. **Expected Output**:
   ```
   1
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   |    delivery_address|city|country|               email|         phone_number|                uuid|  user_id|    user_identifier| dt_current_timestamp|
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   |Sobrado 76 0225 V...|Palmas|   BR|ofelia.barbosa@bo...|(51) 4463-9821|94a1eff2-4dce-c26...|        1|    709.528.582-65|2025-02-05 21:50:...|
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   ```

---

## Step 5: Customizing with Spark-Submit

Add options from the running container:

1. **Set Master**:
   ```bash
   docker exec spark-container spark-submit --master local[2] pr-3-app.py
   ```

2. **Add Configuration**:
   ```bash
   docker exec spark-container spark-submit --conf spark.driver.memory=2g pr-3-app.py
   ```

3. **Verbose Mode**:
   ```bash
   docker exec spark-container spark-submit --verbose pr-3-app.py
   ```

---

## Step 6: Hands-On Exercise

1. **New Script**:
   - Copy `pr-3-app.py` to `pr-4-exercise.py` in `scripts/`.
   - Add before `spark.stop()`:
     ```python
     df_users.select("city", "phone_number").show()
     ```

2. **Run It**:
   ```bash
   docker exec spark-container spark-submit pr-4-exercise.py
   ```

3. **Expected Output**:
   - Original output, then:
     ```
     +------+--------------------+
     |  city|        phone_number|
     +------+--------------------+
     |Palmas|    (51) 4463-9821|
     +------+--------------------+
     ```

4. **Challenge**:
   - Modify `pr-4-exercise.py` to filter `country == "BR"` and show `email`. Run:
     ```bash
     docker exec spark-container spark-submit --master local[4] pr-4-exercise.py
     ```
     - Hint: `df_users.filter(df_users.country == "BR").select("email").show()`.

---

## Step 7: Stop the Container

When finished:
```bash
docker stop spark-container
docker rm spark-container
```

---

## Troubleshooting

- **Path Not Found Error**:
  - **Check Mapping**:
    ```bash
    docker exec spark-container ls -la /app
    ```
    - If empty, verify the local path:
      ```bash
      ls -la /Users/luanmorenomaciel/GitHub/frm-spark-databricks-mec/src/spark/mod-1/scripts
      ```
  - **Docker Permissions (macOS)**:
    - Docker Desktop > Settings > Resources > File Sharing.
    - Add `/Users/luanmorenomaciel/GitHub/` and restart Docker.
- **Container Exited**:
  - Check `docker ps -a`. Restart with:
    ```bash
    docker start spark-container
    ```
- **Wrong Directory**: The `-w /app` flag ensures `users.json` is in the working directory.



# pr-5: Building Your First Docker Custom Spark Image

Welcome to the fifth module of this training course! After running Spark in a Docker container (`pr-4.md`), let’s build a custom Docker image based on `bitnami/spark:latest`. We’ll create a `Dockerfile` in `src/spark/mod-1/scripts/`, add layers with our app files (`pr-3-app.py` and `users.json`), and run it. This is a simple, step-by-step GOAT (Greatest of All Time) class to prep you for distributed systems next!

---

## Prerequisites

- **Docker**: Installed and running (Windows, macOS, or Linux).
  - Get it from [docker.com](https://www.docker.com/get-started).
- Terminal access: Command Prompt (Windows), Terminal (macOS/Linux).
- The project files in `src/spark/mod-1/scripts/`:
  - `pr-3-app.py`
  - `users.json`
- Internet access to pull `bitnami/spark:latest`.

---

## Why Build a Custom Image?

A custom image packages your app with Spark, ensuring portability and consistency. By placing the `Dockerfile` in `scripts/`, we’ll streamline file inclusion and build a reusable image.

---

## Step 1: Set Up Your Dockerfile

1. **Navigate to Scripts**:
   - Go to `src/spark/mod-1/scripts/`:
     ```bash
     cd /Users/luanmorenomaciel/GitHub/frm-spark-databricks-mec/src/spark/mod-1/scripts/
     ```

2. **Verify Files**:
   - Check the directory:
     ```bash
     ls -la
     ```
   - Ensure `pr-3-app.py` and `users.json` are present.

3. **Create the Dockerfile**:
   - Create `Dockerfile` with:
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
   - **Notes**:
     - `COPY pr-3-app.py /app/`: Copies from `scripts/` (build context) to `/app`.
     - No complex paths since files are local to the `Dockerfile`.

---

## Step 2: Build the Custom Image

1. **Build the Image**:
   - From `src/spark/mod-1/scripts/`:
     ```bash
     docker build -t my-spark-app:latest .
     ```
   - `-t my-spark-app:latest`: Names the image.
   - `.`: Uses `scripts/` as the build context.

2. **Verify**:
   ```bash
   docker images
   ```
   - Look for `my-spark-app:latest`.

---

## Step 3: Run Your Custom Image

1. **Start the Container**:
   ```bash
   docker run -d --name my-spark-container my-spark-app:latest
   ```

2. **Check Files**:
   ```bash
   docker exec my-spark-container ls -la /app
   ```
   - Confirms `pr-3-app.py` and `users.json`.

3. **Run Spark-Submit**:
   ```bash
   docker exec my-spark-container spark-submit pr-3-app.py
   ```

4. **Expected Output**:
   ```
   1
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   |    delivery_address|city|country|               email|         phone_number|                uuid|  user_id|    user_identifier| dt_current_timestamp|
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   |Sobrado 76 0225 V...|Palmas|   BR|ofelia.barbosa@bo...|(51) 4463-9821|94a1eff2-4dce-c26...|        1|    709.528.582-65|2025-02-05 21:50:...|
   +--------------------+----+-----+--------------------+--------------------+--------------------+---------+--------------------+--------------------+
   ```

---

## Step 4: Customize with Spark-Submit

1. **Set Master**:
   ```bash
   docker exec my-spark-container spark-submit --master local[2] pr-3-app.py
   ```

2. **Verbose Mode**:
   ```bash
   docker exec my-spark-container spark-submit --verbose pr-3-app.py
   ```

---

## Step 5: Hands-On Exercise

1. **New Script**:
   - In `scripts/`, create `pr-5-exercise.py`:
     ```python
     from pyspark.sql import SparkSession

     spark = SparkSession.builder \
         .appName("pr-5-exercise") \
         .getOrCreate()

     df_users = spark.read.json("users.json")
     df_users.select("email", "city").show()

     spark.stop()
     ```

2. **Update Dockerfile**:
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
   - Stop and remove:
     ```bash
     docker stop my-spark-container
     docker rm my-spark-container
     ```
   - Start:
     ```bash
     docker run -d --name my-spark-container my-spark-app:latest
     ```
   - Execute:
     ```bash
     docker exec my-spark-container spark-submit pr-5-exercise.py
     ```

5. **Expected Output**:
   ```
   +--------------------+------+
   |               email|  city|
   +--------------------+------+
   |ofelia.barbosa@bo...|Palmas|
   +--------------------+------+
   ```

6. **Challenge**:
   - Add `RUN pip install pandas` to the `Dockerfile`, rebuild, and rerun `pr-5-exercise.py`.

---

## Step 6: Stop the Container

```bash
docker stop my-spark-container
docker rm my-spark-container
```

---

## Troubleshooting

- **COPY Error**:
  - Verify files:
    ```bash
    ls -la /Users/luanmorenomaciel/GitHub/frm-spark-databricks-mec/src/spark/mod-1/scripts/
    ```
  - Ensure `pr-3-app.py` and `users.json` are in `scripts/`.
- **Permission Issues (macOS)**:
  - Docker Desktop > Settings > Resources > File Sharing > Add `/Users/luanmorenomaciel/GitHub/`.
- **Build Fails**:
  - Add `--no-cache` if needed:
    ```bash
    docker build -t my-spark-app:latest --no-cache .
    ```

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


























  
