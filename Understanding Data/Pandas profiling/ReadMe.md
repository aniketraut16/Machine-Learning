# Dataset Analysis with pandas-profiling

This project demonstrates the use of `pandas-profiling` to generate a detailed exploratory data analysis (EDA) report on the Titanic dataset. `pandas-profiling` is a Python library that provides an easy way to create profile reports from a pandas DataFrame. The report includes a variety of descriptive statistics, visualizations, and insights that can be useful for understanding the dataset and identifying potential data quality issues.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Dataset](#dataset)
- [Generating the Report](#generating-the-report)
- [Example Output](#example-output)

## Installation

To use `pandas-profiling`, you need to have Python installed on your system. You can install `pandas-profiling` using `pip`. Run the following command in your terminal:

```bash
pip install pandas-profiling
```

Ensure you have the necessary dependencies as well:

```bash
pip install pandas seaborn tqdm scipy htmlmin tangled-up-in-unicode missingno matplotlib requests numpy ipywidgets joblib jinja2
```

## Usage

To generate a profile report, follow these steps:

1. **Import Libraries**: Import the required libraries.
2. **Load Data**: Load your dataset into a pandas DataFrame.
3. **Generate Report**: Use `pandas-profiling` to create the report.

## Project Structure

The project contains the following files:

- `README.md`: This file.
- `train.csv`: The Titanic dataset.
- `titanic_analysis.ipynb`: Jupyter Notebook containing the analysis code.

## Dataset

The dataset used in this project is the Titanic dataset, which includes information about the passengers aboard the Titanic. The dataset has the following columns:

- `PassengerId`: Unique ID for each passenger
- `Survived`: Survival indicator (0 = No, 1 = Yes)
- `Pclass`: Passenger class (1 = 1st, 2 = 2nd, 3 = 3rd)
- `Name`: Name of the passenger
- `Sex`: Gender of the passenger
- `Age`: Age of the passenger
- `SibSp`: Number of siblings/spouses aboard
- `Parch`: Number of parents/children aboard
- `Ticket`: Ticket number
- `Fare`: Fare paid
- `Cabin`: Cabin number
- `Embarked`: Port of embarkation (C = Cherbourg, Q = Queenstown, S = Southampton)

## Generating the Report

Below is a step-by-step guide on how to generate the profile report using the Titanic dataset.

### Step 1: Import Libraries

```python
import pandas as pd
import pandas_profiling
```

### Step 2: Load Data

```python
df = pd.read_csv('train.csv')
```

### Step 3: Generate Report

```python
profile = df.profile_report(title='Titanic Dataset Analysis')
profile.to_file("titanic_report.html")
```

### Complete Code

The complete code in the Jupyter Notebook (`titanic_analysis.ipynb`) is as follows:

```python
# Importing necessary libraries
import pandas as pd

# Loading the Titanic dataset
df = pd.read_csv('train.csv')

# Displaying the first few rows of the dataset
df.head()

# Installing pandas-profiling
!pip install pandas-profiling

# Importing pandas-profiling
import pandas_profiling

# Generating the profiling report
profile = df.profile_report(title='Titanic Dataset Analysis')

# Saving the report to an HTML file
profile.to_file("titanic_report.html")
```

## Example Output

The output of the profiling report provides a comprehensive analysis of the dataset, including:

- Overview of the dataset
- Detailed statistics for each column
- Visualizations (correlation matrix, missing values, distributions, etc.)
- Warnings about potential data quality issues
