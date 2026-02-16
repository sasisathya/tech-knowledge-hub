# 🤖 Machine Learning

Master core ML algorithms and techniques using scikit-learn.

## 🎯 What is Machine Learning?

Machine Learning is teaching computers to learn from data without being explicitly programmed.

**Types of ML**:
1. **Supervised Learning**: Learn from labeled data (most common)
2. **Unsupervised Learning**: Find patterns in unlabeled data
3. **Reinforcement Learning**: Learn through trial and error

---

## 📚 Supervised Learning

### 1. Linear Regression

**Problem**: Predict continuous values (house prices, temperature, sales)

**Algorithm**:
```python
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score

# Sample data
X = [[1], [2], [3], [4], [5]]
y = [2, 4, 5, 4, 5]

# Split data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Train model
model = LinearRegression()
model.fit(X_train, y_train)

# Predict
predictions = model.predict(X_test)

# Evaluate
mse = mean_squared_error(y_test, predictions)
r2 = r2_score(y_test, predictions)

print(f"MSE: {mse}, R²: {r2}")
```

**When to use**: Predicting continuous values with linear relationships

---

### 2. Logistic Regression

**Problem**: Binary classification (spam/not spam, fraud/not fraud)

**Algorithm**:
```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix

# Binary classification
X = [[1, 2], [2, 3], [3, 1], [6, 5], [7, 8], [8, 7]]
y = [0, 0, 0, 1, 1, 1]  # Binary labels

# Train
model = LogisticRegression()
model.fit(X, y)

# Predict
predictions = model.predict(X_test)

# Evaluate
print(f"Accuracy: {accuracy_score(y_test, predictions)}")
print(classification_report(y_test, predictions))
print(confusion_matrix(y_test, predictions))
```

**When to use**: Binary classification problems

---

### 3. Decision Trees

**Problem**: Classification and regression with interpretable rules

**Algorithm**:
```python
from sklearn.tree import DecisionTreeClassifier
from sklearn import tree
import matplotlib.pyplot as plt

# Train decision tree
model = DecisionTreeClassifier(max_depth=3)
model.fit(X_train, y_train)

# Visualize tree
plt.figure(figsize=(12, 8))
tree.plot_tree(model, filled=True, feature_names=['feature1', 'feature2'])
plt.show()

# Feature importance
importances = model.feature_importances_
```

**Advantages**:
- Easy to interpret
- No feature scaling needed
- Handles non-linear relationships

**Disadvantages**:
- Prone to overfitting
- Unstable (small data changes = different tree)

---

### 4. Random Forests

**Problem**: Improved decision trees using ensemble

**Algorithm**:
```python
from sklearn.ensemble import RandomForestClassifier

# Train random forest (100 trees)
model = RandomForestClassifier(n_estimators=100, max_depth=5, random_state=42)
model.fit(X_train, y_train)

# Predict
predictions = model.predict(X_test)
probabilities = model.predict_proba(X_test)

# Feature importance
feature_importance = pd.DataFrame({
    'feature': feature_names,
    'importance': model.feature_importances_
}).sort_values('importance', ascending=False)
```

**When to use**:
- Default choice for many problems
- Handles large datasets
- Reduces overfitting compared to single tree

---

### 5. Support Vector Machines (SVM)

**Problem**: Classification with optimal decision boundary

**Algorithm**:
```python
from sklearn.svm import SVC
from sklearn.preprocessing import StandardScaler

# Scale features (important for SVM!)
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Train SVM
model = SVC(kernel='rbf', C=1.0, gamma='auto')
model.fit(X_train_scaled, y_train)

# Predict
predictions = model.predict(X_test_scaled)
```

**Kernels**:
- `linear`: Linear decision boundary
- `rbf`: Non-linear (Radial Basis Function) - most common
- `poly`: Polynomial

**When to use**: Small to medium datasets with clear margin separation

---

### 6. Naive Bayes

**Problem**: Fast probabilistic classification

**Algorithm**:
```python
from sklearn.naive_bayes import GaussianNB

# Train
model = GaussianNB()
model.fit(X_train, y_train)

# Predict with probabilities
predictions = model.predict(X_test)
probabilities = model.predict_proba(X_test)
```

**When to use**:
- Text classification (spam detection)
- Fast baseline model
- Small datasets

