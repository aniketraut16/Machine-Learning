## Working with CSV

CSV (Comma Separated Values) files are a common format for storing tabular data. This guide provides detailed instructions on how to work with CSV files using the Pandas library in Python.

#### 1. Importing Pandas

First, you need to import the Pandas library.

```python
import pandas as pd
```

Use Case: This is the first step in any script that uses Pandas for data manipulation.

#### 2. Opening a Local CSV File

You can read a local CSV file into a DataFrame using `pd.read_csv`.

```python
df = pd.read_csv('aug_train.csv')
df.head()
```

**Sample Input (`aug_train.csv`):**

```
enrollee_id,gender,education_level,target
1,Male,Graduate,1
2,Female,Masters,0
3,,High School,0
4,Male,Phd,1
5,Female,Graduate,0
```

**Sample Output:**

```
   enrollee_id  gender education_level  target
0            1    Male        Graduate       1
1            2  Female         Masters       0
2            3     NaN      High School       0
3            4    Male             Phd       1
4            5  Female        Graduate       0
```

Use Case: Quickly load and inspect the contents of a CSV file.

#### 3. Opening a CSV File from a URL

You can read a CSV file from a URL.

```python
import requests
from io import StringIO

url = "https://raw.githubusercontent.com/cs109/2014_data/master/countries.csv"
headers = {"User-Agent": "Mozilla/5.0"}
req = requests.get(url, headers=headers)
data = StringIO(req.text)

df = pd.read_csv(data)
df.head()
```

**Sample Output:**

```
       Country      Region
0  Afghanistan      ASIA
1      Albania    EUROPE
2      Algeria    AFRICA
3      Andorra    EUROPE
4       Angola    AFRICA
```

Use Case: Fetch and read CSV data directly from an online source.

#### 4. `sep` Parameter

Specify a different delimiter if the CSV uses something other than a comma.

```python
df = pd.read_csv('movie_titles_metadata.tsv', sep='\t', names=['sno', 'name', 'release_year', 'rating', 'votes', 'genres'])
df.head()
```

**Sample Input (`movie_titles_metadata.tsv`):**

```
1	Avatar	2009	7.9	8555	Action|Adventure|Fantasy
2	Pirates of the Caribbean: At World's End	2007	7.1	4500	Action|Adventure|Fantasy
```

**Sample Output:**

```
   sno                                           name  release_year  rating  votes                    genres
0    1                                        Avatar          2009     7.9   8555    Action|Adventure|Fantasy
1    2  Pirates of the Caribbean: At World's End          2007     7.1   4500    Action|Adventure|Fantasy
```

Use Case: Handle files with different delimiters such as tabs, semicolons, etc.

#### 5. `index_col` Parameter

Set a column as the index of the DataFrame.

```python
df = pd.read_csv('aug_train.csv', index_col='enrollee_id')
df.head()
```

**Sample Output:**

```
             gender education_level  target
enrollee_id
1              Male        Graduate       1
2            Female         Masters       0
3               NaN      High School       0
4              Male             Phd       1
5            Female        Graduate       0
```

Use Case: Use a specific column as the index for easier data manipulation and lookups.

#### 6. `header` Parameter

Specify which row to use as the header.

```python
df = pd.read_csv('test.csv', header=1)
df.head()
```

**Sample Input (`test.csv`):**

```
id,name,age
1,John,25
2,Jane,30
id,name,age
3,Tom,22
4,Alice,28
```

**Sample Output:**

```
   3   Tom  22
0  4  Alice  28
```

Use Case: Skip initial rows if the actual header is not in the first row.

#### 7. `usecols` Parameter

Read specific columns from the CSV.

```python
df = pd.read_csv('aug_train.csv', usecols=['enrollee_id', 'gender', 'education_level'])
df.head()
```

**Sample Output:**

```
   enrollee_id  gender education_level
0            1    Male        Graduate
1            2  Female         Masters
2            3     NaN      High School
3            4    Male             Phd
4            5  Female        Graduate
```

Use Case: Load only the necessary columns to save memory and processing time.

#### 8. `squeeze` Parameter

Convert a single column DataFrame into a Series.

```python
series = pd.read_csv('aug_train.csv', usecols=['gender'], squeeze=True)
series.head()
```

**Sample Output:**

```
0      Male
1    Female
2       NaN
3      Male
4    Female
Name: gender, dtype: object
```

Use Case: Convert DataFrame with one column to a Series for simpler data manipulation.

#### 9. `skiprows`/`nrows` Parameter

Skip a specific number of rows or limit the number of rows read.

```python
df = pd.read_csv('aug_train.csv', nrows=100)
df.head()
```

**Sample Output:**

