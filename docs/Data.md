# Code
## Import pacakages



```python
import requests
import pandas as pd
import plotly.express as px
import matplotlib.pyplot as plt
from plotnine import *
```

## Data Collection
### Exchange Rate API


```python

def get_exchange_rates(start_date, end_date, base_currency, target_currency):
    url = "https://api.apilayer.com/exchangerates_data/timeseries"
    headers = {
        "apikey": "WE love DS105"
    }
    rates = {}
    year = pd.Timedelta(days=365)
    query_date = pd.to_datetime(end_date)
    while query_date >= pd.to_datetime(start_date):
        # Set the start and end dates for the current year
        current_year_start = (query_date - year).strftime('%Y-%m-%d')
        current_year_end = query_date.strftime('%Y-%m-%d')
        params = {'access_key': 'WE love DS105',
                  'start_date': current_year_start,
                  'end_date': current_year_end,
                  'base': base_currency,
                  'symbols': target_currency}
        try:
            response = requests.get(url, params=params, headers=headers)
            response.raise_for_status()
            data = response.json()
            rates.update(data['rates'])
        except requests.exceptions.RequestException as e:
            print("Error: ", e)
        query_date -= year
    # Create a DataFrame from the rates dictionary
    df = pd.DataFrame.from_dict(rates, orient='index')
    return df

df_CNY = get_exchange_rates('2013-12-31','2022-12-31','CNY','USD')
df_CAD = get_exchange_rates('2013-12-31','2022-12-31','CAD','USD')
df_EUR = get_exchange_rates('2013-12-31','2022-12-31','EUR','USD')
df_GBP = get_exchange_rates('2013-12-31','2022-12-31','CNY','USD')
df_JPY = get_exchange_rates('2013-12-31','2022-12-31','JPY','USD')
df_KRW = get_exchange_rates('2013-12-31','2022-12-31','KRW','USD')
df_INR = get_exchange_rates('2013-12-31','2022-12-31','INR','USD')
df_RUB = get_exchange_rates('2013-12-31','2022-12-31','RUB','USD')
```

## Data Cleaning + Preprocessing
### Exchange Rate - Monthly Average 


```python
# Define a function to calculate the monthly average
def monthly_average(df):
    df.index = pd.to_datetime(df.index)
    monthly_average = df.resample('M').mean()
    monthly_average = monthly_average.reset_index(drop=False)
    return monthly_average

monthly_average_CAD=monthly_average(df_CAD)
monthly_average_CNY=monthly_average(df_CNY)
monthly_average_EUR=monthly_average(df_EUR)
monthly_average_GBP=monthly_average(df_GBP)
monthly_average_JPY=monthly_average(df_JPY)
monthly_average_INR=monthly_average(df_INR)
monthly_average_KRW=monthly_average(df_KRW)
monthly_average_RUB=monthly_average(df_RUB)
```

### Inflation Rate


```python
df= pd.read_csv('DP_LIVE_05032023170628727.csv')
# Convert the 'Time' column to datetime format
df['TIME'] = pd.to_datetime(df['TIME'])

# Select rows with 'CHN', 'FRA', 'CAN', 'JPN', 'KOR', 'GBR', 'USA', 'IND', 'RUS', 'DEU' country codes and a timestamp between 2013 and 2022
mask = (df['LOCATION'].isin(['CHN','FRA','CAN','JPN','KOR','GBR','USA','IND','RUS','DEU','ITA'])) & (df['TIME'].dt.year >= 2013) & (df['TIME'].dt.year <= 2022)
CPI_data = df.loc[mask]

# Drop the columns that aren't needed
CPI_data=CPI_data.drop(['INDICATOR','SUBJECT','MEASURE','FREQUENCY','Flag Codes'],axis=1)
```

### Reshaping Data
#### Separate data by country for visualization


```python
df1=CPI_data

def country_data(df, country_code, exchange_rate_df):
    # Filter the data frame to only include rows with the specified country code
    mask = df['LOCATION'] == country_code
    country_data = df.loc[mask].reset_index(drop=True)
    
    exchange_rate_df = exchange_rate_df.reset_index(drop=True)
    
    country_data = pd.concat([country_data, exchange_rate_df], axis=1)
    
    return country_data
```


```python
# Create a data frame for each country
df_CHN=country_data(df1,'CHN',monthly_average_CNY)
df_CAN=country_data(df1,'CAN',monthly_average_CAD)
df_FRA=country_data(df1,'FRA',monthly_average_EUR)
df_ITA=country_data(df1,'ITA',monthly_average_EUR)
df_DEU=country_data(df1,'DEU',monthly_average_EUR)
df_GBR=country_data(df1,'GBR',monthly_average_GBP)
df_IND=country_data(df1,'IND',monthly_average_INR)
df_JPN=country_data(df1,'JPN',monthly_average_JPY)
df_RUS=country_data(df1,'RUS',monthly_average_RUB)
df_KOR=country_data(df1,'KOR',monthly_average_KRW)

# US as the reference
mask = df1['LOCATION'] == 'USA'
df_USA= df1.loc[mask]
```

