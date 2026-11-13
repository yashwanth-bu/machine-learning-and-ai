# Pandas for Data Analysis and Machine Learning: Complete Learning Roadmap

## 1. Introduction to Pandas

### What is Pandas?

**Pandas** is a Python library used to read, organize, clean, transform, analyze, and prepare structured data.

It is commonly used in:

- Data Analysis
- Data Science
- Machine Learning
- Data Preparation
- Statistical Analysis
- Time Series Analysis

Pandas helps convert raw data into a clean and meaningful format that can be used for analysis and Machine Learning.

### Installation

```bash
pip install pandas
```

### Import Pandas

```python
import pandas as pd
```

---

# PART 1: Pandas Fundamentals

## 2. Core Data Structures

Pandas mainly provides two important data structures: Series and DataFrame.

### A. Series

A Series is a one-dimensional labeled data structure.

It is similar to a single column in an Excel spreadsheet.

Example:

```python
import pandas as pd

ages = pd.Series([21, 25, 30, 35])

print(ages)
```

Output:

```text
0    21
1    25
2    30
3    35
dtype: int64
```

Important properties:

| Property   | Purpose                  |
| ---------- | ------------------------ |
| `values` | Access underlying values |
| `index`  | Access index labels      |
| `dtype`  | Get data type            |
| `shape`  | Get dimensions           |
| `size`   | Get number of elements   |

### B. DataFrame

A DataFrame is a two-dimensional, labeled data structure containing rows and columns.

It is similar to an Excel spreadsheet or database table.

Example:

```python
data = {
    "Name": ["John", "David", "Alex"],
    "Age": [21, 25, 30],
    "Salary": [25000, 35000, 45000]
}

df = pd.DataFrame(data)

print(df)
```

Output:

```text
    Name  Age  Salary
0   John   21   25000
1  David   25   35000
2   Alex   30   45000
```

Important properties:

| Property       | Purpose                    |
| -------------- | -------------------------- |
| `df.shape`   | Number of rows and columns |
| `df.columns` | Column names               |
| `df.index`   | Row index                  |
| `df.dtypes`  | Data types                 |
| `df.values`  | Underlying values          |
| `df.size`    | Total number of elements   |
| `df.ndim`    | Number of dimensions       |

### C. Index

An Index represents the labels used to identify rows or columns.

Example:

```python
df = pd.DataFrame(
    {"Name": ["John", "David", "Alex"]},
    index=[101, 102, 103]
)

print(df.index)
```

Output:

```text
Index([101, 102, 103], dtype='int64')
```

Important concepts:

- Default Index
- Custom Index
- Setting an Index: `set_index()`
- Resetting an Index: `reset_index()`
- Index lookup
- Index alignment

An Index is designed to be immutable, meaning its labels cannot be modified directly.

---

## 3. Reading and Writing Data Files

### What is Data Loading?

Data loading means importing external data files into Python for processing and analysis.

Pandas supports multiple file formats.

### Important functions

| Function              | Purpose                |
| --------------------- | ---------------------- |
| `pd.read_csv()`     | Read CSV files         |
| `pd.read_excel()`   | Read Excel files       |
| `pd.read_json()`    | Read JSON files        |
| `pd.read_sql()`     | Read SQL database data |
| `pd.read_parquet()` | Read Parquet files     |
| `pd.read_html()`    | Read HTML tables       |
| `df.to_csv()`       | Save as CSV            |
| `df.to_excel()`     | Save as Excel          |
| `df.to_json()`      | Save as JSON           |
| `df.to_parquet()`   | Save as Parquet        |

### Example: Read CSV

```python
import pandas as pd

df = pd.read_csv("data.csv")

print(df)
```

### Example: Read Excel

```python
df = pd.read_excel("data.xlsx")
```

### Example: Save Data

```python
df.to_csv("output.csv", index=False)
```

The `index=False` argument prevents Pandas from saving the DataFrame index as an additional column.

---

## 4. Data Inspection

### What is Data Inspection?

Data inspection means understanding the dataset before cleaning or analyzing it.

It helps us understand:

- Number of rows and columns.
- Available features.
- Data types.
- Missing values.
- Statistical information.
- Unique values.
- Data distribution.

### Important functions

| Function           | Purpose                     |
| ------------------ | --------------------------- |
| `head()`         | Display first 5 rows        |
| `tail()`         | Display last 5 rows         |
| `sample()`       | Display random rows         |
| `shape`          | Get dimensions              |
| `info()`         | Get dataset information     |
| `describe()`     | Get statistical information |
| `columns`        | Display column names        |
| `dtypes`         | Display data types          |
| `unique()`       | Get unique values           |
| `nunique()`      | Count unique values         |
| `value_counts()` | Count occurrences           |
| `memory_usage()` | Check memory consumption    |

### Example

```python
print(df.head())
print(df.tail())
print(df.sample(5))

print(df.shape)
print(df.info())
print(df.describe())

print(df.columns)
print(df.dtypes)
```

### Understanding Statistical Information

```python
print(df["Age"].mean())
print(df["Age"].median())
print(df["Age"].mode())
print(df["Age"].min())
print(df["Age"].max())
print(df["Age"].std())
```

These functions help understand numerical data.

---

## 5. Data Selection and Indexing

### What is Data Selection?

Data selection means extracting specific rows and columns from a DataFrame.

It allows us to work with only the information required for analysis.

### A. Selecting Columns

```python
df["Age"]
```

Select multiple columns:

```python
df[["Name", "Age", "Salary"]]
```

### B. Label-Based Indexing: loc[]

`loc[]` selects data using row and column labels.

```python
df.loc[0:2, ["Name", "Age"]]
```

Selects rows with index labels 0, 1, and 2.

Important: The ending label is included when slicing with `loc[]`.

### C. Position-Based Indexing: iloc[]

`iloc[]` selects data using integer positions.

```python
df.iloc[0:3, 0:2]
```

Selects the first three rows and first two columns.

Important: The ending position is excluded, following normal Python slicing rules.

### D. Boolean Indexing

Boolean indexing selects rows based on conditions.

```python
df[df["Age"] > 25]
```

Multiple conditions:

```python
df[
    (df["Age"] > 25) &
    (df["Salary"] > 30000)
]
```

Use:

- `&` for AND
- `|` for OR
- `~` for NOT

### E. Querying

The `query()` method filters data using readable string expressions.

```python
df.query("Age > 25")
```

Multiple conditions:

```python
df.query("Age > 25 and Salary > 30000")
```

### F. Indexing and Slicing

```python
df["Age"][0:3]

df.iloc[0:5]

df.loc[0:5]
```

---

# PART 2: Data Cleaning and Preparation

## 6. Data Cleaning

### What is Data Cleaning?

Data cleaning means identifying and correcting inaccurate, inconsistent, duplicate, or unnecessary data.

Real-world datasets often contain:

- Duplicate records.
- Incorrect values.
- Unnecessary columns.
- Extra spaces.
- Inconsistent naming.
- Invalid data.

### Important functions

| Function              | Purpose                  |
| --------------------- | ------------------------ |
| `drop()`            | Remove rows or columns   |
| `drop_duplicates()` | Remove duplicate records |
| `duplicated()`      | Identify duplicates      |
| `rename()`          | Rename columns           |
| `replace()`         | Replace values           |
| `sort_values()`     | Sort data                |
| `sort_index()`      | Sort by index            |

### Example: Remove Duplicates

```python
df = df.drop_duplicates()
```

Check duplicates:

```python
print(df.duplicated().sum())
```

### Example: Remove a Column

```python
df = df.drop("Salary", axis=1)
```

### Example: Rename Columns

```python
df = df.rename(
    columns={"Age": "Student_Age"}
)
```

### Example: Remove Extra Spaces

```python
df["Name"] = df["Name"].str.strip()
```

### Example: Replace Values

```python
df["City"] = df["City"].replace(
    "Bangalore",
    "Bengaluru"
)
```

---

## 7. Missing Value Handling

### What are Missing Values?

Missing values represent information that is unavailable in a dataset.

