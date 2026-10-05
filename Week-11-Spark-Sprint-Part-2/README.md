# Week 11: Spark Sprint — Part 2

## Overview

This phase of my ALX Data Engineering journey continued the **Apache Spark** learning track, building on the foundations established during Weeks 09–10.

The focus this week was on practical **data engineering in Spark**, including data transformation, filtering, aggregation, enrichment, imputation, indexing, ordering, anonymization, encryption, modelling, typecasting, formatting, renaming, and pivoting.

The sprint also introduced **Structured Streaming** and **Delta Lake**, extending my understanding of Spark from static batch processing into streaming data pipelines and reliable data-lake storage.

The learning combined conceptual study, knowledge checks, practical exercises, and hands-on experimentation using **PySpark, Structured Streaming, and Delta Lake**.

---

## Learning Objectives

By the end of this phase, I aimed to:

* Apply Spark to common data-engineering transformation tasks.
* Translate and map data using Spark.
* Filter, aggregate, and summarize datasets.
* Enrich datasets with additional information.
* Handle missing data through appropriate imputation techniques.
* Index and order data appropriately.
* Understand anonymization and encryption techniques in Spark.
* Model and transform data using appropriate data types.
* Typecast Spark columns.
* Format and rename data for downstream processing.
* Pivot datasets for analytical purposes.
* Understand the fundamentals of Structured Streaming.
* Process continuously arriving data using Spark Structured Streaming.
* Understand the role of Delta Lake in modern data engineering.
* Write streaming data to Delta Lake.
* Read Delta Lake tables as streaming sources.
* Update and delete records in Delta tables.
* Use Delta Lake transaction history.
* Use Delta Lake time travel.
* Perform MERGE/UPSERT operations.
* Understand how Spark, Structured Streaming, and Delta Lake can work together in a data pipeline.

---

## Completed Learning Areas

### 1. Data Engineering in Spark

This week focused on applying Spark to practical data-engineering tasks rather than only learning the underlying Spark APIs.

I worked through operations used to prepare, transform, clean, secure, and restructure data for downstream processing.

The learning covered:

* Data translation and mapping
* Data filtering
* Data aggregation
* Data summarization
* Data enrichment
* Data imputation
* Indexing
* Ordering
* Anonymization
* Encryption
* Data modelling
* Typecasting
* Formatting
* Column renaming
* Data pivoting

These operations demonstrated how Spark can be used to transform raw datasets into structured and analysis-ready data.

---

### 2. Data Translation and Mapping

I studied how Spark can be used to transform and map existing data into new representations.

This involved applying transformation logic to Spark DataFrames and understanding how data can be converted from one form into another as part of an ETL or data-processing workflow.

---

### 3. Filtering, Aggregation, and Summarization

I practiced using Spark to select relevant records and generate summary information.

Filtering allows unwanted records to be removed from a processing pipeline, while grouping and aggregation can be used to generate metrics from large datasets.

Typical Spark operations include:

```python
df.filter(...)
df.groupBy(...)
df.agg(...)
```

These operations are important building blocks for analytical and data-engineering workflows.

---

### 4. Data Enrichment and Imputation

I studied techniques for enriching datasets with additional information and handling missing values.

Spark provides functionality for dealing with missing data, including:

```python
df.fillna(...)
df.dropna(...)
```

The appropriate approach depends on the characteristics of the dataset and the requirements of the data pipeline.

---

### 5. Indexing and Ordering Data

I explored techniques for indexing and ordering Spark data.

Ordering is particularly important when preparing datasets for analytical operations, reporting, ranking, and other downstream processes.

I also reinforced the understanding that Spark DataFrames should not be assumed to have a permanent row order unless an explicit ordering operation is applied.

---

### 6. Anonymization and Encryption

I studied the importance of protecting sensitive information within data-processing pipelines.

The learning covered concepts including:

* Anonymization
* Data masking
* Hashing
* Encryption
* Protection of sensitive information

This reinforced the principle that data engineering involves not only processing and making data available, but also protecting data appropriately.

---

### 7. Modelling, Typecasting, Formatting, and Renaming

