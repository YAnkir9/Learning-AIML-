# State Population Analysis

This project analyzes the population and murder rate data of U.S. states using various statistical techniques. The analysis aims to extract meaningful insights and understand the distribution and central tendencies of the population data.

## Dataset

The dataset used in this analysis is `state.csv`, which contains the following columns:

- `State`: Name of the U.S. state.
- `Population`: Population count (2010 Census).
- `Murder Rate`: Number of murders per 100,000 people.

## Analysis Techniques

### 1. Mean Calculation

- **Purpose**: To calculate the average population across all states.
- **Reason**: The mean provides a general idea of the central tendency but is sensitive to outliers.

```python
import pandas as pd

data = pd.read_csv('state.csv')
mean_population = data['Population'].mean()
print("Mean of Population:", mean_population)
```

### 2. Trimmed Mean

- **Purpose**: To compute the mean after removing a certain percentage of the highest and lowest values.
- **Reason**: It provides a more robust estimate by reducing the impact of outliers.

```python
from scipy.stats import trim_mean

trimmed_mean_population = trim_mean(data['Population'], 0.2)
print("Trimmed Mean of Population (by removing highest and lowest 20% data):", trimmed_mean_population)
```

### 3. Density Histogram

- **Purpose**: To visualize the distribution of population data.
- **Reason**: A density histogram helps in understanding the spread and concentration of data points, which is more informative than a simple count histogram.

```python
import matplotlib.pyplot as plt

plt.hist(data['Population'], bins=30, density=True, alpha=0.6, color='g', edgecolor='black')
plt.xlabel('Population')
plt.ylabel('Density')
plt.title('Density Histogram of State Population')
plt.show()
```

### 4. Kernel Density Estimate (KDE) Curve

- **Purpose**: To overlay a smooth curve that represents the distribution of the data.
- **Reason**: KDE provides a continuous probability density function, making it easier to visualize the distribution.

```python
import numpy as np
from scipy.stats import gaussian_kde

kde = gaussian_kde(data['Population'])
population_range = np.linspace(data['Population'].min(), data['Population'].max(), 1000)
kde_values = kde(population_range)

plt.plot(population_range, kde_values, color='r', label='KDE Curve')
plt.xlabel('Population')
plt.ylabel('Density')
plt.title('Density Histogram of State Population with KDE Curve')
plt.legend()
plt.show()
```

### 5. Box Plot

- **Purpose**: To summarize the data distribution using five-number summary: minimum, first quartile, median, third quartile, and maximum.
- **Reason**: Box plots are excellent for identifying outliers and understanding the spread of the data.

```python
import seaborn as sns

sns.boxplot(x=data['Population'])
plt.title('Box Plot of State Population')
plt.show()
```

## Libraries Used

- `pandas`: For data manipulation and analysis.
- `numpy`: For numerical computations.
- `scipy.stats`: For statistical operations.
- `wquantiles`: For weighted quantile calculations.
- `statsmodels`: For robust statistics.
- `matplotlib` and `seaborn`: For data visualization.

## Conclusion

The analysis provided insights into the population distribution across U.S. states and highlighted the importance of using robust statistical techniques to manage outliers and skewed data distributions.

## Future Work

- Extend the analysis to other demographic attributes.
- Apply machine learning models to predict future population trends.
- Explore geospatial visualizations to better understand regional patterns.


