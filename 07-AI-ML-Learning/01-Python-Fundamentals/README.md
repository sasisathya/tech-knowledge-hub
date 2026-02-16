# 🐍 Python Fundamentals for Machine Learning

Master Python libraries essential for ML and data science.

## 📚 What You'll Learn

### Core Libraries:
- **NumPy**: Numerical computing, arrays, linear algebra
- **Pandas**: Data manipulation, DataFrames, analysis
- **Matplotlib**: Data visualization, plotting
- **Seaborn**: Statistical visualizations
- **Jupyter**: Interactive notebooks for experimentation

---

## 🎯 Learning Path

### Week 1: NumPy Mastery

**Topics**:
- NumPy arrays vs Python lists
- Array operations and broadcasting
- Indexing and slicing
- Mathematical operations
- Linear algebra with NumPy

**Practice**:
```python
import numpy as np

# Create arrays
arr = np.array([1, 2, 3, 4, 5])
matrix = np.array([[1, 2], [3, 4]])

# Operations
mean = np.mean(arr)
std = np.std(arr)

# Linear algebra
dot_product = np.dot(matrix, matrix.T)
eigenvalues = np.linalg.eig(matrix)
```

**Resources**:
- [NumPy Official Tutorial](https://numpy.org/doc/stable/user/quickstart.html)
- [100 NumPy Exercises](https://github.com/rougier/numpy-100)

---

### Week 2: Pandas for Data Analysis

**Topics**:
- DataFrames and Series
- Reading data (CSV, Excel, JSON)
- Data cleaning and preprocessing
- Groupby and aggregations
- Merging and joining datasets

**Practice**:
```python
import pandas as pd

# Load data
df = pd.read_csv('data.csv')

# Explore
df.head()
df.info()
df.describe()

# Clean
df.dropna()  # Remove missing values
df.fillna(0)  # Fill missing values

# Analyze
grouped = df.groupby('category').mean()
```

**Resources**:
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [10 Minutes to Pandas](https://pandas.pydata.org/docs/user_guide/10min.html)
- [Kaggle: Pandas Course](https://www.kaggle.com/learn/pandas)

---

### Week 3-4: Visualization

**Matplotlib Basics**:
```python
import matplotlib.pyplot as plt

# Line plot
plt.plot([1, 2, 3, 4], [1, 4, 2, 3])
plt.xlabel('X axis')
plt.ylabel('Y axis')
plt.title('My Plot')
plt.show()

# Histogram
plt.hist(data, bins=50)
plt.show()
```

**Seaborn for Statistics**:
```python
import seaborn as sns

# Correlation heatmap
sns.heatmap(df.corr(), annot=True)

# Distribution plot
sns.distplot(df['column'])

# Scatter plot with regression
sns.lmplot(x='feature1', y='target', data=df)
```

**Resources**:
- [Matplotlib Gallery](https://matplotlib.org/stable/gallery/index.html)
- [Seaborn Tutorial](https://seaborn.pydata.org/tutorial.html)

---

## 🏋️ Practice Exercises

### Exercise 1: Array Operations
Create a NumPy array of 1000 random numbers and:
1. Calculate mean, median, std deviation
2. Find values above 2 standard deviations
3. Reshape into 10x100 matrix
4. Perform matrix multiplication

### Exercise 2: Data Analysis
Download Titanic dataset and:
1. Load into Pandas DataFrame
2. Handle missing values
3. Calculate survival rate by class
4. Create age distribution histogram
5. Find correlation between features

### Exercise 3: Visualization
Using any dataset:
1. Create line plot showing trends
2. Bar chart for categorical data
3. Heatmap for correlations
4. Box plot for distributions
5. Combine multiple plots in subplots

---

## 📊 Mini Projects

### Project 1: Stock Price Analysis
- Download historical stock data
- Calculate moving averages
- Visualize price trends
- Identify patterns

### Project 2: COVID-19 Data Dashboard
- Load COVID-19 dataset
- Clean and preprocess data
- Create visualizations (cases, deaths, recovery)
- Compare countries/regions

### Project 3: Sales Analytics
- Analyze sales dataset
- Find top products and categories
- Time series analysis
- Create executive dashboard

---

## 🔗 Essential Resources

### Documentation:
- [NumPy Docs](https://numpy.org/doc/)
- [Pandas Docs](https://pandas.pydata.org/docs/)
- [Matplotlib Docs](https://matplotlib.org/)

### Books:
- **Python for Data Analysis** by Wes McKinney (Pandas creator)
- **Python Data Science Handbook** by Jake VanderPlas

### Online Courses:
- [Kaggle: Python](https://www.kaggle.com/learn/python)
- [Kaggle: Pandas](https://www.kaggle.com/learn/pandas)
- [DataCamp: Python for Data Science](https://www.datacamp.com/courses/intro-to-python-for-data-science)

### Practice Datasets:
- [Kaggle Datasets](https://www.kaggle.com/datasets)
- [UCI ML Repository](https://archive.ics.uci.edu/ml/index.php)
- [Google Dataset Search](https://datasetsearch.research.google.com/)

---

## ✅ Completion Checklist

Before moving to Math for ML, ensure you can:
- [ ] Create and manipulate NumPy arrays
- [ ] Perform vectorized operations
- [ ] Load and clean data with Pandas
- [ ] Group and aggregate data
- [ ] Create meaningful visualizations
- [ ] Handle missing data
- [ ] Merge and join datasets
- [ ] Export analysis results

---

## 🎯 Time Estimate

- **NumPy**: 1 week (10-12 hours)
- **Pandas**: 1 week (10-12 hours)
- **Visualization**: 1 week (8-10 hours)
- **Projects**: 1 week (10-15 hours)

**Total**: 4 weeks with 10-12 hours/week commitment

---

[⬅️ Back to AI/ML](../)
