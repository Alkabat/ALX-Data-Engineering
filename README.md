# ALX Data Engineering Journey

## Overview

This repository documents my learning journey through the **ALX Data Engineering Programme**, including my notes, practical exercises, projects, reflections, and key milestones.

The programme covers the core skills required to design, build, orchestrate, and optimize modern data pipelines and data-processing systems.

I am using this repository to document not only what I learn, but also how I apply the concepts through hands-on projects and troubleshooting.

---

## Programme Structure

The programme runs for **15 weeks**, covering foundational concepts, data engineering tools, workflow orchestration, distributed data processing, and a final capstone project.

### Weekly Progress

| Week        | Focus Area                                                     | Status         |
| ----------- | -------------------------------------------------------------- | -------------- |
| Week 1      | Professional Foundations                                       | ✅ Completed    |
| Week 2      | Big Data Architecture                                          | ✅ Completed    |
| Week 3      | Big Data Fundamentals                                          | ✅ Completed    |
| Week 4      | Pipeline Orchestration, Airflow Concepts & Hadoop Fundamentals | ✅ Completed    |
| Weeks 5–6   | Docker Sprint                                                  | ✅ Completed    |
| Weeks 7–8   | Apache Airflow Sprint                                          | ✅ Completed    |
| Weeks 9–10  | Apache Spark Sprint                                            | 🔄 In Progress |
| Weeks 11–12 | Advanced Data Engineering                                      | ⏳ Pending      |
| Weeks 13–15 | Capstone Project & Portfolio Development                       | ⏳ Pending      |

---

## Repository Structure

```text
ALX-Data-Engineering/
├── Week-01-Foundations/
├── Week-02-Big-Data-Architecture/
├── Week-03-Big-Data-Fundamentals/
├── Week-04-Pipeline-Orchestration/
├── Week-05-06-Docker-Sprint/
├── Week-08-Airflow-Projects-and-Automation/
└── README.md
```

The repository structure will continue to evolve as new sprints and projects are completed.

---

## Current Progress

### 8 / 15 Weeks Completed

I have completed the first eight weeks of the programme and am currently progressing through the **Apache Spark sprint (Weeks 9–10)**.

The journey so far has progressed from foundational data concepts into practical work with Docker, workflow orchestration, and Apache Airflow.

---

# Docker Sprint — Weeks 5–6

The two-week Docker sprint introduced containerization and its application to data engineering workflows.

### Key Skills Practiced

* Docker fundamentals
* Docker images and containers
* Dockerfiles
* Docker Compose
* Container networking
* Persistent volumes
* Service dependencies
* Health checks
* Multi-container applications
* Running data-related services in containers

### Practical Work

I built and worked with containerized applications involving:

* APIs
* Nginx
* PostgreSQL
* Docker Compose
* Persistent storage
* Service health checks

The sprint helped me understand how containerization can provide reproducible environments for data engineering workflows.

---

# Apache Airflow Sprint — Weeks 7–8

The Airflow sprint introduced workflow orchestration and provided hands-on experience designing, testing, debugging, and monitoring automated data pipelines.

## Week 7 — Airflow Orchestration

I learned the fundamentals of Apache Airflow, including:

* DAGs
* Tasks
* Operators
* Dependencies
* Scheduler
* Webserver
* Workers
* Executors
* Metastore
* Airflow Variables
* XCom
* Task testing and monitoring

I also set up Apache Airflow locally using **Docker Compose**.

---

## Week 8 — Airflow Projects & Automation

During Week 8, I built and extended a practical workflow called the **Linda's Kitten Image Workflow**.

### Basic Pipeline

The DAG is named:

```python
basic_airflow_pipeline
```

The initial workflow consisted of:

```text
fetch_kitten_urls
        ↓
get_kitten_images
        ↓
pipeline_notification
```

The pipeline uses the Unsplash API to retrieve kitten image URLs, downloads the images, and reports the number of downloaded images.

### Extended Pipeline

I then extended the workflow by adding a file-writing task:

