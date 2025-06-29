# Gross Domestic Product Prediction (On Progress)

## Background
The Gross Domestic Product (GDP) is a crucial indicator to measure the total value of overall goods and services produced by a country in a certain period of time, usually in quarter or in a year. GDP is an important benchmark of a country's macroeconomics and a basic basis for formulating economic policies. In addition to endogenous factor such as investment, consumption, and inflation, exogenous factors like conflict and pandemic contribute to decline in the accuracy of GDP forecasting. 

## Goal
The project's aim is: 

1. Data and Model Exploration that can predict the quartiles of U.S. GDP growth in 2025 and above.

## Limitation
In the GDP prediction project, there are many indicators or features that are not included or taken into account because access is restricted by the agency.

## Data Descriptions
This data is open-source and is obtained from the Federal Reserve Economic Data (FRED), an online database created by the financial institution, The Federal Reserve Bank of St. Louis. This data can be in .csv, .xlsx., pdf format, or can be retrieved using the API.

### GDP Data 1947 - 1958
This data has several features that are divided into four group. Several indicators contained in this data:

- Gross Domestic Product (Quarterly GDP) $\rightarrow$ `yoy_gdp`
- Import Goods and Services (Quarterly Import) $\rightarrow$ `yoy_impgs`
- Gross Private Domestic Investment (Quarterly Investment) $\rightarrow$ `yoy_gpdic`
- Personal Consumption Expenditure (Quarterly Consumption) $\rightarrow$ `yoy_pce`
- Export Goods and Services (Quarterly Export) $\rightarrow$ `yoy_expgs`
- Industrial Production: Utilites: Electric and Gas Utilites (Quarterly Index) $\rightarrow$ `yoy_iputil`

### GDP Data 1959 - 1971
The features on this duration are the same as before, but with the addition of:

- Personal Consumption Expenditures: energy goods and services (monthly) $\rightarrow$ `yoy_pceens`

### GDP Data 1972 - 2003
The indicators for this year's interval have additional features in the form of:

- Industrial Production: Manufacturing (Quarterly Index) $\rightarrow$ `yoy_ipman`
- Industrial Production: Manufacturing: Nondurable Goods: Chemical (Quarterly Index) $\rightarrow$ `yoy_chemical_goods`
- Industrial Production: Manufacturing: Nondurable Goods: Food, Beverage, and Tobacco (Quarterly Index) $\rightarrow$ `yoy_food_bev_tob_goods`

### GDP Data 2004 - 2024
Penambahan pada range ini adalah:

- Producer Price Index by Industry: Industrial Gas Manufacturing (Quarterly index) $\rightarrow$ `yoy_ppi_industry`

## Exploratory Data Analysis
The projection of the U.S. GDP from FRED can be seen below.

<p align = 'center'>
<img width = "850" height = "250" src = "figures/gdp growth edited.png">
</p>

Based on the picture, we see several economic events:

1. The Post-War Economic Crisis in 1949: That year was the time towards a peaceful economy after World War 2. The decline in economic activity was caused by a drastic drop in production, which is usually for military purposes. As a result, the government spending plummeted, leading to the unemployment rate skyrocketted and the economic activity significantly dropped.

2. Great Recession 2007-2009: This year's economic crisis is called the subprime mortgage crisis, where banks issue high-risk or high-interest home loans to creditors who have a bad credit history. Consumer demand for homes increased due to low interest rates and easy loan terms in 2001.Many home buyers are applying for adjustable-rate mortgages (a product of subprime mortgages). However, when interest rates started rising in 2005, mortgage payments also increased. Finally, borrowers who default will not be given another loan from the bank, so they are in debt and house prices plummet. The collapse of the subprime mortgage market led to bank failures, a credit freeze, and a global economic downturn.

3. The Pandemic Recession 2020:This crisis is caused by the disease from the COVID-19 virus. Because of this pandemic, the government intervened by imposing a lockdown - limiting community activities - to reduce the spread of this disease. As a result, several shops closed permanently, the unemployment rate increased sharply, and finally the country's GDP dropped. 

<p align = "center">
<img width = "500" height = "350" src = "figures/correlation matrix 1947 1958.png">
</p>

<p align = "center">
<img width = "500" height = "350" src = "figures/correlation matrix 1959 1971.png">
</p>

<p align = "center">
<img width = "500" height = "350" src = "figures/correlation matrix 1972 2003 edited.png">
</p>

