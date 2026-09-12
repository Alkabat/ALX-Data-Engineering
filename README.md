# ALX Data Engineering Journey 🚀

Welcome to my Data Engineering learning journey through the ALX Data Engineering Programme.

## About

This repository documents my progress throughout the 15-week ALX Data Engineering Programme.

The goal is not only to complete the programme but also to build practical projects that demonstrate my skills in:

- Python
- SQL
- ETL Pipelines
- Big Data
- Docker
- Apache Airflow
- PySpark
- Data Engineering Best Practices

## Weekly Progress

| Week | Topic | Status |
|------|--------|--------|
| Week 1 | Data Engineering Foundations | ✅ Completed |
| Week 2 | Big Data Architecture, Security, Quality & Lineage | ✅ Completed |
| Week 3 | Big Data Fundamentals, Data Pipelines & Scalability | ✅ Completed |
| Week 4 | Pipeline Orchestration, Airflow Concepts & Hadoop Fundamentals | ✅ Completed |
| Week 5 | Docker Fundamentals & Containerization | ✅ Completed |
| Week 6 | Docker for Data Engineering Workflows | ✅ Completed |
| Week 7 | Apache Airflow & Workflow Orchestration | ✅ Completed |
| Week 8 | Apache Airflow Projects & Automation | ✅ Completed |
| Week 9 | Apache Spark & Distributed Computing | 🔄 In Progress |
| Week 10 | Apache Spark Data Processing | ⏳ Pending |
| Week 11 | Apache Spark Optimization & Applications | ⏳ Pending |
| Week 12 | Capstone Project | ⏳ Pending |
| Week 13 | Capstone Project | ⏳ Pending |
| Week 14 | Capstone Project | ⏳ Pending |
| Week 15 | Capstone Project & Portfolio Completion | ⏳ Pending |

## Repository Structure

```text
ALX-Data-Engineering/
├── Week-01-Foundations/
├── Week-02-Big-Data-Architecture/
├── Week-03-Big-Data-Fundamentals/
├── Week-04-Pipeline-Orchestration/
├── Week-05-Docker-Fundamentals/
├── Week-06-Docker-Workflows/
├── Week-07-Airflow-Orchestration/
├── Week-08-Airflow-Projects/
├── Week-09-Spark-Distributed-Computing/
└── README.md
```

## Objectives

- Build production-style data engineering projects.
- Develop strong software engineering practices.
- Maintain a professional GitHub portfolio.
- Prepare for remote and international Data Engineering opportunities.

## Current Progress

**Program:** ALX Data Engineering 2026

**Weeks Completed:** 8/15

**Current Sprint:** Apache Spark & Distributed Computing

### Completed Foundation Topics

- Data Engineering Fundamentals  
- Big Data Architecture  
- Data Security, Quality & Lineage  
- Data Pipelines & Scalability  
- Workflow Orchestration Concepts  
- Hadoop Fundamentals (HDFS, MapReduce, YARN)  
- Docker Fundamentals & Containerization  
- Docker for Data Engineering Workflows  
- Apache Airflow Fundamentals & Orchestration  
- Airflow Projects & Automation  

### Docker Sprint Achievements (Weeks 5–6)

- Mastered Docker fundamentals: images, containers, Dockerfile syntax, and lifecycle management  
- Built and pushed custom Docker images to Docker Hub  
- Configured Docker networks (bridge and custom) and practiced container communication  
- Implemented data persistence using named volumes and bind mounts  
- Orchestrated a multi-service stack with Docker Compose (Node.js API, PostgreSQL, Nginx)  
- Set up a custom network (`app-network`) and named volume (`db-data`) for service isolation and persistence  
- Implemented health checks and performed a controlled rollback (Nginx 1.25 → 1.24)  
- Practiced troubleshooting using `docker compose ps`, `logs`, and `inspect`  
- Differentiated image optimization from runtime resource constraints (CPU/memory limits)  
- Applied Docker to data engineering workflows and multi-container orchestration  

### Airflow Sprint Achievements (Weeks 7–8)

- Understood data pipelines and represented them as Directed Acyclic Graphs (DAGs)  
- Learned Airflow architecture: Scheduler, Webserver, Executor, Metadata DB, Workers  
- Defined DAGs in Python and implemented simple to moderately complex workflows  
- Set up and ran a local Airflow instance  
- Navigated the Airflow UI: DAGs view, Graph view, Task Instances, Logs, and Runs  
- Extended DAGs with specifications like `schedule_interval`, `catchup`, `retries`, and `retry_delay`  
- Used multiple Airflow operators and defined task dependencies with `>>`, `<<`, and `set_upstream`/`set_downstream`  
- Configured Airflow Connections to interact with external systems securely  
- Implemented event-based triggers and automated pipelines to run on schedule and in response to events  
- Ran DAGs manually and monitored pipeline scalability considerations  

#### Airflow Projects & Automation Highlights

- Built and ran a complete Airflow DAG (`basic_airflow_pipeline`) that:
  - Fetches kitten image URLs from the Unsplash API using `BashOperator` and `curl`.
  - Downloads images using `PythonOperator`.
  - Sends a notification about how many images were downloaded.
- Configured **Airflow Variables** (`UNSPLASH_ACCESS_KEY`) to manage secrets.
- Defined clear task dependencies and tested individual tasks with `airflow tasks test`.
- Extended the pipeline with a new parallel task (`write_results_to_file`) that:
  - Counts downloaded images.
  - Writes the result to `kitten_state.txt`.
  - Runs in parallel with the notification task.
- Validated the extended DAG: `write_results_to_file` completed successfully and updated the count to 8 images.
- Reinforced key Airflow concepts:
  - Metastore, Scheduler, Workers, Executors
  - DAGs as acyclic graphs and DAG best practices
  - `PythonOperator`, `BashOperator`, XCom, Variables
  - Testing, triggering, and monitoring DAG runs

### Upcoming: Apache Spark Sprint (Weeks 9–10)

- Focus areas:
  - Apache Spark & Distributed Computing  
  - Spark Data Processing with PySpark  
  - Spark optimization and applications  

---

*"Consistency beats intensity."*