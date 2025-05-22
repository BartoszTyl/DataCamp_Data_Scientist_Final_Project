# Data Scientist Practical Exam Submission

## 📌 Problem Statement

The objective is to build a model that predicts whether a recipe featured on a homepage will result in **high traffic** based on its nutritional content, category, and servings. This is a **binary classification** task, and models will be evaluated using **accuracy**, **precision**, and **business relevance**.

## 📂 Dataset Overview

- **File**: `recipe_site_traffic_2212.csv`
- **Original Rows**: 947  
- **Final Cleaned Rows**: 895  
- **Target Variable**: `high_traffic` (High → `True`, Low → `False`)

## ✅ Data Validation

**Steps applied:**

- `recipe`: Unique integer ID, validated (no issues).
- `calories`, `carbohydrate`, `sugar`, `protein`: 52 rows had missing values, all dropped. Correct types (float).
- `category`: 11 unique values — merged `Chicken Breast` with `Chicken`, converted to categorical (10 values total).
- `servings`: Cleaned to keep only numeric values, converted to integers.
- `high_traffic`: Missing values filled with `"Low"`, then mapped to `True/False` and cast to boolean.

## 📊 Exploratory Data Analysis

### Univariate Visualisations

**1. Proportion of High vs Low Traffic Recipes:**

- Majority of recipes resulted in **high traffic**.

```python
sns.countplot(data=df, x='high_traffic')
```

**2. Most Common Recipe Categories:**

- `Chicken`, `Breakfast`, and `Beverages` were most frequently featured.

```python
sns.countplot(data=df, x='category', order=df['category'].value_counts().index)
```

### Multivariate Visualisation

**Proportion of High Traffic by Category:**

- Categories like `Vegetable`, `Potato`, and `Pork` had higher conversion to high traffic, despite being featured less.

```python
sns.countplot(data=df, x='category', hue='high_traffic', order=sorted_categories[::-1])
```

## 🤖 Model Development

### Problem Type

- **Binary Classification**

### Models Used

- **Baseline**: Logistic Regression  
- **Comparison**: Decision Tree Classifier

### Preprocessing

- Dropped `recipe` ID column
- One-hot encoded `category`
- Split: 70% train / 30% test, stratified by target

## 📈 Model Evaluation

### Logistic Regression

- **Precision**: 0.816  
- **Accuracy**: 0.773  

```plaintext
Confusion Matrix:
[[ 79  29]
 [ 32 129]]
```

### Decision Tree Classifier

- **Precision**: 0.764  
- **Accuracy**: 0.691  

```plaintext
Confusion Matrix:
[[ 73  35]
 [ 48 113]]
```

**Conclusion**: Logistic Regression performed better across all metrics and is the recommended model.

## 📊 Business Metrics

- A "high traffic" recipe likely boosts engagement and ad revenue.
- The Logistic Regression model correctly identifies >80% of high traffic recipes.
- Business can use model predictions to **prioritise homepage content** and **improve traffic outcomes**.

## ✅ Final Recommendations

- **Adopt Logistic Regression** to score upcoming recipes for homepage prioritisation.
- **Reassess recipe category emphasis** — less frequent categories (Vegetable, Pork, Potato) are more predictive of success.
- **Continue data collection** to improve model generalisation and retrain periodically.
