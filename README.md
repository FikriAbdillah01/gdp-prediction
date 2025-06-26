# Gross Domestic Product Prediction

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
<img width = "500" height = "350" src = "figures/correlation matrix 1972 2003.png">
</p>

<p align = "center">
<img width = "500" height = "350" src = "figures/correlation matrix 2004 2024.png">
</p>


- The image above is a Pearson correlation matrix for each of the features in it with a certain range in the form of a heatmap plot. The `yoy_pce`, *Personal Consumption Expenditures*, gets the highest value in the Pearson correlation calculation for each year range. This means that the increase in public consumption greatly affects state revenue when compared to other factors.

- Another interesting thing is the correlation between `date` and `yoy_gdp` which, in terms of value, is inconsistent. Of the four groups, the lowest value obtained was **-0.72** in the 1972-2003 group. This indicates a decline in GDP from year to year. Moreover, there are so many factors, either endogenous (e.g. The FED monetary tightening) or exogenous (e.g. oil crisis, the WTC incident), that leads to economic downfall, but cannot be seen only with a single linegraph of GDP growth. 

This project will look at which models can accurately predict GDP, from countries experiencing surplus to economic crisis.

## Method
The prediction models we used in this project is:

- Econometric (AutoRegressive (AR) + Factor Model (FM))
- Machine learning (Linear Regression, Decision Tree, Random Forest, XGBoost)

The experiment will be divided into three configurations with six outputs. First, the model is trained using the 1947-1958 data set to predict GDP for the 1959-1971, 1972-2003, and 2004-2024 year groups. Second, the 1959-1971 data set is used by the model to predict the 1972-2003 and 2004-2024 year groups, and the model with the 1972-2003 data set is trained to predict GDP for the 2004-2024 year group. This is done because the data to be predicted has features that are in the data used to train the model. Each proposed model uses this configuration. The results of the prediction will use the ***root mean squared error*** metric to show the accuracy of the prediction.

<p>
<img width = "800" height = "300" src = "figures/exp config.png">
</p>

## Result
Root mean squared error (RMSE) atau root mean squared deviation merupakan salah satu metrik yang biasanya digunakan untuk evaluasi hasil dari prediksi model, khusunya dalam tugas regressi. Regressi sendiri merupakan metode yang digunakan untuk menganallisa hubungan antara variabel dependen dan variabel independen. 

### Linear Regression

Regressi liner merupakan model regressi yang sederhana dan mudah diintepretasikan secara matematis. Model ini dapat diekspressikan dengan persamaan 

$$\hat{y} = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + ... + \beta_i X_i + \epsilon$$

dimana $\beta_0$ adalah intercept, $\beta_1, \beta_2$ denotes slope, $X_1, X_2, ... , X_i$ as independent variable. The result of prediction ditampilkan berdasarkan urutan konfigurasi.

<p align = "center">
<img width = "800" height = "300" src = "figures/linalg/Linear Regression data 1947 to predict 1959.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/linalg/Linear Regression data 1947 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/linalg/Linear Regression data 1947 to predict 2004.png">
</p>

- The four images above are the results of predictions using data from 1947-1958 which have 6 indicators with a linear regression model. The model with this data can predict accurately if seen from the small RMSE value. However, of the three economic crises discussed, the linear regression with data in 1947 still does not accurately predict them.

<p align = "center">
<img width = "800" height = "300" src = "figures/linalg/Linear Regression data 1959 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/linalg/Linear Regression data 1959 to predict 2004.png">
</p>

- From the two figures above, linear regression with 1959 data predicts more accurately when compared to 1948 in terms of GDP prediction. Moreover, this model can predict the 2020 economic crisis with a smaller RMSE value. 

<p align = "center">
<img width = "800" height = "300" src = "figures/linalg/Linear Regression data 1972 to predict 2004.png">
</p>

- The image above is the result of model prediction with data from 1972 to 2003 which has 10 features. The RMSE of linear regression with this data is smaller when compared to previous data.

### LASSO Regression
LASSO (Least Absolute Shrinkage Selection Operator) Regression, also known as L1 Regression, is one of the regularized regressions that is mathematically almost similar to Linear Regression. However, this model has a regularization $\lambda$ which is used to reduce errors due to overfitting during training. The Residual Sum of Squares (RSS) can be archived by

$$RSS = \min |y - \hat{y}|$$

$$RSS + \lambda \sum_{i=1} \beta_i$$

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

- Based on the three images above, the lasso regression model with 1947 data that has 5 features is able to predict data from 1959 to 1971 with an RMSE of 1.5 smaller than data from 1972 and above. 

<p align = "center">
<img width = "800" height = "300" src = "figures/lassoreg/Lasso Regression data 1959 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/lassoreg/Lasso Regression data 1959 to predict 2004.png">
</p>

- The two images above show a model with 1959 data that has 6 features that can predict GDP growth in 1972 and above with a smaller RMSE when compared to lasso regression with 1948 data and the Linear Regression model with the same data year.

<p align = "center">
<img width = "800" height = "300" src = "figures/lassoreg/Lasso Regression data 1972 to predict 2004.png">
</p>

- The figure above illustrates lasso regression model by using data in 1972 that contains around 10 features can predict yearly US GDP growth with RMSE score below 1.

### eXtreme Gradient Boosting

XGboost (eXtreme) merupakan model tree-based, boosting algorithm which utilize gradient descent. It known for its effiency, speed, and ability to handle large dataset. The prediction results using this model can be seen in the images below.

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
From this project, we can conclude that:

- The ... model outperform all machine learning model. The model can accurately predict GDP 

## Reference

- Board of Governors of the Federal Reserve System (US), Industrial Production: Consumer Goods [IPCONGD], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/IPCONGD, March 13, 2025.

- U.S. Bureau of Economic Analysis, Gross Domestic Product [GDP], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/GDP, March 13, 2025.

- 

- 

## Code