# Pandas Guide

## Introduction

Pandas is a Python library used for data manipulation and analysis. It offers data structures and operations for manipulating numerical tables and time series.

### Key Data Structures

1. **Series**: One-dimensional labeled array.
2. **DataFrame**: Two-dimensional labeled data structure with columns of potentially different types.
3. **Panel**: Three-dimensional data structure (less commonly used).

## Installation

```bash
pip install pandas
```

## Importing Pandas

```python
import pandas as pd
```

## Creating Data Structures

### Series

A Series is a one-dimensional labeled array capable of holding any data type.

```python
import pandas as pd
import numpy as np

# From a list
s = pd.Series([1, 3, 5, np.nan, 6, 8])
print(s)

# From a dictionary
d = {'a': 1, 'b': 2, 'c': 3}
s = pd.Series(d)
print(s)
```

**Output:**

```
0    1.0
1    3.0
2    5.0
3    NaN
4    6.0
5    8.0
dtype: float64

a    1
b    2
c    3
dtype: int64
```

### DataFrame

A DataFrame is a two-dimensional labeled data structure with columns of potentially different types.

```python
# From a dictionary of lists
data = {'A': [1, 2, 3, 4], 'B': [5, 6, 7, 8]}
df = pd.DataFrame(data)
print(df)

# From a list of dictionaries
data = [{'a': 1, 'b': 2}, {'a': 5, 'b': 10, 'c': 20}]
df = pd.DataFrame(data)
print(df)

# From a numpy array
data = np.array([[1, 2, 3], [4, 5, 6]])
df = pd.DataFrame(data, columns=['A', 'B', 'C'])
print(df)
```

**Output:**

```
   A  B
0  1  5
1  2  6
2  3  7
3  4  8

   a   b     c
0  1   2   NaN
1  5  10  20.0

   A  B  C
0  1  2  3
1  4  5  6
```

## Viewing Data

These methods allow you to get a quick overview of the DataFrame.

### `df.head()`

Displays the first 5 rows of the DataFrame by default.

```python
df.head()
```

**Output:**

```
   A  B  C
0  1  2  3
1  4  5  6
```

### `df.tail()`

Displays the last 5 rows of the DataFrame by default.

```python
df.tail()
```

**Output:**

```
   A  B  C
0  1  2  3
1  4  5  6
```

### `df.info()`

Provides a summary of the DataFrame, including the number of non-null entries and data types.

```python
df.info()
```

**Output:**

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 2 entries, 0 to 1
Data columns (total 3 columns):
 #   Column  Non-Null Count  Dtype
---  ------  --------------  -----
 0   A       2 non-null      int64
 1   B       2 non-null      int64
 2   C       2 non-null      int64
dtypes: int64(3)
memory usage: 176.0 bytes
```

### `df.describe()`

Generates descriptive statistics of the DataFrame.

```python
df.describe()
```

**Output:**

```
              A    B    C
count  2.000000  2.0  2.0
mean   2.500000  3.5  4.5
std    2.121320  2.1  2.1
min    1.000000  2.0  3.0
25%    1.750000  2.8  3.8
50%    2.500000  3.5  4.5
75%    3.250000  4.2  5.2
max    4.000000  5.0  6.0
```

### `df.shape`

Returns the dimensions of the DataFrame (rows, columns).

```python
df.shape
```

**Output:**

```
(2, 3)
```

### `df.columns`

Returns the column labels of the DataFrame.

```python
df.columns
```

**Output:**

```
Index(['A', 'B', 'C'], dtype='object')
```

### `df.index`

Returns the index (row labels) of the DataFrame.

```python
df.index
```

**Output:**

```
RangeIndex(start=0, stop=2, step=1)
```

## Selection and Filtering

### Selecting Columns

Select specific columns from the DataFrame.

```python
df['A']  # Select a single column
df[['A', 'B']]  # Select multiple columns
```

**Output:**

```
0    1
1    4
Name: A, dtype: int64

   A  B
