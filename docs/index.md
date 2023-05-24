<div>
   <center>
        <b>
            <font color="34,63,93" size="7">
                SOOOO expensive!💰
            </font>
        </b>
    </center>
</div>

<div>
   <center>
        <b>
            <font color="34,63,93" size="4">
                Data investigation of the correlation between exchange rate vs inflation rate
            </font>
        </b>
    </center>
</div>

<div>
   <center>
        <font color="black" size="3">
                Ke Chen, Yujia Zhu, Maggie Miao
        </font>
    </center>
</div>>

## ⚙️ Introduction
As international students studying abroad, we have chosen this topic since it is closely related to our living standards and the way we live. Inflation measures how much more expensive a set of goods and services has become over a certain period (IMF), which is critical for us to manage the way we allocate money.

Exchange rate is important to us because we constantly face the need to be aware of the change in exchange rate as every single transaction we made is linked to the exchange rate at the time. Hence, both the inflation rate and the exchange rate are linked to our life and motivates us to investigate the correlation between them. 

## 📝 Project description
We want to evaluate the strength and direction of the correlations between inflation and exchange rate in top 10 GDP countries from 2013-2022. 

We use consumer products index (CPI) as the indicator of inflation and calculate the monthly average exchange rate. 

We intend to investigate the correlation between those two factors through exploratory analysis which includes visualisation, Ordinary least squares regression (OLS) and Pearsons correlation coefficient. We focus on R-square，p-value and Pearsons coefficient to evaluate  the correlations. 

Our goal is to provide some insights about the relation between exhcange rate and inflation. In the end, we also mention limitations in this study.

**Plan**
Our project contains two parts: Data collection and preprocessing and Exploratory Data Analysis.

*Data collection and preprocessing*
1. Collecting data from Exchange rates data-API and OECD datasets

2. Cleaning data and preprocessing datasets
    - Selecting the exchange rate of the local currency against the US dollar and calculating the monthly average exchange rate 
    - Cleaning the original static dataframe of CPI 

3. Overall Visualisation
- Map
- Line Chart

*Exploratory Data Analysis*
In this step, our analysis is based on every country since we found that the correlation between exchange rate and inflation is different in different countries.

1. OLS regression + best-fit line
2. Pearson correlation coefficient

## 📊 Data
### Data Source
- [Exchange rates data-API](https://apilayer.com/marketplace/exchangerates_data-api)
- [OECD datasets](https://data.oecd.org/price/inflation-cpi.htm)

### Data collection + cleaning + preprocessing
We use 'Pandas' to get the final 10 dataframe for exploratory analysis which includes 10 countries' CPI and exchange rate from 2013-2022.

### Visualisation
Map


Line chart
![Inflation](../plots/inflation.png)

[Link to Complete code](Data collection.md)

