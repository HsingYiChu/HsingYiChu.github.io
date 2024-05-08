## The relationship between temperature and bikeway usage - the practice of removing seasonality from time series data

**Project description:** This project aims to analyse the usage pattern of the Brisbane bikeway, and investigate if temperature is one of the factors that affect the usage. Furthermore, based on the findings, we examined bikeway data collected by the Brisbane City Council and used it to make predictions of future cycle usage, using time series forecasting techniques. The data is from: https://www.data.brisbane.qld.gov.au/data/dataset/bikeway-counts. It comprises five .csv files, for the years 2016-2020.

### 1. Data preparation

Compile all the bikeway usage data for 2016-2020 into one series and merge it with the maximum temperature data. During the process, It is noticed that the missing values/0s in this data set are not evenly distributed. For daily maximum temperature, most missing values are located in 2018. For cycle traffic, most of the missing values and 0s are located in 2016 (January to March)and 2017 (April to August). This could be caused by multiple possible reasons such as the monitoring system maintenance or the bikeway closure. At this point, we are not sure if these missing values and 0s should be processed differently given the uneven distribution. In this case, we would like to closely examine data within one year, 2019 and 2020 are preferred.

<img src="images/dfbikeway.png?raw=true"/>

