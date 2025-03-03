# File path: ./notebook_tutorials_pandas/tutorials/9_handling_time_series_data.ipynb

import pandas as pd

import matplotlib.pyplot as plt
```


```python
air_quality = pd.read_csv("../data/air_quality_no2_long.csv")
air_quality.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>country</th>
      <th>date.utc</th>
      <th>location</th>
      <th>parameter</th>
      <th>value</th>
      <th>unit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Paris</td>
      <td>FR</td>
      <td>2019-06-21 00:00:00+00:00</td>
      <td>FR04014</td>
      <td>no2</td>
      <td>20.0</td>
      <td>µg/m³</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Paris</td>
      <td>FR</td>
      <td>2019-06-20 23:00:00+00:00</td>
      <td>FR04014</td>
      <td>no2</td>
      <td>21.8</td>
      <td>µg/m³</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Paris</td>
      <td>FR</td>
      <td>2019-06-20 22:00:00+00:00</td>
      <td>FR04014</td>
      <td>no2</td>
      <td>26.5</td>
      <td>µg/m³</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Paris</td>
      <td>FR</td>
      <td>2019-06-20 21:00:00+00:00</td>
      <td>FR04014</td>
      <td>no2</td>
      <td>24.9</td>
      <td>µg/m³</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Paris</td>
      <td>FR</td>
      <td>2019-06-20 20:00:00+00:00</td>
      <td>FR04014</td>
      <td>no2</td>
      <td>21.4</td>
      <td>µg/m³</td>
    </tr>
  </tbody>
</table>
</div>




```python
air_quality = air_quality.rename(columns={"date.utc":"datetime"})
```


```python
air_quality.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>country</th>
      <th>datetime</th>
      <th>location</th>
      <th>parameter</th>
      <th>value</th>
      <th>unit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Paris</td>
      <td>FR</td>
      <td>2019-06-21 00:00:00+00:00</td>
      <td>FR04014</td>
      <td>no2</td>
      <td>20.0</td>
      <td>µg/m³</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Paris</td>
      <td>FR</td>
      <td>2019-06-20 23:00:00+00:00</td>
      <td>FR04014</td>
      <td>no2</td>
      <td>21.8</td>
      <td>µg/m³</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Paris</td>
      <td>FR</td>
      <td>2019-06-20 22:00:00+00:00</td>
      <td>FR04014</td>
      <td>no2</td>
      <td>26.5</td>
      <td>µg/m³</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Paris</td>
      <td>FR</td>
      <td>2019-06-20 21:00:00+00:00</td>
      <td>FR04014</td>
      <td>no2</td>
      <td>24.9</td>
      <td>µg/m³</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Paris</td>
      <td>FR</td>
      <td>2019-06-20 20:00:00+00:00</td>
      <td>FR04014</td>
      <td>no2</td>
      <td>21.4</td>
      <td>µg/m³</td>
    </tr>
  </tbody>
</table>
</div>




```python
air_quality.city.unique()
```




    array(['Paris', 'Antwerpen', 'London'], dtype=object)



# How to handle time series data with ease
## Using pandas datetime properties

We want to work with the dates in the column `datetime` as datetime objects, and *not* as plain text.


```python
air_quality["datetime"] = pd.to_datetime(air_quality["datetime"])
```


```python
air_quality["datetime"]
```




    0      2019-06-21 00:00:00+00:00
    1      2019-06-20 23:00:00+00:00
    2      2019-06-20 22:00:00+00:00
    3      2019-06-20 21:00:00+00:00
    4      2019-06-20 20:00:00+00:00
                      ...           
    2063   2019-05-07 06:00:00+00:00
    2064   2019-05-07 04:00:00+00:00
    2065   2019-05-07 03:00:00+00:00
    2066   2019-05-07 02:00:00+00:00
    2067   2019-05-07 01:00:00+00:00
    Name: datetime, Length: 2068, dtype: datetime64[ns, UTC]



Initially:
* the values in `datetime` are strings and *do not* provide any datetime operations. (e.g. extract the year, day of the week, etc.)
* By applying the `to_datetime` fucntion, pandas interprets the strings and convert these to datetime (i.e. `datetime64[ns, UTC]`) *objects*.
* In pandas, we call these datetime onjects similar to `datetime.datetime` from the standard library as `pandas.Timestamp`.

#### Note:
* As many datasets *do contain datetime info* in one of the columns, pandas input functions, like `pandas.read_csv()` and `pandas.read_json()` can do the transformation to dates when reading the data using the `parse_dates` parameter with a list of the columns to reas as Timestamp:

```
pd.read_csv("../data/air_quality_no2_long.csv", parse_dates=["datetime"])
```

Why are these `pandas.Timestamp` objects useful? Let’s illustrate the added value with some example cases.

#### What is the start and end date of the time series data set we are working with?




```python
air_quality["datetime"].min(), air_quality["datetime"].max()
```




    (Timestamp('2019-05-07 01:00:00+0000', tz='UTC'),
     Timestamp('2019-06-21 00:00:00+0000', tz='UTC'))



##### Using `pandas.Timestamp` for datetimes enables us to calculate with date information and make them comparable. Therefore, we can use this to get the length of our time series:


```python
air_quality["datetime"].max() - air_quality["datetime"].min()
```




    Timedelta('44 days 23:00:00')



The result is a `pandas.Timedelta`object, similar to `datetime.timedelta` from the standard Python library and defining a _**time duration.**_
The various time concepts supported by pandas are explained in the user guide section on <a href="https://pandas.pydata.org/docs/user_guide/timeseries.html#timeseries-overview">time related concepts</a>.

Let's say that now, we want to create a new column and add it to the `DataFrame`. This column should contain *only* the month of the measurement. 


```python
air_quality["month"] = air_quality["datetime"].dt.month
air_quality.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>country</th>
      <th>datetime</th>
      <th>location</th>
      <th>parameter</th>
      <th>value</th>
      <th>unit</th>
      <th>month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Paris</td>
      <td>FR</td>
      <td>2019-06-21 00:00:00+00:00</td>
      <td>FR04014</td>
      <td>no2</td>
      <td>20.0</td>
      <td>µg/m³</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Paris</td>
      <td>FR</td>
      <td>2019-06-20 23:00:00+00:00</td>
      <td>FR04014</td>
      <td>no2</td>
      <td>21.8</td>
      <td>µg/m³</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Paris</td>
      <td>FR</td>
      <td>2019-06-20 22:00:00+00:00</td>
      <td>FR04014</td>
      <td>no2</td>
      <td>26.5</td>
      <td>µg/m³</td>
      <td>6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Paris</td>
      <td>FR</td>
      <td>2019-06-20 21:00:00+00:00</td>
      <td>FR04014</td>
      <td>no2</td>
      <td>24.9</td>
      <td>µg/m³</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Paris</td>
      <td>FR</td>
      <td>2019-06-20 20:00:00+00:00</td>
      <td>FR04014</td>
      <td>no2</td>
      <td>21.4</td>
      <td>µg/m³</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>



