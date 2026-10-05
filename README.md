# ALX Data Engineering Journey

## Overview

This repository documents my learning journey through the **ALX Data Engineering Programme**, including my notes, practical exercises, projects, reflections, troubleshooting experiences, and key milestones.

The programme covers the core skills required to design, build, orchestrate, optimize, and deploy modern data pipelines and data-processing systems.

I am using this repository to document not only what I learn, but also how I apply the concepts through hands-on projects, practical exercises, experimentation, problem solving, and troubleshooting.

---

## Programme Structure

The programme runs for **15 weeks**, covering foundational concepts, data engineering tools, workflow orchestration, distributed data processing, Spark optimization, and a final capstone project.

### Weekly Progress

| Week        | Focus Area                                                                        | Status         |
| ----------- | --------------------------------------------------------------------------------- | -------------- |
| Week 1      | Professional Foundations                                                          | ✅ Completed    |
| Week 2      | Big Data Architecture                                                             | ✅ Completed    |
| Week 3      | Big Data Fundamentals                                                             | ✅ Completed    |
| Week 4      | Pipeline Orchestration, Airflow Concepts & Hadoop Fundamentals                    | ✅ Completed    |
| Weeks 5–6   | Docker Sprint                                                                     | ✅ Completed    |
| Weeks 7–8   | Apache Airflow Sprint                                                             | ✅ Completed    |
| Weeks 9–10  | Apache Spark Sprint — Part 1                                                      | ✅ Completed    |
| Week 11     | Apache Spark Sprint — Part 2: Data Engineering, Structured Streaming & Delta Lake | ✅ Completed    |
| Week 12     | Apache Spark Optimization                                                         | 🔄 In Progress |
| Weeks 13–15 | Capstone Project & Portfolio Development                                          | ⏳ Pending      |

---

## Repository Structure

```text
ALX-Data-Engineering/

├── README.md
├── Week-01-Foundations/
├── Week-02-Big-Data-Architecture/
├── Week-03-Big-Data-Fundamentals/
├── Week-04-Pipeline-Orchestration/
├── Week-05-06-Docker-Sprint/
├── Week-07-08-Airflow-Sprint/
├── Week-09-10-Spark-Sprint-1/
└── Week-11-Spark-Sprint-2/
```

---

# Completed Learning Areas

## Weeks 1–4: Foundations

Covered the foundational concepts required for a career in data engineering, including:

* Professional foundations
* Data engineering concepts
* Big Data architecture
* Big Data fundamentals
* Data pipelines
* Hadoop ecosystem
* Distributed computing concepts
* Pipeline orchestration concepts

---

## Weeks 5–6: Docker Sprint

Focused on containerization and the use of Docker in data engineering workflows.

Key areas included:

* Docker fundamentals
* Docker images and containers
* Dockerfiles
* Docker Compose
* Container networking
* Persistent storage and volumes
* Running data engineering services in containers
* Troubleshooting Docker environments

---

## Weeks 7–8: Apache Airflow Sprint

Focused on workflow orchestration using **Apache Airflow**.

Key areas included:

* Airflow architecture
* DAGs
* Tasks and operators
* Scheduling
* Dependencies
* Sensors
* Task execution
* Airflow UI
* Docker-based Airflow deployment
* Pipeline orchestration and automation

---

# Weeks 9–10: Apache Spark Sprint — Part 1

Focused on the foundations of distributed data processing using **Apache Spark** and **PySpark**.

Key areas included:

* Big Data processing
* Hadoop ecosystem
* Apache Spark architecture
* Spark DataFrames
* Structured APIs
* Spark SQL
* DataFrame transformations and actions
* Aggregations
* Joins
* Window functions
* Complex data types
* User-Defined Functions (UDFs)
* Pandas UDFs
* JDBC connectivity
* Reading from PostgreSQL using Spark
* Writing Spark DataFrames to PostgreSQL

### Practical Environment

The Spark exercises were completed using:

* Python
* PySpark
* Apache Spark 4.2.0
* PostgreSQL 13
* PostgreSQL JDBC Driver
* Docker
* Docker Desktop
* WSL2 Ubuntu
* Windows

A PostgreSQL database was integrated with Spark through JDBC to practice reading and writing data between Spark and a relational database.

Detailed Spark Sprint Part 1 documentation is available in:

```text
Week-09-10-Spark-Sprint-1/

├── README.md
├── Notes.md
└── Reflections.md
```

---

# Week 11: Apache Spark Sprint — Part 2

Week 11 continued the Spark learning track by moving from the foundational Spark concepts covered in Weeks 9–10 into broader **data-engineering workflows**.

The focus was on data transformation, data quality, security, Structured Streaming, and Delta Lake.

### Key Learning Areas

* Data translation and mapping
* Data filtering
* Aggregation and summarization
* Data enrichment
* Data imputation
* Indexing and ordering
* Anonymization
* Encryption
* Data modelling
* Typecasting
* Formatting
* Column renaming
* Pivoting
* Structured Streaming
* Delta Lake