0  1  2
1  4  5
```

### Selecting Rows

Select specific rows from the DataFrame.

```python
df.loc[0]  # Select a row by label
df.iloc[0]  # Select a row by position
df.loc[0:1]  # Select multiple rows by label
df.iloc[0:1]  # Select multiple rows by position
```

**Output:**

```
A    1
B    2
C    3
Name: 0, dtype: int64

A    1
B    2
C    3
Name: 0, dtype: int64

   A  B  C
0  1  2  3
1  4  5  6

   A  B  C
0  1  2  3
```

### Conditional Selection

Select rows based on conditions.

```python
df[df['A'] > 2]  # Rows where column A is greater than 2
df[(df['A'] > 2) & (df['B'] < 8)]  # Multiple conditions
```

**Output:**

```
   A  B  C
1  4  5  6

   A  B  C
1  4  5  6
```

## Adding and Modifying Columns

### Adding a New Column

Add a new column to the DataFrame.

```python
df['D'] = df['A'] + df['B']
print(df)
```

**Output:**

```
   A  B  C   D
0  1  2  3   3
1  4  5  6   9
```

### Modifying an Existing Column

Modify an existing column in the DataFrame.

```python
df['A'] = df['A'] * 2
print(df)
```

**Output:**

```
   A  B  C   D
0  2  2  3   3
1  8  5  6   9
```

## Deleting Columns

Delete columns from the DataFrame.

```python
df.drop('D', axis=1, inplace=True)  # Drop column D
print(df)
```

**Output:**

```
   A  B  C
0  2  2  3
1  8  5  6
```

## Sorting with Pandas

### Sorting by Index

To sort a DataFrame by its index, you can use the `sort_index` method.

### Sorting Rows by Index

```python
import pandas as pd

# Sample DataFrame
data = {'A': [2, 1, 4, 3], 'B': [5, 4, 2, 3]}
df = pd.DataFrame(data, index=[3, 2, 1, 4])
print("Original DataFrame:\n", df)

# Sort rows by index
df_sorted = df.sort_index()
print("DataFrame sorted by index:\n", df_sorted)
```

**Output:**

```
Original DataFrame:
    A  B
3  2  5
2  1  4
1  4  2
4  3  3

DataFrame sorted by index:
    A  B
1  4  2
2  1  4
3  2  5
4  3  3
```

### Sorting Columns by Index

```python
# Sort columns by index
df_sorted_cols = df.sort_index(axis=1)
print("DataFrame with columns sorted by index:\n", df_sorted_cols)
```

**Output:**

```
DataFrame with columns sorted by index:
    A  B
3  2  5
2  1  4
1  4  2
4  3  3
```

### Sorting by Values

To sort a DataFrame by the values in one or more columns, use the `sort_values` method.

### Sorting by a Single Column

```python
# Sort by column 'A'
df_sorted_values = df.sort_values(by='A')
print("DataFrame sorted by column 'A':\n", df_sorted_values)
```

**Output:**

```
DataFrame sorted by column 'A':
    A  B
2  1  4
3  2  5
4  3  3
1  4  2
```

### Sorting by Multiple Columns

You can also sort by multiple columns by passing a list of column names.

```python
# Sort by columns 'A' and then by 'B'
df_sorted_values_multi = df.sort_values(by=['A', 'B'])
print("DataFrame sorted by columns 'A' and then 'B':\n", df_sorted_values_multi)
```

**Output:**

```
DataFrame sorted by columns 'A' and then 'B':
    A  B
2  1  4
3  2  5
4  3  3
1  4  2
```

### Sorting in Descending Order

You can sort in descending order by setting the `ascending` parameter to `False`.

```python
# Sort by column 'A' in descending order
df_sorted_desc = df.sort_values(by='A', ascending=False)
print("DataFrame sorted by column 'A' in descending order:\n", df_sorted_desc)
```

**Output:**

```
DataFrame sorted by column 'A' in descending order:
    A  B
1  4  2
4  3  3
3  2  5
2  1  4
```

### Sorting by Index and Values Simultaneously

You can sort both by index and values by chaining the sorting methods.

```python
# Sort by column 'B' and then by index
df_sorted_values_then_index = df.sort_values(by='B').sort_index()
print("DataFrame sorted by column 'B' and then by index:\n", df_sorted_values_then_index)
```

**Output:**

```
DataFrame sorted by column 'B' and then by index:
    A  B