I practiced transforming Spark datasets into appropriate structures and data types.

Typecasting can be performed using Spark's `cast()` functionality.

For example:

```python
from pyspark.sql.functions import col

df = df.withColumn(
    "age",
    col("age").cast("integer")
)
```

I also worked with formatting and column-renaming operations to make datasets more consistent and suitable for downstream processing.

---

### 8. Pivoting Data

I studied how Spark can transform categorical values into columns using pivot operations.

A typical pattern is:

```python
df.groupBy("department") \
    .pivot("year") \
    .sum("sales")
```

Pivoting is particularly useful when transforming datasets into structures suitable for reporting and analysis.

---

## Structured Streaming

A major focus of this phase was **Structured Streaming in Spark**.

Structured Streaming extends Spark's DataFrame and Structured API concepts to continuously arriving data.

I worked with Spark's built-in `rate` streaming source:

```python
streaming_df = spark.readStream \
    .format("rate") \
    .option("rowsPerSecond", 2) \
    .load()
```

The streaming DataFrame produced a schema containing:

```text
root
 |-- timestamp: timestamp
 |-- value: long
```

This exercise helped demonstrate the difference between a traditional static DataFrame and a streaming DataFrame.

---

## Streaming Data with Delta Lake

I then connected Structured Streaming with Delta Lake.

The streaming data was written into a Delta table using:

```python
stream_query = streaming_df.writeStream \
    .format("delta") \
    .outputMode("append") \
    .option(
        "checkpointLocation",
        "/home/al_kabatal_kabat/spark-learning/delta_stream_checkpoint"
    ) \
    .start(
        "/home/al_kabatal_kabat/spark-learning/delta_streaming_table"
    )
```

The streaming process generated records continuously and stored them in Delta format.

The resulting Delta table contained more than one thousand records during the practical exercise.

This demonstrated how Structured Streaming can be used to continuously ingest data into a reliable data-lake storage layer.

---

## Delta Lake

I also completed a practical introduction to **Delta Lake**.

For this exercise, I used:

```text
Apache Spark 4.2.0
Delta Lake 4.4.0
```

The modern Delta Lake version was selected because it is compatible with the Spark 4.2.0 environment used for this learning sprint.

I created a Delta table containing employee information:

```text
id
name
role
```

The initial dataset contained:

```text
1 — Kabati — Data Engineer
2 — Aisha  — Data Analyst
3 — John   — Software Engineer
```

---

## Delta Lake Update and Delete Operations

I used the Delta Lake API to update an existing record.

For example, Kabati's role was updated from:

```text
Data Engineer
```

to:

```text
Senior Data Engineer
```

I also used a Delta delete operation to remove John's record.

This demonstrated that Delta tables can support modifications without requiring the entire dataset to be manually recreated.

---

## Delta Lake History

Delta Lake maintains a transaction history of operations performed on a table.

I inspected the table history using:

```python
delta_table.history().show(truncate=False)
```

The history recorded operations including:

```text
WRITE
UPDATE
DELETE
MERGE
```

This provided a practical demonstration of Delta Lake's transaction-log approach to tracking table changes.

---

## Delta Lake Time Travel

I used Delta Lake time travel to access an earlier version of the table.

For example:

```python
version1_df = spark.read \
    .format("delta") \
    .option("versionAsOf", 1) \
    .load(
        "/home/al_kabatal_kabat/spark-learning/delta_employees"
    )
```

The earlier version contained John, even though John had subsequently been deleted from the current version.

This demonstrated that historical versions can be queried without changing the current state of the table.

---

## Delta Lake MERGE / UPSERT

I also practiced Delta Lake `MERGE`.

The source data contained an updated record for Kabati and a new record for Mary.

The MERGE operation was:

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

The result was:

```text
Existing record → Updated
New record      → Inserted
```

This demonstrated the concept of an **UPSERT**, combining update and insert behaviour within one operation.

---

## Delta Lake as a Streaming Source

After writing streaming data into Delta, I demonstrated that Delta can also be used as a streaming source.

The Delta table was read using:

```python
delta_stream_df = spark.readStream \
    .format("delta") \
    .load(
        "/home/al_kabatal_kabat/spark-learning/delta_streaming_table"
    )
```

The schema was:

```text
root
 |-- timestamp: timestamp
 |-- value: long
```

I then used a controlled streaming query with:

```python
.trigger(availableNow=True)
```

This allowed Spark to process the currently available data and terminate automatically rather than leaving a continuously running stream.

The query was verified using:

```python
read_query.isActive
```

which returned:

```text
False
```

This confirmed that the controlled streaming query had completed successfully.

---

## Spark and Delta Architecture

The practical exercises helped me understand the relationship between Spark, Structured Streaming, and Delta Lake.

A simplified representation is:

```text
              Data Source
                   |
                   v
        +----------------------+
        |      Spark /         |
        | Structured Streaming |
        +----------+-----------+
                   |
                   v
        +----------------------+
        |     Delta Lake       |
        | Reliable Data Store  |
        +----------+-----------+
                   |
          +--------+--------+
          |                 |
          v                 v
     Batch Read       Stream Read
```

This demonstrates how Spark can process incoming data while Delta Lake provides a reliable storage layer that can subsequently support both batch and streaming consumption.

---

## Practical Environment

The practical work this week was carried out using:

* Python
* PySpark
* Apache Spark 4.2.0
* Delta Lake 4.4.0
* Structured Streaming
* Spark DataFrames
* WSL2 Ubuntu
* Linux virtual environment

The Spark learning environment was maintained inside WSL2 using a dedicated Python virtual environment.

---

## Troubleshooting and Problem Solving

This phase also provided practical experience with Spark streaming behaviour and resource management.

One important lesson came from working with a continuously running Structured Streaming query.

A streaming query does not automatically return control to the interactive PySpark prompt when it is configured to run continuously.

The query therefore had to be stopped manually during the initial experiment.

This generated a Spark job-cancellation message because the running job was interrupted. The message did not indicate a Delta Lake failure.

I subsequently verified that the streaming query was inactive and inspected the Delta table to confirm that streaming records had been successfully written.

I then used:

```python
.trigger(availableNow=True)
```

for the subsequent streaming-read demonstration.

This provided a more controlled approach for the available computing resources and allowed the query to process existing data and terminate automatically.

---

## Key Takeaways

* Spark provides powerful APIs for transforming and processing structured data.
* Data transformation is a major part of practical data-engineering workflows.
* Filtering, aggregation, enrichment, imputation, ordering, and pivoting are fundamental Spark operations.
* Data security must be considered when processing sensitive information.
* Correct data types and data modelling are important for reliable downstream processing.
* Structured Streaming allows Spark to process continuously arriving data.
* Delta Lake provides a reliable storage layer for data-lake workloads.
* Delta tables support updates and deletes.
* Delta Lake maintains transaction history.
* Time travel makes it possible to query previous versions of a table.
* MERGE can be used to implement UPSERT behaviour.
* Delta Lake can act as both a batch data source and a streaming data source.
* Checkpoints are important for managing streaming progress.
* `availableNow=True` provides a controlled way to process currently available streaming data.
* Resource management is important when running Spark on a limited local environment.
* Modern data-engineering pipelines can combine Spark, Structured Streaming, and Delta Lake.

---

## Tools and Technologies

* Apache Spark 4.2.0
* PySpark
* Spark SQL
* Structured Streaming
* Delta Lake 4.4.0
* Python
* WSL2 Ubuntu
* Git
* GitHub

---

## Status

**Spark Sprint Part 2 — Week 11: Completed**

This phase extended the Spark foundations established during Weeks 09–10 into practical data-engineering workflows.

I progressed from working primarily with static Spark DataFrames and JDBC connectivity into **data transformation, Structured Streaming, and Delta Lake**, gaining practical experience with reliable storage, transaction history, time travel, MERGE operations, and streaming data pipelines.

The next phase of the ALX Data Engineering journey will build on these Spark foundations and introduce further concepts required for scalable and production-oriented data-engineering workflows.