---

## 📊 Unsupervised Learning

### 1. K-Means Clustering

**Problem**: Group similar data points

**Algorithm**:
```python
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

# Find optimal number of clusters (Elbow method)
inertias = []
for k in range(1, 11):
    kmeans = KMeans(n_clusters=k, random_state=42)
    kmeans.fit(X)
    inertias.append(kmeans.inertia_)

plt.plot(range(1, 11), inertias)
plt.xlabel('Number of clusters')
plt.ylabel('Inertia')
plt.show()

# Train with optimal k
model = KMeans(n_clusters=3, random_state=42)
clusters = model.fit_predict(X)

# Cluster centers
centers = model.cluster_centers_
```

**Use cases**:
- Customer segmentation
- Image compression
- Anomaly detection

---

### 2. Principal Component Analysis (PCA)

**Problem**: Reduce dimensions while keeping variance

**Algorithm**:
```python
from sklearn.decomposition import PCA
import matplotlib.pyplot as plt

# Reduce to 2 components
pca = PCA(n_components=2)
X_reduced = pca.fit_transform(X)

# Explained variance
print(f"Explained variance: {pca.explained_variance_ratio_}")

# Visualize
plt.scatter(X_reduced[:, 0], X_reduced[:, 1])
plt.xlabel('First Principal Component')
plt.ylabel('Second Principal Component')
plt.show()
```

**When to use**:
- High-dimensional data visualization
- Feature reduction
- Noise reduction

---

## 🛠️ Essential Techniques

### 1. Train-Test Split

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y,
    test_size=0.2,      # 20% for testing
    random_state=42,    # Reproducible
    stratify=y          # Keep class proportions
)
```

---

### 2. Cross-Validation

```python
from sklearn.model_selection import cross_val_score

# 5-fold cross-validation
scores = cross_val_score(model, X, y, cv=5, scoring='accuracy')
print(f"Accuracy: {scores.mean():.2f} (+/- {scores.std():.2f})")
```

---

### 3. Feature Scaling

```python
from sklearn.preprocessing import StandardScaler, MinMaxScaler

# Standardization (mean=0, std=1)
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X_train)

# Normalization (0 to 1)
scaler = MinMaxScaler()
X_normalized = scaler.fit_transform(X_train)
```

**When to scale**:
- ✅ SVM, KNN, Neural Networks, Logistic Regression
- ❌ Decision Trees, Random Forests

---

### 4. Handling Missing Data

```python
import pandas as pd
from sklearn.impute import SimpleImputer

# Remove rows with missing values
df_clean = df.dropna()

# Fill with mean
imputer = SimpleImputer(strategy='mean')
X_imputed = imputer.fit_transform(X)

# Fill with median (better for outliers)
imputer = SimpleImputer(strategy='median')

# Fill with most frequent
imputer = SimpleImputer(strategy='most_frequent')
```

---

### 5. Encoding Categorical Variables

```python
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
import pandas as pd

# Label Encoding (for ordinal data)
le = LabelEncoder()
df['size_encoded'] = le.fit_transform(df['size'])  # Small, Medium, Large → 0, 1, 2

# One-Hot Encoding (for nominal data)
df_encoded = pd.get_dummies(df, columns=['color'])  # Red, Blue, Green → 3 binary columns
```

---

### 6. Hyperparameter Tuning

```python
from sklearn.model_selection import GridSearchCV

# Define parameter grid
param_grid = {
    'n_estimators': [50, 100, 200],
    'max_depth': [3, 5, 10],
    'min_samples_split': [2, 5, 10]
}

# Grid search with cross-validation
grid_search = GridSearchCV(
    RandomForestClassifier(),
    param_grid,
    cv=5,
    scoring='accuracy'
)

grid_search.fit(X_train, y_train)

# Best parameters
print(f"Best params: {grid_search.best_params_}")
print(f"Best score: {grid_search.best_score_}")

# Use best model
best_model = grid_search.best_estimator_
```

---

## 📈 Model Evaluation

### Classification Metrics

```python
from sklearn.metrics import (
    accuracy_score,
    precision_score,
    recall_score,
    f1_score,
    roc_auc_score,
    confusion_matrix,
    classification_report
)

# All metrics
accuracy = accuracy_score(y_test, predictions)
precision = precision_score(y_test, predictions)
recall = recall_score(y_test, predictions)
f1 = f1_score(y_test, predictions)

