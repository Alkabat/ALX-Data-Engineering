## Notes

### Topics Covered

- Moving and processing big data using scalable tools and orchestration.
- Setting up workflows in Apache Airflow.
- Understanding pipeline scalability and automation.
- Implementing Docker for scalable data processing.
- Identifying scalability requirements.
- Scaling data processing with Docker containers.
- Understanding pipeline orchestration and triggers.
- Using schedule-based and event-based orchestration.
- Exploring small-scale serverless processing and integration.
- Working with triggers and schedules.
- Introduction to distributed computation and Apache Hadoop.
- Introduction to big data processing.

### Key Concepts

- A data pipeline is like an assembly line made up of individual data-processing units.
- Data pipelines can be triggered in three main ways:
  - On-demand triggers.
  - Schedule-based triggers.
  - Event-based triggers.
- Data pipelines must be observable. This involves monitoring the health and performance of the pipeline through internal metrics.
- A Directed Acyclic Graph (DAG) defines the order in which tasks are executed.
- Orchestration ensures that processes run in the correct sequence, at the appropriate time, and with proper monitoring.
- Common orchestration tools include Apache Airflow and Azure Data Factory.
- Scalability is the ability of a system to adapt and expand without placing significant constraints on its functionality.
- Factors that influence scalability include:
  - Caching.
  - Pooling.
  - Collocation.
  - Efficient code.
  - Parallelism.
  - Concurrency.
- Other factors that affect scaling include the type of data source, downstream processing requirements, and cloud-provider selection.

### Practical Exercises

- Set up my first Apache Airflow data environment.
- Created my first Airflow DAG.
- Learned how to create and interpret cron jobs.
- Completed an exercise on identifying scalability requirements for an e-commerce company facing the following challenges:
  - Website orders failed because of database contention.
  - Inventory updates were delayed.
  - Daily reports were taking longer to generate, resulting in overselling.
  - New features were difficult to implement.

### Apache Hadoop

Apache Hadoop is a framework for distributed storage and parallel processing of large datasets. Its three primary components are:

- **HDFS:** Hadoop Distributed File System for storing data across multiple machines.
- **MapReduce:** A programming model for processing data in parallel.
- **YARN:** A resource-management and job-scheduling component.

Other emerging tools for big-data processing include Apache Storm, Hive, Spark, Flink, Samza, and Samoa.
