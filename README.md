# Gross Domestic Product Prediction

## Background
The Gross Domestic Product (GDP) is indikator krusial yang mengukur nilai total dari keseluruhan barang dan jasa yang diproduksi negara dalam waktu tertentu, biasanya dalam quartil atau dalam tahun. GDP menjadi tolok ukur penting dari makroekonomi sebuah negara dan menjadi basis dasar untuk merumuskan kebijakan ekonomi. Banyak negara yang telah memasuki era "new normal" setelah dihantam oleh banyak faktor eksterogen, seperti pandemi dan perang, yang membuat prediksi makroekonomi menjadi tidak akurat.

## Goal
The goal of this project is to explore machine learning that can predict GDP accurately.

## Limitation
Dalam proyek GDP prediction, ada banyak sekali indikator atau fitur-fitur yang tidak dimasukkan atau diperhitungkan karena keterbatasan akses dan domain pengetahuan.

## Data Descriptions
This data is open-source and is obtained from the Federal Reserve Economic Data (FRED), an online database created by the financial institution, The Federal Reserve Bank of St. Louis. Data ini dapat berupa format .csv, .xlsx., pdf, atau dapat diambil dengan menggunakan API.

### GDP Data 1947 - 1958
Data ini memiliki beberapa fitur yang terbagi berdasarkan durasi tahun. Beberapa indikator yang terdapat pada data ini:

- Gross Domestic Product (Quarterly GDP)
- Import Goods and Services (Quarterly Import)
- Gross Private Domestic Investment (Quarterly Investment)
- Personal Consumption Expenditure (Quarterly Consumption) 
- Export Goods and Services (Quarterly Export)
- Industrial Production: Utilites: Electric and Gas Utilites (Quarterly Index)

### GDP Data 1959 - 1971
The features on this duration are the same as before, but with the addition of:

- Personal Consumption Expenditures: energy goods and services (monthly) 

### GDP Data 1972 - 2003
Indikator pada jarak tahun ini memiliki tambahan berupa:

- Industrial Production: Manufacturing (Quarterly Index)
- Industrial Production: Manufacturing: Nondurable Goods: Chemical (Quarterly Index)
- Industrial Production: Manufacturing: Nondurable Goods: Food, Beverage, and Tobacco (Quarterly Index) 

### GDP Data 2004 - 2024
Penambahan pada range ini adalah:
- Producer Price Index by Industry: Industrial Gas Manufacturing (Quarterly index)

## Exploratory Data Analysis


## Method
Model Model prediksi yang akan digunakan :

- Econometric (AutoRegressive (AR) + Factor Model (FM))
- Machine learning (Linear Regression, Decision Tree, Random Forest, XGBoost)

Eksperimen akan dibagi menjadi enam konfigurasi. Pertama, model dilatih menggunakan data 1947-1958 untuk memprediksi GDP tahun yang sama. Model yang telah dilatih akan digunakan untuk memprediksi GDP tahun berikutnya, yaitu 1959-1971, 1972-2003, dan 2004-2024. Kedua, data tahun 1959-1971 digunakan model untuk memprediksi tahun 1972-2003 dan 2004-2024, dan begitu pula data tahun 1972-2003. Hal ini dilakukan karena data yang akan diprediksi memiliki fitur-fitur yang ada pada data digunakan untuk melatih model. Setiap model yang diajukan menggunakan konfigurasi tersebut. Hasil dari prediksi akan menggunakan metrik ***root mean squared error***. 

<p>
<img width = "800" height = "300" src = "figures/exp config.png">
</p>

## Result
Root mean squared error (RMSE) atau root mean squared deviation merupakan salah satu metrik yang biasanya digunakan untuk evaluasi hasil dari prediksi model, khusunya dalam tugas regressi. Regressi sendiri merupakan metode yang digunakan untuk menganallisa hubungan antara variabel dependen dan variabel independen. 

### Econometric (AR + FM)
Autoregressive (AR) model merupakan model machine learning yang menggunakan satu atau lebih variabel dari waktu sebelumya untuk meramal hasil yang akan datang. Model ini biasa digunakan pada data yang memiliki deretan waktu.

Factor Model (FM) merupakan alat statistik yang menguraikan variabel menjadi komponen umum (faktor) and unique or idiosyncratic error. Rumus yang mewakilkan definisi tersebut 

$$X_{it} = \lambda_i F_t + \epsilon_{it}$$

dimana $X_{it}$ is observed variable for unit $i$ at time $t$, $\lambda$ is factor loading, $F_{t}$ is common factor at time $t$, and $\epsilon_{it}$ is idiosyncratic (unique) error for unit $i$ at time $t$.
## Conclusion
From this project, we can conclude that:

- The ... model outperform all machine learning model. The model can accurately predict GDP 

## Reference

- Board of Governors of the Federal Reserve System (US), Industrial Production: Consumer Goods [IPCONGD], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/IPCONGD, March 13, 2025.

- U.S. Bureau of Economic Analysis, Gross Domestic Product [GDP], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/GDP, March 13, 2025.

- 

- 

- 