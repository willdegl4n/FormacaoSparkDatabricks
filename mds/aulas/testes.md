#Arquivo Dockerfile.py original
````bash
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
````


1.
````bash
docker pull bitnami/spark:latest
````

2.
````bash
docker images
````

3.
````bash
docker run -d --name spark-container --user root -v /home/willdeglan/vscode/formacao/frm-spark-databricks-mec/src/spark/mod-1/scripts:/app  -w /app -e HOME=/root bitnami/spark:latest tail -f /dev/null
````

4.
````bash
docker exec spark-container ls -la /app
````

6.
````bash
docker exec spark-container spark-submit pr-3-app.py
````
![image](https://github.com/user-attachments/assets/9bbc8c3b-fbca-4f4d-9936-6a040867c4cc)



## Step 6: Hands-On Exercise (pr-4-exercise.py)
1.
````python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .getOrCreate()

df_users = spark.read.json("users.json")
count = df_users.count()
df_users.select("city", "phone_number").show()
spark.stop()
````

2.
```bash
docker exec spark-container spark-submit pr-4-exercise.py
```

3.
```
+------+--------------------+
|  city|        phone_number|
+------+--------------------+
|Palmas|    (51) 4463-9821|
+------+--------------------+
```
![image](https://github.com/user-attachments/assets/d8cd60c3-c278-4a1f-bb50-28786abe6312)

4. **Desafio**:
- Modifique `pr-4-exercise.py` para filtrar `country == "BR"` e exibir `email`. Execute:
```bash
docker exec spark-container spark-submit --master local[4] pr-4-exercise.py
```

- Dica: `df_users.filter(df_users.country == "BR").select("email").show()`.

![image](https://github.com/user-attachments/assets/ce7fdd89-c534-49cf-8ee9-73544af8c76d)

When finished:
```bash
docker stop spark-container
docker rm spark-container
```