By using `Timestamp` objects for dates, a lot of time-related properties are provided by pandas. For example, the `month`, but also `year`, `quarter`,... All of these properties are accessible by the `dt` accessor. 

An overview of the existing date properties is given in the time and date components overview table. More details about the dt accessor to return datetime like properties are explained in a dedicated section on the dt accessor.

https://pandas.pydata.org/docs/user_guide/timeseries.html#timeseries-components <br>
https://pandas.pydata.org/docs/user_guide/basics.html#basics-dt-accessors

## What is the average concentration for each day of the week for each of the measurement locations?


```python
air_quality.groupby([air_quality["datetime"].dt.weekday, "location"])["value"].mean()
```




    datetime  location          
    0         BETR801               27.875000
              FR04014               24.856250
              London Westminster    23.969697
    1         BETR801               22.214286
              FR04014               30.999359
              London Westminster    24.885714
    2         BETR801               21.125000
              FR04014               29.165753
              London Westminster    23.460432
    3         BETR801               27.500000
              FR04014               28.600690
              London Westminster    24.780142
    4         BETR801               28.400000
              FR04014               31.617986
              London Westminster    26.446809
    5         BETR801               33.500000
              FR04014               25.266154
              London Westminster    24.977612
    6         BETR801               21.896552
              FR04014               23.274306
              London Westminster    24.859155
    Name: value, dtype: float64



Remember the split-apply-combine pattern provided by `groupby` from the tutorial on statistics calculation? Here, we want to calculate a given statistic (e.g. mean *NO<sub>2</sub>*) **for each weekday and for each measurement location**. 

To group on weekdays, we use the datetime property `weekday` (with Monday=0 and Sunday=6) of pandas `Timestamp`, which is also accessible by the `dt` accessor. The grouping on both locations and weekdays can be done to split the calculation of the mean on each of these combinations.

> **⚠️ Danger**  
> As we are working with a very short time series in these examples, the analysis does not provide a long-term representative result!

## Plot the typical NO<sub>2</sub> pattern during the day of our time series of all stations together. In other words, what is the average value for each hour of the day?



```python
fig, axs = plt.subplots(figsize=(12,4))
air_quality.groupby(air_quality["datetime"].dt.hour)["value"].mean().plot(
    kind='bar', rot=0, ax=axs
)
plt.xlabel("Hour of the day")
plt.ylabel("$NO_2 (µg/m^3)$");
```


    
![png](9_handling_time_series_data_files/9_handling_time_series_data_22_0.png)
    


Similar to the previous case, we want to calculate a given statistic  (e.g. mean *NO<sub>2</sub>*) **for each hour of the day** and we can use the split-apply-combine approach again. 

For this case, we use the datetime property `hour` of pandas `Timestamp`, which is also accessible by the `dt` accessor.

