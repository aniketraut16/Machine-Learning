## Data Gathering

Data gathering is a crucial step in the machine learning process. There are multiple methods to gather data, but the most common ones are:

1. **CSV (Comma Separated Values) Files**
2. **JSON/SQL Databases**
3. **APIs**
4. **Web Scraping**

Each of these methods has its own advantages and use cases. Below, we provide an overview of each method with examples.

### 1. CSV Files

CSV files are one of the simplest ways to store tabular data. Each line in a CSV file corresponds to a row in the table, and columns are separated by commas.

#### Example

```python
import pandas as pd

# Opening a local CSV file
df = pd.read_csv('local_file.csv')
print(df.head())
```

### 2. JSON/SQL Databases

#### JSON

JSON (JavaScript Object Notation) is a lightweight data-interchange format that is easy for humans to read and write and easy for machines to parse and generate.

#### Example

```python
import pandas as pd

# Reading a JSON file
df = pd.read_json('file.json')
print(df.head())
```

#### SQL

SQL databases are used to store structured data. SQL (Structured Query Language) is used to communicate with databases.

#### Example

```python
import pandas as pd
from sqlalchemy import create_engine

# Connecting to a SQL database
engine = create_engine('sqlite:///database.db')
df = pd.read_sql('SELECT * FROM table_name', engine)
print(df.head())
```

### 3. APIs

APIs (Application Programming Interfaces) allow you to access data from a web service. You send a request to the server, and the server sends back the data.

#### Example

```python
import requests

url = "https://api.example.com/data"
response = requests.get(url)
data = response.json()
print(data)
```

### 4. Web Scraping

Web scraping is a technique used to extract data from websites. It involves fetching the web page and parsing the HTML to find the data you need.

#### Example

```python
import requests
from bs4 import BeautifulSoup

url = "https://example.com"
response = requests.get(url)
soup = BeautifulSoup(response.content, 'html.parser')

data = soup.find_all('div', class_='data')
for item in data:
    print(item.text)
```
