# Week 13: Data Quality With Spark

**Programme:** ALX Data Engineering Programme  
**Author:** Kabati Ishaya  
**Week:** 13 of 15

## Overview

This week focused on data quality validation and testing using PySpark. I explored why data quality matters in data engineering, studied the six dimensions of data quality, practised calculating quality metrics with Spark, and examined approaches to manual and automated data testing.

The practical exercise involved using the UCI Bike Sharing Dataset (`hour.csv`) to inspect its structure and assess completeness by identifying missing values across columns.

## Learning Objectives

- Understand the need for data quality validation and testing.
- Explain the six dimensions of data quality.
- Calculate data quality metrics using PySpark.
- Identify missing values and potential data quality issues.
- Understand the role of manual testing and automated validation.
- Recognise the importance of detecting and handling bad data in data pipelines.

## Lessons Covered

### 6.1 — Lesson Overview: Data Quality with PySpark

Introduced data quality as a key responsibility in building reliable data pipelines and trustworthy datasets.

### 6.2 — The Need for Data Quality Validation and Testing

Explored how poor-quality data can affect reporting, analytics, business decisions, and downstream data systems. Reviewed the importance of validating data before it is consumed.

### 6.3 — The Six Dimensions of Data Quality

Studied the following dimensions:

1. **Completeness:** Whether required data is present.
2. **Uniqueness:** Whether unwanted duplicate records exist.
3. **Validity:** Whether data conforms to defined rules and constraints.
4. **Accuracy:** Whether data correctly represents real-world facts.
5. **Consistency:** Whether related data agrees across records or systems.
6. **Timeliness:** Whether data is sufficiently up to date for its intended use.

### 6.4 — Calculating Data Quality Dimensions with Spark

Practised inspecting a dataset with PySpark, checking its dimensions, and calculating column-level missing-value counts.

The Bike Sharing Dataset contained 17,379 records and 17 columns. The practical exercise generated a CSV report for completeness analysis.

### 6.5 — Tools for Data Quality Validation and Testing

Reviewed manual and automated data testing approaches. Manual testing is useful for discovering data issues and defining business rules, while automated tests support repeatable validation at scale.

### 6.6 — Data Quality with PySpark (MCQ)

Completed knowledge checks on validity, missing-value treatment, consistency, completeness, timeliness, manual testing, and the consequences of bad data passing through a pipeline.

### 6.7 — Data Quality: Additional Resources

Reviewed the lesson's additional-resources section as part of the learning sequence.

## Practical Exercise

**Dataset:** UCI Bike Sharing Dataset (`hour.csv`)  
**Practice workspace:** `~/data-quality-spark`  
**Script:** `check_completeness.py`  
**Output report:** `data_quality_report.csv`

The practical work involved inspecting the dataset structure and assessing missing values across columns using PySpark. The exercise reinforced how Spark can be used to profile data and produce a report for further inspection.

The six dimensions also provide a framework for extending the exercise with duplicate detection, rule-based validation, cross-field consistency checks, accuracy verification against trusted sources, and timeliness checks.

## Key Learnings

- Data quality should be checked systematically rather than assumed.
- Missing values must be handled according to the dataset and business requirements.
- Validity and accuracy are different: a value may satisfy a rule but still be incorrect.
- Negative values are not automatically invalid; their meaning depends on the field and business rules.
- Manual testing can inform the development of automated data quality checks.
- Silent data quality failures can be dangerous because bad data may continue downstream without detection.
- Validation, monitoring, logging, and appropriate error-handling strategies are important parts of reliable data pipelines.

## Conclusion

Week 13 strengthened my understanding of data quality as an essential component of data engineering. Through the lessons, knowledge checks, and practical PySpark exercise, I gained experience with completeness analysis and developed a clearer framework for assessing data quality across its six dimensions.

The next step is to expand the practical work into repeatable automated checks that can detect and report data quality issues consistently.

---

**ALX Data Engineering Programme — Week 13 of 15**