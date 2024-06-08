# Working with JSON/SQL

## Overview

In this section, we'll cover how to work with JSON (JavaScript Object Notation) and SQL (Structured Query Language) for data gathering. These formats are commonly used for data interchange and database management, making them essential skills for data manipulation and analysis in machine learning.

### JSON (JavaScript Object Notation)

JSON is a lightweight data-interchange format that is easy for humans to read and write, and easy for machines to parse and generate. It is commonly used in web applications to exchange data between a server and client.

### SQL (Structured Query Language)

SQL is a standard language for managing and manipulating relational databases. It allows for efficient querying, updating, and managing of structured data, making it a powerful tool for data analysis.

## Working with JSON

### 1. Importing pandas

To work with JSON data in Python, you need to import the pandas library.

```python
import pandas as pd
```

### 2. Opening a Local JSON File

You can read a JSON file stored locally using `pd.read_json`.

```python
df = pd.read_json('train.json')
df.head()
```

**Sample Input (train.json):**

```json
[
  { "id": 1, "name": "Alice", "age": 25 },
  { "id": 2, "name": "Bob", "age": 30 },
  { "id": 3, "name": "Charlie", "age": 35 }
]
```

**Sample Output:**

```
   id    name  age
0   1   Alice   25
1   2     Bob   30
2   3  Charlie  35
```

### 3. Opening a JSON File from a URL

You can also read JSON data directly from a URL using the `requests` library to fetch the data and `pd.read_json` to parse it.

```python
import requests

url = 'https://api.exchangerate-api.com/v4/latest/INR'
response = requests.get(url)
data = response.json()

df = pd.json_normalize(data)
df.head()
```

**Sample Output:**

```
    base_date   rates.INR   rates.USD   rates.EUR
0    INR        1.0         0.014       0.012
```

### Useful Parameters for `pd.read_json`

- `orient`: The format of the JSON string. For example, `records` for a list of dictionaries.
- `typ`: Type of object to return, either `series` or `frame`.
- `convert_dates`: List of columns to convert to datetime.

**Example with Parameters**

```python
df = pd.read_json('train.json', orient='records', convert_dates=['date'])
df.head()
```

**Sample Output:**

```
   id    name   age       date
0   1   Alice   25 2023-01-01
1   2     Bob   30 2023-01-02
2   3  Charlie  35 2023-01-03
```

## Working with SQL

### 1. Installing MySQL Connector

To connect to a MySQL database, you need to install the MySQL connector.

```python
!pip install mysql-connector-python
```

### 2. Importing Required Libraries

Import the necessary libraries for connecting to the database and working with pandas.

```python
import mysql.connector
import pandas as pd
```

### 3. Connecting to a MySQL Database

Establish a connection to your MySQL database.

```python
conn = mysql.connector.connect(
    host='localhost',
    user='root',
    password='',
    database='world'
)
```

### 4. Executing a SQL Query and Loading Data into a DataFrame

You can use `pd.read_sql_query` to execute a SQL query and load the result into a DataFrame.

```python
df = pd.read_sql_query("SELECT * FROM countrylanguage", conn)
df.head()
```

**Sample Output:**

```
   CountryCode Language  IsOfficial  Percentage
0          ABW    Dutch           T         5.3
1          ABW  Papiamento        T        81.2
2          ABW  English           F         7.7
3          ABW  Spanish           F         5.8
4          AFG  Pashto            T        52.4
```

### Useful Parameters for `pd.read_sql_query`

- `params`: Parameters to pass to the SQL query.
- `index_col`: Column(s) to set as index(MultiIndex).
- `coerce_float`: Attempt to convert values to non-string, non-numeric objects to floating point.

**Example with Parameters**

```python
query = "SELECT * FROM countrylanguage WHERE CountryCode = %s"
df = pd.read_sql_query(query, conn, params=['USA'])
df.head()
```

**Sample Output:**

```
   CountryCode Language  IsOfficial  Percentage
0          USA  English         T          82.1
1          USA  Spanish         F          10.7
2          USA  Chinese         F           1.0
3          USA   French         F           1.0
4          USA  Tagalog         F           0.4
```

## Conclusion

Understanding how to work with JSON and SQL databases is essential for effective data gathering in machine learning. JSON is useful for web-based data interchange, while SQL is vital for managing and querying structured data in relational databases.

---