<p align = "center">
<img width = "500" height = "350" src = "figures/correlation matrix 2004 2024.png">
</p>


- The image above is a Pearson correlation matrix for each of the features in it with a certain range in the form of a heatmap plot. The `yoy_pce`, *Personal Consumption Expenditures*, gets the highest value in the Pearson correlation calculation for each year range. This means that the increase in public consumption greatly affects state revenue when compared to other factors.

- Another interesting thing is the correlation between `date` and `yoy_gdp` which, in terms of value, is inconsistent. Of the four groups, the lowest value obtained was **-0.72** in the 1972-2003 group. This indicates a decline in GDP from year to year. Moreover, it also inidicates there are many factors, either endogenous (e.g. The FED monetary tightening) or exogenous (e.g. oil crisis, the WTC incident), that leads to economic downfall in that group of year, but cannot be seen only with a single linegraph of GDP growth. 

This project will look at which models can accurately predict GDP, from countries experiencing surplus to economic crisis.

## Method
The prediction models we used in this project is:

- Econometric (AutoRegressive (AR) + Factor Model (FM))
- Machine learning (Linear Regression, Lasso Regression, Elastic Net, XGBoost)

The experiment will be divided into three configurations with six outputs. First, the model is trained using the 1947-1958 data set to predict GDP for the 1959-1971, 1972-2003, and 2004-2024 year groups. Second, the 1959-1971 data set is used by the model to predict the 1972-2003 and 2004-2024 year groups, and the model with the 1972-2003 data set is trained to predict GDP for the 2004-2024 year group. This is done because the data to be predicted has features that are in the data used to train the model. Each proposed model uses this configuration. The results of the prediction will use the ***root mean squared error*** metric to show the accuracy of the prediction.

<p>
<img width = "800" height = "300" src = "figures/exp config.png">
</p>

## Result
Root mean squared error (RMSE) or root mean squared deviation is one of the metrics commonly used to evaluate the results of model predictions, especially in regression tasks. Regression itself is a method used to analyze the relationship between dependent variables and independent variables.

### Linear Regression

Linear regression is a simple regression model that is easy to interpret mathematically. This model can be expressed by the equation

$$\hat{y} = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + ... + \beta_i X_i + \epsilon$$

where $\beta_0$ adalah intercept, $\beta_1, \beta_2$ denotes slope, $X_1, X_2, ... , X_i$ as independent variable. The result of prediction displayed in configuration.

<p align = "center">
<img width = "800" height = "300" src = "figures/linalg/Linear Regression data 1947 to predict 1959.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/linalg/Linear Regression data 1947 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/linalg/Linear Regression data 1947 to predict 2004.png">
</p>


<p align = "center">
<img width = "800" height = "300" src = "figures/linalg/Linear Regression data 1959 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/linalg/Linear Regression data 1959 to predict 2004.png">
</p>


<p align = "center">
<img width = "800" height = "300" src = "figures/linalg/Linear Regression data 1972 to predict 2004.png">
</p>

| \ | Train | Shape | Predict | RMSE|
|:-------:|:----------:|:-------:|:---------:|:--------:|
| 1     | 1947-1958 | 7 | 1958 - 1971| 1.2|
| 2     | 1947-1958 | 7 |1972 - 2003|2.82 |
| 3     | 1947-1958 | 7 |2004 - 2024|2.85 |
| 4     | 1959-1971 | 8 |1972 - 2003| 1.21|
| 5     | 1959-1971 | 8 |2004 - 2024| 1.12|
| 6     | 1972-2003 | 10 |2004 - 2024| 0.86|

- The table above is the result of model prediction using Linear Regression with the set of parameter is `fit_intercept: True`, `normalize: True`, `copy_X: True`, `n_jobs: -1`. The Shape column represent the size of the data based on the number of index and column (index, column). The Predict column means what year group that model try to forecast. Overall, the lowest RMSE score the model can reach is 0.86 by using 1972-2003 data group with 10 columns to predict 2004-2024 GDP. This indicates that the model with 1972-2003 data group can accurately predict 2004-2024 GDP.


### LASSO Regression
LASSO (Least Absolute Shrinkage Selection Operator) Regression, also known as L1 Regression, is one of the regularized regressions that is mathematically almost similar to Linear Regression. However, this model has a regularization $\lambda$ which is used to reduce errors due to overfitting during training. The Residual Sum of Squares (RSS) can be archived by

