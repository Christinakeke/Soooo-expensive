```python
import requests
import pandas as pd
from sklearn.linear_model import LinearRegression
import statsmodels.api as sm
import matplotlib.pyplot as plt
import numpy as np
from scipy.stats import pearsonr
```

## OLS


```python
def perform_linear_regression(df,title):
    # Perform linear regression
    X = sm.add_constant(df['USD'])
    model = sm.OLS(df['Value'], X)
    results = model.fit()

    # Retrieve the coefficients, intercept, R-squared, and p-values
    coefficients = results.params[1:]  # Exclude the intercept
    intercept = results.params[0]  # Retrieve the intercept separately
    r_squared = results.rsquared
    p_values = results.pvalues[1:]  # Exclude the intercept p-value

    # Print the coefficients, intercept, R-squared, and p-values
    print("Intercept:", intercept)
    print("Coefficients:", coefficients)
    print("R-squared:", r_squared)
    print("p-values:", p_values)

    # Plot the data points and best-fit line
    plt.scatter(df['USD'], df['Value'], color='blue', label='Data Points')
    plt.plot(df['USD'], results.fittedvalues, color='red', label='Best-Fit Line')

    # Add labels and a legend
    plt.xlabel('Exchange rate')
    plt.ylabel('CPI Value')
    plt.title(title)
    plt.legend()

    # Show the plot
    plt.show()

```

## Pearson correlation coefficient


```python
# Compute the Pearson correlation coefficient and p-value
def calculate_pearson_correlation(df):
    X = df['USD']
    Y = df['Value']
    correlation_coef, p_value = pearsonr(X, Y)

    print("Pearson correlation coefficient:", correlation_coef)
    print("p-value:", p_value)
```

## Remove outliers


```python
# Find outliers and reomve them in order to perform linear regression with a p-value < 0.05
def remove_outliers(df, threshold):
    X = sm.add_constant(df['USD'])
    model = sm.OLS(df['Value'], X)
    results = model.fit()

    # find outliers
    residuals = results.resid  # get residuals

    std_residuals = (residuals - np.mean(residuals)) / np.std(residuals)  # standardize residuals

    t = threshold  # set threshold

    outliers = np.abs(std_residuals) > t  # find outliers where abs(s_r) > 1

    # create new dataframe without outliers
    df_without_outliers = df.loc[~outliers]
    
    return df_without_outliers
```

## China


```python
df=pd.read_excel('CHN.xlsx')
perform_linear_regression(df,'China')
```

    Intercept: 7.203868433425461
    Coefficients: USD   -34.032598
    dtype: float64
    R-squared: 0.06905790833335645
    p-values: USD    0.003735
    dtype: float64
    


    

    



```python
calculate_pearson_correlation(df)
```

    Pearson correlation coefficient: -0.2627887142427475
    p-value: 0.003734956600827832
    


```python
filtered_data = df[df['TIME'].dt.year < 2018]
calculate_pearson_correlation(filtered_data)
```

    Pearson correlation coefficient: 0.34047467667291464
    p-value: 0.007770841578111888
    


```python
filtered_data1 = df[df['TIME'].dt.year >= 2018]

calculate_pearson_correlation(filtered_data1 )

```

    Pearson correlation coefficient: -0.5877126878699966
    p-value: 7.935444328076864e-07
    

## Canada


```python
df1=pd.read_excel('CAN.xlsx')
perform_linear_regression(df1,'Canada')
```


```python
calculate_pearson_correlation(df1)
```

    Pearson correlation coefficient: -0.17709031027777195
    p-value: 0.052997127006820625
    


```python
filtered_data = df1[df1['TIME'].dt.year < 2020]
calculate_pearson_correlation(filtered_data )
```

    Pearson correlation coefficient: -0.3532446216766255
    p-value: 0.0009808196431653775
    


```python
filtered_dat1 = df1[(df1['TIME'].dt.year >= 2020) & (df1['TIME'].dt.year < 2022)]
calculate_pearson_correlation(filtered_dat1)
```

    Pearson correlation coefficient: 0.7508732726934924
    p-value: 2.3635338485209442e-05
    


```python
filtered_dat2 = df1[df1['TIME'].dt.year >= 2021]
calculate_pearson_correlation(filtered_dat2)
```

    Pearson correlation coefficient: -0.5348636071741699
    p-value: 0.007082952914225607
    


