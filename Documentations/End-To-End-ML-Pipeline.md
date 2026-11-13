# Pandas to Machine Learning | End to End ML Pipeline

## Introduction

**Pandas** is a Python library used to read, manage, clean, analyze, and prepare data for Machine Learning.

It helps us convert raw data into clean and meaningful data that can be used to train Machine Learning models.

### Installation

```bash
pip install pandas
```

### Import Pandas

```python
import pandas as pd
```

---

# 1. Reading Data Files into DataFrames

### What is a DataFrame?

A DataFrame is a table-like structure containing rows and columns, similar to an Excel sheet.

### Why do we use it?

To load data from different file formats into Python so that we can process and analyze it.

### Important functions

| Function            | Purpose                      |
| ------------------- | ---------------------------- |
| `pd.read_csv()`   | Read CSV files               |
| `pd.read_excel()` | Read Excel files             |
| `pd.read_json()`  | Read JSON files              |
| `pd.read_sql()`   | Read data from SQL databases |
| `df.to_csv()`     | Save data as CSV             |
| `df.to_excel()`   | Save data as Excel           |

### Example

```python
import pandas as pd

df = pd.read_csv("data.csv")

print(df)
```

---

# 2. Data Inspection

### What is Data Inspection?

Data inspection means understanding the dataset before performing data cleaning or Machine Learning operations.

It helps us understand:

- How many rows and columns are present?
- What type of data is available?
- Are there missing values?
- What are the minimum, maximum and average values?

### Important functions

| Function           | Purpose                                |
| ------------------ | -------------------------------------- |
| `head()`         | Display the first 5 rows               |
| `tail()`         | Display the last 5 rows                |
| `shape`          | Get the number of rows and columns     |
| `info()`         | Get dataset information and data types |
| `describe()`     | Get statistical information            |
| `columns`        | Display column names                   |
| `dtypes`         | Display data types                     |
| `unique()`       | Find unique values                     |
| `nunique()`      | Count unique values                    |
| `value_counts()` | Count occurrences of each value        |

### Example

```python
print(df.head())
print(df.tail())
print(df.shape)
print(df.info())
print(df.describe())
```

---

# 3. Data Selection

### What is Data Selection?

Data selection means selecting specific rows and columns from a dataset.

It helps us extract only the information required for our analysis or Machine Learning model.

### Important operations

| Operation                 | Purpose                                 |
| ------------------------- | --------------------------------------- |
| `df['Age']`             | Select a single column                  |
| `df[['Age', 'Salary']]` | Select multiple columns                 |
| `loc[]`                 | Select rows and columns using labels    |
| `iloc[]`                | Select rows and columns using positions |
| Filtering                 | Select rows based on conditions         |

### Example: Select columns

```python
df['Age']

df[['Age', 'Salary']]
```

### Example: Using loc[]

```python
df.loc[0:2, ['Name', 'Age']]
```

Selects rows with index labels 0, 1, 2 and the Name and Age columns.

### Example: Using iloc[]

```python
df.iloc[0:3, 0:2]
```

Selects the first 3 rows and first 2 columns by position.

### Example: Filtering

```python
df[df['Age'] > 25]
```

Selects only the rows where Age is greater than 25.

---

# 4. Data Cleaning

### What is Data Cleaning?

Data cleaning means identifying and removing incorrect, duplicate, or unnecessary data from a dataset.

It helps improve data quality before training a Machine Learning model.

### Common problems

- Duplicate records
- Unnecessary columns
- Incorrect values
- Unwanted spaces
- Inconsistent data

### Important functions

| Function              | Purpose                  |
| --------------------- | ------------------------ |
| `drop()`            | Remove rows or columns   |
| `drop_duplicates()` | Remove duplicate records |
| `rename()`          | Rename columns           |
| `replace()`         | Replace unwanted values  |
| `sort_values()`     | Sort dataset values      |

### Example: Remove duplicates

```python
df = df.drop_duplicates()
```

### Example: Remove a column

```python
df = df.drop('Salary', axis=1)
```

### Example: Rename a column

```python
df = df.rename(columns={'Age': 'Student_Age'})
```

---

# 5. Missing Value Handling

### What are Missing Values?

Missing values are data points where information is not available.

Examples:

- Empty cells
- NaN values
- None values

Missing values can affect Machine Learning model performance.

### Important functions

| Function      | Purpose                   |
| ------------- | ------------------------- |
| `isnull()`  | Identify missing values   |
| `notnull()` | Identify available values |
| `fillna()`  | Fill missing values       |
| `dropna()`  | Remove missing values     |
| `isna()`    | Identify missing values   |

### Example: Check missing values

```python
print(df.isnull().sum())
```

Shows the number of missing values in each column.

