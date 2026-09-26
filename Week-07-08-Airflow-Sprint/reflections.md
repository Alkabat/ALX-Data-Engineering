# Week 8 – Airflow Projects & Automation — Reflection

## My Learning Experience

Week 8 was an important stage in my Data Engineering journey because I moved beyond learning Airflow concepts and started applying them to a working workflow.

Building the **Linda's Kitten Image Workflow** helped me understand how individual Airflow components come together to form an automated data pipeline. Instead of looking at the Scheduler, Workers, Operators, Variables, and DAGs as separate concepts, I was able to see how they interact during actual pipeline execution.

## What I Learned

One of my biggest lessons this week was understanding how to design and manage task dependencies.

I learned how to use operators such as `BashOperator` and `PythonOperator` for different types of work and how to connect them using Airflow's dependency syntax. Adding the `write_results_to_file` task also helped me understand how tasks can branch and execute independently after a common upstream task.

I also gained a better understanding of **Airflow Variables** and why sensitive configuration values should not be hardcoded directly into DAG code. Using the `UNSPLASH_ACCESS_KEY` as an Airflow Variable reinforced the importance of separating configuration from application logic.

## Challenges and Troubleshooting

The practical exercises also exposed me to the type of problems that occur when working with real workflows.

I encountered DAG import and syntax issues while developing the workflow, including problems caused by incorrect imports and code formatting. I also had to troubleshoot task execution and file-permission/path issues when writing the pipeline results to a file.

Rather than treating these errors as failures, I used the Airflow CLI, task testing commands, logs, and the Airflow UI to identify and correct the problems.

This was particularly valuable because it showed me that **debugging is an essential part of building reliable data pipelines**.

## What I Improved

By the end of the sprint, I was more confident in:

* Creating and modifying Airflow DAGs.
* Choosing appropriate operators for different tasks.
* Defining task dependencies and parallel execution.
* Using Airflow Variables for configuration.
* Testing individual tasks before running a complete DAG.
* Reading Airflow logs to troubleshoot failures.
* Monitoring DAG runs and task states through the Airflow UI.
* Working with Airflow in a Docker-based environment.

## Key Takeaway

My biggest takeaway from the Airflow sprint is that orchestration is not simply about scheduling tasks. It is about designing workflows that are **structured, observable, maintainable, and reliable**.

The two-week Airflow sprint has given me a much stronger foundation for understanding how data engineering workflows are automated and monitored.

I am now moving into the **Apache Spark sprint (Weeks 9–10)** with a better understanding of how orchestration fits into the broader data engineering ecosystem.

The next challenge is to combine these orchestration principles with distributed data processing and develop a deeper understanding of **Apache Spark and PySpark**.
