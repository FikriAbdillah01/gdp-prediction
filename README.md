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
This data has several features that are divided based on the duration of the year. Several indicators contained in this data:

- Gross Domestic Product (Quarterly GDP) $\rightarrow$ `yoy_gdp`
- Import Goods and Services (Quarterly Import) $\rightarrow$ `yoy_impgs`
- Gross Private Domestic Investment (Quarterly Investment) $\rightarrow$ `yoy_gpdic`
- Personal Consumption Expenditure (Quarterly Consumption) $\rightarrow$ `yoy_pce`
- Export Goods and Services (Quarterly Export) $\rightarrow$ `yoy_expgs`
- Industrial Production: Utilites: Electric and Gas Utilites (Quarterly Index) $\rightarrow$ `yoy_`

### GDP Data 1959 - 1971
The features on this duration are the same as before, but with the addition of:

- Personal Consumption Expenditures: energy goods and services (monthly) 

### GDP Data 1972 - 2003
The indicators for this year's interval have additional features in the form of:

- Industrial Production: Manufacturing (Quarterly Index)
- Industrial Production: Manufacturing: Nondurable Goods: Chemical (Quarterly Index)
- Industrial Production: Manufacturing: Nondurable Goods: Food, Beverage, and Tobacco (Quarterly Index) 

### GDP Data 2004 - 2024
Penambahan pada range ini adalah:

- Producer Price Index by Industry: Industrial Gas Manufacturing (Quarterly index)

## Exploratory Data Analysis
The projection of the U.S. GDP from FRED can be seen below.

<p align = 'center'>
<img width = "850" height = "250" src = "figures/gdp growth edited.png">
</p>

Based on the picture, we see several economic events:

1. The Post-War Economic Crisis in 1949: Tahun tersebut merupakan waktu transisi menjadi peaceful economy after the world war 2. Penurunan aktivitas ekonomi tersebut diakibatkan produksi yang biasanya untuk keperluan militer turun drastis. As a result, the government spending plummeted, leading to the unemployment rate skyrocketted and the economic activity significantly dropped.

2. Great Recession 2007-2009: Krisis ekonomi tahun ini dikarenakan subprime motgage crisis, dimana bank mengeluarkan pinjaman rumah dengan resiko atau bunga tinggi kepada kreditur yang memiliki sejarah kredit yang buruk. Permintaan konsumen terhadap rumah meningkat karena suku bunga yang rendah dan syarat pinjaman yang mudah pada 2001. Banyak pembeli rumah yang mengajukan adjustable-rate mortgage (produk dari subprime mortgage). Namun, pada saat suku bunga mulai naik pada 2005, nilai pembayaran hipotek juga meningkat. Akhirnya, peminjam-peminjam yang gagal bayar tidak akan diberikan pinjaman laih bank, sehingga mereka terlilit utang dan harga rumah anjlok. The collapse of the subprime mortgage market led to bank failures, a credit freeze, and a global economic downturn.

3. The Pandemic Recession 2020: Krisis ini diakibatkan penyakit dari virus COVID-19. Karena pandemi ini, pemerintah turun tangan dengan memberlakukan lockdown-membatasi aktifitas masyarakat-untuk mengurangi sebaran penyakit ini. Akibatnya, beberapa toko tutup permanen, unemployment rate meningkat tajam, dan akhirnya GDP negara menurun.

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


- Gambar diatas merupakan matriks korelasi untuk setiap fitur-fitur yang ada di dalam dengan renge tertentu dalam bentuk plot heatmap. The `yoy_pce`, *Personal Consumption Expenditures*, mendapatkan nilai tertinggi dalam perhitungan korelasi Pearson untuk setiap jarak tahun. Artinya, peningkatan konsumsi masyarakat sangat mempengaruhi pendapatan negara jika dibandingkan dengan fitur-fitur lain.

