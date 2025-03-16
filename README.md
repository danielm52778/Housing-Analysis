# Housing Market Analysis

Using regression, clustering, and classification to try and accurately predict the median home prices of various neighborhoods.

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

- A K-Means clustering of K=3 was applied to group houses based on similarity.
- After clustering, the relationship between clusters and 'MEDV' was analyzed and can be visualized as follows:

![image](https://github.com/user-attachments/assets/7d0228d0-ff40-40c2-9b0d-fdcfd7a5421e)



