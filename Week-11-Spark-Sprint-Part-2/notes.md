# Week 11 Technical Notes

## 1. Data Engineering in Spark

Spark provides a collection of APIs that can be used to transform and process structured data.

Common DataFrame operations include:

```python
df.select()
df.filter()
df.groupBy()
df.agg()
df.orderBy()
df.withColumn()
df.withColumnRenamed()
df.drop()
```

These operations form the foundation of many Spark-based ETL and analytical workflows.

---

## 2. Filtering

Filtering selects records that meet a specified condition.

```python
df.filter(df.age > 30)
```

Filtering is useful for reducing a dataset to only the records required by a particular processing step.

---

## 3. Aggregation

Aggregation combines records to calculate summary information.

```python
df.groupBy("department").count()
```

Other common aggregation functions include:

```python
count()
sum()
avg()
min()
max()
```

---

## 4. Data Enrichment

Data enrichment involves adding useful information to an existing dataset.

Enrichment may involve:

* Joining additional datasets
* Creating derived columns
* Mapping existing values
* Adding reference information

---

## 5. Missing-Value Imputation

Spark provides several mechanisms for handling missing data.

Examples include:

```python
df.fillna(...)
df.dropna(...)
```

The correct approach depends on the meaning and importance of the missing values.

---

## 6. Ordering

Spark DataFrames can be explicitly ordered.

```python
df.orderBy("salary")
```

Descending order can be specified using:

```python
df.orderBy(df.salary.desc())
```

Spark does not guarantee a permanent DataFrame row order unless an ordering operation is explicitly applied.

---

## 7. Anonymization and Encryption

Sensitive data may need to be protected before being consumed by other systems.

Common approaches include:

* Anonymization
* Masking
* Hashing
* Encryption
* Pseudonymization

The appropriate method depends on the sensitivity of the information and the intended use of the data.

---

## 8. Typecasting

Spark columns can be converted to different data types.

```python
from pyspark.sql.functions import col

df = df.withColumn(
    "age",
    col("age").cast("integer")
)
```

Correct data types are important for calculations, storage, validation, and downstream processing.

---

## 9. Renaming Columns

Columns can be renamed using:

```python
df.withColumnRenamed(
    "old_name",
    "new_name"
)
```

Clear and consistent naming improves data usability.

---

## 10. Pivoting

Pivoting transforms categorical values into columns.

```python
df.groupBy("department") \
    .pivot("year") \
    .sum("sales")
```

This can be useful for reporting and analytical datasets.

---

# Structured Streaming

## 11. What is Structured Streaming?

Structured Streaming is Spark's streaming-processing engine built around the DataFrame and Structured APIs.

Instead of processing only a fixed dataset, Spark can continuously process incoming data.

---

## 12. Rate Source

For learning and testing, Spark provides a built-in rate source.

```python
streaming_df = spark.readStream \
    .format("rate") \
    .option("rowsPerSecond", 2) \
    .load()
```

The resulting schema is:

```text
root
 |-- timestamp: timestamp
 |-- value: long
```

The `rate` source generates rows continuously.

---

## 13. Streaming Sink

A streaming DataFrame can be written to a sink.

For example, Delta Lake can be used as a sink:

```python
stream_query = streaming_df.writeStream \
    .format("delta") \
    .outputMode("append") \
    .option(
        "checkpointLocation",
        "/path/to/checkpoint"
    ) \
    .start("/path/to/delta_table")
```

---

## 14. Checkpointing

A checkpoint stores information about the progress of a streaming query.

Example:

```text
checkpointLocation
```

is specified when starting the streaming query.

Checkpointing is important because Spark needs to maintain information about what has already been processed.

---

# Delta Lake

## 15. What is Delta Lake?

Delta Lake is a storage layer designed to provide reliability and transaction capabilities for data-lake environments.

It works closely with Apache Spark.

Important Delta Lake capabilities include:

* ACID transactions
* Transaction history
* Updates
* Deletes
* MERGE
* Time travel
* Batch processing
* Streaming integration

---

## 16. Creating a Delta Table

A Spark DataFrame can be written in Delta format:

```python
df.write \
    .format("delta") \
    .mode("overwrite") \
    .save("/path/to/delta_table")
```

---

## 17. Reading a Delta Table

A Delta table can be read using:

```python
delta_df = spark.read \
    .format("delta") \
    .load("/path/to/delta_table")
```

---

## 18. Updating Delta Data