#### Yearly data for modeling


```python
# Create an empty dictionary to store the new dataframes
yearly_dfs = {}

df_list = [df_CHN, df_USA, df_FRA, df_DEU, df_ITA, df_IND, df_RUS, df_GBR, df_CAN, df_KOR, df_JPN]

for df in df_list:
    df.loc[:, 'TIME'] = pd.to_datetime(df.loc[:, 'TIME'])

# Loop through each year from 2013 to 2022
for year in range(2013, 2023):
    # Create a list to store the dataframes for the current year
    dfs_for_year = []
    # Loop through each original dataframe
    for df_name in ['df_CHN', 'df_FRA', 'df_DEU', 'df_ITA', 'df_IND', 'df_RUS', 'df_GBR', 'df_CAN', 'df_KOR','df_JPN']:
        # Extract the year from the TIME column and select only the rows for the current year
        df_for_year = globals()[df_name][globals()[df_name]['TIME'].dt.year == year]
        # Append the dataframe to the list
        dfs_for_year.append(df_for_year)
    # Concatenate all the dataframes for the current year into a single dataframe
    yearly_dfs[str(year)] = pd.concat(dfs_for_year, ignore_index=True)

# Access the new dataframes using their year as a key
df_2013=yearly_dfs['2013']  # dataframe for 2013
df_2014=yearly_dfs['2014']
df_2015=yearly_dfs['2015']
df_2016=yearly_dfs['2016']
df_2017=yearly_dfs['2017']
df_2018=yearly_dfs['2018']
df_2019=yearly_dfs['2019']
df_2020=yearly_dfs['2020']
df_2021=yearly_dfs['2021']
df_2022=yearly_dfs['2022']
```

## Data Visualization
### Inflation Map


```python
mask = (df1['TIME'].dt.year == 2022)
df_CPI = df1.loc[mask]
df_CPI = df_CPI.groupby('LOCATION').mean()
#df_CPI = df_CPI.resample('Y', on='TIME').mean()
# change the index to 'Country'
df_CPI = df_CPI.reset_index()
df_CPI = df_CPI.rename(columns={'LOCATION':'Country', 'Value':'CPI'})
# change the country name to full name
df_CPI['Country'] = df_CPI['Country'].replace(['CHN', 'GBR', 'USA','CAN','DEU','FRA','IND','ITA','JPN','KOR','RUS'], ['China', 'United Kingdom', 'United States','Canada','Germany','France','India','Italy','Japan','Korea','Russia'])
```


```python
# Create a choropleth map with the CPI values
fig = px.choropleth(df_CPI, locations='Country', locationmode='country names',
                    color='CPI', range_color=(0, 10),
                    title='2022 Average Consumer Price Index(CPI) by Country')

# Show the map
fig.show()
```

### Line Chart
#### Overall trend


```python
merged_df = pd.concat(yearly_dfs.values())

# Create a line plot of the exchange rate over time
p1 = ggplot(merged_df, aes(x='TIME', y='Exchange Rate', color='LOCATION')) + geom_line() + labs(title='Exchange rate', x='Time', y='Exchange rate') + scale_color_discrete(name='Country') + theme_classic() +  scale_x_datetime(date_labels='%Y')

# Create a line plot of the CPI over time
p2 = ggplot(df1, aes(x='TIME', y='Value', color='LOCATION')) + geom_line() + labs(title='Inflation', x='Time', y='CPI') + scale_color_discrete(name='Country') + theme_classic() +  scale_x_datetime(date_labels='%Y')
```

#### Country trend


```python
# Define a function to plot the exchange rate and CPI for a given country
def plot_exchange_rate(df, title):
    fig,ax=plt.subplots()
    ax.plot(df.TIME, df['USD'], color='#4169E1')
    ax.set_xlabel('TIME',fontsize=14)
    ax.set_ylabel('Exchange rate', color='#4169E1', fontsize=16)
    ax2=ax.twinx()
    ax2.plot(df.TIME, df.Value, color='#CD5C5C')
    ax2.set_ylabel('CPI', color='#CD5C5C', fontsize=16)
    plt.title(title, fontsize=20)
    plt.show()


plot_exchange_rate(df_CHN,'Exchange rate and CPI in China')
plot_exchange_rate(df_CAN,'Exchange rate and CPI in Canada')
plot_exchange_rate(df_FRA,'Exchange rate and CPI in France')
plot_exchange_rate(df_ITA,'Exchange rate and CPI in Italy')
plot_exchange_rate(df_DEU,'Exchange rate and CPI in Germany')
plot_exchange_rate(df_GBR,'Exchange rate and CPI in UK')
plot_exchange_rate(df_IND,'Exchange rate and CPI in India')
plot_exchange_rate(df_JPN,'Exchange rate and CPI in Japan')
plot_exchange_rate(df_RUS,'Exchange rate and CPI in Russia')
plot_exchange_rate(df_KOR,'Exchange rate and CPI in South Korea')
```
