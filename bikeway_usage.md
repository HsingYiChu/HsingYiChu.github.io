## Brisbane bikeway usage forecast model- the practice of analysing time series data with seasonality

**Project description:** This project aims to analyse the usage pattern of the Brisbane bikeway, and investigate if temperature is one of the factors that affect the usage. Furthermore, based on the findings, we examined bikeway data collected by the Brisbane City Council and used it to make predictions of future cycle usage, using time series forecasting techniques. The data is from: https://www.data.brisbane.qld.gov.au/data/dataset/bikeway-counts. It comprises five .csv files, for the years 2016-2020.

### 1. Data preparation

Compile all the bikeway usage data for 2016-2020 into one series and merge it with the maximum temperature data. During the process, It is noticed that the missing values/0s in this data set are not evenly distributed. For daily maximum temperature, most missing values are located in 2018. For cycle traffic, most of the missing values and 0s are located in 2016 (January to March)and 2017 (April to August). This could be caused by multiple possible reasons such as the monitoring system maintenance or the bikeway closure. At this point, we are not sure if these missing values and 0s should be processed differently given the uneven distribution. In this case, we would like to closely examine data within one year, 2019 and 2020 are preferred.

<img src="images/dfbikeway.png?raw=true"/>

### 2. Exploratory Data Analysis (EDA)

Visualise the data and the relationship observed.

<img src="images/bikeway_eda1.png?raw=true"/>

<img src="images/bikeway_eda1s.png?raw=true"/>

<img src="images/bikeway_eda2.png?raw=true"/>

<img src="images/bikeway_eda2s.png?raw=true"/>

For plot 1 and plot 2, it is observed that the bikeway usage in both 2019 and 2020 fluctuated a lot. Thus, we applied the seaborn package to generate smooth trend lines with confidence intervals to observe trends and patterns more clearly. While a relatively clear trend is shown in 2020, both plot 1s and plot 2s pointed out that the trend of usage started low during January and increased to reach a maximum during April/May (February/March for 2019 data), then started to decrease until June/July. After the dent, the usage again climbed until October/November then dropped again.

<img src="images/bikeway_eda5.png?raw=true"/>

<img src="images/bikeway_eda6.png?raw=true"/>

Plots 3 and 4 show the gradient of correlation in the first segment is steeper than the second one (both are positive), which could be interpreted as the usage of Milton bikeway is affected more by low temperature than high temperature.

However, in this case, if we would like to investigate more details about the relationship between temperature and bikeway usage, several possible uncertainties should be taken care of. For example. The endogeneity problem could be caused by omitted variable issues. There are many more exogenous variables we should consider including as controls such as the school holidays distribution (winter/summer vacation).

### 3. STR decomposition process

<img src="images/bikeway_str.png?raw=true"/>

### 4. ARIMA model 

<img src="images/bikeway_arima.png?raw=true"/>




