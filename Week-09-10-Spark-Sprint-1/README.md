# Week 09–10: Spark Sprint — Part 1

## Overview

This phase of my ALX Data Engineering journey focused on the foundations of **Apache Spark** and distributed data processing.

The first part of the Spark Sprint introduced the principles of big data processing, the Hadoop ecosystem, Spark architecture, Spark DataFrames and Structured APIs, Spark SQL, advanced DataFrame operations, User-Defined Functions (UDFs), and connectivity between Spark and relational databases through JDBC.

The learning combined conceptual study, knowledge checks, practical exercises, and hands-on experimentation using **PySpark and PostgreSQL**.

---

## Learning Objectives

By the end of this phase, I aimed to:

* Understand the need for distributed data processing.
* Understand the challenges associated with high-volume, high-velocity, and high-variety data.
* Understand the Hadoop ecosystem and its major components.
* Understand Apache Spark architecture and its major APIs.
* Work with Spark DataFrames and Structured APIs.
* Perform common DataFrame transformations and actions.
* Use Spark SQL to query and manipulate data.
* Work with aggregations, joins, unions, and window functions.
* Understand and use User-Defined Functions (UDFs).
* Understand the role of Pandas UDFs in Spark.
* Understand how Spark connects to relational databases using JDBC.
* Read data from PostgreSQL into Spark.
* Write Spark DataFrames back to PostgreSQL.
* Develop practical troubleshooting skills when working across Windows, WSL2, Docker, PostgreSQL, and PySpark.

---

## Completed Learning Areas

### 1. Introduction to Big Data Processing

Studied the fundamentals of big data processing and why traditional data-processing approaches can become inadequate when dealing with:

* High data volume
* High data velocity
* High data variety

I also reviewed the role of distributed computing in processing large datasets efficiently.

### 2. Hadoop Ecosystem

Reviewed the major components of the Hadoop ecosystem, including:

* HDFS — Hadoop Distributed File System
* YARN — Yet Another Resource Negotiator
* MapReduce
* Hadoop Common

I also explored commonly used big-data processing technologies and compared the general approaches of Hadoop-based processing and Apache Spark.

### 3. Introduction to Apache Spark

Studied the Spark ecosystem and the major components of the Spark API stack:

* Spark Core
* Spark SQL
* Structured Streaming
* MLlib
* GraphX

I also learned about Spark's Structured APIs and the role of DataFrames and Datasets in large-scale data processing.

### 4. Spark Deeper Concepts

Practiced several important Spark DataFrame concepts and operations, including:

* Reading structured data into Spark
* Selecting and projecting columns
* Renaming columns
* Adding columns
* Dropping columns
* Filtering records
* Aggregating data
* Grouping data
* Calculating summary metrics
* Writing processed data to output destinations
* Combining datasets with unions
* Joining datasets
* Using window functions
* Working with Spark SQL
* Working with complex data types
* Using built-in Spark SQL functions
* Creating and using User-Defined Functions

### 5. Spark SQL

Practiced using SQL syntax to query Spark datasets.

I worked with Spark SQL functions and explored operations involving:

* Arrays
* Maps
* Complex data types
* Aggregations
* Filtering
* Data transformation

I also practiced registering and using UDFs.

### 6. User-Defined Functions

Studied how UDFs allow custom Python logic to be applied to Spark data.

A practical example involved creating a function that classified Bitcoin-related values into different messages based on their numerical ranges.

I also learned that UDFs can introduce performance considerations because custom Python execution can be less efficient than Spark's native built-in functions.

---

## JDBC Database Connectivity

A major practical component of this phase was learning how Spark communicates with relational databases through **JDBC (Java Database Connectivity)**.

I learned that Spark requires:

* A JDBC URL
* Database credentials
* A JDBC driver
* The target database/table
* Appropriate connection properties

### JDBC Read Operation

I configured PostgreSQL and successfully read a relational database table into a Spark DataFrame using:

```python
employees_df = spark.read.jdbc(
    url=jdbc_url,
    table="employees",
    properties=connection_properties
)
```

The PostgreSQL `employees` table contained five records, which Spark successfully loaded into a DataFrame.

### JDBC Write Operation

I also created a Spark DataFrame and wrote it back to PostgreSQL:

```python
new_df.write.jdbc(
    url=jdbc_url,
    table="new_employees",
    mode="overwrite",
    properties=connection_properties
)
```

The resulting PostgreSQL table was verified independently using PostgreSQL and contained the expected records.

This demonstrated both directions of JDBC integration:

```text
PostgreSQL
     ↓
   JDBC
     ↓
Spark DataFrame
```

and:

```text
Spark DataFrame
     ↓
   JDBC
     ↓
PostgreSQL
```

---

## Practical Environment

The JDBC practical exercise involved several technologies working together:

* Python
* PySpark
* Apache Spark 4.2.0
* PostgreSQL 13
* PostgreSQL JDBC Driver
* Docker
* Docker Desktop
* WSL2 Ubuntu
* Windows 10

The PostgreSQL database was run in a separate Docker container named `spark-postgres`.

A dedicated PostgreSQL database was created for Spark practice:

```text
Database: sparkdb
User: sparkuser
```

A separate host port was used for the PostgreSQL container to avoid interfering with the PostgreSQL database used by my Airflow environment.

---

## Troubleshooting and Problem Solving

The JDBC exercise also provided practical experience troubleshooting a multi-environment data-engineering setup.

Initially, Spark could not connect to PostgreSQL because PySpark was running inside WSL2 while PostgreSQL was running through Docker Desktop on Windows.

The initial connection used:

```text
localhost:5433
```

but `localhost` from WSL referred to the WSL environment rather than the Windows host.

I identified the WSL default gateway using:

```bash
ip route | grep default
```

The Windows host was reachable through the WSL gateway address.

I then confirmed connectivity using Python's socket library before retrying the Spark JDBC connection.

This resulted in a successful connection using the Windows host/gateway address instead of `localhost`.

This exercise strengthened my understanding of networking between:

```text
Windows
   ↕
WSL2
   ↕
Docker Desktop
   ↕
PostgreSQL
   ↕
JDBC
   ↕
PySpark
```

---

## Key Takeaways

* Distributed processing is important for modern large-scale data workloads.
* Hadoop provides important foundations for distributed storage and processing.
* Apache Spark provides a powerful engine for distributed data processing.
* Spark DataFrames provide a structured way to process large datasets.
* Spark SQL allows familiar SQL syntax to be used with Spark data.
* Built-in Spark functions should generally be preferred where possible for efficient processing.
* UDFs are useful when custom logic is required but can have performance implications.
* JDBC provides a bridge between Spark and relational databases.
* Spark can both read from and write to relational databases.
* Data-engineering problems often involve more than code; networking, containers, operating systems, drivers, and configuration can all affect a pipeline.
* Troubleshooting connectivity issues is an important practical data-engineering skill.

---

## Tools and Technologies

* Apache Spark
* PySpark
* Spark SQL
* Python
* PostgreSQL
* JDBC
* Docker
* Docker Desktop
* WSL2 Ubuntu
* Git & GitHub

---

## Status

**Spark Sprint Part 1 — Weeks 09–10: Completed**

The first part of the Spark Sprint established the conceptual and practical foundation required for more advanced Spark processing, optimization, and data-engineering workflows in the next phase.
