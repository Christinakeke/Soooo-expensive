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
                  <th>p-value</th>
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
          <table style="margin: auto; width: 100%;">
             <tr>
                 <th style="width: 30%;">Time period</th>
                 <th style="width: 30%;">Pearson correlation coefficient</th>
                 <th style="width: 40%;">p-value</th>
             </tr>
             <tr>
                 <td style="width: 30%;">2013-2022</td>
                 <td style="width: 30%;">-0.262789</td>
                 <td style="width: 40%;">0.003735</td>
             </tr>
             <tr>
                 <td style="width: 30%;">2013-2017</td>
                 <td style="width: 30%;">0.340475</td>
                 <td style="width: 40%;">0.007771</td>
             </tr>
             <tr>
                 <td style="width: 30%;">2018-2022</td>
                 <td style="width: 30%;">-0.587713</td>
                 <td style="width: 40%;">7.9354e-07</td>
             </tr>
         </table>
      </div>
  </div>

</details>

<details>
  <summary><strong><u>Canada</u></strong></summary>

  <strong>OLS regression + best-fit line</strong>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/Canada_OLS.png" alt="Best-fit line" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 30px;">
          <table style="margin: auto;">
              <tr>
                  <th>Coefficients</th>
                  <th>R-squared</th>
                  <th>p-value</th>
              </tr>
              <tr>
                  <td>-4.316177</td>
                  <td>0.031361</td>
                  <td>0.052997</td>
              </tr>
          </table>
      </div>
  </div>

  <br>

  <strong>Pearson correlation coefficient</strong>

  <br>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/Canada.png" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 15px;">
          <table style="margin: auto; width: 100%;">
             <tr>
                 <th style="width: 30%;">Time period</th>
                 <th style="width: 30%;">Pearson correlation coefficient</th>
                 <th style="width: 30%;">p-value</th>
             </tr>
             <tr>
                 <td>2013-2022</td>
                 <td>-0.177090</td>
                 <td>0.052997</td>
             </tr>
             <tr>
                 <td>2013-2019</td>
                 <td>-0.353245</td>
                 <td>0.000981</td>
             </tr>
             <tr>
                 <td>2020-2021</td>
                 <td>0.750873</td>
                 <td>2.3635e-05</td>
             </tr>
             <tr>
                 <td>2021-2022</td>
                 <td>-0.534864</td>
                 <td>0.007083</td>
             </tr>
         </table>
      </div>
  </div>

</details>

<details>
  <summary><strong><u>Germany</u></strong></summary>

  <strong>OLS regression + best-fit line</strong>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/Germany_OLS.png" alt="Best-fit line" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 30px;">
          <table style="margin: auto;">
              <tr>
                  <th>Coefficients</th>
                  <th>R-squared</th>
                  <th>p-values</th>
              </tr>
              <tr>
                  <td>-8.809991</td>
                  <td>0.137069</td>
                  <td>0.000032</td>
              </tr>
          </table>
      </div>
  </div>

  <br>

  <strong>Pearson correlation coefficient</strong>

  <br>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/Germany.png" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 15px;">
          <table style="margin: auto; width: 100%;">
             <tr>
                 <th>Time period</th>
                 <th>Pearson correlation coefficient</th>
                 <th>p-value</th>
             </tr>
             <tr>
                 <td>2013-2022</td>
                 <td>-0.370230</td>
                 <td>3.1533e-05</td>
             </tr>
             <tr>
                 <td>2021-2022</td>
                 <td>-0.963904</td>
                 <td>3.9514e-14</td>
             </tr>
         </table>
      </div>
  </div>

</details>

<details>
  <summary><strong><u>France</u></strong></summary>

  <strong>OLS regression + best-fit line</strong>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/France_OLS.png" alt="Best-fit line" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 30px;">
          <table style="margin: auto;">
              <tr>
                  <th>Coefficients</th>
                  <th>R-squared</th>
                  <th>p-values</th>
              </tr>
              <tr>
                  <td>-5.934358</td>
                  <td>0.140726</td>
                  <td>0.000024</td>
              </tr>
          </table>
      </div>
  </div>

  <br>

  <strong>Pearson correlation coefficient</strong>

  <br>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/France.png" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 15px;">
          <table style="margin: auto; width: 100%;">
             <tr>
                 <th>Time period</th>
                 <th>Pearson correlation coefficient</th>
                 <th>p-value</th>
             </tr>
             <tr>
                 <td>2013-2022</td>
                 <td>-0.375135</td>
                 <td>2.4256e-05</td>
             </tr>
             <tr>
                 <td>2013-2015</td>
                 <td>0.779767</td>
                 <td>2.0833e-08</td>
             </tr>
             <tr>
                 <td>2016-2018</td>
                 <td>0.420082</td>
                 <td>0.010748</td>
             </tr>
             <tr>
                 <td>2019-2022</td>
                 <td>-0.744739</td>
                 <td>1.2872e-09</td>
             </tr>
         </table>
      </div>
  </div>