## Datetime as index

In the tutorial on reshaping tables, `pivot()` was introduced to reshape the data table with each of the measurements locations as a separate column:



```python
no_2 = air_quality.pivot(index="datetime", columns="location", values="value")
no_2.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>location</th>
      <th>BETR801</th>
      <th>FR04014</th>
      <th>London Westminster</th>
    </tr>
    <tr>
      <th>datetime</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2019-05-07 01:00:00+00:00</th>
      <td>50.5</td>
      <td>25.0</td>
      <td>23.0</td>
    </tr>
    <tr>
      <th>2019-05-07 02:00:00+00:00</th>
      <td>45.0</td>
      <td>27.7</td>
      <td>19.0</td>
    </tr>
    <tr>
      <th>2019-05-07 03:00:00+00:00</th>
      <td>NaN</td>
      <td>50.4</td>
      <td>19.0</td>
    </tr>
    <tr>
      <th>2019-05-07 04:00:00+00:00</th>
      <td>NaN</td>
      <td>61.9</td>
      <td>16.0</td>
    </tr>
    <tr>
      <th>2019-05-07 05:00:00+00:00</th>
      <td>NaN</td>
      <td>72.4</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



> **ℹ️ Note**  
> By pivoting the data, the datetime information became the index of the table. In general, setting a column as an index can be achieved by the `set_index` function.

Working with a datetime index (i.e. `DatetimeIndex`) provides powerful functionalities. For example, we do not need the `dt` accessor to get the time series properties, but have these properties available on the index directly:



```python
no_2.index.year, no_2.index.weekday
```




    (Index([2019, 2019, 2019, 2019, 2019, 2019, 2019, 2019, 2019, 2019,
            ...
            2019, 2019, 2019, 2019, 2019, 2019, 2019, 2019, 2019, 2019],
           dtype='int32', name='datetime', length=1033),
     Index([1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
            ...
            3, 3, 3, 3, 3, 3, 3, 3, 3, 4],
           dtype='int32', name='datetime', length=1033))



Some other advantages are the convenient subsetting of time period or the adapted time scale on plots. Let’s apply this on our data.

### Create a plot of the *NO<sub>2</sub>* values in the different stations from the 20th of May till the end of 21st of May




```python
no_2["2019-05-20":"2019-05-21"].plot();

```


    
![png](9_handling_time_series_data_files/9_handling_time_series_data_28_0.png)
    


By providing a **string that parses to a datetime**, a specific subset of the data can be selected on a `DatetimeIndex`.
More information on the `DatetimeIndex` and the slicing by using strings is provided in the section on <a href="https://pandas.pydata.org/docs/user_guide/timeseries.html#timeseries-datetimeindex">time series indexing.</a>

## Resample a time series to another frequency

Aggregate the current hourly time series values to the monthly maximum value in each of the stations.


```python
monthly_max = no_2.resample("ME").max()
```


```python
monthly_max
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>location</th>
      <th>BETR801</th>
      <th>FR04014</th>
      <th>London Westminster</th>
    </tr>
    <tr>
      <th>datetime</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2019-05-31 00:00:00+00:00</th>
      <td>74.5</td>
      <td>97.0</td>
      <td>97.0</td>
    </tr>
    <tr>
      <th>2019-06-30 00:00:00+00:00</th>
      <td>52.5</td>
      <td>84.7</td>
      <td>52.0</td>
    </tr>
  </tbody>
</table>
</div>



This showcases a very *powerful* method on time series data witha datetime index, which is the ability to `resample()` time series to another frequency (e.g., converting secondly data into 5-minutely data).

The `resample()` method is similar to a `groupby()` operation.

* it provides a time-based grouping, by using a string (e.g. `M`, `5H`,...) that defines the target frequency
* it requires an aggregation function such as mean, max,...

An overview of the aliases used to define time series frequencies is given in the offset aliases overview table. <br>
https://pandas.pydata.org/docs/user_guide/timeseries.html#timeseries-offset-aliases

When defined,  the frequency of the time series is provided by the `freq` attribute:


```python
monthly_max.index.freq
```




    <MonthEnd>



Make a plot of the daily mean NO<sub>2</sub> value in each of the stations.


```python
no_2.resample("D").mean().plot(style="-o", figsize=(10, 5));

```


    
![png](9_handling_time_series_data_files/9_handling_time_series_data_35_0.png)
    


More details on the power of time series resampling is provided in the user guide section on resampling. <br> https://pandas.pydata.org/docs/user_guide/timeseries.html#timeseries-resampling

## REMEMBER: 
* Valid date strings can be converted to datetime objects using `to_datetime` funct or as part of read functs.
* Datetime objects in pandas support calculations, logical operations and convenient date-related properties using the `dt` accessor.
* A `DatetimeIndex` contains these date-related properties  and supports convenient slicing.
* `resample()` is a powerful method to change the frequency of a time series. 


```python

```
