# Week 8 – Apache Airflow Projects & Automation

## Overview

This week I deepened my Airflow skills by building, testing, debugging, and extending a practical workflow: the **Linda's Kitten Image Workflow**. I moved from understanding Airflow components conceptually to designing and running multi-task DAGs with clear dependencies, parallel execution, and file I/O.

This marks the completion of the two-week Apache Airflow sprint (Weeks 7–8), transitioning from core orchestration concepts to hands-on project implementation.

## Projects & Exercises

### 1. 🐱 Linda's Kitten Image Workflow — Basic Airflow Pipeline

I implemented a basic Airflow DAG called:

```python
basic_airflow_pipeline
```

This pipeline uses the Unsplash API to fetch and download kitten images and then sends a notification.

#### DAG Structure

* **fetch_kitten_urls**

  * Operator: `BashOperator`
  * Uses `curl` to request kitten image URLs from the Unsplash API.
  * Uses the `UNSPLASH_ACCESS_KEY` stored as an **Airflow Variable**.

* **get_kitten_images**

  * Operator: `PythonOperator`
  * Downloads the kitten images using the URLs returned by the previous task.

* **pipeline_notification**

  * Operator: `BashOperator`
  * Reports how many kitten images were downloaded.

#### Key Learnings & Configurations

* Defined and used **Airflow Variables** (`UNSPLASH_ACCESS_KEY`) instead of hardcoding secrets.
* Set up **DAG dependencies** using `>>` to define task order.
* Practiced with:

  * `BashOperator` for shell commands
  * `PythonOperator` for custom Python logic
* Tested tasks individually with:

```bash
airflow tasks test basic_airflow_pipeline <task_id> <execution_date>
```

* Triggered DAG runs manually from the Airflow UI.
* Checked DAG runs, task states, logs, and import errors through the Airflow UI and CLI.

---

### 2. 📝 Extending the Kitten Pipeline

I extended the same workflow by adding a new task:

* **write_results_to_file**

  * Operator: `BashOperator`
  * Counts the downloaded kitten images.
  * Writes a notification, including the current count, to `kitten_state.txt`.
  * Runs **in parallel** with `pipeline_notification`.

#### Final DAG Structure

```text
fetch_kitten_urls
        ↓
get_kitten_images
      ↙             ↘
pipeline_notification    write_results_to_file
```

#### Outcome

* Successfully tested the new task.
* `write_results_to_file` completed with **SUCCESS**.
* Verified that `kitten_state.txt` contained the updated count, which reached **8 kitten images** during testing.

This exercise reinforced how to:

* Add new tasks to an existing DAG without breaking existing dependencies.
* Create parallel branches within a DAG.
* Use `BashOperator` for simple file I/O and reporting tasks.
* Validate task behavior through both the UI and CLI.

---

## Concepts Practiced This Week

From these two exercises and associated quizzes, I solidified the following Airflow concepts:

### Core Architecture

* Metastore (metadata database)
* Scheduler
* Workers
* Executors and their role in task execution and scalability

### DAG Design

* DAGs as Directed Acyclic Graphs (no cycles allowed)
* DAG best practices, including idempotency, clear task separation, and meaningful task IDs
* The relationship between **DAGs → Tasks → Dependencies → Execution**

### Operators & Data Flow

* `PythonOperator` for custom Python logic
* `BashOperator` for shell commands and file operations
* Introduction to **XCom** for passing small pieces of data between tasks
* **Airflow Variables** for configuration and sensitive values

### Testing & Monitoring

* Testing individual tasks with `airflow tasks test`
* Triggering DAG runs manually and on schedule
* Monitoring DAG runs, task states, logs, and import errors
* Troubleshooting DAG import and task execution problems

---

## What This Week Means for My Airflow Journey

This week marked the transition from **understanding Airflow concepts to building, debugging, testing, and extending working DAGs**.

I now have hands-on experience with:

* Designing multi-task workflows with clear dependencies.
* Using Airflow Variables instead of hardcoding sensitive configuration values.
* Extending existing pipelines safely by adding parallel tasks.
* Testing individual tasks before running the complete workflow.
* Monitoring pipeline execution and diagnosing issues through logs and the Airflow UI.
* Working with Airflow in a Docker-based local environment.

With the Airflow sprint complete (Weeks 7–8), I am now moving into the **Apache Spark sprint (Weeks 9–10)**, where I will apply similar workflow and data-engineering principles to distributed data processing with PySpark.

### Next Steps

I plan to:

* Introduce more complex data movement, such as API → database → warehouse pipelines.
* Explore sensors and external triggers for event-driven workflows.
* Explore XCom more deeply for passing small amounts of metadata between tasks where appropriate.
* Apply orchestration concepts to Spark-based data processing pipelines.