### Example: Fill missing values

```python
df['Age'] = df['Age'].fillna(df['Age'].mean())
```

Replaces missing Age values with the average Age.

### Example: Remove missing values

```python
df = df.dropna()
```

Removes rows containing missing values.

---

# 6. Data Type Handling

### What is Data Type Handling?

Data type handling means checking and converting columns into their correct data types.

Sometimes numerical values are stored as text, or dates are stored as strings.

These problems must be corrected before performing calculations or Machine Learning operations.

### Common data types

| Data Type      | Meaning              |
| -------------- | -------------------- |
| `int64`      | Whole numbers        |
| `float64`    | Decimal numbers      |
| `object`     | Text or mixed values |
| `bool`       | True or False        |
| `datetime64` | Date and time        |

### Important functions

| Function          | Purpose                     |
| ----------------- | --------------------------- |
| `dtypes`        | Check data types            |
| `astype()`      | Convert data types          |
| `to_numeric()`  | Convert values into numbers |
| `to_datetime()` | Convert values into dates   |

### Example: Convert text into integer

```python
df['Age'] = df['Age'].astype(int)
```

### Example: Convert text into numbers

```python
df['Salary'] = pd.to_numeric(
    df['Salary'],
    errors='coerce'
)
```

Invalid values are converted into NaN.

### Example: Convert text into dates

```python
df['Date'] = pd.to_datetime(df['Date'])
```

---

# 7. Data Transformation

### What is Data Transformation?

Data transformation means modifying existing data into a useful format.

It helps us create new values, change existing values, and prepare features for analysis.

### Important functions

| Function          | Purpose                             |
| ----------------- | ----------------------------------- |
| `apply()`       | Apply a function to rows or columns |
| `map()`         | Map values in a Series              |
| `replace()`     | Replace existing values             |
| `sort_values()` | Sort data                           |
| `groupby()`     | Group data based on columns         |

### Example: Using apply()

```python
df['Age'] = df['Age'].apply(lambda x: x + 1)
```

Increases every Age value by 1.

### Example: Using map()

```python
df['Gender'] = df['Gender'].map({
    'Male': 1,
    'Female': 0
})
```

Converts text categories into numerical values.

### Example: Using replace()

```python
df['City'] = df['City'].replace(
    'Bangalore',
    'Bengaluru'
)
```

Replaces Bangalore with Bengaluru.

---

# 8. Feature Extraction

### What is Feature Extraction?

Feature extraction means creating useful features from existing data.

Features are the input variables used by Machine Learning models to make predictions.

### Types of Feature Extraction

#### A. Date Feature Extraction

Extract useful information from date columns.

Example:

```python
df['Date'] = pd.to_datetime(df['Date'])

df['Year'] = df['Date'].dt.year
df['Month'] = df['Date'].dt.month
df['Day'] = df['Date'].dt.day
df['Day_Name'] = df['Date'].dt.day_name()
```

#### B. Text Feature Extraction

Extract useful information from text columns.

Example:

```python
df['Name_Length'] = df['Name'].str.len()

df['First_Name'] = df['Name'].str.split().str[0]
```

#### C. Numerical Feature Extraction

Create new features using mathematical operations.

Example:

```python
df['Total'] = df['Maths'] + df['Science']

df['Average'] = df['Total'] / 2
```

### Why is Feature Extraction important?

- Creates meaningful information.
- Helps identify useful patterns.
- Can improve Machine Learning model performance.
- Converts raw data into useful input features.

---

# 9. Correlation Analysis

### What is Correlation?

Correlation measures the relationship between two numerical features.

It helps us understand whether two features move together or in opposite directions.

### Correlation values

| Value | Meaning                      |
| ----- | ---------------------------- |
| +1    | Perfect positive correlation |
| 0     | No linear correlation        |
| -1    | Perfect negative correlation |

### Types of Correlation

**1. Positive Correlation**

When one feature increases, another feature also tends to increase.

Example: Study hours and marks.

**2. Negative Correlation**

When one feature increases, another feature tends to decrease.

Example: Speed and travel time for a fixed distance.

**3. No Linear Correlation**

There is little or no linear relationship between two features.

### Important function

`corr()` – Calculates the correlation between numerical columns.

### Example

```python
correlation = df.corr(numeric_only=True)

print(correlation)
```

### Find highly correlated features

```python
correlation = df.corr(numeric_only=True)

high_corr = correlation[
    (correlation > 0.8) &
    (correlation < 1.0)
]

print(high_corr)
```

### Why is Correlation Analysis important?

- Understand relationships between features.
- Identify highly correlated features.
- Reduce unnecessary or redundant features.
- Help in feature selection.

**Note:** High correlation does not always mean a feature should be removed. Check its relationship with the target and the requirements of the model before removing it.

