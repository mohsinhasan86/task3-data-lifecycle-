# task3-data-lifecycle-
GitHub repository ke **Description** ke liye ye short aur professional rakho:  > Data lifecycle and lineage mapping project covering data sources, validation, cleaning, transformations, source of truth, and end-to-end metric tracing using Python and Pandas.
# Task 3 — Source of Truth & Data Lineage

## 1. Project Overview

This document describes the data lifecycle and lineage of the sales dataset used in the PlaceMux Data Analyst Phase 1 project.

The lifecycle was traced from the original CSV source through data validation, cleaning, transformation, analysis, and final reporting.

## 2. Data Source

The original source is the Task 2 raw sales CSV file.

The dataset contains the following key fields:

* order_id
* order_date
* customer_id
* customer_name
* city
* category
* product
* quantity
* unit_price
* discount_pct
* payment_method
* sales_channel
* status

The raw dataset contained 125 rows and 13 columns.

## 3. Data Validation

The raw dataset was checked for duplicate records and missing values.

Findings:

* 5 duplicate rows were identified.
* Missing values were found in:

  * city: 3
  * quantity: 2
  * unit_price: 7

These issues were addressed during the cleaning stage.

## 4. Data Cleaning

A cleaned dataset named `df_clean` was created.

Cleaning actions included:

* Removing 5 duplicate rows.
* Filling missing city values using the mode.
* Filling missing quantity values using the median.
* Filling missing unit_price values using the median.

After cleaning, the dataset contained:

* No duplicate rows.
* No missing values.

Therefore, `df_clean` was used as the analytical source of truth for this project.

## 5. Data Transformation

The key business metric selected for lineage validation was Net Sales.

The calculation was performed in three stages.

### Gross Sales

`Gross Sales = Quantity × Unit Price`

### Discount Amount

`Discount Amount = Gross Sales × Discount % / 100`

### Net Sales

`Net Sales = Gross Sales − Discount Amount`

## 6. Source of Truth

For this project, `df_clean` is the source of truth for analytical calculations because it is the cleaned and validated version of the original dataset.

The original CSV remains the source of the raw records, while `df_clean` is the source used for analysis and reporting.

## 7. Key Metric Validation

The final calculated metric was:

**Total Net Sales = ₹323,569.50**

The metric was independently validated by comparing the calculated total with the sum of all individual `net_sales` values.

Validation result:

**True**

This confirms that the final metric can be traced from the underlying transaction-level data through the documented transformation steps.

## 8. Data Ownership

| Stage                  | Owner                      |
| ---------------------- | -------------------------- |
| Raw data source        | Data source / sales system |
| Data loading           | Data Analyst               |
| Data validation        | Data Analyst               |
| Data cleaning          | Data Analyst               |
| Data transformation    | Data Analyst               |
| Analysis and reporting | Data Analyst               |
| Business decision      | Business / Management      |

## 9. Retention and Privacy

Source and analytical data should be retained according to the applicable project or company data-retention policy.

Customer-related fields should be protected and accessed only when required for the analysis.

When the applicable retention period ends, data should be securely archived or removed according to the relevant policy.

## 10. End-to-End Lineage

The complete lineage is:

**Raw CSV → Pandas DataFrame → Validation → Cleaning → `df_clean` → Gross Sales → Discount Amount → Net Sales → Reporting → Business Decision**

This demonstrates how a business metric can be traced from its original data source to its final use.