$$RSS = \min |y - \hat{y}|$$

$$Lasso = RSS + \lambda \sum_{i=1} \beta_i$$

where $\lambda$ denotes regularization parameter that controls the amount of regularizatio applied. The RSS represent the measurement the error between predicted and actual values. This indicator can be any error measurement such as RMSE, MSE, or MAE.The result of Lasso Regression model can be seen below.

<p align = "center">
<img width = "800" height = "300" src = "figures/lassoreg/Lasso Regression data 1947 to predict 1959.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/lassoreg/Lasso Regression data 1947 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/lassoreg/Lasso Regression data 1947 to predict 2004.png">
</p>


<p align = "center">
<img width = "800" height = "300" src = "figures/lassoreg/Lasso Regression data 1959 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/lassoreg/Lasso Regression data 1959 to predict 2004.png">
</p>


<p align = "center">
<img width = "800" height = "300" src = "figures/lassoreg/Lasso Regression data 1972 to predict 2004.png">
</p>

| \ | Train | Feature | Predict | RMSE|
|:-------:|:----------:|:-------:|:---------:|:--------:|
| 1     | 1947-1958 | 7 | 1958 - 1971| 1.2|
| 2     | 1947-1958 | 7 |1972 - 2003|2.76 |
| 3     | 1947-1958 | 7 |2004 - 2024|2.76 |
| 4     | 1959-1971 | 8 |1972-2003| 1.49|
| 5     | 1959-1971 | 8 |2004-2024| 1.1|
| 6     | 1972-2003 | 10 |2004-2024| 0.86|

- Parameter pada model Lasso Regression adalah `alpha = 0.1`, and `random_state = 42`. Similar to the Linear Regression results, the lowest RMSE obtained was 0.86 when the model predict 2004-2024 GDP by using 1972-2003 data group with 10 features.

### eXtreme Gradient Boosting

XGboost (eXtreme) is tree-based and boosting algorithm which utilize gradient descent. It known for its effiency, speed, and ability to handle large dataset. The prediction results using this model can be seen in the images below.

<p align = "center">
<img width = "800" height = "300" src = "figures/xgboost/XGBoost data 1947 to predict 1959.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/xgboost/XGBoost data 1947 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/xgboost/XGBoost data 1947 to predict 2004.png">
</p>

- Based on the three figures above, the 1947-data-group model is not able to predict GDP on 1959-1971 as well as Lasso and Linear Regression, but is able to predict GDP with a range of 1972-2003 and 2004-2024 with a smaller RMSE than the two models.

<p align = "center">
<img width = "800" height = "300" src = "figures/xgboost/XGBoost data 1959 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/xgboost/XGBoost data 1959 to predict 2004.png">
</p>

- The YoY Growth GDP plot for 1972-2003 shows that the model with the 1959-1971 data group can predict with almost the same RMSE as the Lasso and Regular Linear Regression models, but is quite poor in predicting GDP for 2004-2024.

<p align = "center">
<img width = "800" height = "300" src = "figures/xgboost/XGBoost data 1972 to predict 2004.png">
</p>

- The image above shows that the XGBoost model trained with 1972-2003 data has not been able to predict GDP for the 2004-2024 period when compared to Linear and Lasso Regression. This model is not accurate because the number of data used in this project is not abundance.

| \ | Train | Feature | Predict | RMSE|
|:-------:|:----------:|:-------:|:---------:|:--------:|
| 1     | 1947-1958 | 7 | 1958 - 1971| 1.6|
| 2     | 1947-1958 | 7 |1972 - 2003|1.95 |
| 3     | 1947-1958 | 7 |2004 - 2024|1.94 |
| 4     | 1959-1971 | 8 |1972-2003| 1.55|
| 5     | 1959-1971 | 8 |2004-2024| 2.98|
| 6     | 1972-2003 | 10 |2004-2024| 2.16|

- Berdasarkan hasil eksperimen dengan XGBoost dengan parameter `eta = 0.1`,and  `max_depth = 3`, the model performance is not good enough if we compared to the linear regression groups. The lowest RMSE that can be reached is 1.55 when using data group of 1959-1971 to predict 1972-2003.

### Elastic Net
This model was introduced by Zou and Hastie in 2005. If Lasso regression is L1 Regularized regression and Ridge regression is L2 version, then elastic net is a combination of both. L1 is used as feature selector, while L2 for feature shrinkage. The equation of this model

