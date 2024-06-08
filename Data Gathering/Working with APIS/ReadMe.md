# Working with APIs

## Overview

Getting complete and high-performance data is not always the case in Machine Learning. While working on any real-world problem statement or trying to build any sort of project as a Machine Learning Practitioner, you need data. To accomplish the need for data, most of the time, it is required to fetch data from APIs. If the website does not provide an API, then the only option left is Web Scraping.

## Importing Necessary Libraries

To work with APIs and handle data, you'll need to import the `requests` library for making HTTP requests and the `pandas` library for data manipulation.

```python
import pandas as pd
import requests
```

## Fetching Data from an API

### 1. Basic Example: Fetching Data from a Single API Endpoint

First, let's fetch data from a single API endpoint. Here, we use the TheMovieDB API to get the top-rated movies.

```python
response = requests.get('https://api.themoviedb.org/3/movie/top_rated?api_key=YOUR_API_KEY&language=en-US&page=1')
temp_df = pd.DataFrame(response.json()['results'])[['id', 'title', 'overview', 'release_date', 'popularity', 'vote_average', 'vote_count']]
temp_df.head()
```

**Sample Output:**

```
      id                                title                                            overview release_date  popularity  vote_average  vote_count
0  19404           Dilwale Dulhania Le Jayenge  Raj is a rich, carefree, happy-go-lucky second...   1995-10-20      18.433           8.7        2763
1 724089           Gabriel's Inferno Part II   Professor Gabriel Emerson finally learns the t...   2020-07-31       8.439           8.7        1223
2    278           The Shawshank Redemption    Framed in the 1940s for the double murder of h...   1994-09-23      65.570           8.7       18637
3    238           The Godfather              Spanning the years 1945 to 1955, a chronicle o...   1972-03-14      63.277           8.7       14052
4 761053           Gabriel's Inferno Part III  The final part of the film adaption of the ero...   2020-11-19      26.691           8.7         773
```

### 2. Fetching Data from Multiple Pages

When dealing with APIs that paginate results, you often need to fetch data from multiple pages. Here’s how you can do it:

```python
df = pd.DataFrame()

for i in range(1, 429):
    response = requests.get('https://api.themoviedb.org/3/movie/top_rated?api_key=YOUR_API_KEY&language=en-US&page={}'.format(i))
    temp_df = pd.DataFrame(response.json()['results'])[['id', 'title', 'overview', 'release_date', 'popularity', 'vote_average', 'vote_count']]
    df = df.append(temp_df, ignore_index=True)

df.head()
```

**Sample Output:**

```
      id                                title                                            overview release_date  popularity  vote_average  vote_count
0  19404           Dilwale Dulhania Le Jayenge  Raj is a rich, carefree, happy-go-lucky second...   1995-10-20      18.433           8.7        2763
1 724089           Gabriel's Inferno Part II   Professor Gabriel Emerson finally learns the t...   2020-07-31       8.439           8.7        1223
2    278           The Shawshank Redemption    Framed in the 1940s for the double murder of h...   1994-09-23      65.570           8.7       18637
3    238           The Godfather              Spanning the years 1945 to 1955, a chronicle o...   1972-03-14      63.277           8.7       14052
4 761053           Gabriel's Inferno Part III  The final part of the film adaption of the ero...   2020-11-19      26.691           8.7         773
```

### 3. Saving Data to CSV

Once you have fetched and compiled your data, you can save it to a CSV file for later use.

```python
df.to_csv('movies.csv', index=False)
```

**Sample Output:**
The above command will create a `movies.csv` file in your working directory with the fetched data.

### Use Cases

1. **Real-time Data Analysis**: APIs are often used to get real-time data for applications like stock market analysis, weather forecasting, and more.
2. **Data Integration**: APIs allow different systems to communicate and share data seamlessly, making it easier to integrate different data sources.
3. **Automation**: Automate data collection from various sources without manual intervention, which is useful for regular updates and monitoring.

### Important Considerations

- **API Rate Limits**: Many APIs have rate limits that restrict the number of requests you can make in a given time period. Always check the API documentation for such limits.
- **Error Handling**: Implement proper error handling to manage scenarios where the API call fails or returns unexpected results.
- **Authentication**: Some APIs require authentication via API keys or OAuth tokens. Ensure you handle these securely.

By following these steps, you can efficiently fetch and manipulate data from APIs, which is an essential skill for any data scientist or machine learning practitioner.

---