1  4  2
2  1  4
4  3  3
3  2  5
```

### Sorting with NaNs

When sorting, NaNs are placed at the end by default.

### Sorting with NaNs

```python
import numpy as np

# DataFrame with NaNs
data_with_nans = {'A': [np.nan, 1, 4, 3], 'B': [5, np.nan, 2, 3]}
df_with_nans = pd.DataFrame(data_with_nans)
print("Original DataFrame with NaNs:\n", df_with_nans)

# Sort by column 'A'
df_sorted_nans = df_with_nans.sort_values(by='A')
print("DataFrame with NaNs sorted by column 'A':\n", df_sorted_nans)
```

**Output:**

```
Original DataFrame with NaNs:
      A    B
0  NaN  5.0
1  1.0  NaN
2  4.0  2.0
3  3.0  3.0

DataFrame with NaNs sorted by column 'A':
      A    B
1  1.0  NaN
3  3.0  3.0
2  4.0  2.0
0  NaN  5.0
```

## Handling Missing Data

Methods for dealing with missing data in the DataFrame.

### `df.isnull()`

Check for missing values.

```python
df.isnull()
```

**Output:**

```
       A      B      C
0  False  False  False
1  False  False  False
```

### `df.dropna()`

Drop rows with missing values.

```python
df.dropna()
```

**Output:**

```
   A  B  C
0  2  2  3
1  8  5  6
```

### `df.fillna()`

Fill missing values with a specified value.

```python
df.fillna(0)
```

**Output:**

```
   A  B  C
0  2  2  3
1  8  5  6
```

### `df.fillna(method='ffill')`

Fill missing values forward.

```python
df.fillna(method='ffill')
```

**Output:**

```


 A  B  C
0  2  2  3
1  8  5  6
```

### `df.fillna(method='bfill')`

Fill missing values backward.

```python
df.fillna(method='bfill')
```

**Output:**

```
   A  B  C
0  2  2  3
1  8  5  6
```

# Deleting Duplicate Rows in Pandas

### Identifying Duplicate Rows

To identify duplicate rows in a DataFrame, you can use the `duplicated` method, which returns a boolean Series indicating whether each row is a duplicate of a previous row.

```python
import pandas as pd

# Sample DataFrame with duplicate rows
data = {'A': [1, 2, 2, 3, 4, 2], 'B': ['a', 'b', 'b', 'c', 'd', 'b']}
df = pd.DataFrame(data)
print("Original DataFrame:\n", df)

# Check for duplicate rows
duplicate_rows = df.duplicated()
print("\nDuplicate Rows:\n", duplicate_rows)
```

**Output:**

```
Original DataFrame:
    A  B
0  1  a
1  2  b
2  2  b
3  3  c
4  4  d
5  2  b

Duplicate Rows:
 0    False
1    False
2     True
3    False
4    False
5     True
dtype: bool
```

### Removing Duplicate Rows

To remove duplicate rows from a DataFrame, you can use the `drop_duplicates` method, which returns a new DataFrame with duplicate rows removed.

```python
# Remove duplicate rows
df_no_duplicates = df.drop_duplicates()
print("\nDataFrame with No Duplicate Rows:\n", df_no_duplicates)
```

**Output:**

```
DataFrame with No Duplicate Rows:
    A  B
0  1  a
1  2  b
3  3  c
4  4  d
```

### Removing Duplicate Rows Based on Specific Columns

You can remove duplicate rows based on specific columns by passing those columns to the `subset` parameter of the `drop_duplicates` method.

```python
# Remove duplicate rows based on column 'A'
df_no_duplicates_A = df.drop_duplicates(subset=['A'])
print("\nDataFrame with No Duplicate Rows (Based on Column 'A'):\n", df_no_duplicates_A)
```

**Output:**

```
DataFrame with No Duplicate Rows (Based on Column 'A'):
    A  B
