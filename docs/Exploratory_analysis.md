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

## China


```python
df=pd.read_excel('CHN.xlsx')
perform_linear_regression(df,'China')
```  

```python
calculate_pearson_correlation(df)
```

```python
filtered_data = df[df['TIME'].dt.year < 2018]
calculate_pearson_correlation(filtered_data)
```


```python
filtered_data1 = df[df['TIME'].dt.year >= 2018]

calculate_pearson_correlation(filtered_data1 )

```


## Canada


```python
df1=pd.read_excel('CAN.xlsx')
perform_linear_regression(df1,'Canada')
```


```python
calculate_pearson_correlation(df1)
```


```python
filtered_data = df1[df1['TIME'].dt.year < 2020]
calculate_pearson_correlation(filtered_data )
```


```python
filtered_dat1 = df1[(df1['TIME'].dt.year >= 2020) & (df1['TIME'].dt.year < 2022)]
calculate_pearson_correlation(filtered_dat1)
```


```python
filtered_dat2 = df1[df1['TIME'].dt.year >= 2021]
calculate_pearson_correlation(filtered_dat2)
```


## Germany


```python
df2=pd.read_excel('DEU.xlsx')
perform_linear_regression(df2,'Germany')
```


```python
calculate_pearson_correlation(df2)
```


```python
filtered_data = df2[df2['TIME'].dt.year > 2020]
calculate_pearson_correlation(filtered_data )
```


## France


```python
df3=pd.read_excel('FRA.xlsx')
perform_linear_regression(df3,'France')
```


```python
calculate_pearson_correlation(df3)
```


```python
filtered_data = df3[df3['TIME'].dt.year < 2016]
calculate_pearson_correlation(filtered_data)
```


```python
filtered_data1 = df3[(df3['TIME'].dt.year >= 2016) & (df3['TIME'].dt.year < 2019)]
calculate_pearson_correlation(filtered_data1)
```


```python
filtered_data2 = df3[df3['TIME'].dt.year >= 2019]
calculate_pearson_correlation(filtered_data2)
```


## Britain


```python
df4=pd.read_excel('GBR.xlsx')
perform_linear_regression(df4,'United Kingdom')
```


```python
calculate_pearson_correlation(df4)
```


```python
filtered_data = df4[df4['TIME'].dt.year < 2016]
calculate_pearson_correlation(filtered_data)
```


```python
filtered_data = df4[(df4['TIME'].dt.year >= 2016)&(df4['TIME'].dt.year < 2017)]
calculate_pearson_correlation(filtered_data)
```


```python
filtered_data = df4[(df4['TIME'].dt.year >= 2017)&(df4['TIME'].dt.year < 2022)]
calculate_pearson_correlation(filtered_data)
```


```python
filtered_data1 = df4[df4['TIME'].dt.year >= 2022]
calculate_pearson_correlation(filtered_data1)
```


## India


```python
df5=pd.read_excel('IND.xlsx')
perform_linear_regression(df5,'India')
```


```python
calculate_pearson_correlation(df5)
```


```python
filtered_data = df5[df5['TIME'].dt.year < 2017]
calculate_pearson_correlation(filtered_data)
```


```python
filtered_data1 = df5[(df5['TIME'].dt.year >= 2017) & (df5['TIME'].dt.year < 2019)]
calculate_pearson_correlation(filtered_data1)
```


```python
filtered_data2= df5[df5['TIME'].dt.year >= 2019]
calculate_pearson_correlation(filtered_data2)
```


## Italy


```python
df6=pd.read_excel('ITA.xlsx')
perform_linear_regression(df6,'Italy')
```


```python
calculate_pearson_correlation(df6)
```


```python
filtered_data = df6[df6['TIME'].dt.year < 2017]
calculate_pearson_correlation(filtered_data)
```


```python
filtered_data1 = df6[(df6['TIME'].dt.year >= 2017) & (df6['TIME'].dt.year < 2018)]
calculate_pearson_correlation(filtered_data1)
```


```python
filtered_data2 = df6[df6['TIME'].dt.year >= 2018]
calculate_pearson_correlation(filtered_data2)
``` 


## Japan


```python
df7=pd.read_excel('JPN.xlsx')
perform_linear_regression(df7,'Japan')
```


```python
calculate_pearson_correlation(df7)
```


```python
filtered_data = df7[(df7['TIME'].dt.year >= 2017) & (df6['TIME'].dt.year < 2019)]
calculate_pearson_correlation(filtered_data)
```


```python
filtered_data1 = df7[df7['TIME'].dt.year >= 2019]
calculate_pearson_correlation(filtered_data1)
```


## South Korea


```python
df8=pd.read_excel('KOR.xlsx')
perform_linear_regression(df8,'South Korea')
```


```python
calculate_pearson_correlation(df8)
```


```python
filtered_data = df8[df8['TIME'].dt.year < 2021]
calculate_pearson_correlation(filtered_data)
```


```python
filtered_data1 = df8[df8['TIME'].dt.year >= 2021]
calculate_pearson_correlation(filtered_data1)
```


## Russia 


```python
df9=pd.read_excel('RUS.xlsx')
perform_linear_regression(df9,'Russia')
```


```python
filtered_data = df9[df9['TIME'].dt.year > 2020]
calculate_pearson_correlation(filtered_data)
```

