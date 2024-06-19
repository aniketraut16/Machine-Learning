# EDA (Bivariate and Multivariate)

In this we explore techniques for conducting bivariate and multivariate exploratory data analysis (EDA) using datasets as examples. Bivariate and multivariate analysis involves examining relationships between variables to understand patterns, correlations, and dependencies within the dataset.

## 1. Scatterplot (Numerical - Numerical)

### Approach:

- **Scatterplot**: Use scatterplots to visualize the relationship between two numerical variables. This helps understand patterns, correlations, and outliers.

  ```python
  import seaborn as sns
  import matplotlib.pyplot as plt

  sns.scatterplot(data=tips, x='total_bill', y='tip', hue='sex', style='smoker', size='size')
  plt.title('Scatterplot of Total Bill vs Tip')
  plt.show()
  ```

### Outcome:

- **Conclusion**: Scatterplots reveal how the relationship between two numerical variables ('total_bill' and 'tip' in this case) varies based on additional categorical variables ('sex' and 'smoker'). They help identify clusters, trends, and potential outliers.

## 2. Bar Plot (Numerical - Categorical)

### Approach:

- **Bar Plot**: Use bar plots to compare numerical data across different categories. They visualize the mean or aggregated values of numerical variables grouped by categories.

  ```python
  import seaborn as sns
  import matplotlib.pyplot as plt

  sns.barplot(data=titanic, x='Pclass', y='Age', hue='Sex')
  plt.title('Average Age by Passenger Class and Gender')
  plt.show()
  ```

### Outcome:

- **Conclusion**: Bar plots illustrate how numerical data ('Age' in this case) varies across different categories ('Pclass' and 'Sex'). They provide insights into average values and comparisons between groups.

## 3. Box Plot (Numerical - Categorical)

### Approach:

- **Box Plot**: Use box plots to visualize the distribution of numerical data across categories. They display the median, quartiles, and outliers, helping understand variability within groups.

  ```python
  import seaborn as sns
  import matplotlib.pyplot as plt

  sns.boxplot(data=titanic, x='Sex', y='Age', hue='Survived')
  plt.title('Age Distribution by Gender and Survival')
  plt.show()
  ```

### Outcome:

- **Conclusion**: Box plots highlight how the distribution of numerical data ('Age' in this case) varies across different categories ('Sex') and further segmented by another categorical variable ('Survived'). They help identify differences in central tendency and variability between groups.

## 4. Distplot (Numerical - Categorical)

### Approach:

- **Distplot**: Use distribution plots to compare the distribution of numerical variables across categories. Overlaying distributions helps visualize differences in data distribution.

  ```python
  import seaborn as sns
  import matplotlib.pyplot as plt

  sns.distplot(titanic[titanic['Survived'] == 0]['Age'], hist=False, label='Not Survived')
  sns.distplot(titanic[titanic['Survived'] == 1]['Age'], hist=False, label='Survived')
  plt.title('Age Distribution by Survival')
  plt.xlabel('Age')
  plt.ylabel('Density')
  plt.legend()
  plt.show()
  ```

### Outcome:

- **Conclusion**: Distplots compare the distribution of numerical data ('Age' in this case) between two categories ('Survived' and 'Not Survived'). They help visualize differences in the spread and shape of data distributions.

## 5. Heatmap (Categorical - Categorical)

### Approach:

- **Heatmap**: Use heatmaps to visualize the relationship between two categorical variables using frequency or aggregated values.

  ```python
  import seaborn as sns
  import matplotlib.pyplot as plt

  correlation_matrix = titanic.groupby('Pclass')['Survived'].mean().unstack()
  sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')
  plt.title('Survival Rate by Passenger Class')
  plt.show()
  ```

### Outcome:

- **Conclusion**: Heatmaps display the relationship between two categorical variables ('Pclass' and 'Survived') using color intensity. They help identify patterns and correlations, such as higher survival rates in certain passenger classes.

## 6. Clustermap (Categorical - Categorical)

### Approach:

- **Clustermap**: Use clustermaps to visualize hierarchical clustering of categorical variables based on similarity.

  ```python
  import seaborn as sns

  cluster_grid = sns.clustermap(pd.crosstab(titanic['Parch'], titanic['Survived']), cmap='coolwarm')
  plt.title('Hierarchical Clustering of Parent-Child Relationships vs Survival')
  plt.show()
  ```

### Outcome:

- **Conclusion**: Clustermaps depict hierarchical clustering of categorical variables ('Parch' and 'Survived' in this example), revealing patterns and similarities in grouped data.

## 7. Pairplot (Multivariate)

### Approach:

- **Pairplot**: Use pairplots to visualize relationships between multiple numerical variables at once, with additional categorical hue for differentiation.

  ```python
  import seaborn as sns

  sns.pairplot(iris, hue='species')
  plt.title('Pairplot of Iris Dataset')
  plt.show()
  ```

### Outcome:

- **Conclusion**: Pairplots show pairwise relationships between numerical variables ('sepal_length', 'sepal_width', 'petal_length', 'petal_width' in the Iris dataset) and differentiate by categorical variable ('species'). They help identify correlations and clusters across multiple dimensions.

## 8. Line Plot (Numerical - Numerical)

### Approach:

- **Line Plot**: Use line plots to visualize trends and patterns in numerical data over time or another continuous variable.

  ```python
  import seaborn as sns
  import matplotlib.pyplot as plt

  new_flights = flights.groupby('year').sum().reset_index()
  sns.lineplot(data=new_flights, x='year', y='passengers')
  plt.title('Trend of Passengers Over Years')
  plt.show()
  ```

### Outcome:

- **Conclusion**: Line plots illustrate trends and changes in numerical data ('passengers' in the Flights dataset) over time ('year'). They help identify growth trends or fluctuations over continuous variables.

---

By applying these techniques in bivariate and multivariate EDA, we gain insights into relationships, patterns, and dependencies between variables within datasets. These insights inform further analysis and modeling decisions, facilitating a deeper understanding of data characteristics.
