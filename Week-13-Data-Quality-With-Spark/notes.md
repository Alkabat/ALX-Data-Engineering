# Week 13 Notes: Data Quality With Spark

## 6.1 — Lesson Overview: Data Quality with PySpark

Data quality is the process of assessing whether data is suitable for its intended purpose. In data engineering, quality checks help ensure that data flowing through pipelines is reliable enough for analytics, reporting, and downstream applications.

Spark supports data profiling and validation across large datasets, making it useful for repeatable data quality checks.

## 6.2 — The Need for Data Quality Validation and Testing

Poor data quality can lead to incorrect reports, unreliable analysis, operational problems, and poor business decisions.

Data quality validation helps identify issues before data is used downstream.

Important practices include:

- Defining business rules and expected data conditions.
- Inspecting incoming data.
- Checking for missing, duplicate, invalid, or inconsistent values.
- Recording failures and notifying the appropriate people.
- Deciding whether bad records should be corrected, quarantined, rejected, or allowed through with a warning.

A pipeline that continues running while silently passing bad data downstream can be more dangerous than one that fails visibly.

## 6.3 — The Six Dimensions of Data Quality

### 1. Completeness

Completeness measures whether the required data is present.

Missing or null values reduce completeness when the field is expected to contain a value.

Example: A customer dataset contains 1,000 records, but 100 records have missing email addresses. If every customer is expected to have an email address, email completeness is 90%.

### 2. Uniqueness

Uniqueness measures whether unwanted duplicate records or values exist.

Example: A transaction table should contain only one record per transaction ID, but a transaction appears five times.

Possible investigation using PySpark:

```python
df.groupBy("transaction_id") \
  .count() \
  .filter("count > 1") \
  .show()
```

Duplicates should be investigated before removal because repeated records may sometimes be legitimate.

### 3. Validity

Validity checks whether data conforms to defined rules, formats, data types, permitted values, and acceptable ranges.

Example: An account status is expected to be `Active`, `Inactive`, or `Closed`, but a record contains `UnknownStatus`.

```python
from pyspark.sql.functions import col

invalid_records = df.filter(
    ~col("account_status").isin(
        "Active", "Inactive", "Closed"
    )
)

invalid_records.show()
```

A negative financial value is not automatically invalid. Refunds, reversals, and accounting adjustments can legitimately be negative. The relevant business rule determines validity.

### 4. Accuracy

Accuracy measures whether data correctly represents the real-world fact it is intended to capture.

Example: A transaction is recorded as ₦50,000 when the actual transaction amount was ₦5,000.

A value can be valid but inaccurate. An age of 35 may fall within an acceptable range but still be wrong for the individual.

Accuracy often requires comparison with a trusted source or authoritative reference.

### 5. Consistency

Consistency checks whether related data agrees across records, fields, datasets, or systems.

Examples:

- One system records an account as `Active`, while another records it as `Closed`.
- A total does not agree with the sum of its component values.
- The same entity is represented differently in systems that are expected to use a common standard.

Grouping values can help identify unexpected variations:

```python
df.groupBy("account_status").count().show()
```

The results should be investigated before changes are made. Different values are not necessarily inconsistent unless they violate an agreed rule.

### 6. Timeliness

Timeliness measures whether data is sufficiently current and available when needed.

Example: A fraud detection system requires transaction data within five minutes, but the records arrive two hours late.

Timeliness differs from ingestion speed and update frequency. Data may be ingested quickly but still be outdated.

## 6.4 — Calculating Data Quality Dimensions with Spark

### Inspect dataset dimensions and schema

```python
print("Total records:", df.count())
print("Total columns:", len(df.columns))

df.printSchema()
```

In the practical exercise, the UCI Bike Sharing Dataset contained 17,379 records and 17 columns.

### Count missing values in one column

```python
from pyspark.sql.functions import col, when, count

df.select(
    count(
        when(col("cnt").isNull(), 1)
    ).alias("missing_cnt")
).show()
```

The column name must exist in the DataFrame. For the Bike Sharing Dataset, `cnt` is an actual column.

### Count null values across all columns

```python
from pyspark.sql.functions import col, when, sum as spark_sum

null_counts = df.select([
    spark_sum(
        when(col(c).isNull(), 1).otherwise(0)
    ).alias(c)
    for c in df.columns
])

null_counts.show(truncate=False)
```

### Calculate completeness

For a column where every record is expected to have a value:

**Completeness (%) = (Non-missing values / Total records) × 100**

For example, if 950 out of 1,000 expected values are present:

Completeness = (950 / 1,000) × 100 = 95%.

A null count alone may not capture all missing values. Depending on the source, empty strings and whitespace-only strings may also need to be treated as missing.

### Other possible Spark checks

- **Uniqueness:** Group by a key and identify counts greater than one.
- **Validity:** Filter values outside approved ranges or permitted sets.
- **Consistency:** Compare related columns using defined business rules.
- **Accuracy:** Reconcile values with a trusted source.
- **Timeliness:** Compare event or update timestamps against freshness requirements.

For the Bike Sharing Dataset, a possible consistency check is whether `cnt` equals `casual + registered`. Such a rule should be verified against the dataset definition before it is enforced.

## 6.5 — Tools for Data Quality Validation and Testing

### Manual testing

Manual testing involves inspecting data and performing checks directly.

Advantages:
- Flexible during exploration.
- Useful for discovering unexpected patterns.
- Helps establish business rules and test requirements.

Disadvantages:
- Time-consuming and repetitive.
- Difficult to scale to large datasets.
- Prone to human error.
- Harder to execute consistently over time.

### Automated testing

Automated testing applies predefined rules programmatically.

Advantages:
- Repeatable and consistent.
- Suitable for recurring pipeline checks.
- Can produce logs, reports, and alerts.
- Can detect regressions when new data arrives.

A useful approach is to explore data manually, define agreed business rules, convert those rules into automated checks, and monitor the results.

## 6.6 — Data Quality with PySpark: Knowledge Check Review

### Missing values

The appropriate response depends on the use case. Possible actions include dropping affected rows, removing an unneeded column, or imputing values where a defensible method exists.

Do not automatically replace missing financial values with an average, because that may create false transaction information.

### Consistency

Group and profile values to identify suspicious differences. Correct only confirmed inconsistencies using approved rules.

### Completeness

Completeness concerns the presence of required values, not simply the number of records in the dataset.

### Timeliness

Timeliness concerns whether data is current enough for its intended use.

### Validity

Validity concerns whether data follows defined constraints and business rules.

### Manual testing

Manual testing helps explore data and discover constraints. Automated tests make recurring checks more repeatable and scalable.

### Bad data in a running pipeline

Silent failures may allow unreliable data to contaminate downstream systems. Pipelines should detect quality problems and use an appropriate handling strategy, such as quarantine, rejection, correction, or alerting.

## 6.7 — Data Quality: Additional Resources

Additional resources can deepen understanding of data validation, Spark profiling, and automated testing frameworks.

When using a framework, check its documentation and compatibility with the project's Python and Spark versions.

## Practical Exercise Record

- **Dataset:** UCI Bike Sharing Dataset (`hour.csv`)
- **Workspace:** `~/data-quality-spark`
- **Script:** `check_completeness.py`
- **Report:** `data_quality_report.csv`
- **Observed dataset size:** 17,379 records and 17 columns
- **Focus:** Column-level completeness and missing-value profiling

Always inspect the actual output before concluding that a data quality check has passed.