0  1  a
1  2  b
3  3  c
4  4  d
```

### In-Place Deletion of Duplicate Rows

You can perform the deletion of duplicate rows in-place by setting the `inplace` parameter to `True`.

```python
# Remove duplicate rows in-place
df.drop_duplicates(inplace=True)
print("\nDataFrame after In-Place Deletion of Duplicate Rows:\n", df)
```

**Output:**

```
DataFrame after In-Place Deletion of Duplicate Rows:
    A  B
0  1  a
1  2  b
3  3  c
4  4  d
```

## Data Transformation

### Applying Functions

Apply functions to the DataFrame.

```python
df['A'] = df['A'].apply(np.sqrt)  # Apply numpy function
print(df)

df['A'] = df['A'].apply(lambda x: x ** 2)  # Apply lambda function
print(df)
```

**Output:**

```
         A  B  C
0  1.414214  2  3
1  2.828427  5  6

   A  B  C
0  2  2  3
1  8  5  6
```

### Mapping

Replace values using a dictionary.

```python
df['A'] = df['A'].map({2: 'two', 8: 'eight'})
print(df)
```

**Output:**

```
       A  B  C
0    two  2  3
1  eight  5  6
```

### Renaming Columns

Rename columns in the DataFrame.

```python
df.rename(columns={'A': 'Alpha', 'B': 'Beta'}, inplace=True)
print(df)
```

**Output:**

```
   Alpha  Beta  C
0    two     2  3
1  eight     5  6
```

### Changing Data Types

Change the data type of a column.

```python
df['Beta'] = df['Beta'].astype(float)
print(df.dtypes)
```

**Output:**

```
Alpha     object
Beta     float64
C          int64
dtype: object
```

## Grouping and Aggregation

Group data and perform aggregation.

### Grouping

Group by a specific column.

```python
grouped = df.groupby('Alpha')
print(grouped.size())
```

**Output:**

```
Alpha
eight    1
two      1
dtype: int64
```

### Aggregation

Perform aggregation on grouped data.

```python
grouped.sum()
```

**Output:**

```
        Beta  C
Alpha
eight     5  6
two       2  3
```

### Multiple Aggregation Functions

Apply multiple aggregation functions.

```python
grouped.agg({'Beta': ['sum', 'mean'], 'C': 'max'})
```

**Output:**

```
        Beta           C
         sum  mean  max
Alpha
eight      5   5.0    6
two        2   2.0    3
```

## Merging and Joining

Combine DataFrames using merging and joining.

### Concatenation

Concatenate DataFrames by rows or columns.

```python
df1 = pd.DataFrame({'A': [1, 2], 'B': [3, 4]})
df2 = pd.DataFrame({'A': [5, 6], 'B': [7, 8]})
print(pd.concat([df1, df2]))  # Concatenate rows
print(pd.concat([df1, df2], axis=1))  # Concatenate columns
```

**Output:**

```
   A  B
0  1  3
1  2  4
0  5  7
1  6  8

   A  B  A  B
0  1  3  5  7
1  2  4  6  8
```

### Merging

Merge DataFrames on a specific column.

```python
left = pd.DataFrame({'key': ['A', 'B', 'C'], 'value': [1, 2, 3]})
right = pd.DataFrame({'key': ['B', 'C', 'D'], 'value': [4, 5, 6]})
print(pd.merge(left, right, on='key'))
```

**Output:**

```
  key  value_x  value_y
0   B        2        4
1   C        3        5
```

### Joining

Join DataFrames on their index.

```python
left = left.set_index('key')
right = right.set_index('key')
print(left.join(right, lsuffix='_left', rsuffix='_right'))
```

**Output:**

```
      value_left  value_right
key
A            1.0          NaN
B            2.0          4.0
C            3.0          5.0
D            NaN          6.0
```

## Time Series

Work with time series data.

### Creating a Date Range

Generate a range of dates.

```python
dates = pd.date_range('20230101', periods=6)
df = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=list('ABCD'))
print(df)
```

**Output:**

```
                   A         B         C         D
