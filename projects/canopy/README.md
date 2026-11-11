# Canopy: Supplier Performance Data Pipeline

**Radford University · CS440 · Group 7 · Fall 2026**  
**Platform:** Databricks | **Languages/Tools:** Python, PySpark

## Overview

Canopy is a team data-engineering project focused on preparing supplier-performance data for downstream analysis and supplier-risk assessment. This page documents **my individual contribution** to the team's Databricks pipeline: cleaning, validation, and automated testing.

## My responsibilities

- Implemented cleaning logic in `clean.py`: trimmed excess whitespace, converted blank text to null, and removed exact duplicate rows.
- Worked on `validate.py` to separate accepted and rejected records and preserve the reasons that a record failed validation.
- Debugged the pipeline in Databricks, including resolving an initial missing-CSV input issue before rerunning the workflow.
- Tested cleaning and validation behavior; the project reported **25 passing validation tests**.

## Results

| Measure | Result |
| --- | ---: |
| Input rows | 50,000 |
| Input columns | 25 |
| Exact duplicate rows removed | 500 |
| Rows after deduplication | 49,500 |
| Valid rows | 46,458 |
| Rejected rows | 3,042 |
| Validation tests passing | 25 / 25 |

**Reconciliation:** 46,458 valid + 3,042 rejected = 49,500 rows after deduplication.

## Pipeline outline

```text
CSV source (50,000 rows)
    ↓
PySpark cleaning (trim / blank-to-null / deduplication)
    ↓
49,500 unique rows
    ↓
Validation with retained rejection reasons
    ├── 46,458 accepted rows
    └── 3,042 rejected rows
    ↓
Clean, validated supplier data for downstream analysis
```

## Engineering takeaways

The project emphasized data quality, reproducible validation, and debugging real pipeline failures. Rather than silently discarding problematic records, validation retained failure reasons to make downstream review possible.

## Code and project boundaries

This is a **case study**, not a copy of the team's full repository. The original `clean.py`, `validate.py`, tests, and dataset have **not been published here**. Any source code or screenshots added later should be the student's own work and should be cleared for public sharing under course and team rules. No confidential or restricted supplier data is included.

## Author

Kalkidan Bekele Argaw · [Portfolio](https://kalkidan9292.github.io/) · [GitHub](https://github.com/kalkidan9292)