```
   enrollee_id  gender education_level  target
0            1    Male        Graduate       1
1            2  Female         Masters       0
2            3     NaN      High School       0
3            4    Male             Phd       1
4            5  Female        Graduate       0
```

Use Case: Work with a subset of the data for quick testing or processing.

#### 10. `encoding` Parameter

Specify the encoding of the file.

```python
df = pd.read_csv('zomato.csv', encoding='latin-1')
df.head()
```

**Sample Output:**

```
   url                                address
0  zomato.com/ncr/the-oberoi-patisserie-and...  The Oberoi, 1st Floor, Dr. Zakir Hussain Mar...
1  zomato.com/ncr/the-coffee-shop-raddisson...  Raddisson Blu Marina, Connaught Place, New D...
2  zomato.com/ncr/bukhara-itc-maurya-chanak...  ITC Maurya, Chanakyapuri, New Delhi
3  zomato.com/ncr/bukhara-itc-maurya-chanak...  ITC Maurya, Chanakyapuri, New Delhi
4  zomato.com/ncr/bukhara-itc-maurya-chanak...  ITC Maurya, Chanakyapuri, New Delhi
```

Use Case: Handle CSV files with different character encodings.

#### 11. Skip Bad Lines

Skip bad lines while reading the file.

```python
df = pd.read_csv('BX-Books.csv', sep=';', encoding='latin-1', error_bad_lines=False)
df.head()
```

**Sample Input (`BX-Books.csv`):**

```
book_id;title;author
1;Harry Potter;J.K. Rowling
2;Lord of the Rings;J.R.R. Tolkien
badline;with;incorrect;number;of;columns
3;The Catcher in the Rye;J.D. Salinger
```

**Sample Output:**

```
   book_id                   title           author
0        1           Harry Potter    J.K. Rowling
1        2  Lord of the Rings  J.R.R. Tolkien
2        3  The Catcher in the Rye  J.D. Salinger
```

Use Case: Ignore corrupted or malformed lines in the CSV file.

#### 12. `dtype` Parameter

Specify data types for columns.

```python
df = pd.read_csv('aug_train.csv', dtype={'target': int})
df.info()
```

**Sample Output:**

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 5 entries, 0 to 4
Data columns (total 4 columns):
 #   Column          Non-Null Count  Dtype
---  ------          --------------  -----
 0   enrollee_id     5 non-null      int64
 1   gender          4 non-null      object
 2   education_level 5 non-null      object
 3   target          5 non-null      int32
dtypes: int32(1), int64(1), object(2)
memory usage: 300.0+ bytes
```

Use Case: Ensure that columns have the correct data types for analysis.

#### 13. Handling Dates

Parse dates while reading the file.

```python
df = pd.read_csv('IPL Matches 2008-2020.csv', parse_dates=['date'])
df.info()
```

**Sample Output:**

```
<class

 'pandas.core.frame.DataFrame'>
RangeIndex: 5 entries, 0 to 4
Data columns (total 3 columns):
 #   Column          Non-Null Count  Dtype
---  ------          --------------  -----
 0   id              5 non-null      int64
 1   team1           5 non-null      object
 2   date            5 non-null      datetime64[ns]
dtypes: datetime64 , int64(1), object(1)
memory usage: 248.0+ bytes
```

Use Case: Automatically convert columns to datetime objects for time series analysis.

#### 14. Converters

Use converters to transform data while reading the file.

```python
def rename(team):
    return team.upper()

df = pd.read_csv('IPL Matches 2008-2020.csv', converters={'team1': rename})
df.head()
```

**Sample Output:**

```
   id    team1       date
0   1  MUMBAI  2020-09-19
1   2  CHENNAI  2020-09-20
2   3  BANGALORE  2020-09-21
3   4  HYDERABAD  2020-09-22
4   5  KOLKATA  2020-09-23
```

Use Case: Apply custom transformations to data while loading it.

#### 15. `na_values` Parameter

Specify additional strings to recognize as NA/NaN.

```python
df = pd.read_csv('aug_train.csv', na_values=['Male'])
df.head()
```

**Sample Output:**

```
   enrollee_id gender education_level  target
0            1    NaN        Graduate       1
1            2  Female         Masters       0
2            3    NaN      High School       0
3            4    NaN             Phd       1
4            5  Female        Graduate       0
```

Use Case: Treat specific strings as missing values.

#### 16. Loading a Huge Dataset in Chunks

Read a large CSV file in chunks to avoid memory issues.

```python
dfs = pd.read_csv('aug_train.csv', chunksize=5000)
for chunk in dfs:
    print(chunk.shape)
```

**Sample Output:**

```
(5000, 4)
(5000, 4)
...
```

Use Case: Process large datasets in smaller, manageable chunks.