```python

perform_linear_regression(remove_outliers(df, 1),'Canada without outliers')
df_outliers = df.drop(remove_outliers(df_1, 1).index)
print(df_outliers)
```

## Germany


```python
df2=pd.read_excel('DEU.xlsx')
perform_linear_regression(df2,'Germany')
```

    Intercept: 12.259640825533705
    Coefficients: USD   -8.809991
    dtype: float64
    R-squared: 0.13706995527137533
    p-values: USD    0.000032
    dtype: float64
    


    

    



```python
calculate_pearson_correlation(df2)
```

    Pearson correlation coefficient: -0.3702295980487993
    p-value: 3.1532925195141835e-05
    


```python
filtered_data = df2[df2['TIME'].dt.year > 2020]
calculate_pearson_correlation(filtered_data )
```

    Pearson correlation coefficient: -0.9639041331154689
    p-value: 3.95135415624807e-14
    

## France


```python
df3=pd.read_excel('FRA.xlsx')
perform_linear_regression(df3,'France')
```

    Intercept: 8.226708400475648
    Coefficients: USD   -5.934358
    dtype: float64
    R-squared: 0.1407260979034931
    p-values: USD    0.000024
    dtype: float64
    


    

    



```python
calculate_pearson_correlation(df3)
```

    Pearson correlation coefficient: -0.3751347729863138
    p-value: 2.4255521937479907e-05
    


```python
filtered_data = df3[df3['TIME'].dt.year < 2016]
calculate_pearson_correlation(filtered_data)
```

    Pearson correlation coefficient: 0.7797667673145577
    p-value: 2.083292839042368e-08
    


```python
filtered_data1 = df3[(df3['TIME'].dt.year >= 2016) & (df3['TIME'].dt.year < 2019)]
calculate_pearson_correlation(filtered_data1)
```

    Pearson correlation coefficient: 0.42008169647438487
    p-value: 0.010748448223336083
    


```python
filtered_data2 = df3[df3['TIME'].dt.year >= 2019]
calculate_pearson_correlation(filtered_data2)
```

    Pearson correlation coefficient: -0.7447394442562059
    p-value: 1.287151264258049e-09
    

## Britain


```python
df4=pd.read_excel('GBR.xlsx')
perform_linear_regression(df4,'United Kingdom')
```

    Intercept: 12.15958919418014
    Coefficients: USD   -64.434459
    dtype: float64
    R-squared: 0.04980810404447522
    p-values: USD    0.014278
    dtype: float64
    


    

    



```python
calculate_pearson_correlation(df4)
```

    Pearson correlation coefficient: -0.22317729285139012
    p-value: 0.01427839208970721
    


```python
filtered_data = df4[df4['TIME'].dt.year < 2016]
calculate_pearson_correlation(filtered_data)
```

    Pearson correlation coefficient: 0.503769799100714
    p-value: 0.0017342842261415775
    


```python
filtered_data = df4[(df4['TIME'].dt.year >= 2016)&(df4['TIME'].dt.year < 2017)]
calculate_pearson_correlation(filtered_data)
```

    Pearson correlation coefficient: -0.9337542014192667
    p-value: 8.984169956546348e-06
    


```python
filtered_data = df4[(df4['TIME'].dt.year >= 2017)&(df4['TIME'].dt.year < 2022)]
calculate_pearson_correlation(filtered_data)
```

    Pearson correlation coefficient: 0.4385307520802292
    p-value: 0.0004571071529150877
    


```python
filtered_data1 = df4[df4['TIME'].dt.year >= 2022]
calculate_pearson_correlation(filtered_data1)
```

    Pearson correlation coefficient: -0.8994499656425519
    p-value: 6.822691575494531e-05
    

## India


```python
df5=pd.read_excel('IND.xlsx')
perform_linear_regression(df5,'India')
```

    Intercept: -3.0596363142690564
    Coefficients: USD    608.837721
    dtype: float64
    R-squared: 0.1403525941936612
    p-values: USD    0.000025
    dtype: float64
    


    

    



```python
calculate_pearson_correlation(df5)
```

    Pearson correlation coefficient: 0.37463661619449484
    p-value: 2.491537539760061e-05
    


```python
filtered_data = df5[df5['TIME'].dt.year < 2017]
calculate_pearson_correlation(filtered_data)
```

    Pearson correlation coefficient: 0.7156597406441483
    p-value: 1.0850504841988628e-08
    


