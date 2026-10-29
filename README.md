
# House Price Prediction with Linear Regression

## Overview

This project explores housing prices using exploratory data analysis and multiple linear regression. It examines relationships between house prices and property characteristics, encodes categorical variables, selects predictors, and evaluates a regression model.

## Dataset

- **File:** `Housing.csv`
- **Source:** The notebook loads a local file named `Housing.csv`
- **Size:** 545 rows and 13 columns
- **Target:** `price`

### Variables

| Variable | Description |
|---|---|
| `price` | House price; prediction target |
| `area` | Area of the property |
| `bedrooms` | Number of bedrooms |
| `bathrooms` | Number of bathrooms |
| `stories` | Number of stories |
| `mainroad` | Whether the property is connected to a main road |
| `guestroom` | Whether the property has a guest room |
| `basement` | Whether the property has a basement |
| `hotwaterheating` | Whether the property has hot-water heating |
| `airconditioning` | Whether the property has air conditioning |
| `parking` | Number of parking spaces |
| `prefarea` | Whether the property is in a preferred area |
| `furnishingstatus` | Furnishing status: furnished, semi-furnished, or unfurnished |

The notebook does not specify the measurement unit for `area` or the currency for `price`.

## Workflow

### 1. Data inspection

- Inspected the dataset's dimensions, columns, data types, and descriptive statistics.
- Checked for missing values and duplicate rows.
- Found no missing values and no duplicate rows in the original dataset.

### 2. Exploratory data analysis

- Examined the distribution and spread of house prices using a histogram and boxplot.
- Visualized categorical variables with bar charts.
- Compared house prices across categorical groups using boxplots.
- Explored numerical variables against price using scatter plots.
- Used a pair plot and correlation heatmap to examine relationships among numerical variables.

### 3. Preprocessing

- Converted categorical variables into dummy variables using `pandas.get_dummies()` with `drop_first=True`.
- Split the data into training and test sets using a 75/25 split and `random_state=100`.
- Applied `MinMaxScaler` to numerical columns.

### 4. Feature selection and regression

- Applied Recursive Feature Elimination (RFE) with `LinearRegression`, selecting 10 features.
- Fitted Ordinary Least Squares (OLS) models using Statsmodels.
- Removed `bedrooms` after examining its p-value.
- Calculated Variance Inflation Factor (VIF) values to examine multicollinearity.
- Removed a column named `yes` following the high VIF values.

The final model uses four predictors:

- `area`
- `bathrooms`
- `stories`
- `parking`

### 5. Diagnostics and evaluation

- Examined a histogram of the training residuals.
- Generated predictions for the test set.
- Calculated the test-set R² score.
- Plotted actual test values against predicted values.

## Reported results

| Metric | Value |
|---|---:|
| Training R² | 0.549 |
| Adjusted training R² | 0.544 |
| Test R² | 0.4613 |

The training statistics come from the final OLS model. The test R² is the value produced by the notebook's evaluation code.

**Evaluation limitation:** The notebook fits `MinMaxScaler` separately on the training and test sets. It also scales `price` independently in each set, because `price` is included in the numerical columns. Therefore, the test R² is calculated using differently scaled target values and predictions. It should not be interpreted as a reliable measure of performance on unseen house prices in their original scale.

The notebook's final evaluation cell for MSE, RMSE, and MAE also references variables inconsistently. Those metrics are therefore not reported here.

## Libraries

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Statsmodels
