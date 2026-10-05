# Week 11 Reflections — Spark Sprint Part 2

## Overview

Week 11 continued my Apache Spark journey after establishing the core Spark foundations during Weeks 09–10.

This week shifted my focus from learning the basic Spark ecosystem and DataFrame operations toward applying Spark to broader **data-engineering workflows**, including data preparation, security, streaming, and reliable data-lake storage.

The most significant part of the week was connecting the concepts of **Spark, Structured Streaming, and Delta Lake**.

---

## What I Learned

I strengthened my understanding of the different stages involved in preparing data for downstream use.

The lessons on filtering, aggregation, summarization, enrichment, imputation, indexing, ordering, modelling, typecasting, formatting, renaming, and pivoting showed me that data engineering involves much more than simply moving data from one location to another.

A data engineer must transform raw information into data that is accurate, structured, useful, secure, and suitable for downstream consumers.

The lessons on anonymization and encryption also reinforced the importance of protecting sensitive information throughout the data lifecycle.

---

## Structured Streaming

Structured Streaming was one of the most important concepts I encountered this week.

I learned that Spark can process continuously arriving data using the same structured programming model used for DataFrames.

Working with the Spark `rate` source gave me a simple way to understand streaming data because records were generated continuously.

This helped me appreciate the difference between:

```text
Batch Processing
```

and:

```text
Streaming Processing
```

In batch processing, a defined dataset is processed at a particular point in time.

In streaming processing, new data can continuously enter the processing pipeline.

---

## My Delta Lake Experience

Delta Lake was probably the most valuable practical part of the week.

I moved beyond simply reading and writing data and started working with data versioning and transactional operations.

I created a Delta table and successfully practiced:

* Writing data
* Reading data
* Updating records
* Deleting records
* Viewing transaction history
* Time travel
* MERGE/UPSERT
* Streaming writes
* Streaming reads

The time-travel exercise was particularly useful because it demonstrated that deleting a record from the current table does not mean that its previous version immediately becomes inaccessible.

I was able to query an earlier version of the table and retrieve data that was no longer present in the current version.

This made the concept of data versioning much more concrete for me.

---

## Understanding MERGE

The MERGE exercise also helped me understand a common real-world data-engineering requirement.

Instead of manually checking whether every incoming record already exists, a MERGE operation can compare incoming data with the target table.

Existing records can be updated while new records can be inserted.

This is commonly referred to as an **UPSERT**.

The exercise helped me understand how this pattern can be useful when building pipelines that receive incremental data.

---

## Connecting Streaming and Delta Lake

Another major learning point was seeing that Delta Lake can work on both sides of a streaming pipeline.

I first used Structured Streaming to generate data and write it to Delta.

I then used Delta as a streaming source.

This gave me a practical understanding of a pipeline such as:

```text
Streaming Source
       ↓
     Spark
       ↓
  Delta Lake
       ↓
Streaming Consumer
```

This was an important step because it connected several concepts that I had previously learned separately.

---

## Challenges

One challenge was understanding the behaviour of a continuously running streaming query.

Unlike a normal Spark operation that executes and returns to the prompt, a continuously running streaming query can remain active indefinitely.

During the first experiment, I had to interrupt the running query manually.

Although Spark reported a job-cancellation message after the interruption, I learned that this was a consequence of stopping the active job rather than a failure of Delta Lake.

I then checked the Delta table and confirmed that streaming data had already been successfully written.

For the next experiment, I used:

```python
.trigger(availableNow=True)
```

This allowed the available data to be processed and the streaming query to stop automatically.

---

## Resource Awareness

Working with Spark on my local laptop also reinforced an important practical lesson: distributed data-engineering technologies can still require careful resource management when used locally.

My computer has limited memory compared with a production Spark cluster, so I learned to keep experiments small and controlled.

This is not simply a hardware limitation. It is also a reminder that data engineers must understand the resource requirements of the systems they operate.

---

## Biggest Takeaway

My biggest takeaway from Week 11 is that **Spark is not just a data-processing library; it can form part of a complete data-engineering architecture.**

Spark can transform and process data.

Structured Streaming can process continuously arriving data.

Delta Lake can provide reliable, versioned storage.

Together, they can form the foundation of a modern data pipeline.

The progression from Weeks 09–10 into Week 11 therefore feels significant:

```text
Spark Foundations
       ↓
DataFrame Processing
       ↓
Advanced Data Engineering
       ↓
Structured Streaming
       ↓
Delta Lake
       ↓
Streaming Data Pipelines
```

This week gave me a much clearer picture of how the individual Spark concepts fit together in real data-engineering workflows.

---

## Looking Ahead

With the Spark foundations from Weeks 09–10 and the practical data-engineering concepts from Week 11, I now have a stronger foundation for tackling the next stages of the ALX Data Engineering programme.

My focus going forward will be to continue building practical pipelines while improving my understanding of scalability, reliability, orchestration, and production-oriented data engineering.