Examples:

- Empty cells.
- `NaN`.
- `None`.
- `NaT` for missing date/time values.

Missing values can affect statistical calculations and Machine Learning algorithms.

### Important functions

| Function      | Purpose                   |
| ------------- | ------------------------- |
| `isnull()`  | Identify missing values   |
| `isna()`    | Identify missing values   |
| `notnull()` | Identify available values |
| `fillna()`  | Replace missing values    |
| `dropna()`  | Remove missing values     |

### A. Detect Missing Values

```python
print(df.isnull())
```

Count missing values:

```python
print(df.isnull().sum())
```

Calculate missing percentage:

```python
missing_percentage = (
    df.isnull().mean() * 100
)

print(missing_percentage)
```

### B. Remove Missing Values

```python
df = df.dropna()
```

Remove rows where a particular column is missing:

```python
df = df.dropna(subset=["Age"])
```

### C. Fill Missing Values

Fill with mean:

```python
df["Age"] = df["Age"].fillna(
    df["Age"].mean()
)
```

Fill with median:

```python
df["Salary"] = df["Salary"].fillna(
    df["Salary"].median()
)
```

Fill with a fixed value:

```python
df["City"] = df["City"].fillna("Unknown")
```

Fill with the previous available value:

```python
df = df.ffill()
```

Fill with the next available value:

```python
df = df.bfill()
```

### Important Concept

Different missing-value strategies are suitable for different data.

- Mean: Useful for relatively symmetric numerical data.
- Median: Useful when numerical data contains outliers or is skewed.
- Mode: Useful for categorical data.
- Constant values: Useful when missingness has a meaningful interpretation.

For Machine Learning, calculate imputation values using training data only to prevent data leakage.

---

## 8. Data Type Handling

### What is Data Type Handling?

Data type handling means checking and converting columns into their appropriate data types.

Sometimes numerical values are stored as strings, and dates are stored as ordinary text.

These must be corrected before calculations or Machine Learning operations.

### Common Data Types

| Data Type      | Meaning                      |
| -------------- | ---------------------------- |
| `int64`      | Whole numbers                |
| `float64`    | Decimal numbers              |
| `object`     | Usually text or mixed values |
| `string`     | String values                |
| `bool`       | True or False                |
| `datetime64` | Date and time                |
| `category`   | Categorical values           |

### Important functions

| Function             | Purpose                     |
| -------------------- | --------------------------- |
| `dtypes`           | Check data types            |
| `astype()`         | Convert data types          |
| `pd.to_numeric()`  | Convert values into numbers |
| `pd.to_datetime()` | Convert values into dates   |

### Example: Convert String to Integer

```python
df["Age"] = df["Age"].astype(int)
```

### Example: Convert Text to Numbers

```python
df["Salary"] = pd.to_numeric(
    df["Salary"],
    errors="coerce"
)
```

Invalid values become `NaN`.

### Example: Convert Text to Dates

```python
df["Date"] = pd.to_datetime(
    df["Date"],
    errors="coerce"
)
```

### Example: Convert to Categorical Data

```python
df["Gender"] = df["Gender"].astype("category")
```

---

## 9. String Manipulation

### What is String Manipulation?

String manipulation means modifying, cleaning, searching, and extracting information from text columns.

Pandas provides the `.str` accessor for vectorized string operations.

### Important functions

| Function              | Purpose                      |
| --------------------- | ---------------------------- |
| `.str.lower()`      | Convert to lowercase         |
| `.str.upper()`      | Convert to uppercase         |
| `.str.strip()`      | Remove surrounding spaces    |
| `.str.len()`        | Calculate text length        |
| `.str.contains()`   | Search for a pattern         |
| `.str.replace()`    | Replace text                 |
| `.str.split()`      | Split text                   |
| `.str.startswith()` | Check starting text          |
| `.str.endswith()`   | Check ending text            |
| `.str.extract()`    | Extract patterns using regex |

### Examples

Convert names to lowercase:

```python
df["Name"] = df["Name"].str.lower()
```

Remove unwanted spaces:

```python
df["Name"] = df["Name"].str.strip()
```

Find names containing John:

```python
df[df["Name"].str.contains(
    "john",
    case=False,
    na=False
)]
```

Extract first names:

```python
df["First_Name"] = (
    df["Name"].str.split().str[0]
)
```

---

# PART 3: Data Transformation and Feature Engineering

## 10. Data Transformation

### What is Data Transformation?

Data transformation means modifying existing data into a more useful format.

It helps us:

- Change existing values.
- Create new values.
- Convert categories.
- Apply mathematical operations.
- Prepare data for analysis.

### Important functions

| Function          | Purpose                               |
| ----------------- | ------------------------------------- |
| `apply()`       | Apply functions to rows or columns    |
| `map()`         | Map values in a Series                |
| `replace()`     | Replace existing values               |
| `assign()`      | Create or modify columns              |
| `where()`       | Keep values satisfying a condition    |
| `mask()`        | Replace values satisfying a condition |
| `clip()`        | Restrict values to a range            |
| `sort_values()` | Sort values                           |

### A. apply()

Apply a custom function to a Series or DataFrame.

```python
df["Age"] = df["Age"].apply(
    lambda x: x + 1
)
```

Apply to rows:

```python
df["Total"] = df.apply(
    lambda row: row["Maths"] + row["Science"],
    axis=1
)
```

### B. map()

Map individual Series values using a dictionary or function.

```python
df["Gender"] = df["Gender"].map({
    "Male": 1,
    "Female": 0
})
```

Unmapped values become missing values.

### C. replace()

```python
df["City"] = df["City"].replace(
    "Bangalore",
    "Bengaluru"
)
```

### D. assign()

Create a new column:

```python
df = df.assign(
    Bonus=df["Salary"] * 0.10
)
```

### Important Difference

- `map()`: Primarily used for element-wise mapping of Series values.
- `apply()`: Applies a function along a Series or DataFrame axis.
- Vectorized operations: Usually faster and preferred for ordinary mathematical transformations.

---

## 11. Feature Extraction

### What is Feature Extraction?

Feature extraction means creating useful information from existing data.

In Machine Learning, these extracted values become features used by algorithms to identify patterns and make predictions.

### A. Date Feature Extraction

Extract useful information from date columns.

```python
df["Date"] = pd.to_datetime(df["Date"])

df["Year"] = df["Date"].dt.year

df["Month"] = df["Date"].dt.month

df["Day"] = df["Date"].dt.day

df["Day_Name"] = df["Date"].dt.day_name()

df["Hour"] = df["Date"].dt.hour
```

### B. Text Feature Extraction

```python
df["Name_Length"] = df["Name"].str.len()

df["First_Name"] = (
    df["Name"].str.split().str[0]
)
```

Extract email domains:

```python
df["Email_Domain"] = (
    df["Email"].str.split("@").str[-1]
)
```

### C. Numerical Feature Extraction

Create features using mathematical operations.

```python
df["Total"] = (
    df["Maths"] + df["Science"]
)

df["Average"] = df["Total"] / 2
```

Create age groups:

```python
df["Age_Group"] = pd.cut(
    df["Age"],
    bins=[0, 18, 30, 50, 100],
    labels=["Child", "Young", "Adult", "Senior"]
)
```

### Why is Feature Extraction Important?

- Creates meaningful information.
- Identifies useful patterns.
- Improves model performance when useful features are created.
- Converts raw information into model-ready features.

---

## 12. Sorting and Ranking

### Sorting

Sorting means arranging data based on values or index labels.

Sort by one column:

```python
df = df.sort_values("Age")
```

Descending order:

```python
df = df.sort_values(
    "Salary",
    ascending=False
)
```

Sort by multiple columns:

```python
df = df.sort_values(
    ["Age", "Salary"],
    ascending=[True, False]
)
```

Sort by index:

```python
df = df.sort_index()
```

### Ranking

Ranking assigns positions to values based on their order.

```python
df["Salary_Rank"] = df["Salary"].rank()
```

Descending ranking:

```python
df["Salary_Rank"] = df["Salary"].rank(
    ascending=False
)
```

Important methods:

- `average`
- `min`
- `max`
- `first`
- `dense`

Example:

```python
df["Rank"] = df["Salary"].rank(
    method="dense",
    ascending=False
)
```

---

## 13. Grouping and Aggregation

### What is groupby()?

`groupby()` divides a DataFrame into groups based on one or more columns.

It follows three main steps:

1. Split: Divide data into groups.
2. Apply: Perform operations on each group.
3. Combine: Collect the results.

Example dataset:

```python
data = {
    "Department": [
        "IT", "HR", "IT", "HR", "Finance"
    ],
    "Salary": [
        40000, 30000, 50000, 35000, 45000
    ]
}

df = pd.DataFrame(data)
```

### A. Group Data

```python
df.groupby("Department")
```

### B. Calculate Mean

```python
df.groupby("Department")["Salary"].mean()
```

### C. Multiple Aggregations

`agg()` allows multiple statistical operations.

```python
df.groupby("Department").agg({
    "Salary": ["mean", "max", "min", "count"]
})
```

### D. Group by Multiple Columns

```python
df.groupby(
    ["Department", "Gender"]
)["Salary"].mean()
```

### Important Functions

| Function        | Purpose                                             |
| --------------- | --------------------------------------------------- |
| `groupby()`   | Create groups                                       |
| `agg()`       | Perform multiple aggregations                       |
| `sum()`       | Calculate total                                     |
| `mean()`      | Calculate average                                   |
| `median()`    | Calculate median                                    |
| `count()`     | Count non-missing values                            |
| `size()`      | Count rows in each group                            |
| `min()`       | Minimum value                                       |
| `max()`       | Maximum value                                       |
| `std()`       | Standard deviation                                  |
| `transform()` | Return group-based results aligned to original rows |
| `filter()`    | Keep or remove entire groups                        |

### E. transform()

Unlike aggregation, `transform()` returns results aligned with the original DataFrame.

```python
df["Department_Average"] = (
    df.groupby("Department")["Salary"]
      .transform("mean")
)
```

---

## 14. Correlation Analysis

### What is Correlation?

Correlation measures the strength and direction of the relationship between two numerical variables.

It helps us understand whether two variables tend to change together.

### Correlation Values

| Value | Meaning                      |
| ----- | ---------------------------- |
| +1    | Perfect positive correlation |
| 0     | No linear correlation        |
| -1    | Perfect negative correlation |

### Types of Correlation

**1. Positive Correlation**

When one variable increases, another variable tends to increase.

Example: Study hours and examination marks.

**2. Negative Correlation**

When one variable increases, another variable tends to decrease.

Example: Speed and travel time for a fixed distance.

**3. No Linear Correlation**

There is little or no linear relationship between two variables.

### Important function

`corr()` calculates correlation between numerical columns.

```python
correlation = df.corr(numeric_only=True)

print(correlation)
```

### Correlation Methods

```python
df.corr(method="pearson", numeric_only=True)

df.corr(method="spearman", numeric_only=True)

df.corr(method="kendall", numeric_only=True)
```

- Pearson: Measures linear correlation.
- Spearman: Measures rank-based monotonic relationships.
- Kendall: Measures rank association.

### Find Highly Correlated Features

```python
correlation = df.corr(numeric_only=True)

high_corr = correlation[
    (correlation > 0.8) &
    (correlation < 1.0)
]

print(high_corr)
```

### Why is Correlation Analysis Important?

- Understand relationships between features.
- Identify redundant features.
- Support feature selection.
- Understand numerical patterns.

Important: Correlation does not establish causation. High correlation does not automatically mean a feature should be removed.

---

# PART 4: Combining and Reshaping Data

## 15. Merging and Joining

### What is Merging?

Merging combines two DataFrames using common columns or keys.

It is similar to SQL JOIN operations.

Example:

```python
students = pd.DataFrame({
    "Student_ID": [1, 2, 3],
    "Name": ["John", "David", "Alex"]
})

marks = pd.DataFrame({
    "Student_ID": [1, 2, 3],
    "Marks": [85, 90, 75]
})
```

### A. Inner Join

Returns only matching records.

```python
result = pd.merge(
    students,
    marks,
    on="Student_ID",
    how="inner"
)
```

### B. Left Join

Returns all records from the left DataFrame and matching records from the right.

```python
result = pd.merge(
    students,
    marks,
    on="Student_ID",
    how="left"
)
```

### C. Right Join

Returns all records from the right DataFrame.

```python
result = pd.merge(
    students,
    marks,
    on="Student_ID",
    how="right"
)
```

### D. Outer Join

Returns all records from both DataFrames.

```python
result = pd.merge(
    students,
    marks,
    on="Student_ID",
    how="outer"
)
```

### Important Parameters

| Parameter     | Purpose                            |
| ------------- | ---------------------------------- |
| `on`        | Common column                      |
| `left_on`   | Key from left DataFrame            |
| `right_on`  | Key from right DataFrame           |
| `how`       | Type of join                       |
| `suffixes`  | Rename overlapping columns         |
| `validate`  | Validate relationship between keys |
| `indicator` | Identify the source of merged rows |

### E. join()

`join()` is commonly used to combine DataFrames using their indexes.

```python
result = students.join(
    marks.set_index("Student_ID"),
    on="Student_ID"
)
```

---

## 16. Concatenation

### What is Concatenation?

Concatenation combines multiple DataFrames vertically or horizontally.

### A. Vertical Concatenation

Stacks DataFrames row by row.

```python
result = pd.concat(
    [df1, df2],
    axis=0,
    ignore_index=True
)
```

### B. Horizontal Concatenation

Combines DataFrames column by column using their indexes.

```python
result = pd.concat(
    [df1, df2],
    axis=1
)
```

### Important Parameters

- `axis=0`: Combine rows.
- `axis=1`: Combine columns.
- `ignore_index=True`: Create a new sequential index.
- `join="outer"`: Keep the union of labels.
- `join="inner"`: Keep common labels.

---

## 17. Pivoting and Melting

### What is Reshaping?

Reshaping changes the structure of a DataFrame without necessarily changing the underlying information.

Two important operations are Pivoting and Melting.

### A. pivot()

Converts long-format data into wide-format data.

```python
df = pd.DataFrame({
    "Name": ["John", "John", "David", "David"],
    "Subject": ["Maths", "Science", "Maths", "Science"],
    "Marks": [80, 90, 70, 85]
})

result = df.pivot(
    index="Name",
    columns="Subject",
    values="Marks"
)
```

### B. pivot_table()

Similar to `pivot()`, but supports aggregation when multiple records exist for the same combination.

```python
result = df.pivot_table(
    index="Name",
    columns="Subject",
    values="Marks",
    aggfunc="mean"
)
```

### C. melt()

Converts wide-format data into long-format data.

```python
result = pd.melt(
    df,
    id_vars=["Name"],
    var_name="Subject",
    value_name="Marks"
)
```

Important distinction:

- `pivot()`: Reshapes without aggregation and requires unique index-column combinations.
- `pivot_table()`: Reshapes and aggregates duplicate combinations.
- `melt()`: Converts columns into rows.

---

## 18. Stack and Unstack

These operations are used to reshape hierarchical or MultiIndex data.

### A. stack()

Moves column levels into the row index.

```python
result = df.stack()
```

### B. unstack()

Moves index levels into columns.

```python
result = df.unstack()
```

These operations are particularly useful when working with MultiIndex DataFrames.

---

# PART 5: Advanced Pandas Concepts

## 19. MultiIndex (Hierarchical Indexing)

### What is MultiIndex?

MultiIndex allows a DataFrame to have multiple levels of indexes on a single axis.

It helps represent complex, hierarchical data.

Example:

```python
data = {
    "Sales": [10000, 15000, 20000, 25000]
}

index = pd.MultiIndex.from_tuples([
    ("India", "Bangalore"),
    ("India", "Mumbai"),
    ("USA", "New York"),
    ("USA", "California")
], names=["Country", "City"])

df = pd.DataFrame(
    data,
    index=index
)

print(df)
```