Proyek kali ini akan memperhatikan model mana saja yang dapat memprediksi GDP secara akurat, mulai dari negara mengalami surplus hingga krisis ekonomi.

## Method
The prediction models we used in this project is:

- Econometric (AutoRegressive (AR) + Factor Model (FM))
- Machine learning (Linear Regression, Decision Tree, Random Forest, XGBoost)

Eksperimen akan dibagi menjadi enam konfigurasi. Pertama, model dilatih menggunakan data 1947-1958 untuk memprediksi GDP tahun yang sama. Model yang telah dilatih akan digunakan untuk memprediksi GDP tahun berikutnya, yaitu 1959-1971, 1972-2003, dan 2004-2024. Kedua, data tahun 1959-1971 digunakan model untuk memprediksi tahun 1972-2003 dan 2004-2024, dan begitu pula data tahun 1972-2003. Hal ini dilakukan karena data yang akan diprediksi memiliki fitur-fitur yang ada pada data digunakan untuk melatih model. Setiap model yang diajukan menggunakan konfigurasi tersebut. Hasil dari prediksi akan menggunakan metrik ***root mean squared error***. 

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

- Empat Gambar diatas merupakan hasil prediksi menggunakan data dari 1947-1958 yang memiliki 6 indikator dengan linear regression model. Model dengan data ini dapat memprediksi secara akurat jika dilihat dari nilai RMSE yang kecil. Namun, dari ketiga krisis ekonomi yang dibahas, the linear regression with data in 1947 still not accurately predict them.

<p align = "center">
<img width = "800" height = "300" src = "figures/linalg/Linear Regression data 1959 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/linalg/Linear Regression data 1959 to predict 2004.png">
</p>

- Dari dua gambar diatas, regressi linear dengan data tahun 1959 memprediksi lebih akurat jika dibandingkan dengan 1948 dalam hal prediksi GDP. Terlebih, model ini dapat memprediksi krisis ekonomi tahun 2020 dengan nilai RMSE yang lebih kecil. 

<p align = "center">
<img width = "800" height = "300" src = "figures/linalg/Linear Regression data 1972 to predict 2004.png">
</p>

- Gambar diatas merupakan hasil prediksi model dengan data dari tahun 1972 hingga 2003 yang memiliki 10 fitur. RMSE regressi linear dengan data ini lebih kecil jika dibandinkan dengan data-data sebelumnya.

### LASSO Regression
LASSO (Least Absolute Shrinkage Selection Operator) Regression, also known as L1 Regression, merupakan salah satu regularized regression yang secara matematis hampir mirip dengan Linear Regression. Namun, model ini memiliki regularization $\lambda$ yang digunakan untuk mengurangi error dikarenakan overfitting pada saat pelatihan. The Residual Sum of Squares (RSS) can be archevied by

$$RSS = \min |y - \hat{y}|$$

$$RSS + \lambda \sum_{i=1} \beta_i$$

where $\lambda$ denotes regularization parameter that controls the amount of regularizatio applied. The RSS represent the measurement the error between predicted and actual values. This indicator can be any error measurement such as RMSE, MSE, or MAE. Hasil dari Lasso Regression dapat dilihat dibawah ini.

<p align = "center">
<img width = "800" height = "300" src = "figures/lassoreg/Lasso Regression data 1947 to predict 1959.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/lassoreg/Lasso Regression data 1947 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/lassoreg/Lasso Regression data 1947 to predict 2004.png">
</p>

- Berdasarkan tiga gambar diatas, model lasso regression dengan data 1947 yang memiliki 5 fitur mampu memprediksi data tahun 1959 ke 1971 dengan RMSE 1.5 lebih kecil daripada data tahun 1972 keatas.  

<p align = "center">
<img width = "800" height = "300" src = "figures/lassoreg/Lasso Regression data 1959 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/lassoreg/Lasso Regression data 1959 to predict 2004.png">
</p>

