# Web Scraping

## Overview

Web scraping is a powerful technique for gathering data from websites, making it an invaluable tool for machine learning practitioners. By extracting large and diverse datasets, you can train, validate, and test machine learning models more effectively. This guide will introduce you to web scraping using Python, highlighting the necessary libraries, their key functions, use cases in the context of machine learning, and practical implementation steps.

## Libraries Needed

To perform web scraping in Python, the following libraries are essential:

1. **requests**: To make HTTP requests and fetch web pages.
2. **BeautifulSoup**: For parsing HTML and XML documents to extract data.
3. **pandas**: For storing and processing the scraped data in a structured format.

### Main Functions of Each Library

#### `requests`

- **`get(url, headers)`**: Sends a GET request to the specified URL with optional headers. Returns the response object.
- **`status_code`**: Checks the HTTP status code of the response to ensure the request was successful.

#### `BeautifulSoup`

- **`BeautifulSoup(html, parser)`**: Parses the HTML content using the specified parser (e.g., 'lxml').
- **`find_all(tag, class_)`**: Finds all occurrences of the specified HTML tag and class.
- **`find(tag, class_)`**: Finds the first occurrence of the specified HTML tag and class.
- **`get_text()`**: Extracts all the text from the HTML elements.
- **`get(attribute)`**: Retrieves the value of an attribute of an HTML element.
- **`select(css_selector)`**: Finds all elements matching the CSS selector.

#### `pandas`

- **`DataFrame(data)`**: Creates a DataFrame from the provided data.
- **`to_csv(filename)`**: Saves the DataFrame to a CSV file.

## Use Cases of Web Scraping in Machine Learning

Web scraping can significantly enhance machine learning projects by providing large and diverse datasets. Here are some specific use cases:

- **Training Data**: Collecting vast amounts of data from various websites to train machine learning models. For example, scraping product information from e-commerce sites to build recommendation systems.
- **Feature Extraction**: Extracting specific features from web pages to improve model performance. For instance, gathering job descriptions and requirements for resume matching algorithms.
- **Sentiment Analysis**: Scraping reviews, comments, or social media posts to perform sentiment analysis. This can be used to gauge public opinion on products, services, or events.
- **Market Analysis**: Gathering data on products, prices, and trends from different websites to build predictive models for market analysis. This is useful for forecasting market trends and making business decisions.
- **Image Recognition**: Collecting images from the web to train computer vision models. For example, scraping labeled images from multiple sources to improve the accuracy of an object detection model.

## Implementation

### Step 1: Setting Up the Environment

First, import the necessary libraries:

```python
import pandas as pd
import requests
from bs4 import BeautifulSoup
import time
```

### Step 2: Define the Base URL and Headers

Set the base URL of the website you want to scrape and define headers to mimic a real browser request:

```python
base_url = 'https://www.ambitionbox.com/list-of-companies?page='
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36',
    'Accept-Language': 'en-US,en;q=0.9',
    'Accept-Encoding': 'gzip, deflate, br',
    'Connection': 'keep-alive',
    'Upgrade-Insecure-Requests': '1',
    'Referer': 'https://google.com',
}
```

### Step 3: Data Storage

Initialize an empty list to store the scraped data:

```python
data = []
```

### Step 4: Scraping a Single Page

Create a function to scrape data from a single page:

```python
def scrape_page(page_number):
    url = base_url + str(page_number)
    response = requests.get(url, headers=headers)
    if response.status_code != 200:
        return

    webpage = BeautifulSoup(response.text, 'lxml')

    for company in webpage.find_all('div', class_='companyCardWrapper'):
        one_company = {}

        name_tag = company.find('h2', class_='companyCardWrapper__companyName')
        if name_tag:
            one_company["name"] = name_tag.text.strip()

        rating_tag = company.find('span', class_='companyCardWrapper__companyRatingValue')
        if rating_tag:
            one_company["rating"] = float(rating_tag.text.strip())

        other_info_tag = company.find('span', class_='companyCardWrapper__interLinking')
        if other_info_tag:
            other_info_list = other_info_tag.text.strip().split("|")
            one_company["sector"] = other_info_list[0].strip()
            for item in other_info_list[1:]:
                if 'Employees' in item:
                    one_company["no_of_employees"] = item.strip()
                elif 'years old' in item:
                    one_company["age_of_company"] = int(item.split()[0].strip())
                elif 'more' in item:
                    one_company["headquarters_location"] = item.split("+")[0].strip()
                else:
                    one_company["ownership_status"] = item.strip()

        actions = company.find_all('a', class_='companyCardWrapper__ActionWrapper')
        for action in actions:
            if 'Reviews' in action.text:
                continue
            elif 'Salaries' in action.text:
                one_company['salary'] = parse_range(action.text.strip().split()[0])
            elif 'Jobs' in action.text:
                one_company['available_jobs'] = convert_to_number(action.text.strip().split()[0])

        data.append(one_company)
```

### Step 5: Scraping Multiple Pages

Use a loop to scrape multiple pages, adding a delay between requests to avoid overloading the server:

```python
start_time = time.time()

n_pages = 10  # Number of pages to scrape

for page_number in range(1, n_pages + 1):
    scrape_page(page_number)
    time.sleep(1)  # Delay to avoid getting blocked

end_time = time.time()
time_taken = end_time - start_time
print(f'It took {time_taken} seconds to scrape {n_pages} pages')
```

### Step 6: Storing the Data

Convert the data into a pandas DataFrame and save it to a CSV file:

```python
df = pd.DataFrame(data)
df.to_csv('company_data.csv', index=False)
```

### Example Output

The resulting DataFrame might look like this:

```
           name  rating               sector        no_of_employees  ... headquarters_location     salary  available_jobs
0           TCS     3.8  IT Services & Consulting  1 Lakh+ Employees  ...                Mumbai  870000.0         1100.0
1     Accenture     4.0  IT Services & Consulting  1 Lakh+ Employees  ...                Dublin  590000.0        43200.0
...
```

### Summary

Web scraping involves fetching web pages, parsing HTML to extract relevant information, and storing the data in a structured format like a pandas DataFrame. This guide provides a robust framework for scraping websites while ensuring ethical practices, like adding delays between requests to avoid server overload.