### Important Functions

| Function                     | Purpose                       |
| ---------------------------- | ----------------------------- |
| `MultiIndex.from_tuples()` | Create MultiIndex from tuples |
| `set_index()`              | Set multiple index columns    |
| `reset_index()`            | Convert indexes into columns  |
| `swaplevel()`              | Exchange index levels         |
| `sort_index()`             | Sort hierarchical indexes     |
| `xs()`                     | Select cross-sections         |

### Example: Select Data

```python
df.loc["India"]
```

Select a particular country and city:

```python
df.loc[("India", "Bangalore")]
```

---

## 20. Window Operations

### What are Window Operations?

Window operations calculate statistics over a moving or expanding section of data.

They are useful for:

- Financial analysis.
- Time series analysis.
- Trend detection.
- Moving averages.
- Cumulative calculations.

### A. rolling()

Calculates statistics over a fixed-size moving window.

```python
df["Moving_Average"] = (
    df["Sales"].rolling(window=3).mean()
)
```

This calculates the average of the current row and the previous two rows.

### B. expanding()

Calculates statistics using all available values from the beginning up to the current row.

```python
df["Cumulative_Average"] = (
    df["Sales"].expanding().mean()
)
```

### C. ewm()

Calculates exponentially weighted statistics.

Recent observations receive more weight than older observations.

```python
df["EMA"] = (
    df["Sales"].ewm(span=3).mean()
)
```

### D. Cumulative Operations

```python
df["Cumulative_Sum"] = df["Sales"].cumsum()

df["Cumulative_Max"] = df["Sales"].cummax()

df["Cumulative_Min"] = df["Sales"].cummin()

df["Cumulative_Product"] = df["Sales"].cumprod()
```

---

## 21. Time Series Analysis

### What is Time Series Data?

Time series data consists of observations collected over time.

Examples:

- Daily stock prices.
- Monthly sales.
- Hourly temperatures.
- Website traffic.
- Daily electricity consumption.

Pandas provides specialized functionality for working with dates and time-based data.

### A. Convert to Datetime

```python
df["Date"] = pd.to_datetime(df["Date"])
```

### B. Extract Date Components

```python
df["Year"] = df["Date"].dt.year

df["Month"] = df["Date"].dt.month

df["Day"] = df["Date"].dt.day

df["Weekday"] = df["Date"].dt.dayofweek
```

### C. Set Date as Index

```python
df = df.set_index("Date")
```

### D. Resampling

Resampling changes the frequency of time series data.

Daily data into monthly data:

```python
monthly_sales = df["Sales"].resample("ME").sum()
```

Daily data into weekly averages:

```python
weekly_average = df["Sales"].resample("W").mean()
```

### E. shift()

Moves values forward or backward by a specified number of periods.

```python
df["Previous_Sales"] = df["Sales"].shift(1)
```

### F. Time Differences

```python
df["Sales_Change"] = (
    df["Sales"] - df["Sales"].shift(1)
)
```

### G. Time Zone Conversion

```python
df.index = df.index.tz_localize("UTC")

df.index = df.index.tz_convert(
    "Asia/Kolkata"
)
```

---

## 22. Categorical Data

### What is Categorical Data?

Categorical data represents values belonging to a limited number of categories.

Examples:

- Gender.
- City.
- Department.
- Product type.
- Education level.

Pandas provides `category` to represent categorical data efficiently.

### Example

```python
df["Department"] = df["Department"].astype("category")
```

### Create Categories Manually

```python
df["Size"] = pd.Categorical(
    df["Size"],
    categories=["Small", "Medium", "Large"],
    ordered=True
)
```

### Important Functions

| Function                            | Purpose                  |
| ----------------------------------- | ------------------------ |
| `astype("category")`              | Convert to categorical   |
| `pd.Categorical()`                | Create categorical data  |
| `.cat.categories`                 | Get available categories |
| `.cat.codes`                      | Get category codes       |
| `.cat.rename_categories()`        | Rename categories        |
| `.cat.add_categories()`           | Add categories           |
| `.cat.remove_unused_categories()` | Remove unused categories |

Categorical data can reduce memory usage when a column contains a limited number of repeated values.

---

# PART 6: Pandas for Machine Learning

## 23. Understanding Machine Learning Data

### What is Machine Learning Data Preparation?

Machine Learning algorithms require structured and appropriately prepared input data.

Raw datasets usually cannot be passed directly into every algorithm.

We need to:

- Clean the data.
- Handle missing values.
- Convert categorical values.
- Extract useful features.
- Separate inputs and outputs.
- Split the dataset.
- Scale numerical features when required.

Pandas handles much of the data manipulation, while Scikit-learn provides many Machine Learning preprocessing and training tools.

---

## 24. Separating Features (X) and Target (y)

### What are Features?

Features are input variables used by a Machine Learning model to make predictions.

### What is a Target?

The target is the output variable that the model needs to predict.

Example:

```python
X = df[["Age", "Salary", "Experience"]]

y = df["Purchased"]
```

Here:

- X contains input features.
- y contains the target variable.

### Different Types of Machine Learning Problems

**Classification:**

Predicts categories.

Example: Purchased or Not Purchased.

**Regression:**

Predicts numerical values.

Example: Predicting house prices.

**Clustering:**

Groups similar data points without requiring predefined target labels.

Example: Customer segmentation.

---

## 25. Encoding Categorical Data

### What is Encoding?

Encoding converts categorical information into numerical representations that Machine Learning algorithms can process.

### A. Label Mapping

```python
df["Gender"] = df["Gender"].map({
    "Male": 1,
    "Female": 0
})
```

This works when the mapping is appropriate for the feature.

### B. One-Hot Encoding

One-Hot Encoding creates separate binary columns for categories.

```python
df = pd.get_dummies(
    df,
    columns=["City"],
    dtype=int
)
```

Example:

Original:

| City      |
| --------- |
| Bangalore |
| Mumbai    |
| Delhi     |

After encoding:

| City_Bangalore | City_Mumbai | City_Delhi |
| -------------- | ----------- | ---------- |
| 1              | 0           | 0          |
| 0              | 1           | 0          |
| 0              | 0           | 1          |

### C. Ordinal Encoding

Used when categories have a meaningful order.

Example:

```text
Low = 1
Medium = 2
High = 3
```

For more advanced Machine Learning workflows, Scikit-learn provides `OrdinalEncoder` and `OneHotEncoder`.

---

## 26. Train-Test Split

### What is Train-Test Split?

Train-test split divides a dataset into separate portions.

**Training Data:** Used to train the Machine Learning model.

**Testing Data:** Used to evaluate the model on unseen data.

### Example

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)
```

Here:

- 80% of the data is used for training.
- 20% is used for testing.
- `random_state=42` makes the random split reproducible.

### Important Parameters

| Parameter        | Purpose                       |
| ---------------- | ----------------------------- |
| `test_size`    | Testing data percentage       |
| `train_size`   | Training data percentage      |
| `random_state` | Reproducible splitting        |
| `shuffle`      | Shuffle data before splitting |
| `stratify`     | Preserve class proportions    |

For classification problems with imbalanced classes, stratified splitting is often useful.

For time series problems, use chronological splitting instead of randomly shuffling future and past observations.

---

## 27. Normalization and Feature Scaling

### What is Feature Scaling?

Feature scaling brings numerical features into comparable ranges.

Some Machine Learning algorithms are sensitive to differences in feature scales.

Example:

```text
Age       = 25
Salary    = 50000
Experience = 3
```

Salary has a much larger numerical range than the other features.

Scaling helps prevent large numerical ranges from dominating distance-based or gradient-based calculations.

### A. Min-Max Scaling

Transforms values into a specified range, usually 0 to 1.

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()

X_train_scaled = scaler.fit_transform(X_train)

X_test_scaled = scaler.transform(X_test)
```

### B. Standardization

Transforms data to approximately zero mean and unit variance.

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_train_scaled = scaler.fit_transform(X_train)

