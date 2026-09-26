# Week 09–10: Spark Sprint — Part 1 Reflections

## Introduction

The first part of the Spark Sprint has been one of the most practically significant stages of my Data Engineering learning journey so far.

Before this sprint, I understood the general idea of big data and distributed processing, but working through Apache Spark helped me begin connecting those concepts to actual data-engineering workflows.

The most important lesson for me was that data engineering is not only about writing code. It also requires understanding the systems around the code, including databases, operating systems, containers, networking, drivers, and data-processing engines.

---

## What I Learned

### Understanding the Need for Distributed Processing

I gained a clearer understanding of why traditional data-processing approaches can struggle as datasets grow in size and complexity.

The concepts of volume, velocity, and variety helped me understand why distributed systems are necessary for modern data workloads.

This provided the foundation for understanding why technologies such as Hadoop and Spark exist.

### Understanding Spark

Learning about Spark Core, Spark SQL, Structured Streaming, MLlib, and GraphX helped me understand that Spark is more than simply a tool for running Python code against large datasets.

I began to see Spark as a broader distributed data-processing platform with different APIs designed for different types of workloads.

### Working with DataFrames

The practical DataFrame exercises helped me become more comfortable with operations such as:

* Selecting columns
* Filtering records
* Adding and removing columns
* Aggregating data
* Joining datasets
* Using window functions
* Working with complex data types

These operations also helped me understand the importance of thinking in terms of transformations and distributed processing rather than simply manipulating data row by row.

---

## My Experience with Spark SQL

Spark SQL was particularly useful because it allowed me to use familiar SQL concepts while working with Spark datasets.

Working with arrays, maps, aggregations, and other SQL functions helped me understand that Spark SQL can be used for more than simple `SELECT` statements.

It also reinforced the importance of understanding both SQL and DataFrame APIs as a data engineer.

---

## Learning About UDFs

The UDF exercises helped me understand how custom Python logic can be introduced into Spark processing.

At the same time, I learned that custom UDFs should be used carefully because Spark's native functions are generally better optimized for distributed processing.

This helped me begin thinking not only about whether code works, but also about whether it is an appropriate approach for scalable data processing.

---

## My Biggest Practical Learning: JDBC

The JDBC section was especially valuable because I moved from theoretical learning to building an actual connection between Spark and a relational database.

I created a PostgreSQL database inside Docker, connected to it from my WSL-based PySpark environment, read PostgreSQL data into Spark, and then wrote Spark data back into PostgreSQL.

The process demonstrated the complete movement of data between a relational database and Spark.

This was an important step because it made the concept of data pipelines much more concrete.

---

## Troubleshooting Experience

The JDBC exercise initially failed even though the database and Spark configuration appeared correct.

The problem turned out to involve the difference between the environments in which the components were running.

PySpark was running inside WSL2, while PostgreSQL was running in Docker Desktop on Windows.

Using `localhost` from WSL did not point to the Windows host where PostgreSQL was exposed.

I investigated the network configuration, identified the WSL gateway, tested the PostgreSQL port using Python sockets, and eventually established a successful connection.

This experience reinforced an important lesson:

> When a data pipeline fails, the problem may not be in the code itself.

It can be caused by:

* Networking
* Ports
* Drivers
* Authentication
* Containers
* Operating-system boundaries
* Environment configuration

Learning to isolate each part of the system is therefore an important skill.

---

## Challenges I Encountered

Some of the main challenges during this phase included:

1. Understanding how Spark operates across distributed environments.
2. Becoming comfortable with Spark SQL syntax and complex data types.
3. Understanding the role and limitations of UDFs.
4. Configuring the PostgreSQL JDBC driver.
5. Understanding the networking relationship between WSL2, Windows, Docker Desktop, and PostgreSQL.
6. Avoiding interference with the PostgreSQL database already being used by my Airflow environment.

---

## How I Addressed the Challenges

I approached the challenges incrementally rather than changing several components at once.

For the JDBC exercise, I:

1. Created a separate PostgreSQL Docker container for Spark practice.
2. Used a separate database and user.
3. Published PostgreSQL through a dedicated host port.
4. Verified that the PostgreSQL container was running.
5. Tested network connectivity independently of Spark.
6. Identified the WSL gateway.
7. Confirmed that the PostgreSQL port was reachable.
8. Started PySpark with the correct PostgreSQL JDBC driver.
9. Successfully read data from PostgreSQL.
10. Successfully wrote data back to PostgreSQL.
11. Verified the written data directly inside PostgreSQL.

This step-by-step approach made the troubleshooting process much easier to understand.

---

## What I Am Taking Forward

The biggest lesson I am taking into the next phase is the importance of understanding the complete data pipeline rather than focusing only on individual technologies.

A typical pipeline may involve:

```text
Source
  ↓
Database / File System
  ↓
Network
  ↓
JDBC / API / Connector
  ↓
Spark
  ↓
Transformations
  ↓
Output Storage
```

Every component can introduce its own configuration and failure points.

I also want to continue improving my ability to write Spark code that is not only correct but also scalable and efficient.

---

## Looking Ahead

The next part of the Spark journey will build on these foundations.

I expect to deepen my understanding of:

* Spark execution
* Performance optimization
* Partitioning
* Caching
* Shuffling
* Query optimization
* Distributed processing behavior
* Advanced Spark workloads

My goal is to move from simply knowing how to use Spark commands to understanding **why Spark behaves the way it does and how to build efficient data pipelines with it**.

---

## Final Reflection

This phase has strengthened my confidence in working with Apache Spark.

More importantly, the JDBC practical exercise showed me the value of combining multiple technologies into a working data pipeline.

I am beginning to see Data Engineering less as a collection of individual tools and more as the ability to connect those tools together to reliably move, transform, store, and analyze data.
