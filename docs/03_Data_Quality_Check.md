# 3. Data Quality Check

Before conducting exploratory data analysis, a data quality assessment was performed to identify potential issues that might affect subsequent analyses.

The objective of this section is to evaluate data completeness and determine whether missing values could influence the reliability of business insights.

---

## 3.1 Missing Value Inspection

The first step was to examine missing values across all columns.

### Python Code

```python
df.isnull().sum()
```

### Finding

The inspection shows that only three temporal features contain missing values, while all behavioural features remain complete.

Three temporal columns (`time`, `date`, and `timestamp`) each contain **181,992 missing values**, accounting for approximately **3.9%** of the dataset.

---

## 3.2 Validation

A preliminary observation suggested that the three temporal columns contain exactly the same number of missing values.

This raised an important question:

> Do these missing values belong to the same group of records?

To verify this assumption, a subset containing records with missing `time` values was created.

### Python Code

```python
missing_data = df[df["time"].isnull()]
```

Then the missing values in `date` and `timestamp` were examined.

```python
missing_data["date"].isnull().sum()

missing_data["timestamp"].isnull().sum()
```

### Finding

The validation confirms that all records with missing `time` also have missing `date` and `timestamp`.

This indicates that the missing temporal information consistently occurs within the same group of records.

---

## 3.3 Impact Assessment

Approximately **3.9%** of the dataset contains missing temporal information.

These records can still be used for analyses unrelated to time, such as user behaviour or video engagement.

However, they should be excluded from analyses involving temporal patterns or user activity over time.

At this stage, the missing ratio does not appear sufficiently large to affect the overall reliability of the dataset.

---

## 3.4 Next Step

The next step is to investigate whether missing temporal information is evenly distributed across different users.

If missing values are concentrated within only a few users, time-based analyses for those users may be unreliable.

Otherwise, if missing values are randomly distributed across users, their impact is expected to be minimal.
