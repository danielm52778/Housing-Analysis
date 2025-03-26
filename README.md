# Housing Market Analysis

Using regression, clustering, and classification to try and accurately predict the median home prices of various neighborhoods.


# Dataset Description
The dataset includes various features related to housing prices. 

- CRIM → per capita crime rate by town.
- ZN → proportion of residential land zoned for lots over 25,000 sq.ft.
- INDUS → proportion of non-retail business acres per town.
- RIVER → Yes if the tract is bordered by the Charles river, No of not.
- NOX → nitric oxides concentration (parts per 10 million).
- RM → average number of rooms per dwelling.
- AGE → proportion of owner-occupied units built prior to 1940.
- DIS → weighted distances to five Boston employment centers.
- RAD → index of accessibility to radial highways.
- TAX → full-value property-tax rate per $10,000.
- PRATIO → pupil-teacher ratio by town.
- LSTAT → % lower status of the population.
- MEDV → Median value of owner-occupied homes in $1000's.

_Note: This dataset uses a modified version of the set published by Harrison, D. and Rubinfeld, D.L. 'Hedonic prices and the demand for clean air', J. Environ. Economics & Management, vol.5, 81-102, 1978._

# Regression 

This section compares Simple Linear Regression and Multiple Linear Regression models using an Ordinary Least Squares test in order to determine which model can most accurately predict the target variable 'MEDV.'

### Simple Linear Regression (SLR)

By plotting the dataset's variables against the target variable 'MEDV.' the variables with stronger correlations can be selected to predict 'MEDV.'

![graphs3x4](https://github.com/user-attachments/assets/9b7f8806-e1a6-40fb-b968-4b07516e020b)

The selected variables are: NOX, RM, DIS, and LSTAT

### Multiple Linear Regression (MLR)

The approach taken was to include every variable in the dataset and then tweak the model from there. From limited testing, the best model was found to include all variables in the model:

<img width="668" alt="Screenshot 2025-03-16 at 12 18 38 AM" src="https://github.com/user-attachments/assets/db7b6eef-56f9-4133-9f9c-41c8f62145a0" />

### Predictions

SLR (Average % Error compared to the actual value.)
- NOX: 30.22%
- RM: 25.77%
- DIS: 33.25%
- LSTAT: 21.25%

MLR
- 16.92% Average Percent Error

### Findings
- LSTAT is the most significant indepentent variable in predicting 'MEDV' and had the lowest percent error in simple regression models. 
- Multiple regression model achieved an R-squared score of 73.4% in price prediction. 

# Clustering

This section displays how K-Means clustering was used to group houses into distinct segments based on their features, and predicts which cluster a hypothetical new house belongs to and compares it with known prices. 

### Setup

- A K-Means clustering of K=3 was applied to group houses based on similarity.
- Using Principle Component Analysis (PCA) to aid visualizations, the clusters can be graphed.

![image](https://github.com/user-attachments/assets/7d0228d0-ff40-40c2-9b0d-fdcfd7a5421e)

### Understanding Cluster Assignments

To better understand which features contribute to each PCA Component, the following chart was generated.

![image](https://github.com/user-attachments/assets/711f8fc5-fb4b-4efe-a1bd-2cfc14de909f)

- PC1 appears to be most influenced by house value features.
- PC2 appears to to be most influenced by geographical features.

### Predictions

A created "New House" can be assigned to a cluster based on its features.
- If the created house falls into Cluster 0, it likely belongs to an expensive neighborhood.
- If it falles into Cluster 2, it likely belongs to a more affordable area.

Using the following features, 

This type of analysis can help group similar properties, create a price range estimate based on similar homes, and identify high-value vs. low-value areas.

# Classification
This method uses Decision Tree and Random Foreset classifiers to identify an accurate method by categorizing house prices into Low, Medium, and High price ranges.

### Accuracy Comparison (Decision Tree vs. Random Forest)
![image](https://github.com/user-attachments/assets/c9a2e211-a144-4f77-ac91-f692f419df45) 

Accuracy Score: 74%

![image](https://github.com/user-attachments/assets/dce0a877-d062-401d-8345-d12453cb06f3)

Accuracy Score: 81%

### Predictions
```
new_house = pd.DataFrame({
    'CRIM': [0.1],
    'ZN': [25.0],
    'INDUS': [5.0],
    'RIVER': [1], 
    'NOX': [0.45],
    'RM': [6.5],
    'AGE': [60.0],
    'DIS': [4.0],
    'RAD': [3],
    'TAX': [300],
    'PRATIO': [15.0],
    'LSTAT': [10.0]
})

# Predict the house price category
predicted_category = rf_clf.predict(new_house)[0]
category_mapping = {0: "Low Price", 1: "Medium Price", 2: "High Price"}

```

_Output: Predicted House Price Category: High Price_

```
new_houses = pd.DataFrame({
    'CRIM': [0.2, 0.05, 1.5],
    'ZN': [30.0, 0.0, 10.0],
    'INDUS': [6.0, 2.0, 15.0],
    'RIVER': [0, 1, 0],
    'NOX': [0.5, 0.3, 0.6],
    'RM': [5.5, 7.0, 4.5],
    'AGE': [70.0, 50.0, 80.0],
    'DIS': [3.5, 6.0, 2.0],
    'RAD': [4, 2, 5],
    'TAX': [350, 250, 400],
    'PRATIO': [18.0, 12.0, 20.0],
    'LSTAT': [15.0, 5.0, 25.0]
})

# Predict house price categories
predicted_categories = rf_clf.predict(new_houses)
predicted_labels = [category_mapping[c] for c in predicted_categories]
```
_Output: Predicted Categories for New Houses: ['Medium Price', 'High Price', 'Low Price']_



