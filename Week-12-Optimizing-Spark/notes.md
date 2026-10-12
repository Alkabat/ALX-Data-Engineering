# Week 12 Notes — Apache Spark: Optimizing Spark

## Sprint Overview

**Sprint:** Apache Spark  
**Section:** 5 — Optimizing Spark  
**Week:** 12

During Week 12, I studied and practised concepts related to Apache Spark performance optimisation. I worked through the lessons alongside practical activities in my Ubuntu Spark environment, reinforcing my understanding of workload scaling, caching, cluster execution, monitoring, debugging, and PySpark code optimisation.

## 5.1 Lesson Overview: Optimizing Spark

Spark optimisation focuses on improving application performance and resource efficiency while maintaining correct results.

During this lesson, I reinforced the importance of understanding how Spark executes operations and how coding decisions, data distribution, and resource availability influence performance.

Key concepts covered:
- CPU and memory utilisation.
- Parallel processing and partitioning.
- Shuffle operations and data movement.
- Repeated computations.
- Execution plans and performance monitoring.
- Resource allocation and workload management.

**Practical learning:** I connected the optimisation concepts to the Spark exercises I carried out alongside the training and developed a more systematic approach to identifying potential performance issues.

## 5.2 Scaling Spark for Large Workloads

I studied how Spark applications can be scaled to handle larger datasets and more demanding processing requirements.

### Key concepts

**Partitioning:** Spark divides data into partitions so that multiple tasks can process data concurrently. Poor partitioning can limit parallelism or introduce unnecessary task overhead.

**Resource allocation:** Executor memory, CPU cores, and the number of executors affect the resources available to process a workload.

**Data skew:** Uneven data distribution can cause some tasks to process significantly more data than others.

**Shuffle operations:** Joins, aggregations, and repartitioning can require data to move between executors, increasing execution cost.

**Input and output:** File sizes, file counts, and data layout can influence processing efficiency.

### Practical learning

Through the accompanying Spark learning activities, I reinforced the relationship between workload characteristics, parallelism, and resource utilisation.

I learned that adding more resources is not always sufficient to resolve performance problems. The underlying code, partitioning strategy, and distribution of data must also be considered.

## 5.3 Caching and Persistence in Spark

I studied caching and persistence as techniques for retaining computed data so it can be reused without unnecessary recomputation.

### When caching is useful

Caching is particularly useful when:
- A DataFrame or RDD is reused by multiple operations.
- Producing the data requires expensive computation.
- Recomputing the same intermediate result would cost more than retaining it.

Caching may be unnecessary when data is used only once or is inexpensive to recompute.

### Example

```python
df = spark.read.parquet("data/events")

df.cache()

# Trigger computation and populate the cache
df.count()

# Reuse the cached DataFrame
df.groupBy("event_type").count().show()

df.filter("event_type IS NOT NULL").count()

# Release cached data when no longer needed
df.unpersist()
```

### Practical learning

I reinforced how caching and persistence can reduce repeated computation when data is reused. I also learned that caching consumes resources and should be applied selectively.

Spark uses lazy evaluation, so transformations do not necessarily execute immediately. An action such as `count()` can trigger execution and materialise cached data.

## 5.4 Running Spark Applications on Clusters

I studied the components involved in running Spark applications in a distributed environment.

### Main components

- **Driver:** Coordinates the Spark application and schedules work.
- **Executors:** Execute tasks and may store intermediate or persisted data.
- **Cluster manager:** Allocates resources to applications.

### Important configuration considerations

- Executor memory and CPU cores.
- Number of executors.
- Deployment mode and cluster manager.
- Dependency availability.
- File paths and permissions.
- Access to input and output data.
- Cluster capacity and resource limits.

### Practical learning

The lesson strengthened my understanding of how Spark distributes work and why application configuration matters when workloads run across