```text
fetch_kitten_urls
        ↓
get_kitten_images
      ↙             ↘
pipeline_notification    write_results_to_file
```

The new task writes the current number of downloaded kitten images to:

```text
kitten_state.txt
```

During testing, the workflow successfully recorded **8 kitten images**.

### Airflow Skills Demonstrated

* Creating multi-task DAGs
* Using `BashOperator`
* Using `PythonOperator`
* Defining task dependencies
* Creating parallel task branches
* Using Airflow Variables
* Testing individual tasks
* Triggering DAG runs
* Monitoring task states and logs
* Troubleshooting DAG import errors
* Working with Airflow in Docker

The Airflow sprint strengthened my understanding of how data workflows can be automated, monitored, and maintained.

---

# Apache Spark Sprint — Weeks 9–10

The next stage of my learning journey focuses on **Apache Spark and distributed data processing**.

I will be building on the orchestration and data-engineering concepts learned during the Docker and Airflow sprints while developing practical skills with **PySpark**.

### Planned Focus Areas

* Apache Spark architecture
* Distributed computing
* PySpark
* DataFrames
* Spark SQL
* Transformations and actions
* Data processing at scale
* Performance and optimization
* Spark-based data pipelines

---

# Learning Approach

My approach throughout the programme is based on a combination of:

1. **Learning the concepts**
2. **Building practical examples**
3. **Troubleshooting errors**
4. **Documenting the process**
5. **Reflecting on what I learned**
6. **Applying the knowledge to data engineering projects**

I believe that understanding why a technology works is just as important as knowing how to use it.

---

# Key Tools & Technologies

Throughout the programme, I am developing practical experience with:

* Python
* SQL
* Excel
* Power BI
* Git & GitHub
* Linux
* Docker
* Docker Compose
* Apache Airflow
* Apache Spark
* PySpark
* PostgreSQL
* Big Data technologies
* Data pipeline orchestration

---

# Projects & Practical Work

Some of the data engineering projects and exercises I have worked on include:

### Maji Ndogo

A practical data analysis and engineering project involving:

* SQL
* Python
* Power BI
* Data cleaning
* Data transformation
* Data analysis

### Airflow Kitten Image Pipeline

A practical workflow demonstrating:

* API interaction
* Airflow DAGs
* BashOperator
* PythonOperator
* Airflow Variables
* Task dependencies
* Parallel task execution
* File output

### Docker Projects

Hands-on containerization exercises involving:

* API services
* Nginx
* PostgreSQL
* Docker Compose
* Persistent volumes
* Service health checks

---

# What I Am Building

The ultimate goal of this journey is to develop the skills required to build reliable, scalable, and maintainable data pipelines.

I am particularly interested in developing practical experience in:

```text
Data Sources
     ↓
Data Ingestion
     ↓
Data Transformation
     ↓
Workflow Orchestration
     ↓
Data Storage
     ↓
Analytics / BI
     ↓
Insights
```

I will continue combining these technologies into increasingly realistic data engineering projects as the programme progresses.

---

# GitHub Portfolio Goal

This repository serves as a record of my progression from foundational concepts to practical data engineering implementation.

Each stage of the programme will include:

* Learning notes
* Practical exercises
* Projects
* Reflections
* Troubleshooting experiences
* Key lessons learned

By the end of the programme, I aim to have a portfolio demonstrating not only what I have learned, but also my ability to apply data engineering concepts to practical problems.

---

## Current Status

**Programme:** ALX Data Engineering
**Progress:** 8 / 15 weeks completed
**Current Sprint:** Apache Spark — Weeks 9–10
**Repository:** ALX-Data-Engineering

---

## Next Steps

My immediate focus is to complete the **Apache Spark sprint**, deepen my understanding of distributed data processing, and begin integrating Spark with the orchestration and pipeline concepts I have already learned.

The long-term goal is to bring these skills together in the programme's **capstone projects** and build production-style data engineering solutions.

---

**Learning. Building. Troubleshooting. Documenting. Improving.**