X_test_scaled = scaler.transform(X_test)
```

### C. Robust Scaling

Uses median and interquartile range, making it less sensitive to outliers.

```python
from sklearn.preprocessing import RobustScaler

scaler = RobustScaler()

X_train_scaled = scaler.fit_transform(X_train)

X_test_scaled = scaler.transform(X_test)
```

### Important Rule: Avoid Data Leakage

Always fit preprocessing operations using training data only.

Correct:

```python
scaler.fit(X_train)

X_train_scaled = scaler.transform(X_train)

X_test_scaled = scaler.transform(X_test)
```

Incorrect:

```python
scaler.fit(X)

X_train_scaled = scaler.transform(X_train)

X_test_scaled = scaler.transform(X_test)
```

The incorrect approach allows information from the testing data to influence preprocessing.

For real Machine Learning projects, Scikit-learn Pipelines are usually safer because they combine preprocessing and model training into one workflow.

---

## 28. Data Leakage and Preprocessing Order

### What is Data Leakage?

Data leakage happens when information that should not be available during training influences the training process.

It can produce misleadingly high evaluation scores.

Common examples:

- Calculating missing-value replacements using the complete dataset before splitting.
- Fitting scalers on training and testing data together.
- Using future information to predict past events.
- Including information that directly reveals the target.

### Recommended Workflow

```text
Raw Dataset
     |
     v
Understand Dataset
     |
     v
Identify Target and Features
     |
     v
Train-Test Split
     |
     v
Handle Missing Values
     |
     v
Encode Categorical Features
     |
     v
Scale Numerical Features
     |
     v
Train Machine Learning Model
     |
     v
Evaluate Using Test Data
```

In practice, fit preprocessing steps on training data and apply the same fitted transformations to testing data.

---

# PART 7: Complete Practical Workflow

## 29. End-to-End Data Preparation Example

This example combines Pandas operations into a practical Machine Learning data preparation workflow.

### Step 1: Create Dataset

```python
import pandas as pd

data = {
    "Age": [22, 25, 30, 35, None, 28],
    "Salary": [25000, 35000, 45000, 55000, 40000, 38000],
    "Experience": [1, 2, 5, 8, 4, 3],
    "Gender": [
        "Male", "Female", "Male",
        "Female", "Male", "Female"
    ],
    "Purchased": [0, 1, 1, 1, 0, 1]
}

df = pd.DataFrame(data)

print(df)
```

### Step 2: Inspect Dataset

```python
print(df.head())

print(df.shape)

print(df.info())

print(df.describe())

print(df.isnull().sum())
```

### Step 3: Handle Missing Values

```python
df["Age"] = df["Age"].fillna(
    df["Age"].median()
)
```

For an actual Machine Learning workflow, calculate the median using training data only.

### Step 4: Encode Categorical Features

```python
df["Gender"] = df["Gender"].map({
    "Male": 1,
    "Female": 0
})
```

### Step 5: Separate Features and Target

```python
X = df[
    ["Age", "Salary", "Experience", "Gender"]
]

y = df["Purchased"]
```

### Step 6: Split Dataset

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42,
    stratify=y
)
```

### Step 7: Scale Features

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_train_scaled = scaler.fit_transform(X_train)

X_test_scaled = scaler.transform(X_test)
```

### Step 8: Train a Machine Learning Model

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression()

model.fit(X_train_scaled, y_train)
```

### Step 9: Make Predictions

```python
predictions = model.predict(X_test_scaled)

print(predictions)
```

### Step 10: Evaluate Model

```python
from sklearn.metrics import accuracy_score

accuracy = accuracy_score(
    y_test,
    predictions
)

print("Accuracy:", accuracy)
```

This demonstrates how Pandas and Scikit-learn work together in a basic Machine Learning workflow.

Note: This is a small demonstration dataset, not a meaningful model evaluation benchmark.

---

# PART 8: Complete Learning Summary

## 30. Pandas Complete Roadmap

| No. | Topic                    | Important Functions / Concepts             |
| --- | ------------------------ | ------------------------------------------ |
| 1   | Core Data Structures     | Series, DataFrame, Index                   |
| 2   | Reading and Writing Data | read_csv, read_excel, to_csv               |
| 3   | Data Inspection          | head, tail, shape, info, describe          |
| 4   | Data Selection           | loc, iloc, Boolean Indexing, query         |
| 5   | Data Cleaning            | drop, drop_duplicates, rename, replace     |
| 6   | Missing Values           | isnull, fillna, dropna                     |
| 7   | Data Types               | astype, to_numeric, to_datetime            |
| 8   | String Manipulation      | str.lower, str.strip, str.contains         |
| 9   | Data Transformation      | apply, map, assign, transform              |
| 10  | Feature Extraction       | dt, str, mathematical operations           |
| 11  | Sorting and Ranking      | sort_values, sort_index, rank              |
| 12  | Grouping and Aggregation | groupby, agg, filter                       |
| 13  | Correlation Analysis     | corr, Pearson, Spearman, Kendall           |
| 14  | Merging and Joining      | merge, join                                |
| 15  | Concatenation            | concat                                     |
| 16  | Reshaping                | pivot, pivot_table, melt                   |
| 17  | Advanced Reshaping       | stack, unstack                             |
| 18  | Hierarchical Indexing    | MultiIndex, set_index, reset_index         |
| 19  | Window Operations        | rolling, expanding, ewm                    |
| 20  | Cumulative Operations    | cumsum, cummax, cummin                     |
| 21  | Time Series Analysis     | resample, shift, timezone conversion       |
| 22  | Categorical Data         | category, Categorical                      |
| 23  | ML Feature Preparation   | X, y, feature extraction                   |
| 24  | Encoding                 | Mapping, One-Hot, Ordinal Encoding         |
| 25  | Train-Test Split         | train_test_split                           |
| 26  | Feature Scaling          | MinMaxScaler, StandardScaler, RobustScaler |
| 27  | Data Leakage Prevention  | Correct preprocessing order                |
| 28  | Complete ML Workflow     | Data preparation, training, evaluation     |

---

# Objective

After completing this roadmap, you should be able to:

1. Load datasets from different file formats.
2. Understand and inspect structured datasets.
3. Select and filter specific data.
4. Clean incorrect, duplicate, and missing values.
5. Handle different data types.
6. Manipulate and extract information from text.
7. Transform existing data and create new features.
8. Perform statistical analysis and correlation analysis.
9. Group, aggregate, merge, and reshape datasets.
10. Work with hierarchical indexes and time series.
11. Prepare numerical and categorical features.
12. Separate input features and target variables.
13. Apply encoding and feature scaling.
14. Split datasets correctly for Machine Learning.
15. Build a complete data preparation workflow using Pandas and Scikit-learn.

**Important distinction:** Pandas is primarily a data manipulation and analysis library. It does not replace NumPy, Scikit-learn, or Machine Learning algorithms. It prepares and organizes the data that those tools use.

**Recommended learning order:** Master Parts 1–3 first, then Parts 4–5, and finally Parts 6–7 by building practical datasets and Machine Learning projects.

---

# **Section 29: Advanced Pandas Concepts**

We'll cover all five concepts with Python implementations and examples. The goal is to understand how to use them when handling real datasets for machine learning, not just memorize Pandas methods.

We'll use Pandas and NumPy.

```
import pandas as pdimport numpy as np
```

## **29.1 Vectorization and Broadcasting**

### **1. What is vectorization?**

Vectorization means performing an operation on an entire Series or DataFrame instead of processing individual values using Python loops.

For example, suppose you have 5,000 employee salaries and want to increase every salary by 10%.

**Without vectorization:**

```python
salaries = [25000, 30000, 35000, 40000, 45000]
updated_salaries = []
for salary in salaries:  
    updated_salaries.append(salary * 1.10)print(updated_salaries)
```

**With Pandas vectorization:**

```python
df = pd.DataFrame({
    "salary": [25000, 30000, 35000, 40000, 45000]
})
df["updated_salary"] = df["salary"] * 1.10print(df)
```