---

# 10. Machine Learning Preparation

### What is Machine Learning Data Preparation?

It means converting cleaned data into a format that Machine Learning algorithms can understand.

Before training a model, we need to prepare input features and target values.

### A. Separate Features (X) and Target (y)

**X:** Input features used to make predictions.

**y:** Target column that the model needs to predict.

Example:

```python
X = df[['Age', 'Salary', 'Experience']]

y = df['Purchased']
```

### B. Encoding

Encoding converts categorical text values into numerical values.

Example:

```python
df['Gender'] = df['Gender'].map({
    'Male': 1,
    'Female': 0
})
```

For multiple categories, we can use One-Hot Encoding:

```python
df = pd.get_dummies(
    df,
    columns=['City'],
    dtype=int
)
```

### C. Train-Test Split

We divide the dataset into two parts:

- Training Data: Used to train the model.
- Testing Data: Used to evaluate the model.

Example:

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

- 80% of data is used for training.
- 20% of data is used for testing.
- `random_state=42` makes the split reproducible.

### D. Normalization and Scaling

Scaling brings numerical features into a comparable range.

It is useful for algorithms that are sensitive to feature scales.

Example using Scikit-learn:

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()

X_train_scaled = scaler.fit_transform(X_train)

X_test_scaled = scaler.transform(X_test)
```

**Important:** Fit the scaler only on training data to avoid data leakage.

---

# 11. Model Training

### What is Model Training?

Model training is the process of teaching a Machine Learning algorithm to identify patterns from training data.

The model learns relationships between input features (X) and target values (y).

### Important steps

1. Select a Machine Learning algorithm.
2. Create the model.
3. Train the model using training data.
4. The model learns patterns from the dataset.

### Example: Train a Classification Model

```python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(
    n_estimators=100,
    random_state=42
)

model.fit(X_train, y_train)
```

**Explanation:**

- `RandomForestClassifier()` creates the model.
- `n_estimators=100` creates 100 decision trees.
- `fit()` trains the model using training data.

---

# 12. Model Prediction and Testing

### What is Model Prediction?

Prediction means using a trained model to generate outputs for new input data.

### What is Model Testing?

Testing means checking how well the trained model performs on data it has not seen during training.

### Important functions

| Function            | Purpose                             |
| ------------------- | ----------------------------------- |
| `predict()`       | Generate predictions                |
| `predict_proba()` | Generate prediction probabilities   |
| `score()`         | Calculate the model's default score |

### Example: Predict Test Data

```python
y_pred = model.predict(X_test)

print(y_pred)
```

### Compare Actual and Predicted Values

```python
results = pd.DataFrame({
    "Actual": y_test,
    "Predicted": y_pred
})

print(results)
```

This helps us understand how accurately the model predicts unseen data.

---

# 13. Model Evaluation

### What is Model Evaluation?

Model evaluation measures how well a trained Machine Learning model performs.

It helps us understand the accuracy, errors, and reliability of predictions.

### Important Evaluation Metrics

| Metric           | Purpose                                                 |
| ---------------- | ------------------------------------------------------- |
| Accuracy         | Measures the percentage of correct predictions          |
| Precision        | Measures how many positive predictions were correct     |
| Recall           | Measures how many actual positive cases were identified |
| F1-Score         | Combines precision and recall                           |
| Confusion Matrix | Shows correct and incorrect predictions                 |

### Example: Evaluate the Model

```python
from sklearn.metrics import (
    accuracy_score,
    precision_score,
    recall_score,
    f1_score,
    confusion_matrix,
    classification_report
)

print("Accuracy:", accuracy_score(y_test, y_pred))

print("Precision:", precision_score(y_test, y_pred))

print("Recall:", recall_score(y_test, y_pred))

print("F1 Score:", f1_score(y_test, y_pred))

print("Confusion Matrix:")
print(confusion_matrix(y_test, y_pred))

print(classification_report(y_test, y_pred))
```

**Note:** These metrics are for classification problems. Regression models use metrics such as MAE, MSE, RMSE, and R².

---

# 14. Saving a Trained Model

### What is Model Saving?

Model saving means storing a trained Machine Learning model as a file so that we can reuse it without training it again.

### Why do we save models?

- Avoid repeated training.
- Reuse trained models.
- Deploy models into applications.
- Make predictions using new data.

### Important Libraries

| Library    | Purpose                                  |
| ---------- | ---------------------------------------- |
| `joblib` | Save and load Machine Learning models    |
| `pickle` | Serialize and deserialize Python objects |

### Example: Save a Model Using Joblib

```python
import joblib

