# EDA (Univarient)

In this folder, we explore various techniques for conducting univariate exploratory data analysis (EDA) using datasets as examples. Univariate analysis involves examining individual variables one at a time to understand their distribution and characteristics.

## 1. Categorical Data

### Approach:

- **Counting Categories (Countplot)**: Use a countplot to visualize the frequency of each category in categorical variables. This helps understand the distribution and prevalence of different categories among the dataset.

  ```python
  import seaborn as sns
  import matplotlib.pyplot as plt

  sns.countplot(df['Categorical_Column'])
  plt.title('Count of Categories')
  plt.show()
  ```

### Outcome:

- **Conclusion**: Countplots provide insights into the distribution of categorical variables. They help visualize the prevalence of different categories, such as customer segments, types of products, or geographical regions.

## 2. Numerical Data

### Approach:

- **Histograms**: Histograms display the distribution of numerical data by dividing it into bins and plotting the frequency of values within each bin. This helps visualize the range and distribution pattern of variables like 'Age' or 'Income'.

  ```python
  import matplotlib.pyplot as plt

  plt.hist(df['Numerical_Column'], bins=10)
  plt.title('Distribution of Numerical Data')
  plt.xlabel('Numerical Data')
  plt.ylabel('Count')
  plt.show()
  ```

- **Boxplots**: Boxplots summarize the distribution of numerical data using quartiles. They show the median, interquartile range, and outliers. Boxplots are useful for detecting outliers and understanding the spread and skewness of data.

  ```python
  import seaborn as sns
  import matplotlib.pyplot as plt

  sns.boxplot(df['Numerical_Column'])
  plt.title('Boxplot of Numerical Data')
  plt.xlabel('Numerical Data')
  plt.show()
  ```

- **Summary Statistics**: Calculating summary statistics such as minimum, maximum, mean, and skewness provides a quantitative understanding of numerical data. These statistics help in assessing the central tendency, variability, and shape of the distribution.

  ```python
  df['Numerical_Column'].describe()
  ```

### Outcome:

- **Conclusion**: Histograms and boxplots provide insights into the distribution and spread of numerical variables. They help identify patterns and outliers, such as age distribution in a population or income disparities.
- **Summary statistics** complement visualizations by providing numerical insights, such as the average value or variability in the dataset.

---

By applying these techniques in univariate EDA, we gain a comprehensive understanding of individual variables within datasets. This understanding helps in identifying patterns, outliers, and potential relationships that inform further analysis and modeling decisions.