$$Elastic\space Net = RSS + \lambda ((1-\alpha) |\beta|^2 + \alpha |\beta|)$$

where $\alpha |\beta|$ represent L1 penalty and $(1 -\alpha) \beta^2$ as L2 penalty. The experimental result can be seen below.

<p align = "center">
<img width = "800" height = "300" src = "figures/elasticnet/Elastic Net Regression data 1947 to predict 1959.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/elasticnet/Elastic Net Regression data 1947 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/elasticnet/Elastic Net Regression data 1947 to predict 2004.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/elasticnet/Elastic Net Regression data 1959 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/elasticnet/Elastic Net Regression data 1959 to predict 2004.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/elasticnet/Elastic Net Regression data 1972 to predict 2004.png">
</p>

### Econometric (AR + FM)
Autoregressive (AR) model is a machine learning model that uses one or more variables from previous time periods to predict future outcomes. This model is commonly used on time-series data. In an AR model, the output is a future data point expressed as a linear combination of past data points $p$. $p$ is the number of lags entered into the equation. If $p = 1$, and the case study is GDP forecasting, then the mathematical expression is

$$GDP_t = \delta + \psi_1 GDP_{t-1} + \epsilon_t$$

where $\psi_1$ is coefficient, $\delta$ denotes the constant (or intercept in linear regression). If we add one exogenous variable, then the equation will be

$$GDP_t = \delta + \psi_1 GDP_{t-1} + \phi_t Q_t + \epsilon_t $$

whit $\phi_t$ as a coefficient of exogenous variables $Q_t$ at time $t$. 

Factor Model (FFM) is a statistical tool that decomposes variables into common components (factors) and unique or idiosyncratic errors. The formula that represents this definition is

$$X_{it} = \lambda_i F_t + \epsilon_{it}$$

where $X_{it}$ is observed variable for unit $i$ at time $t$, $\lambda$ is factor loading, $F_{t}$ is common factor at time $t$, and $\epsilon_{it}$ is idiosyncratic (unique) error for unit $i$ at time $t$.

<p align = 'center'>
    <img width = '800' height = '300' src = "figures/rmse based on lags.png">
</p>

- From the figure above, nilai *RMSE* atau Root Mean Squared Error dapat meningkat seiring dengan bertambahnya AR lags. Maka dari itu, agar mencapai nilai maksimal dari akurasi, nilai lags yang besar tidak disarankan.

<p align = 'center'>
    <img width = "500" height = "300" src = "figures/rmse based on exog variables.png">
</p>

- Gambar diatas merupakan nilai *RMSE* berdasrkan variabel Exog.

## Conclusion

Berdasarkan project ini, dapat disimpulkan bahwa semakin banyak fitur dan kebaruan data tersebut, maka semakin akurat prediksi yang dihasilkan.

## Reference

- Board of Governors of the Federal Reserve System (US), Industrial Production: Consumer Goods [IPCONGD], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/IPCONGD, March 13, 2025.

- U.S. Bureau of Economic Analysis, Gross Domestic Product [GDP], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/GDP, March 13, 2025.

- Board of Governors of the Federal Reserve System (US), Industrial Production: Utilities: Electric and Gas Utilities (NAICS = 2211,2) [IPUTIL], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/IPUTIL, June 25, 2025.

- U.S. Bureau of Economic Analysis, Imports of Goods and Services [IMPGS], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/IMPGS, June 25, 2025.

- U.S. Bureau of Economic Analysis, Exports of Goods and Services [EXPGS], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/EXPGS, June 25, 2025.

- U.S. Bureau of Economic Analysis, Personal Consumption Expenditures [PCE], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/PCE, June 25, 2025.

- U.S. Bureau of Economic Analysis, Gross Private Domestic Investment [GPDI], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/GPDI, June 25, 2025.

- Board of Governors of the Federal Reserve System (US), Industrial Production: Manufacturing: Nondurable Goods: Food, Beverage, and Tobacco (NAICS = 311,2) [IPG311A2S], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/IPG311A2S, June 25, 2025

- Board of Governors of the Federal Reserve System (US), Industrial Production: Manufacturing: Nondurable Goods: Chemical (NAICS = 325) [IPG325SQ], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/IPG325SQ, June 25, 2025.

- U.S. Bureau of Economic Analysis, Personal consumption expenditures: Energy goods and services [DNRGRC1M027SBEA], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/DNRGRC1M027SBEA, June 25, 2025


## Code