### Structured Streaming

I explored Spark Structured Streaming and worked with Spark's built-in `rate` source to generate continuously arriving data.

This helped me understand the difference between traditional batch processing and streaming data processing.

I also practiced writing streaming data into Delta Lake.

### Delta Lake

I worked practically with **Delta Lake 4.4.0** alongside **Apache Spark 4.2.0**.

The Delta Lake exercises included:

* Creating Delta tables
* Reading Delta tables
* Updating records
* Deleting records
* Viewing transaction history
* Time travel
* MERGE / UPSERT operations
* Writing streaming data to Delta
* Reading Delta as a streaming source

I also used:

```python
.trigger(availableNow=True)
```

to process currently available streaming data and allow the streaming query to terminate automatically.

### Spark + Delta Architecture

The practical exercises helped me understand how Spark and Delta Lake can work together:

```text
              Data Source
                   |
                   v
        +----------------------+
        |      Apache Spark    |
        | Structured Streaming |
        +----------+-----------+
                   |
                   v
        +----------------------+
        |      Delta Lake      |
        | Reliable Storage     |
        | Version History      |
        | Updates / Deletes    |
        | MERGE / UPSERT       |
        +----------+-----------+
                   |
          +--------+--------+
          |                 |
          v                 v
      Batch Read       Stream Read
```

Detailed Week 11 documentation is available in:

```text
Week-11-Spark-Sprint-2/

├── README.md
├── Notes.md
└── Reflections.md
```

---

# Week 12: Apache Spark Optimization

Week 12 will focus on **Spark Optimization**.

Building on the Spark processing and Structured Streaming foundations from Weeks 9–11, this phase will focus on understanding how Spark applications can be made more efficient, scalable, and resource-conscious.

### Planned Learning Areas

The focus will include concepts such as:

* Spark execution and performance
* Lazy evaluation
* Query execution plans
* Catalyst Optimizer
* Tungsten execution engine
* Partitioning
* Repartitioning
* Coalescing
* Shuffles
* Data skew
* Caching and persistence
* Broadcast joins
* Join optimization
* Serialization
* Memory management
* Spark UI and performance monitoring
* Adaptive Query Execution
* Optimization of Spark transformations and actions

The goal is to understand not only **how to make Spark work**, but also **how to make Spark work efficiently**.

---

# Upcoming Learning

## Week 12: Spark Optimization

The immediate focus is **Spark Optimization**.

This will build directly on the Spark DataFrame, Structured Streaming, and Delta Lake knowledge developed during Weeks 9–11.

The objective is to develop a deeper understanding of what happens inside Spark when a job is executed and how data engineers can identify and resolve performance bottlenecks.

---

## Weeks 13–15: Capstone Project & Portfolio Development

The final phase will focus on applying the knowledge gained throughout the programme to a practical data-engineering capstone project.

Planned areas include:

* End-to-end data pipeline development
* Data ingestion
* Data transformation
* Data quality
* Workflow orchestration
* Data storage
* Distributed data processing
* Pipeline automation
* Documentation
* Testing
* Troubleshooting
* Portfolio development

The capstone will provide an opportunity to bring together the technologies and concepts learned throughout the programme.

---

# Tools & Technologies

The programme and personal projects involve working with a range of data engineering technologies, including:

* Python
* SQL
* PostgreSQL
* Apache Hadoop
* Apache Spark
* PySpark
* Delta Lake
* Apache Airflow
* Docker
* Docker Compose
* Power BI
* Git
* GitHub
* Linux / WSL2
* Jupyter
* Google Colab

---

# Learning Approach

This repository is more than a collection of completed exercises.

It documents the process of learning data engineering through:

* Practical implementation
* Hands-on experimentation
* Problem solving
* Debugging
* Troubleshooting
* Technical documentation
* Reflection on lessons learned
* Building and testing data pipelines
* Understanding why technologies work, not just how to use them

Throughout the programme, I have also documented challenges encountered across different environments, including Windows, WSL2, Docker, PostgreSQL, Apache Airflow, and Apache Spark.

These experiences have helped me develop a more practical understanding of the relationship between code, infrastructure, networking, configuration, and data-processing systems.

---

# Progress

**Current Stage:** Week 11 completed — **Apache Spark Sprint, Part 2**

**Next Stage:** Week 12 — **Apache Spark Optimization**

### Current Journey

```text
Weeks 1–4
Foundations
     ↓
Weeks 5–6
Docker
     ↓
Weeks 7–8
Apache Airflow
     ↓
Weeks 9–10
Spark Sprint — Part 1
     ↓
Week 11
Spark Sprint — Part 2
     ↓
Week 12
Spark Optimization
     ↓
Weeks 13–15
Capstone & Portfolio
```

---

# Author

**Kabati Ishaya**

ALX Data Engineering Programme

GitHub: [Alkabat](https://github.com/Alkabat)
