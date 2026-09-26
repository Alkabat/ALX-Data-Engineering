# Week 8 – Airflow Projects & Automation – Notes

## Context

This week focused on applying Airflow concepts in two hands-on projects:

1. Building a basic Airflow pipeline that fetches and downloads kitten images from Unsplash.
2. Extending that pipeline with an additional task that writes results to a file.

The emphasis was on end-to-end DAG creation, testing, dependency management, and monitoring. This completes the two-week Airflow sprint (Weeks 7–8).

## Key Topics Revisited

### Data Pipelines & DAGs

- Data pipelines modeled as **Directed Acyclic Graphs (DAGs)**.  
- Tasks = nodes; dependencies = directed edges.  
- No cycles allowed: ensures pipelines can terminate and be scheduled reliably.

### Airflow Architecture (Applied)

- **Scheduler**: parses DAGs, creates task instances, triggers runs.  
- **Webserver**: serves the UI for monitoring and manual triggering.  
- **Executor**: decides how/where tasks run (local, celery, k8s).  
- **Workers**: execute the actual task logic.  
- **Metastore**: stores DAG metadata, task states, variables, connections.

### DAG Definition in Python

- DAGs defined in `.py` files under `dags/`.  
- Use `DAG` context manager with parameters like:
  - `dag_id`
  - `schedule_interval`
  - `start_date`
  - `catchup`
  - `retries`, `retry_delay`
- Tasks created using operators:
  - `BashOperator` for shell commands.
  - `PythonOperator` for Python functions.

### Operators, Dependencies, and Execution

- Used:
  - `BashOperator` to call `curl` and write files.
  - `PythonOperator` to run Python download logic.
- Defined dependencies using:
  - `task1 >> task2`
  - `task2 >> [task3, task4]` for branching/parallelism.
- Tasks execute in order respecting dependencies; independent tasks can run in parallel.

### Airflow Variables & Connections

- Stored `UNSPLASH_ACCESS_KEY` as an **Airflow Variable**.  
- Accessed in tasks via:
  - `Variable.get("UNSPLASH_ACCESS_KEY")` in Python.
  - Or templated in BashOperator commands where appropriate.
- Reinforced the practice of not hardcoding secrets in DAG code.

### Testing & Monitoring

- Tested individual tasks with:
  ```bash
  airflow tasks test <dag_id> <task_id> <execution_date>
  ```
- Triggered DAG runs:
  - Manually via UI (“Trigger DAG”).
  - Automatically based on `schedule_interval`.
- Monitored:
  - DAG runs list.
  - Task instance states (success, running, failed).
  - Logs per task instance.
  - Import errors in the DAGs view.

## Exercise 1 – Basic Kitten Pipeline

### DAG: `basic_airflow_pipeline`

Tasks:

1. `fetch_kitten_urls`
   - `BashOperator`
   - Calls Unsplash API with `curl`.
   - Uses `UNSPLASH_ACCESS_KEY` from Variables.

2. `get_kitten_images`
   - `PythonOperator`
   - Parses JSON response.
   - Downloads images to a local directory.

3. `pipeline_notification`
   - `BashOperator`
   - Counts downloaded images.
   - Prints a summary message.

Flow:

```text
fetch_kitten_urls → get_kitten_images → pipeline_notification
```

Key points:

- Verified DAG import with no errors.  
- Ran `airflow tasks test` for each task before full DAG run.  
- Triggered DAG from UI and confirmed all tasks succeeded.  

## Exercise 2 – Extending the Kitten Pipeline

### New Task: `write_results_to_file`

- `BashOperator`
- Counts downloaded kitten images.
- Writes a message including the count to `kitten_state.txt`.
- Runs in parallel with `pipeline_notification`.

Updated flow:

```text
fetch_kitten_urls
        ↓
get_kitten_images
      ↙             ↘
pipeline_notification    write_results_to_file
```

Key points:

- Added task without changing existing dependencies.  
- Used `>>` to set:
  ```python
  get_kitten_images >> [pipeline_notification, write_results_to_file]
  ```
- Tested new task in isolation, then ran full DAG.  
- Confirmed `kitten_state.txt` updated correctly (count reached 8).

## Airflow Concepts Solidified

- **Metastore**: central DB for DAG metadata, task states, variables, connections.  
- **Scheduler**: continuously parses DAGs and schedules task instances.  
- **Workers + Executor**: execute tasks according to executor type.  
- **Operators**:
  - `BashOperator` – run shell commands.
  - `PythonOperator` – run Python callables.
- **XCom** (conceptually): mechanism to pass small data between tasks.  
- **Variables**: key–value config stored in Airflow, used for secrets and parameters.  
- **DAG best practices**:
  - Keep DAGs acyclic.
  - Use meaningful task IDs.
  - Make tasks idempotent where possible.
  - Separate concerns: fetch, process, notify, persist.

## Commands & UI Patterns Used

- `airflow tasks test <dag_id> <task_id> <execution_date>`  
- Trigger DAG from UI → “Play” button.  
- Inspect:
  - DAGs view (list of DAGs, import errors).
  - Graph view (task dependencies).
  - Task Instances (state, duration, logs).  

## Position in the Overall Journey

- Weeks 7–8 together form the **Apache Airflow sprint**.  
- Week 7 focused on core orchestration concepts and initial DAGs.  
- Week 8 focused on projects, automation, and extending existing DAGs.  
- With Airflow complete, the next sprint is **Apache Spark (Weeks 9–10)**:
  - Week 9: Spark & Distributed Computing  
  - Week 10: Spark Data Processing  

These notes capture the main technical content and patterns from Week 8’s Airflow projects, closing out the Airflow portion of the programme.