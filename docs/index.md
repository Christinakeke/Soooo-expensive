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

Exchange rate is important to us because we constantly face the need to be aware of the change in exchange rate as every single transaction we made is linked to the exchange rate at the time. Hence, both the inflation rate and the exchange rate are linked to our life and motivates us to investigate the correlation between them. <br><br>


## 📝 Project description
We want to evaluate the strength and direction of the correlations between inflation and exchange rate in top 10 GDP countries from 2013-2022. 

We use consumer products index (CPI) as the indicator of inflation and calculate the monthly average exchange rate. 

We intend to investigate the correlation between those two factors through exploratory analysis which includes visualisation, Ordinary least squares regression (OLS) and Pearsons correlation coefficient. We focus on R-square，p-value and Pearsons coefficient to evaluate  the correlations. 

Our goal is to provide some insights about the relation between exhcange rate and inflation. In the end, we also mention limitations in this study.

### Plan

Our project contains two parts: Data collection and preprocessing and Exploratory Data Analysis.

**Data collection and preprocessing**
1. Collecting data from Exchange rates data-API and OECD datasets

2. Cleaning data and preprocessing datasets
    - Selecting the exchange rate of the local currency against the US dollar and calculating the monthly average exchange rate 
    - Cleaning the original static dataframe of CPI 

3. Overall Visualisation
- Map
- Line Chart

**Exploratory Data Analysis**

In this step, our analysis is based on every country since we found that the correlation between exchange rate and inflation is different in different countries.

1. OLS regression + best-fit line
2. Pearson correlation coefficient<br><br>


## 📊 Data
### Data Source
- [Exchange rates data-API](https://apilayer.com/marketplace/exchangerates_data-api)
- [OECD data](https://data.oecd.org/price/inflation-cpi.htm)

### Data collection + cleaning + preprocessing

We mainly use ‘pandas' package to obtain the final 10 data frames for exploratory analysis, each including the country's CPI and exchange rate for the period 2013-2022.

The complete cleaning and preprocessing process can be found in link at the end of this part.

### Visualisation

We use the following visualisation to show the overall trend of exchange rate and inflation in each country.

[**Map**](Map.html)

**Line chart**

<div style="display: flex; justify-content: space-between;">
    <img src="./plots/exchange_rate.png" alt="Exchange Rate" width="400" />
    <img src="./plots/inflation.png" alt="Inflation" width="400" />
</div>

We found that the variation of exchange rate and inflation is different in different countries, so we further investigate the correlation between them in each country.<br>

**Country trend**

We combine the trend of exchange rate and inflation together to visualise the correlation between them.

Here is the example of China and Russia: 

<div style="display: flex; justify-content: space-between;">
    <img src="./plots/China.png" alt="Exchange rate and CPI in China" width="400" />
    <img src="./plots/Russia.png" alt="Exchange rate and CPI in Russia" width="400" />
</div>

We will specify the country trend in the following part.<br>

*Here is the link for code used in data collection and preprocessing*
[Link to view code](Data.md)<br><br>


## 📈 Exploratory Data Analysis

In the second part of our study, we take steps closer to every country.

<details>
  <summary><strong><u>China</u></strong></summary>

  <strong>OLS regression + best-fit line</strong>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/China_OLS.png" alt="Best-fit line" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 30px;">
          <table style="margin: auto;">
              <tr>
                  <th>Coefficients</th>
                  <th>R-squared</th>
                  <th>p-values</th>
              </tr>
              <tr>
                  <td>-34.032598</td>
                  <td>0.069058</td>
                  <td>0.003735</td>
              </tr>
          </table>
      </div>
  </div>

  <br>

  <strong>Pearson correlation coefficient</strong>

  <br>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/China.png" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 15px;">
          <table style="margin: auto;">
             <tr>
                 <th>Time period</th>
                 <th>Pearson correlation coefficient</th>
                 <th>p-value</th>
             </tr>
             <tr>
                 <td>2013-2022</td>
                 <td>-0.262789</td>
                 <td>0.003735</td>
             </tr>
             <tr>
                 <td>2013-2017</td>
                 <td>0.340475</td>
                 <td>0.007771</td>
             </tr>
             <tr>
                 <td>2018-2022</td>
                 <td>-0.587713</td>
                 <td>7.935444e-07</td>
             </tr>
         </table>
      </div>
  </div>

</details>