joblib.dump(model, "trained_model.pkl")
```

This saves the trained model as `trained_model.pkl`.

### Load the Saved Model

```python
loaded_model = joblib.load("trained_model.pkl")
```

Now we can use the saved model without training it again.

**Important:** Only load model files from trusted sources. Loading untrusted pickle or joblib files can execute malicious code.

---

# 15. Using the Saved Model with New Data

### What is New Data Prediction?

New data prediction means providing previously unseen input data to a saved Machine Learning model to generate predictions.

### Important steps

1. Load the saved model.
2. Prepare new input data.
3. Ensure the input features match the training features.
4. Generate predictions.
5. Display the results.

### Example

```python
import pandas as pd
import joblib

# Load the saved model
loaded_model = joblib.load("trained_model.pkl")

# Create new input data
new_data = pd.DataFrame({
    "Age": [25, 35],
    "Salary": [30000, 50000],
    "Experience": [2, 8]
})

# Generate predictions
predictions = loaded_model.predict(new_data)

print("Predictions:")
print(predictions)
```

**Important:** New data must have the same feature names, order, data types, and preprocessing expected by the model.

If scaling or encoding was used during training, the same fitted transformations must also be applied to new data. A Scikit-learn Pipeline can store preprocessing and the model together.

---

# 16. Complete End-to-End Machine Learning Workflow

An end-to-end Machine Learning workflow includes all the major stages, from raw data to predictions using a saved model.

### Complete Workflow

```text
RAW DATA
   |
   v
DATA LOADING
   |
   v
DATA UNDERSTANDING
   |
   +--> Data Inspection
   +--> Data Visualization
   +--> Statistical Analysis
   |
   v
DATA PREPROCESSING
   |
   +--> Data Cleaning
   +--> Missing Value Handling
   +--> Duplicate Removal
   +--> Data Type Correction
   +--> Outlier Handling
   |
   v
FEATURE ENGINEERING
   |
   +--> Data Transformation
   +--> Feature Extraction
   +--> Feature Encoding
   +--> Feature Selection
   |
   v
DEFINE INPUT (X) AND TARGET (y)
   |
   v
TRAIN-TEST SPLITTING
   |
   +--> Training Dataset
   |
   +--> Testing Dataset
   |
   v
FEATURE SCALING / NORMALIZATION
   |
   v
MODEL DEVELOPMENT
   |
   +--> Algorithm Selection
   +--> Model Initialization
   +--> Model Training
   +--> Hyperparameter Tuning
   |
   v
MODEL TESTING
   |
   v
MODEL EVALUATION
   |
   +--> Performance Metrics
   +--> Error Analysis
   +--> Model Comparison
   |
   v
FINALIZE MODEL
   |
   v
SAVE TRAINED MODEL
   |
   v
MODEL DEPLOYMENT / REUSABILITY
   |
   v
LOAD SAVED MODEL
   |
   v
NEW / UNSEEN DATA
   |
   v
APPLY SAME PREPROCESSING
   |
   v
MODEL INFERENCE
   |
   v
GENERATE PREDICTIONS
   |
   v
OUTPUT / RESULTS
```

**Important:** Fit preprocessing operations only on training data. Use the fitted transformations on testing and new data to prevent data leakage.

---

# Final Updated Learning Summary

| No. | Topic                  | Important Functions / Concepts                    |
| --- | ---------------------- | ------------------------------------------------- |
| 1   | Reading Data           | `read_csv()`, `read_excel()`                  |
| 2   | Data Inspection        | `head()`, `shape`, `info()`, `describe()` |
| 3   | Data Selection         | `loc[]`, `iloc[]`, filtering                  |
| 4   | Data Cleaning          | `drop()`, `drop_duplicates()`, `rename()`   |
| 5   | Missing Values         | `isnull()`, `fillna()`, `dropna()`          |
| 6   | Data Types             | `astype()`, `to_numeric()`, `to_datetime()` |
| 7   | Data Transformation    | `apply()`, `map()`, `replace()`             |
| 8   | Feature Extraction     | `dt`, `str`, mathematical operations          |
| 9   | Correlation            | `corr()`                                        |
| 10  | ML Preparation         | X, y, encoding, train-test split, scaling         |
| 11  | Model Training         | `fit()`                                         |
| 12  | Prediction and Testing | `predict()`, `predict_proba()`                |
| 13  | Model Evaluation       | Accuracy, Precision, Recall, F1, Confusion Matrix |
| 14  | Model Saving           | `joblib.dump()`, `pickle`                     |
| 15  | Model Loading          | `joblib.load()`                                 |
| 16  | New Data Prediction    | Load model, prepare data, `predict()`           |

**Final Goal:** Learn to build a complete Machine Learning workflow: load raw data, clean and prepare it, train a model, test and evaluate its performance, save the trained model, and reuse it to make predictions on new data.
