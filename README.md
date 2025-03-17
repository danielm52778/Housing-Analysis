# Housing Market Analysis

Using regression, clustering, and classification to try and accurately predict the median home prices of various neighborhoods.


# Dataset Description
The dataset includes various features related to housing prices. 

- CRIM → per capita crime rate by town
- ZN → proportion of residential land zoned for lots over 25,000 sq.ft.
- INDUS → proportion of non-retail business acres per town
- RIVER → Yes if the tract is bordered by the Charles river, No of not.
- NOX → nitric oxides concentration (parts per 10 million)
- RM → average number of rooms per dwelling
- AGE → proportion of owner-occupied units built prior to 1940
- DIS → weighted distances to five Boston employment centers
- RAD → index of accessibility to radial highways
- TAX → full-value property-tax rate per $10,000
- PRATIO → pupil-teacher ratio by town
- LSTAT → % lower status of the population
- MEDV → Median value of owner-occupied homes in $1000's

_Note: This dataset uses a modified version of the set published by Harrison, D. and Rubinfeld, D.L. 'Hedonic prices and the demand for clean
air', J. Environ. Economics & Management, vol.5, 81-102, 1978._

# Regression 

_Data was analyzed using Numpy and visualized using Matplotlib and OLS Regression Results were generated using Statsmodels_

### Singular Regression Models


By plotting the dataset's variables against the target variable 'MEDV.' the variables with stronger correlations can be selected to predict 'MEDV.'

![graphs3x4](https://github.com/user-attachments/assets/9b7f8806-e1a6-40fb-b968-4b07516e020b)

Using the single predictor equation, for the first 5 rows, yields varying prediction results. This indicates a multiple regression model may be a better fit for the data 

<img width="821" alt="Screenshot 2025-03-15 at 11 42 36 PM" src="https://github.com/user-attachments/assets/afeaf80e-512a-4df2-ab14-7cd10c736996" />


### Multiple Regression Models

The approach taken was to include every variable in the dataset and then tweak the model from there. 

<img width="668" alt="Screenshot 2025-03-16 at 12 18 38 AM" src="https://github.com/user-attachments/assets/db7b6eef-56f9-4133-9f9c-41c8f62145a0" />

Ultimately, this model resulted in being the best fit with an R-squared of 0.734 and and Adj. R-squared of 0.728.

Prediction results (over entire dataset) using the multiple regression model are as follows:

Average % Error: 16.9211%

Min % Error: 0.0016%

Max % Error: 144.7910%

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

Here is the prediction for the following New House:

```
new_house = pd.DataFrame({
    'CRIM': [0.1], 'ZN': [25.0], 'INDUS': [5.0], 'RIVER': [1],  
    'NOX': [0.45], 'RM': [6.5], 'AGE': [60.0], 'DIS': [4.0], 
    'RAD': [3], 'TAX': [300], 'PRATIO': [15.0], 'LSTAT': [10.0]
})
```
```
House Price Analysis per Cluster:
          count       mean       std   min     25%    50%    75%   max
Cluster                                                              
0         90.0  29.191111  7.765418  17.1  23.425  27.95  33.10  50.0
1        169.0  16.356213  7.708690   5.0  12.000  15.00  19.50  50.0
2        247.0  24.332794  8.097120  11.9  19.500  22.20  25.85  50.0

The new house belongs to Cluster 2

Existing houses in this cluster have the following price range:

count    247.000000
mean      24.332794
std        8.097120
min       11.900000
25%       19.500000
50%       22.200000
75%       25.850000
max       50.000000
```

This type of analysis can help group similar properties, create a price range estimate based on similar homes, and identify high-value vs. low-value areas.

# Classification
This method uses Decision Tree and Random Foreset classifiers to identify an accurate method by categorizing house prices into Low, Medium, and High price ranges.