```python
filtered_data1 = df5[(df5['TIME'].dt.year >= 2017) & (df5['TIME'].dt.year < 2019)]
calculate_pearson_correlation(filtered_data1)
```

    Pearson correlation coefficient: -0.5769386412916497
    p-value: 0.00316237470524235
    


```python
filtered_data2= df5[df5['TIME'].dt.year >= 2019]
calculate_pearson_correlation(filtered_data2)
```

    Pearson correlation coefficient: 0.42853071007267013
    p-value: 0.002375446716548677
    

## Italy


```python
df6=pd.read_excel('ITA.xlsx')
perform_linear_regression(df6,'Italy')
```

    Intercept: 12.755109187599217
    Coefficients: USD   -9.691246
    dtype: float64
    R-squared: 0.13520809158071723
    p-values: USD    0.000036
    dtype: float64
    


    

    



```python
calculate_pearson_correlation(df6)
```

    Pearson correlation coefficient: -0.36770652915160085
    p-value: 3.603012830204642e-05
    


```python
filtered_data = df6[df6['TIME'].dt.year < 2017]
calculate_pearson_correlation(filtered_data)
```

    Pearson correlation coefficient: 0.5903750263216097
    p-value: 1.0020361148180345e-05
    


```python
filtered_data1 = df6[(df6['TIME'].dt.year >= 2017) & (df6['TIME'].dt.year < 2018)]
calculate_pearson_correlation(filtered_data1)
```

    Pearson correlation coefficient: -0.679279625891747
    p-value: 0.015118014744650252
    


```python
filtered_data2 = df6[df6['TIME'].dt.year >= 2018]
calculate_pearson_correlation(filtered_data2)
```

    Pearson correlation coefficient: -0.6994199235689817
    p-value: 5.080627294995416e-10
    

## Japan


```python
df7=pd.read_excel('JPN.xlsx')
perform_linear_regression(df7,'Japan')
```

    Intercept: 6.616624067052131
    Coefficients: USD   -643.358812
    dtype: float64
    R-squared: 0.16169154305655353
    p-values: USD    0.000005
    dtype: float64
    


    

    



```python
calculate_pearson_correlation(df7)
```

    Pearson correlation coefficient: -0.4021088696566562
    p-value: 5.302314792042343e-06
    


```python
filtered_data = df7[(df7['TIME'].dt.year >= 2017) & (df6['TIME'].dt.year < 2019)]
calculate_pearson_correlation(filtered_data)
```

    Pearson correlation coefficient: 0.35283669964859626
    p-value: 0.09080770027736342
    


```python
filtered_data1 = df7[df7['TIME'].dt.year >= 2019]
calculate_pearson_correlation(filtered_data1)
```

    Pearson correlation coefficient: -0.9302124250082526
    p-value: 1.1858643975312138e-21
    

## South Korea


```python
df8=pd.read_excel('KOR.xlsx')
perform_linear_regression(df8,'South Korea')
```

    Intercept: 14.102585592361303
    Coefficients: USD   -14241.785181
    dtype: float64
    R-squared: 0.2744454732527142
    p-values: USD    8.246803e-10
    dtype: float64
    


    

    



```python
calculate_pearson_correlation(df8)
```

    Pearson correlation coefficient: -0.523875436771676
    p-value: 8.246802889587533e-10
    


```python
filtered_data = df8[df8['TIME'].dt.year < 2021]
calculate_pearson_correlation(filtered_data)
```

    Pearson correlation coefficient: 0.38208363172157567
    p-value: 0.000122326678643089
    


```python
filtered_data1 = df8[df8['TIME'].dt.year >= 2021]
calculate_pearson_correlation(filtered_data1)
```

    Pearson correlation coefficient: -0.9182036529521644
    p-value: 2.57905667875742e-10
    

## Russia 


```python
df9=pd.read_excel('RUS.xlsx')
perform_linear_regression(df9,'Russia')
```

    Intercept: nan
    Coefficients: USD   NaN
    dtype: float64
    R-squared: nan
    p-values: USD   NaN
    dtype: float64
    


    

    



```python
filtered_data = df9[df9['TIME'].dt.year > 2020]
calculate_pearson_correlation(filtered_data)
```

    Pearson correlation coefficient: -0.8722468871313641
    p-value: 2.2337683294874898e-05
    
