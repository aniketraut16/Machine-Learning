# Asking Questions

In this folder, we focus on the essential questions you need to ask to understand your dataset comprehensively. Asking the right questions helps you gain insights into the data and make informed decisions about your data analysis and preprocessing steps. Below are seven key questions you should consider:

## 1. How big is the data?

```python
df.shape
```

By using `df.shape`, you can determine the size of your dataset. This command returns the number of rows and columns, helping you understand the scale of your data, which is crucial for deciding your further approaches.

## 2. How does the data look like?

```python
df.sample(5)
```

The `df.sample(5)` command provides a random sample of five rows from your dataset. This gives you a general overview of how your data looks. While methods like `head()` and `tail()` are useful, they often don't provide a complete picture. Sampling is a better option for getting a representative snapshot of your data.

## 3. What is the data type of columns?

```python
df.info()
```

The `df.info()` method displays a summary of the DataFrame, including the data types of each column. This information is useful for identifying columns that may need type conversion. For example, if an age column is represented as float but should be int, you can change the data type to reduce the size of your data.

## 4. Are there any missing values?

```python
df.isnull().sum()
```

Using `df.isnull().sum()`, you can check for missing values in your dataset. This command returns the number of missing values in each column. Identifying and handling missing values is crucial for maintaining data quality and integrity.

## 5. How does the data look mathematically?

```python
df.describe()
```

The `df.describe()` method provides a statistical summary of your data. It includes measures such as mean, median, standard deviation, and percentiles for numerical columns. This mathematical overview helps you understand the distribution and central tendency of your data.

## 6. Are there duplicate values?

```python
df.duplicated().sum()
```

The `df.duplicated().sum()` command checks for duplicate rows in your dataset. It returns the number of duplicate entries, which is important to identify as duplicates can skew your analysis and models. Removing duplicates ensures the uniqueness and quality of your data.

## 7. How is the correlation between columns?

```python
df.corr()['outcome_col']
```

The `df.corr()['outcome_col']` method calculates the correlation between each column and the specified outcome column. This information is valuable for understanding relationships between variables. High correlation between features and the outcome variable can indicate potential predictors for your models.

---

By addressing these questions, you gain a thorough understanding of your dataset, enabling you to make informed decisions in your data analysis and preprocessing steps.
