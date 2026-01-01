# Lecture Notes  
## 1.0 Introduction: Why Data Preparation Is the Core of Effective Data Visualization

Before any meaningful or aesthetically compelling data visualization can be produced, a critical prerequisite must be addressed: **data preparation**. The integrity, accuracy, and interpretability of a visualization are fundamentally determined by the quality of the underlying data. If raw data contain missing values, inconsistencies, extreme outliers, or incorrect data types, the resulting visualizations may misrepresent reality and lead to flawed analytical conclusions.

From a theoretical perspective, data visualization functions as a *mapping* between data and visual encodings (e.g., position, color, size). When the input data are unreliable, this mapping becomes distorted. Consequently, data preparation should not be viewed as a purely technical preprocessing step, but rather as a **methodological foundation** for valid data analysis and trustworthy visual communication.

This workshop module is designed to establish that foundation through hands-on practice with Python and the `pandas` library.

### Learning Outcomes

By the end of this module, students will be able to:

- **Explain the systematic process of data preparation** prior to visualization.
- **Recognize and evaluate data quality issues**, including missing values, outliers, and formatting problems.
- **Apply basic data preparation techniques** using Python to improve dataset reliability for visualization tasks.

---

## 2.0 Data Preparation Workflow: From Raw Data to Visualization-Ready Data

Data preparation typically follows a structured workflow consisting of inspection, diagnosis, and transformation. This workflow reflects best practices in data science and ensures that decisions made during cleaning are transparent and justifiable.

In this module, we demonstrate the workflow using a sample dataset: `student-raw.csv`.

---

## 2.1 Initial Step: Data Loading and Exploratory Inspection

The first step is to load the dataset into the analytical environment.

```python
import pandas as pd

# Load raw dataset
df = pd.read_csv("student-raw.csv")
````

Once the data are loaded, **exploratory inspection** is essential. The goal at this stage is not to fix problems, but to *identify* them.

### 2.1.1 Previewing the Data Structure

```python
# Display the first five rows
df.head()
```

This operation provides an immediate sense of:

* Column names
* Data formats
* Obvious inconsistencies or anomalies

### 2.1.2 Understanding Dataset Dimensions

```python
# Dataset dimensions (rows, columns)
df.shape
```

Knowing the size of the dataset helps contextualize later findings, such as the proportion of missing values.

### 2.1.3 Statistical Summary for Early Diagnostics

```python
# Statistical summary
df.describe(include="all")
```

From a theoretical standpoint, this summary supports *data validation*. Key indicators include:

* **Missing Values**: If the `count` of a column is less than the total number of rows, missing values are present.
* **Potential Outliers**: Implausible minimum or maximum values (e.g., GPA < 0 or GPA > 4.0) suggest data entry or measurement errors.

---

## 2.2 Addressing Data Quality Issues

After identifying potential problems, the next stage involves **data quality management**. In this module, we focus on three core issues: missing values, outliers, and data formatting.

---

## 2.2.1 Handling Missing Values

Missing data are common in real-world datasets and do not necessarily imply error. However, they must be handled deliberately.

### Common Strategies (Theoretical Overview)

1. **Deletion (Dropping)**
   Appropriate when missing values are rare and randomly distributed.

2. **Imputation (Replacement)**
   Suitable when preserving sample size is important (e.g., replacing with mean or median).

3. **Retention for Pattern Analysis**
   Used when missingness itself may convey information.

### Practical Inspection

```python
# Count missing values per column
df.isna().sum()
```

### Example: Mean Imputation for GPA

```python
# Replace missing GPA values with the mean
df["gpa"] = df["gpa"].fillna(df["gpa"].mean())
```

While mean imputation preserves dataset size, it slightly reduces variance. This trade-off must be considered when interpreting visualizations derived from the cleaned data.

---

## 2.2.2 Identifying and Interpreting Outliers

Outliers are values that deviate markedly from the majority of observations. Statistically, they may arise from:

* Measurement or data entry errors
* Rare but valid real-world events

```python
# Inspect GPA distribution statistics
df["gpa"].describe()
```

**Important principle:**
Outliers should not be removed automatically. Their treatment must be guided by domain knowledge and analytical goals, especially because outliers can significantly influence visual scales and perceived patterns.

---

## 2.2.3 Data Formatting and Type Consistency

Correct data types are essential for effective visualization. For example, time-series visualizations require date variables to be stored in a datetime format.

```python
# Inspect data types
df.dtypes
```

### Converting Date Columns

```python
# Convert enrollment_date to datetime
df["enrollment_date"] = pd.to_datetime(df["enrollment_date"])
```

This transformation enables chronological sorting, time-based aggregation, and temporal visualization.

---

## 3.0 Tangible Outcomes: Comparing Data Before and After Preparation

Evaluating the impact of data preparation is a critical analytical step. It ensures that cleaning operations have improved data quality without introducing unintended bias.

```python
# Raw dataset snapshot
df_raw = pd.read_csv("student-raw.csv")

# Cleaned dataset snapshot
df_clean = df.copy()

# Statistical comparison
df_raw.describe()
df_clean.describe()
```

### Analytical Reflection

Even small changes in summary statistics (e.g., mean or maximum GPA) can lead to substantially different visual narratives.

Key questions to consider:

* **Impact on Visualization**: How do distributions and trends differ before and after cleaning?
* **Impact on Interpretation**: Would analytical conclusions change based on the cleaned data?

These reflections emphasize that data preparation is an interpretive process, not merely a mechanical one.

---

## 4.0 Summary and Further Learning Directions

Data preparation is the foundational stage of the data visualization pipeline. High-quality visualizations emerge not from sophisticated charts alone, but from **carefully examined and thoughtfully cleaned data**.

### Key Takeaways

1. Data preparation directly determines the credibility of visualizations.
2. Exploratory inspection is essential before applying cleaning techniques.
3. Handling missing values and outliers requires both technical methods and contextual judgment.

> **Good visualization starts with good data.**

---

## Self-Study Exercises

To deepen understanding, students are encouraged to:

* Create boxplots comparing GPA distributions before and after data preparation.
* Experiment with alternative missing-value strategies (e.g., median imputation, row deletion).
* Analyze how each strategy alters the resulting visualizations and insights.