Both produce the same result, but vectorized operations are generally faster and simpler for large datasets.

**How vectorization works**

**Original Series**

`[25000, 30000, 35000, 40000]`

Multiply by 1.10

**Updated Series**

`[27500, 33000, 38500, 44000]`

One operation is applied across the entire Series.

### **2. Vectorized operations on Series**

```python
df = pd.DataFrame({
    "price": [100, 200, 300, 400],  
    "quantity": [2, 3, 4, 5]
})
df["total"] = df["price"] * df["quantity"]
df["discounted_price"] = df["price"] * 0.90df["tax"] = df["price"] * 0.18print(df)
```

You can perform:

| Operation      | Example               |
| -------------- | --------------------- |
| Addition       | `df["A"] + df["B"]` |
| Subtraction    | `df["A"] - df["B"]` |
| Multiplication | `df["A"] * df["B"]` |
| Division       | `df["A"] / df["B"]` |
| Comparison     | `df["A"] > 100`     |
| Power          | `df["A"] ** 2`      |

### **3. Broadcasting**

Broadcasting allows NumPy and Pandas-compatible operations to combine arrays or columns of different shapes under defined compatibility rules.

Example:

```python
df = pd.DataFrame({  
    "math": [80, 70, 90],  
    "science": [75, 85, 95],  
    "english": [90, 80, 85]
})

subject_bonus = 5df[["math", "science", "english"]] += subject_bonusprint(df)
```

Here, the single value `5` is applied to every selected cell.

Another example:

```python
df = pd.DataFrame({  
    "math": [80, 70, 90],  
    "science": [75, 85, 95],  
    "english": [90, 80, 85]
})
subject_bonus = pd.Series({  
    "math": 5,  
    "science": 10,  
    "english": 3
})
df = df + subject_bonusprint(df)
```

Pandas aligns the Series values with matching column names.

**Important:** Pandas aligns Series by index labels, not simply by position. If labels do not match, you may get missing values. This is a common source of bugs.

### **4.&#x20;**`np.where()`**&#x20;and&#x20;**`np.select()`

These are useful for creating new features based on conditions.

**Using&#x20;**`np.where()`**:**

```python
df = pd.DataFrame({  
    "marks": [35, 45, 75, 90, 28]
})
df["result"] = np.where(  
    df["marks"] >= 40,  
    "Pass",  
    "Fail"
)
print(df)
```

**Using&#x20;**`np.select()`**&#x20;for multiple conditions:**

```python
conditions = [  
    df["marks"] >= 80,  
    df["marks"] >= 60,  
    df["marks"] >= 40]
    choices = ["Excellent", "Good", "Average"]df["grade"] = np.select(  
        conditions,  
        choices,  
        default="Poor"
    )
print(df)
```

### **5. Applying operations across rows and columns**

Use `apply()` when an operation cannot be expressed conveniently as a vectorized operation.

```python
import pandas as pd

df = pd.DataFrame({
    "math": [80, 70, 90],
    "science": [75, 85, 95],
    "english": [90, 80, 85]
})

df["average"] = df[["math", "science", "english"]].mean(axis=1)

print(df)
```

- `axis=0`: operate down each column.
- `axis=1`: operate across each row.

Prefer built-in vectorized operations such as `mean()`, `sum()`, and arithmetic expressions over `apply()` where possible.

### **When will you use vectorization?**

- Calculating prices, taxes and discounts.
- Creating ML features.
- Normalizing numerical columns.
- Applying conditions to datasets.
- Processing thousands or millions of rows efficiently.

## **29.2 Hierarchical Data and Advanced MultiIndex**

### **1. What is a MultiIndex?**

Normally, a DataFrame has one index for identifying rows.

A MultiIndex allows you to use multiple levels of indexes to identify a row.

For example, imagine sales data from different cities across different years.

| Year | City      | Sales |
| ---- | --------- | ----- |
| 2024 | Bangalore | 50000 |
| 2024 | Chennai   | 40000 |
| 2025 | Bangalore | 65000 |
| 2025 | Chennai   | 55000 |

You can use both `Year` and `City` as index levels.

### **2. Creating a MultiIndex DataFrame**

```Python
import pandas as pd

df = pd.DataFrame({
    "year": [2024, 2024, 2025, 2025],
    "city": ["Bangalore", "Chennai", "Bangalore", "Chennai"],
    "sales": [50000, 40000, 65000, 55000]
})

df = df.set_index(["year", "city"])

print(df)
```

The resulting index has two levels:

- Level 0: `year`
- Level 1: `city`

### **3. Selecting data using multiple index levels**

Select all records for 2024:

```Python
print(df.loc[2024])
```

Select Bangalore's sales in 2025:

```Python
print(df.loc[(2025, "Bangalore")])
```

Select a particular column for 2024:

```Python
print(df.loc[2024, "sales"])
```

### **4. Using&#x20;**`xs()`**&#x20;for cross-section selection**

`xs()` selects data from a particular index level.

```Python
print(df.xs("Bangalore", level="city"))
```

This selects Bangalore's records across all years.

### **5. Sorting MultiIndex**

```Python
df = df.sort_index()print(df)
```

Sorting is useful because some MultiIndex selection operations work more efficiently with a sorted index.

### **6. Swapping index levels**

Use `swaplevel()` to change the order of index levels.

```Python
df = df.swaplevel("year", "city")print(df)
```

Now the index order is:

1. City
2. Year

### **7. Resetting and setting multiple indexes**

Convert index levels back into ordinary columns:

```Python
df = df.reset_index()print(df)
```

Create a MultiIndex again:

```Python
df = df.set_index(["city", "year"])
```

### **8. Aggregating hierarchical data**

Suppose you want total sales for each city.

```Python
print(df.groupby(level="city")["sales"].sum())
```

Or calculate sales by year and city:

```Python
print(df.groupby(level=["year", "city"])["sales"].sum())
```

**When will you use MultiIndex?**

- Sales analysis across years and regions.
- Financial data with multiple time dimensions.
- Grouped datasets with nested categories.
- Working with hierarchical datasets returned by aggregation or pivot operations.

For normal ML preprocessing, you won't need MultiIndex every day. Understand how it works, but don't force it into every project.

## **29.3 Outlier Detection and Handling**

### **1. What is an outlier?**

An outlier is a value that is unusually far from most other values in a dataset.

Example:

```Python
df = pd.DataFrame({  
    "salary": [25000, 28000, 30000, 32000, 35000, 40000, 500000]
})
print(df)
```

Most salaries are between 25,000 and 40,000, but one value is 500,000.

That value may be an outlier.

**Illustrative salary distribution**

Most observations

Unusual observation

25k

28k

30k

32k

35k

40k

500k

One unusually large value can distort averages and statistical models.

Outliers can affect:

- Mean and standard deviation.
- Correlation.
- Linear regression.
- Distance-based ML algorithms such as KNN and K-Means.

But an outlier is not automatically an error. A high salary may be perfectly real.

### **2. Detecting outliers using IQR**

IQR means Interquartile Range.

It measures the spread of the middle 50% of the data.

- Q1: 25th percentile.
- Q3: 75th percentile.
- IQR: Q3 minus Q1.

The usual outlier boundaries are:

\\[ Lower = Q1 - 1.5(IQR) \\]

\\[ Upper = Q3 + 1.5(IQR) \\]

Values outside these boundaries are flagged as potential outliers.

**Implementation:**

```Python
import pandas as pd

df = pd.DataFrame({
    "salary": [
        25000, 28000, 30000, 32000,
        35000, 40000, 42000, 45000,
        50000, 500000
    ]
})

Q1 = df["salary"].quantile(0.25)
Q3 = df["salary"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

outliers = df[
    (df["salary"] < lower) |
    (df["salary"] > upper)
]

print("Lower boundary:", lower)
print("Upper boundary:", upper)
print(outliers)
```

To identify normal values:

```
normal_data = df[(df["salary"] >= lower) & (df["salary"] <= upper)]
```

### **3. Detecting outliers using Z-score**