# Detailed report
print(classification_report(y_test, predictions))

# Confusion matrix
cm = confusion_matrix(y_test, predictions)
sns.heatmap(cm, annot=True, fmt='d')
```

**Choosing the right metric**:
- **Accuracy**: Overall correctness (use when classes are balanced)
- **Precision**: Of predicted positives, how many are correct (minimize false positives)
- **Recall**: Of actual positives, how many did we catch (minimize false negatives)
- **F1-Score**: Harmonic mean of precision and recall (balanced metric)

### Regression Metrics

```python
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score

mse = mean_squared_error(y_test, predictions)
rmse = mean_squared_error(y_test, predictions, squared=False)
mae = mean_absolute_error(y_test, predictions)
r2 = r2_score(y_test, predictions)
```

---

## 🏋️ Practice Projects

### Project 1: Titanic Survival Prediction
- **Dataset**: Kaggle Titanic
- **Goal**: Predict survival
- **Skills**: Data cleaning, feature engineering, classification
- **Models**: Logistic Regression, Random Forest

### Project 2: House Price Prediction
- **Dataset**: Boston Housing or Kaggle House Prices
- **Goal**: Predict house prices
- **Skills**: Regression, feature scaling, hyperparameter tuning
- **Models**: Linear Regression, Random Forest Regressor

### Project 3: Customer Segmentation
- **Dataset**: Customer data
- **Goal**: Group customers
- **Skills**: Clustering, PCA, visualization
- **Models**: K-Means, Hierarchical Clustering

### Project 4: Spam Email Detection
- **Dataset**: SMS Spam Collection
- **Goal**: Classify spam vs ham
- **Skills**: Text processing, TF-IDF, classification
- **Models**: Naive Bayes, Logistic Regression

---

## 📚 Complete ML Pipeline Example

```python
import pandas as pd
from sklearn.model_selection import train_test_split, GridSearchCV
from sklearn.preprocessing import StandardScaler
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report, accuracy_score

# 1. Load data
df = pd.read_csv('data.csv')

# 2. Exploratory Data Analysis
print(df.head())
print(df.info())
print(df.describe())

# 3. Handle missing values
df = df.dropna()

# 4. Feature engineering
df['new_feature'] = df['feature1'] / df['feature2']

# 5. Encode categorical variables
df = pd.get_dummies(df, columns=['category'])

# 6. Split features and target
X = df.drop('target', axis=1)
y = df['target']

# 7. Train-test split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# 8. Feature scaling
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# 9. Hyperparameter tuning
param_grid = {'n_estimators': [50, 100], 'max_depth': [5, 10]}
grid = GridSearchCV(RandomForestClassifier(), param_grid, cv=5)
grid.fit(X_train_scaled, y_train)

# 10. Train best model
best_model = grid.best_estimator_

# 11. Evaluate
predictions = best_model.predict(X_test_scaled)
print(f"Accuracy: {accuracy_score(y_test, predictions)}")
print(classification_report(y_test, predictions))

# 12. Save model
import joblib
joblib.dump(best_model, 'model.pkl')
joblib.dump(scaler, 'scaler.pkl')
```

---

## ✅ Completion Checklist

- [ ] Understand supervised vs unsupervised learning
- [ ] Implemented Linear/Logistic Regression
- [ ] Trained Decision Trees and Random Forests
- [ ] Used K-Means clustering
- [ ] Applied PCA for dimensionality reduction
- [ ] Performed cross-validation
- [ ] Tuned hyperparameters with GridSearchCV
- [ ] Handled missing data and categorical variables
- [ ] Evaluated models with appropriate metrics
- [ ] Built 3+ end-to-end ML projects
- [ ] Participated in at least 1 Kaggle competition

---

## 🔗 Resources

- **Andrew Ng's ML Course** (Coursera) - THE foundational course
- **Hands-On ML with Scikit-Learn** by Aurélien Géron
- **Scikit-Learn Documentation** - Excellent tutorials
- **Kaggle Learn** - Micro-courses
- **Kaggle Competitions** - Practice with real problems

---

## 🎯 Time Estimate

**Total**: 8-10 weeks with 10-15 hours/week

---

[⬅️ Back to AI/ML](../)
