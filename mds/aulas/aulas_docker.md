# pr-5: Construindo Sua Primeira Imagem Docker Personalizada do Spark

Bem-vindo ao quinto módulo deste curso de treinamento! Após executar o Spark em um contêiner Docker (`pr-4.md`), vamos construir uma imagem Docker personalizada baseada em `bitnami/spark:latest`. Criaremos um `Dockerfile` em `src/spark/mod-1/scripts/`, adicionaremos camadas com nossos arquivos de aplicativo (`pr-3-app.py` e `users.json`) e o executaremos. Esta é uma aula simples e passo a passo sobre o GOAT (O Maior de Todos os Tempos) para prepará-lo para sistemas distribuídos!

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
