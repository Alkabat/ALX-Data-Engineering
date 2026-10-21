# Week 13 Reflections — Data Quality With Spark

This week helped me see data quality as an essential engineering responsibility rather than a final cleaning step. A pipeline can run successfully from a technical perspective while still producing data that is incomplete, invalid, inconsistent, inaccurate, duplicated, or too old for its intended purpose.

The six dimensions gave me a clearer way to describe different kinds of problems. Completeness is about whether required values are present; uniqueness is about unwanted duplicates; validity is about compliance with rules; accuracy is about truth; consistency is about agreement; and timeliness is about freshness. These dimensions overlap in practice, but they are not interchangeable.

The PySpark exercise using the UCI Bike Sharing Dataset gave me practical experience inspecting a dataset's structure and profiling missing values. The dataset contained 17,379 records and 17 columns, and the exercise produced a CSV report for column-level completeness checks. This reinforced the value of using Spark to make data profiling repeatable rather than relying only on manual inspection.

One important lesson was that data quality rules must reflect the meaning of the data. A negative value, for example, is not automatically wrong; refunds or accounting adjustments can legitimately be negative. Similarly, different status values are not necessarily inconsistent unless they conflict with an agreed rule or representation.

I also learned to distinguish visible failures from silent failures. A pipeline that stops and raises an alert gives engineers a chance to investigate. A pipeline that continues while distributing bad data can mislead downstream users without drawing attention to the problem. Validation, monitoring, logging, and clear handling policies are therefore important parts of a reliable pipeline.

Going forward, I want to build on this exercise by turning the business rules identified during profiling into repeatable automated tests, including checks for duplicates, allowed ranges, and relationships between related columns. I will also make sure to verify test results before documenting a check as passed.

## What I am taking forward

- Profile data before deciding how to clean it.
- Define business rules before marking values as invalid.
- Avoid dropping or imputing missing data without considering the use case.
- Use manual exploration to discover rules, then automate the checks.
- Record findings and generated reports so the work is reproducible.
- Treat data quality as part of pipeline design and monitoring, not just a one-time task.