A Z-score tells you how many standard deviations a value is away from the mean.

\\[ \text{Z-score} = \frac{x-\mu}{\sigma} \\]

\\(z = \frac{x - \mu}{\sigma}\\)

\\(z=\frac{(\text{4})-(\text{1.5})}{\text{1.8}}=\text{1.389}\\)

\\(\Phi(z)\approx \text{91.8\\%}\\)

\\(x\\)

\\(\mu\\)

\\(\sigma\\)

μxΦ(z)

Give feedback

For example, a Z-score of 2 means the value is two standard deviations above the mean.

A common rule is to flag values with an absolute Z-score greater than 3.

```Python
import pandas as pd

df = pd.DataFrame({
    "salary": [
        25000, 28000, 30000, 32000,
        35000, 40000, 42000, 45000,
        50000, 500000
    ]
})

mean = df["salary"].mean()
std = df["salary"].std()

df["z_score"] = (df["salary"] - mean) / std

outliers = df[df["z_score"].abs() > 3]

print(outliers)
```

**Important difference:**

| IQR                             | Z-score                                      |
| ------------------------------- | -------------------------------------------- |
| Based on quartiles              | Based on mean and standard deviation         |
| More robust to extreme values   | Can be distorted by extreme values           |
| Useful for skewed distributions | Most useful for roughly normal distributions |

### **4. Handling outliers using clipping**

Clipping replaces values outside specified boundaries with the boundary values.

```Python
import pandas as pd

df = pd.DataFrame({
    "salary": [25000, 28000, 30000, 35000, 500000]
})

lower = df["salary"].quantile(0.05)
upper = df["salary"].quantile(0.95)

df["salary_clipped"] = df["salary"].clip(
    lower=lower,
    upper=upper
)

print(df)
```

The extreme values are capped instead of being deleted.

### **5. Removing outliers**

```Python
df_clean = df[(df["salary"] >= lower) & (df["salary"] <= upper)]
```

This removes rows outside the selected boundaries.

Be careful: removing valid extreme observations can destroy useful information.

### **6. When should you handle outliers?**

| Situation                         | Possible approach          |
| --------------------------------- | -------------------------- |
| Data entry error                  | Correct or remove          |
| Extreme but valid value           | Keep or transform          |
| Strongly skewed numerical feature | Log transformation         |
| Extreme values affect model       | Clipping or robust scaling |
| Important rare event              | Preserve and investigate   |

**ML warning:** Calculate outlier thresholds using the training dataset only. Applying thresholds calculated from the full dataset before splitting can cause data leakage.

## **29.4 Advanced Missing-Data Analysis**

### **1. Understanding missing values**

Missing values occur when a dataset does not contain information for a particular observation.

Pandas usually represents missing values using `NaN`, `None`, or `pd.NA`, depending on the data type.

Example:

```Python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "name": ["Alex", "John", "David", "Sara", "Mike"],
    "age": [25, np.nan, 30, 28, np.nan],
    "salary": [30000, 40000, np.nan, 35000, 50000]
})

print(df)
```

### **2. Measuring missing-value percentages**

First, count missing values in each column:

```Python
print(df.isnull().sum())
```

Calculate the percentage:

```Python
missing_percentage = (df.isnull().mean() * 100)print(missing_percentage)
```

Why does this work?

- `isnull()` produces `True` for missing values.
- `mean()` treats `True` as 1 and `False` as 0.
- Multiplying by 100 gives the percentage.

You can also inspect missing values across rows:

```Python
print(df.isnull().sum(axis=1))
```

### **3. Understanding missing-data patterns**

There are three important statistical categories.

**MCAR: Missing Completely At Random**

Missingness has no relationship with the data.

Example: Some survey responses are lost because of a random technical failure.

**MAR: Missing At Random**

Missingness depends on other observed variables.

Example: Younger customers are less likely to provide their income, but age is available.

**MNAR: Missing Not At Random**

Missingness depends on the missing value itself or an unobserved factor.

Example: People with very high incomes may be less likely to disclose their income.

These distinctions matter because the reason for missing data influences how you should handle it.

### **4. Basic missing-value handling**

**Remove rows containing missing values:**

```Python
df.dropna()
```

**Remove columns containing missing values:**

```Python
df.dropna(axis=1)
```

**Fill missing values with a constant:**

```Python
df.fillna(0)
```

These are simple options, but blindly replacing every missing value with zero is usually a bad preprocessing strategy.

### **5. Choosing an imputation strategy**

Imputation means replacing missing values with estimated or substituted values.

| Data type        | Common strategy               |
| ---------------- | ----------------------------- |
| Numerical        | Mean or median                |
| Categorical      | Mode                          |
| Time-series data | Forward fill or interpolation |
| Group-based data | Group median or mean          |
| Complex data     | Model-based imputation        |

**Mean imputation:**

```Python
df["age"] = df["age"].fillna(df["age"].mean())
```

**Median imputation:**

```Python
df["salary"] = df["salary"].fillna(df["salary"].median())
```

Median is often safer when numerical data contains extreme values.

**Mode imputation:**

```Python
df["department"] = df["department"].fillna(df["department"].mode()[0])
```

### **6. Group-based imputation**

Sometimes filling missing values using the entire column's mean is inaccurate.

For example, employee salaries differ between departments.

Use the department's median salary instead.

```Python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "department": [
        "IT", "IT", "HR", "HR", "Finance", "Finance"
    ],
    "salary": [
        50000, np.nan, 30000, np.nan, 60000, 65000
    ]
})

df["salary"] = df.groupby("department")[
    "salary"
].transform(
    lambda x: x.fillna(x.median())
)

print(df)
```

This calculates a separate median for each department.

### **7. Forward fill and backward fill**

These methods are particularly useful for time-series data.

**Forward fill (**`ffill`**)**

Uses the previous available value.

```Python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "temperature": [25, np.nan, np.nan, 28, np.nan]
})

df["temperature"] = df["temperature"].ffill()

print(df)
```

Result:

```
25
25
25
28
28
```

**Backward fill (**`bfill`**)**

Uses the next available value.

```Python
df["temperature"] = df["temperature"].bfill()
```

These methods should only be used when carrying values forward or backward is meaningful.

### **8. Interpolation**

Interpolation estimates missing values using surrounding observations.

```Python
df = pd.DataFrame({"temperature": [20, np.nan, 30, np.nan, 40]})
df["temperature"] = df["temperature"].interpolate()
print(df)
```

Result:

```
20
25
30
35
40
```

Linear interpolation estimates values along a straight line between known observations.

You can also use different interpolation methods, such as polynomial interpolation, when the data and assumptions justify them.

### **9. Missing values and machine learning**

Missing-value handling is an important part of ML preprocessing.

A practical approach is to use Scikit-learn's `SimpleImputer`.

```Python
import pandas as pd
import numpy as np
from sklearn.impute import SimpleImputer

df = pd.DataFrame({
    "age": [25, np.nan, 30, 35],
    "salary": [30000, 40000, np.nan, 50000]
})

imputer = SimpleImputer(strategy="median")

df[["age", "salary"]] = imputer.fit_transform(
    df[["age", "salary"]]
)

print(df)
```

For actual model training, split the dataset first. Fit the imputer on training data only, then transform the training and test data using that same fitted imputer.

**When will you use missing-data analysis?**

- Cleaning real-world datasets.
- Preparing data for ML models.
- Understanding incomplete customer records.
- Handling sensor and time-series data.
- Preventing biased analysis caused by missing observations.

## **29.5 Performance and Memory Optimization**

### **1. Why does performance optimization matter?**

Imagine processing:

- 1,000 rows: usually easy.
- 100,000 rows: still manageable in many cases.
- 10 million rows: memory and processing choices become important.

Pandas stores data in memory. Large datasets can consume substantial RAM.

The goal is to reduce unnecessary memory usage and avoid inefficient operations.

### **2. Measuring memory usage**

Use `memory_usage()` to inspect how much memory each column consumes.