</details>

<details>
  <summary><strong><u>United Kingdom</u></strong></summary>

  <strong>OLS regression + best-fit line</strong>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/UK_OLS.png" alt="Best-fit line" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 30px;">
          <table style="margin: auto;">
              <tr>
                  <th>Coefficients</th>
                  <th>R-squared</th>
                  <th>p-values</th>
              </tr>
              <tr>
                  <td>-64.43446</td>
                  <td>0.049808</td>
                  <td>0.014278</td>
              </tr>
          </table>
      </div>
  </div>

  <br>

  <strong>Pearson correlation coefficient</strong>

  <br>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/UK.png" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 15px;">
          <table style="margin: auto; width: 100%;">
             <tr>
                 <th>Time period</th>
                 <th>Pearson correlation coefficient</th>
                 <th>p-value</th>
             </tr>
             <tr>
                 <td>2013-2022</td>
                 <td>-0.223177</td>
                 <td>0.014278</td>
             </tr>
             <tr>
                 <td>2013-2015</td>
                 <td>0.503770</td>
                 <td>2.0833e-08</td>
             </tr>
             <tr>
                 <td>2016</td>
                 <td>-0.933754</td>
                 <td>8.9842e-06</td>
             </tr>
             <tr>
                 <td>2017-2021</td>
                 <td>0.438531</td>
                 <td>0.000457</td>
             </tr>
             <tr>
                 <td>2022</td>
                 <td>-0.899450</td>
                 <td>6.8227e-05</td>
             </tr>
         </table>
      </div>
  </div>

</details>

<details>
  <summary><strong><u>India</u></strong></summary>

  <strong>OLS regression + best-fit line</strong>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/India_OLS.png" alt="Best-fit line" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 30px;">
          <table style="margin: auto;">
              <tr>
                  <th>Coefficients</th>
                  <th>R-squared</th>
                  <th>p-values</th>
              </tr>
              <tr>
                  <td>608.83772</td>
                  <td>0.140353</td>
                  <td>0.000025</td>
              </tr>
          </table>
      </div>
  </div>

  <br>

  <strong>Pearson correlation coefficient</strong>

  <br>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/India.png" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 15px;">
          <table style="margin: auto; width: 100%;">
             <tr>
                 <th>Time period</th>
                 <th>Pearson correlation coefficient</th>
                 <th>p-value</th>
             </tr>
             <tr>
                 <td>2013-2022</td>
                 <td>0.374637</td>
                 <td>2.4915e-05</td>
             </tr>
             <tr>
                 <td>2013-2016</td>
                 <td>0.715660</td>
                 <td>1.0851e-08</td>
             </tr>
             <tr>
                 <td>2017-2018</td>
                 <td>-0.576939</td>
                 <td>0.003162</td>
             </tr>
             <tr>
                 <td>2019-2022</td>
                 <td>0.428531</td>
                 <td>0.002375</td>
             </tr>
         </table>
      </div>
  </div>

</details>

<details>
  <summary><strong><u>Italy</u></strong></summary>

  <strong>OLS regression + best-fit line</strong>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/Italy_OLS.png" alt="Best-fit line" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 30px;">
          <table style="margin: auto;">
              <tr>
                  <th>Coefficients</th>
                  <th>R-squared</th>
                  <th>p-values</th>
              </tr>
              <tr>
                  <td>-9.691246</td>
                  <td>0.135208</td>
                  <td>0.000036</td>
              </tr>
          </table>
      </div>
  </div>

  <br>

  <strong>Pearson correlation coefficient</strong>

  <br>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/India.png" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 15px;">
          <table style="margin: auto; width: 100%;">
             <tr>
                 <th>Time period</th>
                 <th>Pearson correlation coefficient</th>
                 <th>p-value</th>
             </tr>
             <tr>
                 <td>2013-2022</td>
                 <td>-0.367707</td>
                 <td>3.6030e-05</td>
             </tr>
             <tr>
                 <td>2013-2016</td>
                 <td>0.590375</td>
                 <td>1.0020e-05</td>
             </tr>
             <tr>
                 <td>2017</td>
                 <td>-0.679280</td>
                 <td>0.015118</td>
             </tr>
             <tr>
                 <td>2018-2022</td>
                 <td>-0.699420</td>
                 <td>5.0806e-10</td>
             </tr>
         </table>
      </div>
  </div>

