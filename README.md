# Concrete Compressive Strength Prediction

This notebook explores various regression models to predict the compressive strength of concrete based on its composition and age.

## **Created By**

- Esteban Arroyave
- Juan Sebastian Plazas
- Juan Guillermo Gómez

## **Dataset**

The dataset used in this notebook is the Concrete Compressive Strength dataset from the UCI Machine Learning Repository (id=165). It contains information about the proportions of different ingredients used in a concrete mix, the age of the concrete, and its resulting compressive strength.

**Explanation of each column:**

1.  **Cement (component 1) (kg in a m^3 mixture):** Amount of Portland cement.
2.  **Blast Furnace Slag (component 2) (kg in a m^3 mixture):** Amount of blast furnace slag.
3.  **Fly Ash (component 3) (kg in a m^3 mixture):** Amount of fly ash.
4.  **Water (component 4) (kg in a m^3 mixture):** Amount of water.
5.  **Superplasticizer (component 5) (kg in a m^3 mixture):** Amount of superplasticizer.
6.  **Coarse Aggregate (component 6) (kg in a m^3 mixture):** Amount of coarse aggregate.
7.  **Fine Aggregate (component 7) (kg in a m^3 mixture):** Amount of fine aggregate.
8.  **Age (day):** Age of the concrete when tested.
9.  **Concrete compressive strength (MPa, megapascals):** The target variable.

## **Objective**

The objective is to find the model that best predicts the average compressive strength of concrete.

## **Methodology**

1.  **Data Loading and Understanding:**
    *   Load the dataset and examine its structure and initial rows.
    *   Understand the meaning of each feature.
2.  **Exploratory Data Analysis (EDA):**
    *   Change column names for better readability.
    *   Check data types and identify numerical and categorical columns.
    *   Check for and handle duplicate records.
    *   Perform univariate analysis using histograms and box plots to understand the distribution of each variable and identify outliers.
    *   Analyze the distribution of variables with a high concentration of zero values.
    *   Perform multivariate analysis using pair plots to explore relationships between variables, including the target variable and categorical indicators for the presence of Blast Furnace Slag and Superplasticizer.
    *   Address outliers by clipping values to the IQR bounds.
    *   Apply logarithmic transformation to skewed variables with a high presence of zeros and large ranges.
3.  **Feature Engineering:**
    *   Select relevant features based on correlation analysis and statistical tests. Fly Ash was discarded due to weak correlation with the target variable and no significant difference in compressive strength when present. Log-transformed Superplasticizer and the original Age feature were also discarded based on correlation and distribution analysis.
    *   Check for zero variance features (none found).
4.  **Data Splitting:**
    *   Split the data into training and test sets (70% train, 30% test).
    *   Verify the distribution of the target variable is similar in both sets using a KDE plot and Mann-Whitney U test.
5.  **Data Standardization:**
    *   Standardize the features using `StandardScaler`.
6.  **Model Training and Evaluation:**
    *   Train and evaluate the following regression models:
        *   Linear Regression
        *   Ridge Regression (with GridSearchCV for alpha tuning)
        *   Lasso Regression (with GridSearchCV for alpha tuning)
        *   Polynomial Regression (degree 2)
        *   Support Vector Regression (SVR) (with RBF kernel and manual C tuning)
        *   Decision Tree Regression (with manual hyperparameter tuning)
        *   K-Nearest Neighbors (KNN) (with manual K tuning and MinMaxScaler)
    *   Evaluate each model using R², RMSE, MAE, and MAPE metrics on both the training and test sets.
    *   Visualize actual vs. predicted values for training and test sets to assess model fit and generalization.
7.  **Model Comparison:**
    *   Compare the performance of all models based on the evaluation metrics, particularly on the test set.
    *   Visualize the R² scores and other metrics for all models.
8.  **Conclusion:**
    *   Identify the best-performing model based on the evaluation metrics.
    *   Summarize the findings from the EDA and modeling stages.
9.  **Model Saving:**
    *   Save the best-performing model (SVR) and the scaler object using `pickle`.

## **Results**

The Support Vector Regression (SVR) model with an RBF kernel and C=10 demonstrated the best performance on the test set, achieving the highest R² (0.859) and lowest RMSE (6.31 MPa). This model provides the most accurate and reliable predictions for concrete compressive strength in this analysis.