```Python
import pandas as pd

df = pd.DataFrame({
    "age": [20, 25, 30, 35],
    "salary": [25000, 30000, 35000, 40000],
    "city": ["Delhi", "Mumbai", "Delhi", "Chennai"]
})

print(df.memory_usage(deep=True))
```

`deep=True` also accounts for the memory used by object-based data such as strings.

Get total memory usage:

```Python
print(df.memory_usage(deep=True).sum())
```

Convert the result into MB:

```Python
memory_mb = (df.memory_usage(deep=True).sum() / (1024 ** 2))print(memory_mb, "MB")
```

### **3. Understanding efficient data types**

Pandas supports different numerical data types.

| Data type   | Typical use                     |
| ----------- | ------------------------------- |
| `int64`   | Large integer values            |
| `int32`   | Smaller integer values          |
| `int16`   | Small integer values            |
| `int8`    | Very small integer values       |
| `float64` | Higher-precision decimal values |
| `float32` | Lower-precision decimal values  |

For example, if an age column contains values between 18 and 80, storing it as `int64` may be unnecessary.

You can use:

```Python
df["age"] = df["age"].astype("int8")
```

Only do this when the values fit safely within the selected type.

### **4. Downcasting numerical columns**

Pandas provides `to_numeric()` with a downcasting option.

```Python
import pandas as pd

df = pd.DataFrame({
    "age": [20, 25, 30, 35],
    "salary": [25000, 30000, 35000, 40000]
})

df["age"] = pd.to_numeric(
    df["age"],
    downcast="integer"
)

df["salary"] = pd.to_numeric(
    df["salary"],
    downcast="integer"
)

print(df.dtypes)
```

This selects a smaller compatible integer type where possible.

For floating-point columns:

```Python
df["price"] = pd.to_numeric(df["price"], downcast="float")
```

Remember that smaller floating-point types can lose numerical precision. Check that this is acceptable for your task.

### **5. Using&#x20;**`category`**&#x20;for repeated strings**

Consider a dataset with one million customer records and a `city` column containing only five unique city names.

Storing the same city strings repeatedly as ordinary object values can waste memory.

Use the categorical data type:

```Python
import pandas as pd

df = pd.DataFrame({
    "city": [
        "Delhi", "Mumbai", "Chennai",
        "Delhi", "Mumbai", "Delhi"
    ]
})

df["city"] = df["city"].astype("category")

print(df.dtypes)
```

Compare memory usage:

```Python
import pandas as pd

df = pd.DataFrame({
    "city": ["Delhi", "Mumbai", "Chennai"] * 10000
})

print("Original:")
print(df.memory_usage(deep=True))

df["city"] = df["city"].astype("category")

print("Categorical:")
print(df.memory_usage(deep=True))
```

Categorical data can reduce memory usage when a column contains relatively few unique values compared with its total number of rows.

It is useful for:

- City names.
- Product categories.
- Department names.
- Customer types.
- Status labels.

It is not automatically beneficial for columns where almost every value is unique.

### **6. Selecting columns by data type**

Sometimes you want to perform an operation only on numerical columns.

Use `select_dtypes()`.

```Python
import pandas as pd

df = pd.DataFrame({
    "age": [20, 25, 30],
    "salary": [30000, 40000, 50000],
    "city": ["Delhi", "Mumbai", "Chennai"],
    "is_active": [True, False, True]
})

numeric_columns = df.select_dtypes(
    include=["number"]
)

print(numeric_columns)
```

Select categorical or string columns:

```Python
categorical_columns = df.select_dtypes(include=["object", "category", "string"])
```

Exclude numerical columns:

```Python
non_numeric = df.select_dtypes(exclude=["number"])
```

This is particularly useful when building preprocessing pipelines.

### **7. Avoiding unnecessary copies**

Consider:

```Python
df_copy = df.copy()
```

This creates a separate DataFrame.

If you only need to inspect the original data, don't create unnecessary copies.

Also avoid repeatedly creating intermediate DataFrames when one operation can do the job.

For example:

```Python
# Less efficient approach
df1 = df[df["age"] > 20]

df2 = df1[df1["salary"] > 30000]


# More direct approach
df2 = df[
    (df["age"] > 20) &
    (df["salary"] > 30000)
]
```

A copy is still useful when you need to modify data independently.

Avoid chained assignment such as:

```Python
df[df["age"] > 20]["salary"] = 50000
```

Use `.loc` instead:

```Python
df.loc[df["age"] > 20, "salary"] = 50000
```

This makes the intended modification explicit and avoids chained-assignment problems.

### **8. Optimizing large DataFrame operations**

Some practical rules:

| Less efficient habit         | Better approach                    |
| ---------------------------- | ---------------------------------- |
| Python loops over rows       | Vectorized operations              |
| Repeated string objects      | `category` when suitable         |
| Unnecessary `float64`      | Smaller safe numeric dtype         |
| Loading every CSV column     | Use `usecols`                    |
| Loading incorrect data types | Specify `dtype`                  |
| Repeated filtering           | Combine conditions where practical |
| Unnecessary copies           | Modify or select carefully         |

Example: load only required CSV columns.

```Python
import pandas as pd

df = pd.read_csv(
    "employees.csv",
    usecols=["name", "age", "salary"],
    dtype={
        "age": "int16",
        "salary": "float32"
    }
)
```

This can reduce the amount of data loaded into memory.

### **9. When should you consider alternatives to Pandas?**

Pandas is useful for many datasets that fit comfortably in memory. But it is not the best tool for every scale.

- **Pandas:** General-purpose tabular data processing.
- **Polars:** Fast DataFrame processing, including lazy query execution.
- **Dask:** Parallel and distributed DataFrame workloads.
- **PySpark:** Large-scale distributed data processing.

Don't switch tools just because another library claims to be faster. Measure your actual workload first.

## **29.6 How to combine all five concepts in an ML preprocessing workflow**

Now let's combine these concepts into one practical example.

Imagine you have an employee dataset and want to prepare it for a machine learning model.

```Python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "age": [22, 25, np.nan, 35, 40, 120],
    "salary": [25000, 30000, 35000, np.nan, 50000, 900000],
    "experience": [1, 2, 4, 8, 12, 20],
    "department": [
        "IT", "HR", "IT", "Finance", "HR", "IT"
    ]
})
```

**Step 1: Inspect missing values**

```Python
print(df.isnull().sum())
```

**Step 2: Handle missing numerical values**

```Python
df["age"] = df["age"].fillna(df["age"].median())
df["salary"] = df["salary"].fillna(df["salary"].median())
```

**Step 3: Detect potential outliers**

```Python
Q1 = df["salary"].quantile(0.25)
Q3 = df["salary"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

print(df[
    (df["salary"] < lower) |
    (df["salary"] > upper)
])
```

**Step 4: Create new features using vectorization**

```Python
df["salary_per_experience"] = (df["salary"] / df["experience"])
```

**Step 5: Encode categorical data**

```Python
df = pd.get_dummies(df, columns=["department"], dtype=int)
```

**Step 6: Optimize data types**

```Python
df["age"] = df["age"].astype("int16")df["experience"] = df["experience"].astype("int8")
```

**Step 7: Check memory usage**

```Python
print(df.memory_usage(deep=True))
```

This demonstrates how the five concepts contribute to a real preprocessing workflow.

One important correction to the simplified example: in a real ML project, split your data into training and testing sets before fitting imputers, outlier thresholds, encoders, or scalers. Learn their parameters from training data only, then apply them to test data. Otherwise, you risk data leakage.

## **Final checklist**

0/13 completed

- Understand vectorized Series and DataFrame operations
- Understand broadcasting and index alignment
- Use np.where() and np.select()
- Work with MultiIndex selection and aggregation
- Detect outliers using IQR and Z-score
- Choose suitable outlier-handling strategies
- Analyze missing-value patterns
- Apply mean, median, mode and group-based imputation
- Use forward fill, backward fill and interpolation
- Measure DataFrame memory usage
- Optimize numeric and categorical data types
- Use select_dtypes() and avoid unnecessary copies
- Combine preprocessing steps without data leakage
