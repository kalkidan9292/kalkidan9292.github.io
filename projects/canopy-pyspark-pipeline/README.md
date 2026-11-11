# Canopy: PySpark Data Cleaning & Validation

**Role:** Data cleaning and validation contributor, Group 7, CS 440 (Fall 2026)  
**Tools:** Databricks, Python, PySpark  
**Project type:** Collaborative course data-engineering pipeline

## Overview

Canopy is a team-built data pipeline for cleaning, validating, transforming, and preparing a 50,000-record dataset. My primary contributions were the cleaning and validation components in `clean.py` and `validate.py`.

## Verified results

| Pipeline stage | Records |
| --- | ---: |
| Input | 50,000 |
| Exact duplicates removed | 500 |
| Records after cleaning | 49,500 |
| Valid | 46,458 |
| Rejected | 3,042 |
| Validation test cases passed | 25 / 25 |

The counts reconcile: **46,458 + 3,042 = 49,500**.

## What I implemented

- **Data normalization:** Trimmed surrounding whitespace and converted blank text fields to null.
- **Duplicate handling:** Removed exact duplicate rows while preserving records that differed in meaningful fields such as `product_id`.
- **Validation:** Separated accepted and rejected records and retained **all** failure reasons for each rejected row, instead of stopping after the first violation.
- **Testing:** Used a three-row cleaning test (two identical rows and one distinct product), confirmed two records remained, and passed 25 validation tests.
- **Troubleshooting:** Fixed an initial Databricks input-file path/volume issue and reran the notebook successfully.

## Engineering decisions

**Preserve distinct records.** Deduplicating only by `customer_id` would have incorrectly removed a valid row with a different `product_id`. I used an exact-duplicate approach and tested this edge case.

**Keep multiple rejection reasons.** Recording all validation violations made debugging more informative, at the cost of more complex validation logic and longer error details. A four-error test verified that all four codes were retained.

## Team pipeline context

Other team members contributed the transformation and output stages. The team transformation step added financial and delivery measures to valid rows. I do **not** claim authorship of those components.

## Limitations and lessons

The 25 passing tests provide useful evidence but do not establish correctness for every possible input. The initial run also showed why checking file availability and validating notebook exports are important before a full pipeline execution.

## Source-code availability

This case study documents my verified work. The original submission contains collaborative course code and datasets; those files are **not published here** pending confirmation that public redistribution is permitted. A sanitized, reproducible code release may follow.

---

*Evidence: PM02 Engineering Discussion, Group 7, and the team's saved Databricks pipeline execution report (November 2026).*