Using `DeltaTable`:

```python
from delta.tables import DeltaTable

delta_table = DeltaTable.forPath(
    spark,
    "/path/to/delta_table"
)
```

An update can then be performed:

```python
delta_table.update(
    condition="name = 'Kabati'",
    set={"role": "'Senior Data Engineer'"}
)
```

---

## 19. Deleting Delta Data

Records can be deleted using:

```python
delta_table.delete(
    "name = 'John'"
)
```

---

## 20. Delta Table History

Delta maintains a transaction history.

```python
delta_table.history().show(
    truncate=False
)
```

The history can show operations such as:

```text
WRITE
UPDATE
DELETE
MERGE
```

This provides visibility into how the table has changed.

---

## 21. Time Travel

Time travel allows an earlier table version to be queried.

```python
version1_df = spark.read \
    .format("delta") \
    .option("versionAsOf", 1) \
    .load("/path/to/delta_table")
```

This does not change the current table.

It simply allows historical data to be queried.

---

## 22. MERGE / UPSERT

Delta Lake supports MERGE operations.

```python
delta_table.alias("target") \
    .merge(
        updates_df.alias("source"),
        "target.id = source.id"
    ) \
    .whenMatchedUpdateAll() \
    .whenNotMatchedInsertAll() \
    .execute()
```

The basic logic is:

```text
If record exists
       ↓
    UPDATE

If record does not exist
       ↓
     INSERT
```

This is commonly called an **UPSERT**.

---

## 23. Delta as a Streaming Sink

Structured Streaming can write directly to Delta:

```python
streaming_df.writeStream \
    .format("delta") \
    .outputMode("append") \
    .option(
        "checkpointLocation",
        "/path/to/checkpoint"
    ) \
    .start("/path/to/delta_table")
```

This allows continuously arriving data to be stored in Delta.

---

## 24. Delta as a Streaming Source

Delta can also be read as a streaming source:

```python
delta_stream_df = spark.readStream \
    .format("delta") \
    .load("/path/to/delta_table")
```

This means Delta can participate in both sides of a streaming architecture.

---

## 25. `availableNow=True`

A streaming query can be configured to process currently available data and then stop:

```python
read_query = delta_stream_df.writeStream \
    .format("console") \
    .outputMode("append") \
    .option("truncate", "false") \
    .option("numRows", 10) \
    .trigger(availableNow=True) \
    .start()
```

This is useful when the goal is to process available data in a controlled manner rather than run a continuous stream indefinitely.

The query status can be checked using:

```python
read_query.isActive
```

A result of:

```text
False
```

means the query is no longer active.

---

# Spark + Delta Architecture

The practical relationship can be summarized as:

```text
             Incoming Data
                  |
                  v
       +----------------------+
       |        Spark         |
       | Structured Streaming |
       +----------+-----------+
                  |
                  v
       +----------------------+
       |     Delta Lake       |
       |                      |
       | Transactions         |
       | Version History      |
       | Updates / Deletes    |
       | MERGE                |
       +----------+-----------+
                  |
          +-------+-------+
          |               |
          v               v
      Batch Read     Stream Read
```

---

# Key Definitions

### Spark

A distributed data-processing engine.

### DataFrame

A distributed collection of structured data organized into named columns.

### Structured Streaming

Spark's engine for processing continuously arriving data using structured APIs.

### Delta Lake

A storage layer that adds transaction and version-management capabilities to data lakes.

### Transaction History

A record of operations performed on a Delta table.

### Time Travel

The ability to query an earlier version of a Delta table.

### MERGE

A Delta operation that can update matching records and insert non-matching records.

### UPSERT

A combination of update and insert behaviour.

### Checkpoint

Persistent information used by Structured Streaming to track processing progress and state.

### `availableNow`

A trigger mode that processes currently available streaming data and then terminates the query.

---

# Week 11 Concept Summary

The major progression from this week's learning can be represented as:

```text
Data Preparation
       ↓
Transformation
       ↓
Aggregation
       ↓
Enrichment
       ↓
Data Quality & Security
       ↓
Structured Streaming
       ↓
Delta Lake
       ↓
Reliable Batch + Streaming Pipelines
```

The key lesson is that modern data engineering involves more than transforming data.

A reliable pipeline must also consider:

* Data quality
* Security
* Scalability
* Storage
* Reliability
* Historical data
* Incremental processing
* Streaming workloads
* Resource management