- Dua gambar diatas menunjukkan model dengan data 1959 yang memiliki 6 fitur yang dapat memprediksi GDP growth tahun 1972 keatas dengan RMSE yang lebih kecil jika dibandingkan dengan lasso regression dengan data 1948 dan model Linear Regression dengan tahun data yang sama. 

<p align = "center">
<img width = "800" height = "300" src = "figures/lassoreg/Lasso Regression data 1972 to predict 2004.png">
</p>

- Gambar diatas menunjukkan lasso regression dengan data tahun 1972 yang berisi sekitar 10 fitur dapat memprediksi pertumbuhan tahunan GDP di Amerika dengan nilai RMSE dibawah 1. Nilai tersebut sama dengan Regressi Linear. 

### eXtreme Gradient Boosting

XGboost (eXtreme) merupakan model tree-based, boosting algorithm yang memanfaatkan gradient descent. It known for its effiency, speed, and ability to handle large dataset. The prediction results using this model can be seen in the images below.

<p align = "center">
<img width = "800" height = "300" src = "figures/xgboost/XGBoost data 1947 to predict 1959.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/xgboost/XGBoost data 1947 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/xgboost/XGBoost data 1947 to predict 2004.png">
</p>

- Berdasarkan tiga gambar diatas, model dengan data tahun 1947 tidak mampu melakukan prediksi GDP dengan range tahun 1959 ke 1971 sebaik Lasso dan Linear Regression, tapi mampu memprediksi GDP dengan range tahun 1972-2003 dan 2004-2024 dengan RMSE yang lebih kecil dari dua model tersebut.

<p align = "center">
<img width = "800" height = "300" src = "figures/xgboost/XGBoost data 1959 to predict 1972.png">
</p>

<p align = "center">
<img width = "800" height = "300" src = "figures/xgboost/XGBoost data 1959 to predict 2004.png">
</p>

- Plot YoY Growth GDP tahun 1972-2003 menunjukkan model dengan data tahun 1959-1971 dapat memprediksi dengan RMSE yang hampir sama dengan model Lasso dan Regular Linear Regression, tapi cukup buruk dalam memprediksi GDP tahun 2004-2024.

<p align = "center">
<img width = "800" height = "300" src = "figures/xgboost/XGBoost data 1972 to predict 2004.png">
</p>

- Gambar diatas menunjukkan model XGBoost yang dilatih dengan data tahun 1972-2003 belum mampu memprediksi GDP periode 2004-2024 jika dibandingkan dengan Linear dan Lasso Regression. Model ini tidak akurat dikarenakan jumlah data yang digunakan pada proyek ini tidak banyak.

### Econometric (AR + FM)
Autoregressive (AR) model merupakan model machine learning yang menggunakan satu atau lebih variabel dari waktu sebelumya untuk meramal hasil yang akan datang. Model ini biasa digunakan pada data yang memiliki deretan waktu. Dalam model AR, output nya adalah titik data masa depan yang diekspressikan sebagai kombinasi linear dari titik data masa lalu $p$. $p$ adalah jumlah lags yang dimasukkan ke persamaan. Jika $p = 1$, dan studi kasusnya adalah prediksi GDP, maka ekspressi matematisnya adalah

$$GDP_t = \delta + \psi_1 GDP_{t-1} + \epsilon_t$$

dengan $\psi_1$ adalah koeffisien, $\delta$ denotes the constant (or intercept in linear regression). If we add one exogenous variable, then the equation will be

$$GDP_t = \delta + \psi_1 GDP_{t-1} + \phi_t Q_t + \epsilon_t $$

dimana $\phi_t$ sebagai koefisien dari exogenous variabel $Q_t$ saat waktu $t$. 

Factor Model (FM) merupakan alat statistik yang menguraikan variabel menjadi komponen umum (faktor) and unique or idiosyncratic error. Rumus yang mewakilkan definisi tersebut

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