</details>

<details>
  <summary><strong><u>Japan</u></strong></summary>

  <strong>OLS regression + best-fit line</strong>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/Japan_OLS.png" alt="Best-fit line" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 30px;">
          <table style="margin: auto;">
              <tr>
                  <th>Coefficients</th>
                  <th>R-squared</th>
                  <th>p-values</th>
              </tr>
              <tr>
                  <td>-643.3588</td>
                  <td>0.161692</td>
                  <td>0.000005</td>
              </tr>
          </table>
      </div>
  </div>

  <br>

  <strong>Pearson correlation coefficient</strong>

  <br>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/Japan.png" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 15px;">
          <table style="margin: auto; width: 100%;">
             <tr>
                 <th>Time period</th>
                 <th>Pearson correlation coefficient</th>
                 <th>p-value</th>
             </tr>
             <tr>
                 <td>2013-2022</td>
                 <td>-0.402109</td>
                 <td>5.3023e-06</td>
             </tr>
             <tr>
                 <td>2017-2018</td>
                 <td>0.352837</td>
                 <td>0.090808</td>
             </tr>
             <tr>
                 <td>2019-2022</td>
                 <td>-0.930212</td>
                 <td>1.185864e-21</td>
             </tr>
         </table>
      </div>
  </div>

</details>

<details>
  <summary><strong><u>South Korea</u></strong></summary>

  <strong>OLS regression + best-fit line</strong>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/SK_OLS.png" alt="Best-fit line" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 30px;">
          <table style="margin: auto;">
              <tr>
                  <th>Coefficients</th>
                  <th>R-squared</th>
                  <th>p-values</th>
              </tr>
              <tr>
                  <td>-14241.785</td>
                  <td>0.274445</td>
                  <td>8.2468e-10</td>
              </tr>
          </table>
      </div>
  </div>

  <br>

  <strong>Pearson correlation coefficient</strong>

  <br>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/South Korea.png" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 15px;">
          <table style="margin: auto; width: 100%;">
             <tr>
                 <th>Time period</th>
                 <th>Pearson correlation coefficient</th>
                 <th>p-value</th>
             </tr>
             <tr>
                 <td>2013-2022</td>
                 <td>-0.523875</td>
                 <td>8.2468e-10</td>
             </tr>
             <tr>
                 <td>2013-2020</td>
                 <td>0.382084</td>
                 <td>0.000122</td>
             </tr>
             <tr>
                 <td>2021-2022</td>
                 <td>-0.918204</td>
                 <td>2.579057e-10</td>
             </tr>
         </table>
      </div>
  </div>

</details>

<details>
  <summary><strong><u>Russia</u></strong></summary>

  <strong>OLS regression + best-fit line</strong>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/Russia_OLS.png" alt="Best-fit line" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 30px;">
          <table style="margin: auto;">
              <tr>
                  <th>Coefficients</th>
                  <th>R-squared</th>
                  <th>p-values</th>
              </tr>
              <tr>
                  <td>NaN</td>
                  <td>NaN</td>
                  <td>NaN</td>
              </tr>
          </table>
      </div>
  </div>

  <br>

  <strong>Pearson correlation coefficient</strong>

  <br>
  
  <div style="display: flex;">
      <div style="flex: 50%;">
          <img src="./plots/Russia.png" style="width: 100%;">
      </div>
      <div style="flex: 50%; display: flex; align-items: center; margin-left: 15px;">
          <table style="margin: auto; width: 100%;">
             <tr>
                 <th>Time period</th>
                 <th>Pearson correlation coefficient</th>
                 <th>p-value</th>
             </tr>
             <tr>
                 <td>2020-2022</td>
                 <td>-0.872247</td>
                 <td>2.2338e-05</td>
             </tr>
         </table>
      </div>
  </div>

</details>