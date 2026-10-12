# Week 12 Reflections — Optimizing Spark

## Introduction

Week 12 focused on Section 5 of my Apache Spark sprint: Optimizing Spark. I studied how Spark applications can be made more efficient, how larger workloads can be managed, and how errors and performance bottlenecks can be investigated.

I did not approach the section as theory alone. I continued practising alongside the lessons in my Ubuntu Spark environment, using the practical work to reinforce the concepts as I progressed through the training material.

## What I Learned and Practised

### 1. Scaling Spark for Large Workloads

I explored the factors that influence Spark's ability to process larger datasets, including partitioning, available resources, parallelism, and the cost of data movement.

The practical learning helped me connect these concepts to Spark execution and understand why adding resources alone may not resolve every performance problem.

### 2. Caching and Persistence

I studied caching and persistence and their role in reducing repeated computations when intermediate datasets are reused.

Through the accompanying learning activities, I reinforced the importance of considering data reuse, computation cost, and available memory before deciding whether caching is appropriate.

I learned that caching is a performance optimisation technique that should be applied selectively rather than automatically.

### 3. Running Spark Applications on Clusters

I examined how Spark distributes work between the driver and executors and how resource allocation and application configuration affect execution.

This strengthened my understanding of the considerations involved in running Spark workloads beyond a basic local development setup, including dependencies, available resources, and access to data.

### 4. Applying the Spark UI

I studied how the Spark UI can be used to investigate jobs, stages, tasks, storage, and execution performance.

The practical learning reinforced the value of monitoring application behaviour when trying to understand slow execution, failed tasks, and expensive shuffle operations.

### 5. Common PySpark Errors and Troubleshooting

I worked through the concepts involved in recognising common PySpark errors and investigating their causes.

I reinforced a structured troubleshooting approach: reading the complete error message, inspecting the traceback, checking schemas and data types, and considering configuration, dependencies, and resource limitations.

This helped me understand why identifying the underlying cause is more useful than simply trying random fixes.

### 6. Debugging Tools and Error Logs

I studied the debugging techniques available when working with PySpark, including inspecting DataFrames, reviewing execution plans, and examining error logs.

I learned how these tools can help narrow down the location of a failure and provide evidence for determining the next troubleshooting step.

### 7. Optimizing PySpark Code

I explored practical optimisation principles, including selecting only the required columns, filtering data appropriately, avoiding unnecessary computations, reviewing partitioning, and using built-in Spark functions where suitable.

These lessons helped me understand how coding decisions can influence execution efficiency and why optimisation should be guided by the characteristics of the workload.

## Challenges and Lessons Learned

One major lesson from this section was that Spark performance issues can originate from several different areas. An application may be slow because of inefficient code, repeated computation, excessive shuffling, data skew, or resource constraints.

I also reinforced the importance of understanding Spark's execution behaviour when troubleshooting errors. An error that appears during an action may originate from a transformation defined earlier.

Working through the lessons alongside practical exercises helped me connect these concepts and approach troubleshooting more systematically.

## Skills Strengthened During Week 12

By completing the lessons and accompanying practice, I strengthened my understanding of:

- Spark workload scaling and resource considerations.
- Caching and persistence.
- Cluster execution concepts.
- Spark UI monitoring and performance investigation.
- PySpark error interpretation and troubleshooting.
- Debugging tools and execution-plan inspection.
- Code optimisation and efficient DataFrame processing.

## Overall Reflection

Week 12 was an important part of my Apache Spark learning journey because it brought together coding, execution, performance, and troubleshooting.

Practising alongside the lessons helped me reinforce the concepts as I encountered them, rather than postponing practical application until the end of the section.

My main takeaway is that effective Spark optimisation requires an understanding of both the code and how Spark executes it. Monitoring, careful investigation, and measured changes are essential for diagnosing problems and improving performance.

Completing this section has strengthened my foundation for working with more demanding Spark workloads and investigating PySpark performance issues with greater confidence.
