# Week 09–10: Spark Sprint — Part 1 Technical Notes

## 1. Big Data Processing

### Why Big Data Requires Distributed Processing

Traditional systems can become inefficient when datasets grow significantly in:

* Volume
* Velocity
* Variety

Distributed processing divides work across multiple resources so that large workloads can be processed more efficiently.

---

# 2. Hadoop Ecosystem

Important Hadoop components:

| Component     | Purpose                        |
| ------------- | ------------------------------ |
| HDFS          | Distributed storage            |
| YARN          | Cluster resource management    |
| MapReduce     | Distributed batch processing   |
| Hadoop Common | Shared libraries and utilities |

Hadoop established important foundations for large-scale distributed data processing.

---

# 3. Apache Spark

Apache Spark is a distributed data-processing engine designed for large-scale workloads.

### Major Spark Components

* Spark Core
* Spark SQL
* Structured Streaming
* MLlib
* GraphX

### Structured APIs

The major structured APIs include:

* DataFrames
* Datasets
* Spark SQL

---

# 4. Spark DataFrames

A DataFrame is a distributed collection of data organized into named columns.

Common operations include:

```python
df.select(...)
df.filter(...)
df.withColumn(...)
df.drop(...)
df.groupBy(...)
df.agg(...)
df.join(...)
df.union(...)
```

---

# 5. Spark SQL

A DataFrame can be made available to Spark SQL by creating a temporary view:

```python
df.createOrReplaceTempView("my_table")
```

Then SQL can be executed with:

```python
spark.sql("""
    SELECT *
    FROM my_table
""").show()
```

The `spark.sql()` method returns a Spark DataFrame for SQL queries that produce tabular results.

---

# 6. Complex Data Types

Spark supports complex types such as:

* Arrays
* Maps
* Structs

Examples of useful functions include:

```python
array_sort(...)
array_intersect(...)
array_except(...)
map_from_arrays(...)
cardinality(...)
element_at(...)
```

---

# 7. Aggregations

Common aggregation functions include:

```python
count()
sum()
avg()
min()
max()
```

Example:

```python
df.groupBy("department").count().show()
```

---

# 8. Joins

Spark supports common join types such as:

* Inner join
* Left join
* Right join
* Full outer join
* Cross join

Example:

```python
df1.join(
    df2,
    df1.id == df2.id,
    "inner"
)
```

---

# 9. Window Functions

Window functions allow calculations to be performed across related rows without collapsing the result into a single row per group.

Typical uses include:

* Ranking
* Running totals
* Moving calculations
* Comparing a row with related rows

---

# 10. User-Defined Functions

A UDF allows custom logic to be applied to Spark data.

Example:

```python
from pyspark.sql.types import StringType

def my_function(x):
    return str(x)

udf_function = F.udf(my_function, StringType())
```

UDFs are useful when Spark's built-in functions cannot express the required logic.

However, native Spark functions are generally preferable where possible because Spark can optimize them more effectively.

---

# 11. JDBC

JDBC stands for:

**Java Database Connectivity**

It provides a standard mechanism for applications such as Spark to communicate with relational databases.

Spark can connect through JDBC to databases such as:

* PostgreSQL
* MySQL
* SQL Server
* Oracle

---

# 12. JDBC Requirements

A typical Spark JDBC connection requires:

1. JDBC URL
2. Username
3. Password
4. JDBC driver
5. Target database/table

Example:

```python
jdbc_url = "jdbc:postgresql://host:5432/database"

connection_properties = {
    "user": "username",
    "password": "password",
    "driver": "org.postgresql.Driver"
}
```

---

# 13. PostgreSQL JDBC Driver

For the practical exercise, PySpark was started with:

```bash
pyspark --packages org.postgresql:postgresql:42.7.8
```

This allowed Spark to obtain the PostgreSQL JDBC driver.

---

# 14. Reading from PostgreSQL

Spark can read a JDBC table using:

```python
df = spark.read.jdbc(
    url=jdbc_url,
    table="table_name",
    properties=connection_properties
)
```

Practical example:

```python
employees_df = spark.read.jdbc(
    url=jdbc_url,
    table="employees",
    properties=connection_properties
)
```

The result is a Spark DataFrame.

---

# 15. Writing to PostgreSQL

A Spark DataFrame can be written to a JDBC database using:

```python
df.write.jdbc(
    url=jdbc_url,
    table="table_name",
    mode="overwrite",
    properties=connection_properties
)
```

Practical example:

```python
new_df.write.jdbc(
    url=jdbc_url,
    table="new_employees",
    mode="overwrite",
    properties=connection_properties
)
```

---

# 16. JDBC Practical Environment

The practical JDBC environment consisted of:

```text
Windows 10
    │
    ├── Docker Desktop
    │      └── PostgreSQL 13
    │
    └── WSL2 Ubuntu
           └── Python virtual environment
                  └── PySpark
```

PostgreSQL configuration:

```text
Database: sparkdb
User: sparkuser
Container: spark-postgres
Windows host port: 5433
PostgreSQL container port: 5432
```

---

# 17. WSL2 Networking

Because PySpark was running inside WSL2 and PostgreSQL was running through Docker Desktop on Windows, using:

```text
localhost:5433
```

from WSL did not successfully reach the PostgreSQL service.

The WSL default route was identified using:

```bash
ip route | grep default
```

The gateway was:

```text
172.17.128.1
```

The JDBC URL was therefore configured as:

```python
jdbc_url = "jdbc:postgresql://172.17.128.1:5433/sparkdb"
```

Connectivity was independently tested using Python:

```bash
python -c "import socket; s=socket.socket(); s.settimeout(3); s.connect(('172.17.128.1',5433)); print('SUCCESS: PostgreSQL port 5433 is reachable'); s.close()"
```

---

# 18. PostgreSQL Practice Table

A PostgreSQL table was created:

```sql
CREATE TABLE employees (
    id INTEGER PRIMARY KEY,
    name VARCHAR(50),
    department VARCHAR(50),
    salary INTEGER
);
```

Sample records:

```sql
INSERT INTO employees (id, name, department, salary) VALUES
(1, 'Alice', 'Engineering', 85000),
(2, 'Bob', 'Finance', 72000),
(3, 'Carol', 'Engineering', 91000),
(4, 'David', 'HR', 65000),
(5, 'Eva', 'Finance', 78000);
```

The table was successfully read into Spark using JDBC.

---

# 19. Spark-to-PostgreSQL Write Test

A Spark DataFrame was created:

```python
new_data = [
    (6, "Frank", "IT", 88000),
    (7, "Grace", "Marketing", 76000),
    (8, "Henry", "Engineering", 95000)
]

new_df = spark.createDataFrame(
    new_data,
    ["id", "name", "department", "salary"]
)
```

It was then written to PostgreSQL:

```python
new_df.write.jdbc(
    url=jdbc_url,
    table="new_employees",
    mode="overwrite",
    properties=connection_properties
)
```

The resulting PostgreSQL table was independently verified with:

```sql
SELECT * FROM new_employees;
```

---

# 20. Important JDBC Pattern

### Read

```text
Relational Database
        ↓
   JDBC Driver
        ↓
spark.read.jdbc()
        ↓
 Spark DataFrame
```

### Write

```text
Spark DataFrame
        ↓
df.write.jdbc()
        ↓
   JDBC Driver
        ↓
Relational Database
```

---

# 21. Troubleshooting Checklist

When Spark cannot connect to a JDBC database, check:

### 1. Is the database running?

For Docker:

```powershell
docker ps
```

### 2. Is the port published?

```powershell
docker port spark-postgres
```

Expected:

```text
5432/tcp -> 0.0.0.0:5433
```

### 3. Can the network reach the database?

From WSL:

```bash
python -c "import socket; s=socket.socket(); s.settimeout(3); s.connect(('HOST',5433)); print('SUCCESS'); s.close()"
```

### 4. Is the JDBC driver available?

Start PySpark with:

```bash
pyspark --packages org.postgresql:postgresql:42.7.8
```

### 5. Are the credentials correct?

Verify:

```python
connection_properties = {
    "user": "sparkuser",
    "password": "sparkpass",
    "driver": "org.postgresql.Driver"
}
```

### 6. Is the JDBC URL correct?

Example:

```python
jdbc_url = "jdbc:postgresql://172.17.128.1:5433/sparkdb"
```

---

# 22. Key Commands to Remember

Start PySpark with PostgreSQL JDBC:

```bash
pyspark --packages org.postgresql:postgresql:42.7.8
```

Read a JDBC table:

```python
df = spark.read.jdbc(
    url=jdbc_url,
    table="table_name",
    properties=connection_properties
)
```

Write a DataFrame:

```python
df.write.jdbc(
    url=jdbc_url,
    table="table_name",
    mode="overwrite",
    properties=connection_properties
)
```

Inspect schema:

```python
df.printSchema()
```

Display records:

```python
df.show()
```

Create a temporary SQL view:

```python
df.createOrReplaceTempView("my_table")
```

Run Spark SQL:

```python
spark.sql("""
    SELECT *
    FROM my_table
""").show()
```

---

# 23. Core Lessons

1. Spark is a distributed data-processing engine.
2. DataFrames provide a structured API for distributed data processing.
3. Spark SQL provides SQL-based access to Spark datasets.
4. Spark's built-in functions should generally be preferred over UDFs when they can perform the required operation.
5. JDBC enables Spark to communicate with relational databases.
6. `spark.read.jdbc()` reads database data into Spark.
7. `DataFrame.write.jdbc()` writes Spark data to a database.
8. JDBC connectivity depends on correct drivers, URLs, credentials, ports, and network accessibility.
9. Containerized data services introduce additional networking considerations.
10. Effective troubleshooting requires isolating each layer of the data pipeline.