2023-01-01  1.496714  0.861736 -0.268293 -0.679001
2023-01-02  0.624933  0.238925 -1.180913 -0.532086
2023-01-03 -1.227064  0.208863  0.518150 -0.204849
2023-01-04  0.647247  0.366885 -1.262563 -1.126357
2023-01-05  0.780324  0.072227 -0.288618  0.471931
2023-01-06  0.675752 -0.284303 -0.366605  1.063456
```

### Slicing by Date

Select data within a date range.

```python
df['20230102':'20230104']
```

**Output:**

```
                   A         B         C         D
2023-01-02  0.624933  0.238925 -1.180913 -0.532086
2023-01-03 -1.227064  0.208863  0.518150 -0.204849
2023-01-04  0.647247  0.366885 -1.262563 -1.126357
```

### Rolling Window

Calculate a rolling mean.

```python
df['A'].rolling(window=3).mean()
```

**Output:**

```
2023-01-01         NaN
2023-01-02         NaN
2023-01-03   -0.035806
2023-01-04    0.015039
2023-01-05    0.066502
2023-01-06    0.034312
Freq: D, Name: A, dtype: float64
```

### Expanding Window

Calculate an expanding mean.

```python
df['A'].expanding().mean()
```

**Output:**

```
2023-01-01    1.496714
2023-01-02    1.060824
2023-01-03    0.298861
2023-01-04    0.385458
2023-01-05    0.464830
2023-01-06    0.499651
Freq: D, Name: A, dtype: float64
```

## Advanced Operations

### Pivot Tables

Create pivot tables.

```python
df.pivot_table(values='D', index='A', columns='B', aggfunc=np.sum)
```

**Output:**

```
B        0.208863  0.238925  0.366885  0.861736
A
-1.227064      NaN      NaN      NaN -0.204849
 0.624933      NaN -0.532086      NaN      NaN
 0.647247      NaN      NaN -1.126357      NaN
 0.675752      NaN      NaN      NaN  1.063456
 0.780324      NaN      NaN      NaN  0.471931
 1.496714      NaN      NaN      NaN -0.679001
```

### Reshaping

Reshape data with `melt`.

```python
df = pd.DataFrame({'A': ['foo', 'bar', 'foo', 'bar'],
                   'B': ['one', 'one', 'two', 'two'],
                   'C': np.random.randn(4),
                   'D': np.random.randn(4)})
df_melted = pd.melt(df, id_vars=['A', 'B'], value_vars=['C', 'D'])
print(df_melted)
```

**Output:**

```
     A    B variable     value
0  foo  one        C  0.423554
1  bar  one        C -

0.045748
2  foo  two        C -0.124377
3  bar  two        C -1.381074
4  foo  one        D -0.768407
5  bar  one        D -0.136762
6  foo  two        D  0.442735
7  bar  two        D  0.892358
```

### Categorical Data

Work with categorical data.

```python
df['A'] = df['A'].astype('category')
print(df['A'].cat.categories)

df['A'].cat.categories = ['one', 'two']
print(df['A'])

df['A'] = df['A'].cat.set_categories(['three', 'two', 'one'])
print(df['A'])
```

**Output:**

```
Index(['bar', 'foo'], dtype='object')

0    foo
1    bar
2    foo
3    bar
Name: A, dtype: category
Categories (2, object): ['one', 'two']

0    foo
1    bar
2    foo
3    bar
Name: A, dtype: category
Categories (3, object): ['three', 'two', 'one']
```

## Exporting Data

### CSV

Export to and import from CSV.

```python
df.to_csv('data.csv', index=False)  # Export to CSV
df = pd.read_csv('data.csv')  # Import from CSV
```

### Excel

Export to and import from Excel.

```python
df.to_excel('data.xlsx', sheet_name='Sheet1', index=False)  # Export to Excel
df = pd.read_excel('data.xlsx', sheet_name='Sheet1')  # Import from Excel
```

### JSON

Export to and import from JSON.

```python
df.to_json('data.json')  # Export to JSON
df = pd.read_json('data.json')  # Import from JSON
```

## Conclusion

Pandas is an essential library for data manipulation and preparation in machine learning. Mastering it enables efficient handling of datasets, leading to better model training and evaluation.
