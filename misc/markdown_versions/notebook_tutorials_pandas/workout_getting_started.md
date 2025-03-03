# File path: ./notebook_tutorials_pandas/workout_getting_started.ipynb


Welcome to your **hands-on** Pandas workout! This worksheet will guide you through **core Pandas skills**, all derived from the tutorials you’ve just studied. 

**Happy Data Wrangling!** 🎉

**Enjoy your worksheet!** Feel free to adapt any steps based on your actual dataset’s needs (e.g., skip time series if no date column exists). Above all, **have fun** exploring and remember: **the best way to learn Pandas is by doing**!

## 💡 Step 0: Choose & Download a Dataset
Head over to the **[Google Dataset Search Engine](https://datasetsearch.research.google.com/)** and pick a dataset that intrigues you! Aim for a **CSV or Excel** file with **at least a few columns**—and ideally one or two interesting features to explore.

> **Suggested Datasets (Just Ideas!)**  
> - **World Happiness Report**  
> - **Global Earthquakes** (USGS)  
> - **IMDb Movies / TV Shows**  
> - **Weather Data** (NOAA)  
> - **Spotify / Music Streaming** Statistics  
>
> Feel free to pick **any** dataset that piques your curiosity—just make sure it’s not **Titanic** or **Air Quality** so you can practice on something fresh!

## 📥 Step 1: Import Pandas & Load Your Data
1. Import **pandas** (as `pd`) and optionally **matplotlib** for plotting.
2. Load your dataset using either `pd.read_csv(...)` or `pd.read_excel(...)`.
3. Preview the **first few rows** with `.head()`, and **last few rows** with `.tail()`.

<details>
<summary>Example Code Snippet</summary>

```python
import pandas as pd
import matplotlib.pyplot as plt  # optional, only if you plan to do plots

# Replace the file name/path below with your actual data
df = pd.read_csv("your_dataset.csv")

df.head()

```



```python
import pandas as pd
import matplotlib as plt
```


```python
ave_prices = pd.read_csv("../data/Average-prices-2024-07.csv")

```


```python
ave_prices.head()
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
      <th>Date</th>
      <th>Region_Name</th>
      <th>Area_Code</th>
      <th>Average_Price</th>
      <th>Monthly_Change</th>
      <th>Annual_Change</th>
      <th>Average_Price_SA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1968-04-01</td>
      <td>Northern Ireland</td>
      <td>N92000001</td>
      <td>3661.485500</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1968-04-01</td>
      <td>England</td>
      <td>E92000001</td>
      <td>3408.108064</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1968-04-01</td>
      <td>Wales</td>
      <td>W92000004</td>
      <td>2885.414162</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1968-04-01</td>
      <td>Scotland</td>
      <td>S92000003</td>
      <td>2844.980688</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1968-04-01</td>
      <td>London</td>
      <td>E12000007</td>
      <td>4418.489911</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
ave_prices.tail()
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
      <th>Date</th>
      <th>Region_Name</th>
      <th>Area_Code</th>
      <th>Average_Price</th>
      <th>Monthly_Change</th>
      <th>Annual_Change</th>
      <th>Average_Price_SA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>142195</th>
      <td>2024-07-01</td>
      <td>Caerphilly</td>
      <td>W06000018</td>
      <td>191369.0</td>
      <td>0.3</td>
      <td>4.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>142196</th>
      <td>2024-07-01</td>
      <td>Blaenau Gwent</td>
      <td>W06000019</td>
      <td>131157.0</td>
      <td>-2.5</td>
      <td>3.1</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>142197</th>
      <td>2024-07-01</td>
      <td>England and Wales</td>
      <td>K04000001</td>
      <td>301172.0</td>
      <td>0.2</td>
      <td>1.6</td>
      <td>296273.0</td>
    </tr>
    <tr>
      <th>142198</th>
      <td>2024-07-01</td>
      <td>Great Britain</td>
      <td>K03000001</td>
      <td>292495.0</td>
      <td>0.6</td>
      <td>2.2</td>
      <td>287077.0</td>
    </tr>
    <tr>
      <th>142199</th>
      <td>2024-07-01</td>
      <td>United Kingdom</td>
      <td>K02000001</td>
      <td>289723.0</td>
      <td>0.6</td>
      <td>2.2</td>
      <td>284433.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
ave_prices.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 142200 entries, 0 to 142199
    Data columns (total 7 columns):
     #   Column            Non-Null Count   Dtype  
    ---  ------            --------------   -----  
     0   Date              142200 non-null  object 
     1   Region_Name       142200 non-null  object 
     2   Area_Code         142200 non-null  object 
     3   Average_Price     142200 non-null  float64
     4   Monthly_Change    141776 non-null  float64
     5   Annual_Change     137388 non-null  float64
     6   Average_Price_SA  4989 non-null    float64
    dtypes: float64(4), object(3)
    memory usage: 7.6+ MB



```python
ave_prices.describe()
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
      <th>Average_Price</th>
      <th>Monthly_Change</th>
      <th>Annual_Change</th>
      <th>Average_Price_SA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1.422000e+05</td>
      <td>141776.000000</td>
      <td>137388.000000</td>
      <td>4989.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1.785838e+05</td>
      <td>0.544986</td>
      <td>6.307396</td>
      <td>167574.205414</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.218362e+05</td>
      <td>1.955980</td>
      <td>8.745112</td>
      <td>88186.645899</td>
    </tr>
    <tr>
      <th>min</th>
      <td>2.712016e+03</td>
      <td>-30.297781</td>
      <td>-35.786566</td>
      <td>40405.313840</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.005275e+05</td>
      <td>-0.446124</td>
      <td>1.242361</td>
      <td>116567.964000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.545933e+05</td>
      <td>0.500000</td>
      <td>5.361429</td>
      <td>156422.914300</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2.252271e+05</td>
      <td>1.478041</td>
      <td>10.408504</td>
      <td>209484.507200</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.531416e+06</td>
      <td>35.286646</td>
      <td>98.437940</td>
      <td>534253.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
ave_prices.dtypes
```




    Date                 object
    Region_Name          object
    Area_Code            object
    Average_Price       float64
    Monthly_Change      float64
    Annual_Change       float64
    Average_Price_SA    float64
    dtype: object



## 🔍 Step 3: Selecting Data (Subsets of Rows & Columns)

1.  **Select a single column** (e.g., `df["ColumnName"]`).
2.  **Select multiple columns** at once (e.g., `df[["ColA", "ColB"]]`).
3.  Use **boolean indexing** to filter rows (e.g., `df[df["ColA"] > 100]`).
4.  Try combining conditions with `&` (AND) or `|` (OR).

-   Use **`.loc[]`** or **`.iloc[]`** to grab a specific subset, e.g., rows 10–20 and columns 2–4.
-   Find all rows that match a certain condition (e.g., a specific category or numeric threshold).


```python
ave_prices["Region_Name"]
```




    0          Northern Ireland
    1                   England
    2                     Wales
    3                  Scotland
    4                    London
                    ...        
    142195           Caerphilly
    142196        Blaenau Gwent
    142197    England and Wales
    142198        Great Britain
    142199       United Kingdom
    Name: Region_Name, Length: 142200, dtype: object




```python
ave_prices[["Region_Name", "Average_Price"]]
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
      <th>Region_Name</th>
      <th>Average_Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Northern Ireland</td>
      <td>3661.485500</td>
    </tr>
    <tr>
      <th>1</th>
      <td>England</td>
      <td>3408.108064</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wales</td>
      <td>2885.414162</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Scotland</td>
      <td>2844.980688</td>
    </tr>
    <tr>
      <th>4</th>
      <td>London</td>
      <td>4418.489911</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>142195</th>
      <td>Caerphilly</td>
      <td>191369.000000</td>
    </tr>
    <tr>
      <th>142196</th>
      <td>Blaenau Gwent</td>
      <td>131157.000000</td>
    </tr>
    <tr>
      <th>142197</th>
      <td>England and Wales</td>
      <td>301172.000000</td>
    </tr>
    <tr>
      <th>142198</th>
      <td>Great Britain</td>
      <td>292495.000000</td>
    </tr>
    <tr>
      <th>142199</th>
      <td>United Kingdom</td>
      <td>289723.000000</td>
    </tr>
  </tbody>
</table>
<p>142200 rows × 2 columns</p>
</div>




```python
ave_prices[ave_prices["Average_Price"]>200000]
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
      <th>Date</th>
      <th>Region_Name</th>
      <th>Area_Code</th>
      <th>Average_Price</th>
      <th>Monthly_Change</th>
      <th>Annual_Change</th>
      <th>Average_Price_SA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6615</th>
      <td>1995-10-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>200005.8308</td>
      <td>1.501157</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7341</th>
      <td>1995-12-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>200722.0684</td>
      <td>0.524405</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8797</th>
      <td>1996-04-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>201218.2139</td>
      <td>1.894697</td>
      <td>9.252678</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9150</th>
      <td>1996-05-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>202340.5680</td>
      <td>0.557780</td>
      <td>5.675156</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9854</th>
      <td>1996-07-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>207443.2875</td>
      <td>4.063483</td>
      <td>4.788751</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>142192</th>
      <td>2024-07-01</td>
      <td>Vale of Glamorgan</td>
      <td>W06000014</td>
      <td>292562.0000</td>
      <td>-3.300000</td>
      <td>-1.500000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>142193</th>
      <td>2024-07-01</td>
      <td>Cardiff</td>
      <td>W06000015</td>
      <td>272349.0000</td>
      <td>1.100000</td>
      <td>3.600000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>142197</th>
      <td>2024-07-01</td>
      <td>England and Wales</td>
      <td>K04000001</td>
      <td>301172.0000</td>
      <td>0.200000</td>
      <td>1.600000</td>
      <td>296273.0</td>
    </tr>
    <tr>
      <th>142198</th>
      <td>2024-07-01</td>
      <td>Great Britain</td>
      <td>K03000001</td>
      <td>292495.0000</td>
      <td>0.600000</td>
      <td>2.200000</td>
      <td>287077.0</td>
    </tr>
    <tr>
      <th>142199</th>
      <td>2024-07-01</td>
      <td>United Kingdom</td>
      <td>K02000001</td>
      <td>289723.0000</td>
      <td>0.600000</td>
      <td>2.200000</td>
      <td>284433.0</td>
    </tr>
  </tbody>
</table>
<p>45645 rows × 7 columns</p>
</div>




```python
ave_prices[(ave_prices["Average_Price"]<200000) & (ave_prices["Region_Name"] == "Kensington and Chelsea")]
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
      <th>Date</th>
      <th>Region_Name</th>
      <th>Area_Code</th>
      <th>Average_Price</th>
      <th>Monthly_Change</th>
      <th>Annual_Change</th>
      <th>Average_Price_SA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3370</th>
      <td>1995-01-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>182694.8326</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3730</th>
      <td>1995-02-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>182345.2463</td>
      <td>-0.191350</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4101</th>
      <td>1995-03-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>182878.8231</td>
      <td>0.292619</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4449</th>
      <td>1995-04-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>184176.9168</td>
      <td>0.709811</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4803</th>
      <td>1995-05-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>191474.1141</td>
      <td>3.962059</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5167</th>
      <td>1995-06-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>197265.7602</td>
      <td>3.024767</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5520</th>
      <td>1995-07-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>197963.3169</td>
      <td>0.353613</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5906</th>
      <td>1995-08-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>198037.4218</td>
      <td>0.037434</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6258</th>
      <td>1995-09-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>197047.8333</td>
      <td>-0.499698</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6991</th>
      <td>1995-11-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>199674.9633</td>
      <td>-0.165429</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7699</th>
      <td>1996-01-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>198311.8840</td>
      <td>-1.200757</td>
      <td>8.548163</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8061</th>
      <td>1996-02-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>195949.6001</td>
      <td>-1.191196</td>
      <td>7.460767</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8412</th>
      <td>1996-03-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>197476.6295</td>
      <td>0.779297</td>
      <td>7.982229</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9505</th>
      <td>1996-06-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>199343.0172</td>
      <td>-1.481438</td>
      <td>1.053025</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
ave_prices.iloc[10:21]
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
      <th>Date</th>
      <th>Region_Name</th>
      <th>Area_Code</th>
      <th>Average_Price</th>
      <th>Monthly_Change</th>
      <th>Annual_Change</th>
      <th>Average_Price_SA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>1968-05-01</td>
      <td>England</td>
      <td>E92000001</td>
      <td>3408.108064</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1968-05-01</td>
      <td>Northern Ireland</td>
      <td>N92000001</td>
      <td>3661.485500</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1968-05-01</td>
      <td>Wales</td>
      <td>W92000004</td>
      <td>2885.414162</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1968-05-01</td>
      <td>Scotland</td>
      <td>S92000003</td>
      <td>2844.980688</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1968-05-01</td>
      <td>Yorkshire and The Humber</td>
      <td>E12000003</td>
      <td>2712.015577</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1968-05-01</td>
      <td>West Midlands Region</td>
      <td>E12000005</td>
      <td>3328.858802</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1968-05-01</td>
      <td>London</td>
      <td>E12000007</td>
      <td>4418.489911</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1968-05-01</td>
      <td>East Midlands</td>
      <td>E12000004</td>
      <td>3025.670615</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1968-05-01</td>
      <td>South West</td>
      <td>E12000009</td>
      <td>3468.159279</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1968-05-01</td>
      <td>United Kingdom</td>
      <td>K02000001</td>
      <td>3594.602239</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1968-06-01</td>
      <td>Scotland</td>
      <td>S92000003</td>
      <td>2844.980688</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
ave_prices.loc[:,"Date"]
```




    0         1968-04-01
    1         1968-04-01
    2         1968-04-01
    3         1968-04-01
    4         1968-04-01
                 ...    
    142195    2024-07-01
    142196    2024-07-01
    142197    2024-07-01
    142198    2024-07-01
    142199    2024-07-01
    Name: Date, Length: 142200, dtype: object




```python
london = ave_prices.loc[ave_prices["Area_Code"].str.startswith("E09")]
london
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
      <th>Date</th>
      <th>Region_Name</th>
      <th>Area_Code</th>
      <th>Average_Price</th>
      <th>Monthly_Change</th>
      <th>Annual_Change</th>
      <th>Average_Price_SA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3351</th>
      <td>1995-01-01</td>
      <td>Tower Hamlets</td>
      <td>E09000030</td>
      <td>59865.18995</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3352</th>
      <td>1995-01-01</td>
      <td>Waltham Forest</td>
      <td>E09000031</td>
      <td>61319.44913</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3353</th>
      <td>1995-01-01</td>
      <td>Kingston upon Thames</td>
      <td>E09000021</td>
      <td>80875.84843</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3354</th>
      <td>1995-01-01</td>
      <td>Lambeth</td>
      <td>E09000022</td>
      <td>67770.98843</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3355</th>
      <td>1995-01-01</td>
      <td>Lewisham</td>
      <td>E09000023</td>
      <td>60491.26109</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>141907</th>
      <td>2024-07-01</td>
      <td>Bexley</td>
      <td>E09000004</td>
      <td>401026.00000</td>
      <td>-1.4</td>
      <td>1.2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>141908</th>
      <td>2024-07-01</td>
      <td>Brent</td>
      <td>E09000005</td>
      <td>513133.00000</td>
      <td>-3.6</td>
      <td>-0.1</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>141909</th>
      <td>2024-07-01</td>
      <td>Bromley</td>
      <td>E09000006</td>
      <td>503529.00000</td>
      <td>1.4</td>
      <td>1.3</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>141910</th>
      <td>2024-07-01</td>
      <td>Camden</td>
      <td>E09000007</td>
      <td>858303.00000</td>
      <td>2.6</td>
      <td>2.8</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>141911</th>
      <td>2024-07-01</td>
      <td>Croydon</td>
      <td>E09000008</td>
      <td>396032.00000</td>
      <td>0.4</td>
      <td>-0.6</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>11715 rows × 7 columns</p>
</div>




```python
high_prices = ave_prices.loc[ave_prices["Average_Price"]>100000]
high_prices.head()
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
      <th>Date</th>
      <th>Region_Name</th>
      <th>Area_Code</th>
      <th>Average_Price</th>
      <th>Monthly_Change</th>
      <th>Annual_Change</th>
      <th>Average_Price_SA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3359</th>
      <td>1995-01-01</td>
      <td>Camden</td>
      <td>E09000007</td>
      <td>120932.8881</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3362</th>
      <td>1995-01-01</td>
      <td>Hammersmith and Fulham</td>
      <td>E09000013</td>
      <td>124902.8602</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3364</th>
      <td>1995-01-01</td>
      <td>City of Westminster</td>
      <td>E09000033</td>
      <td>133025.2772</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3370</th>
      <td>1995-01-01</td>
      <td>Kensington and Chelsea</td>
      <td>E09000020</td>
      <td>182694.8326</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3381</th>
      <td>1995-01-01</td>
      <td>Richmond upon Thames</td>
      <td>E09000027</td>
      <td>109326.1245</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
negative_change = ave_prices.loc[ave_prices['Annual_Change'] < 0]
negative_change
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
      <th>Date</th>
      <th>Region_Name</th>
      <th>Area_Code</th>
      <th>Average_Price</th>
      <th>Monthly_Change</th>
      <th>Annual_Change</th>
      <th>Average_Price_SA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>157</th>
      <td>1969-07-01</td>
      <td>East Midlands</td>
      <td>E12000004</td>
      <td>3159.821224</td>
      <td>1.587302</td>
      <td>-0.461584</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>165</th>
      <td>1969-08-01</td>
      <td>East Midlands</td>
      <td>E12000004</td>
      <td>3159.821224</td>
      <td>1.587302</td>
      <td>-0.461584</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>177</th>
      <td>1969-09-01</td>
      <td>East Midlands</td>
      <td>E12000004</td>
      <td>3159.821224</td>
      <td>1.587302</td>
      <td>-0.461584</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>182</th>
      <td>1969-10-01</td>
      <td>Northern Ireland</td>
      <td>N92000001</td>
      <td>3703.571540</td>
      <td>2.325581</td>
      <td>-5.376344</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>193</th>
      <td>1969-11-01</td>
      <td>Northern Ireland</td>
      <td>N92000001</td>
      <td>3703.571540</td>
      <td>2.325581</td>
      <td>-5.376344</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>142156</th>
      <td>2024-07-01</td>
      <td>Isle of Wight</td>
      <td>E06000046</td>
      <td>274859.000000</td>
      <td>-0.300000</td>
      <td>-2.100000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>142163</th>
      <td>2024-07-01</td>
      <td>Rutland</td>
      <td>E06000017</td>
      <td>377274.000000</td>
      <td>1.000000</td>
      <td>-8.700000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>142173</th>
      <td>2024-07-01</td>
      <td>Torbay</td>
      <td>E06000027</td>
      <td>250339.000000</td>
      <td>-0.500000</td>
      <td>-2.300000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>142176</th>
      <td>2024-07-01</td>
      <td>North Lincolnshire</td>
      <td>E06000013</td>
      <td>180655.000000</td>
      <td>-3.500000</td>
      <td>-0.200000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>142192</th>
      <td>2024-07-01</td>
      <td>Vale of Glamorgan</td>
      <td>W06000014</td>
      <td>292562.000000</td>
      <td>-3.300000</td>
      <td>-1.500000</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>25800 rows × 7 columns</p>
</div>




```python
ave_prices.iloc[10:21,2:5]
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
      <th>Area_Code</th>
      <th>Average_Price</th>
      <th>Monthly_Change</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>E92000001</td>
      <td>3408.108064</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>N92000001</td>
      <td>3661.485500</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>W92000004</td>
      <td>2885.414162</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>S92000003</td>
      <td>2844.980688</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>E12000003</td>
      <td>2712.015577</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>E12000005</td>
      <td>3328.858802</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>E12000007</td>
      <td>4418.489911</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>E12000004</td>
      <td>3025.670615</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>E12000009</td>
      <td>3468.159279</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>K02000001</td>
      <td>3594.602239</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>S92000003</td>
      <td>2844.980688</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
england.plot()
```




    <Axes: >




    
![png](workout_getting_started_files/workout_getting_started_21_1.png)
    



```python
england.plot.hist(bins=20)
```




    <Axes: ylabel='Frequency'>




    
![png](workout_getting_started_files/workout_getting_started_22_1.png)
    



```python
# First, i need to change Date column to datetime format
ave_prices["Date"] = pd.to_datetime(ave_prices["Date"])
```


```python
_2010_2024 = ave_prices.loc[(ave_prices["Date"].dt.year>=2010)&(ave_prices["Date"].dt.year<=2024)]
_2010_2024
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
      <th>Date</th>
      <th>Region_Name</th>
      <th>Area_Code</th>
      <th>Average_Price</th>
      <th>Monthly_Change</th>
      <th>Annual_Change</th>
      <th>Average_Price_SA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>71325</th>
      <td>2010-01-01</td>
      <td>Wales</td>
      <td>W92000004</td>
      <td>127732.6597</td>
      <td>-3.944716</td>
      <td>2.168675</td>
      <td>128754.1867</td>
    </tr>
    <tr>
      <th>71326</th>
      <td>2010-01-01</td>
      <td>Northern Ireland</td>
      <td>N92000001</td>
      <td>135701.4807</td>
      <td>-4.431390</td>
      <td>-3.201716</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>71327</th>
      <td>2010-01-01</td>
      <td>Scotland</td>
      <td>S92000003</td>
      <td>128972.9001</td>
      <td>-3.054670</td>
      <td>3.605994</td>
      <td>129959.1321</td>
    </tr>
    <tr>
      <th>71328</th>
      <td>2010-01-01</td>
      <td>England</td>
      <td>E92000001</td>
      <td>174457.5959</td>
      <td>0.184625</td>
      <td>7.244661</td>
      <td>174872.8599</td>
    </tr>
    <tr>
      <th>71329</th>
      <td>2010-01-01</td>
      <td>Inner London</td>
      <td>E13000001</td>
      <td>324531.4238</td>
      <td>1.851917</td>
      <td>8.967159</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>142195</th>
      <td>2024-07-01</td>
      <td>Caerphilly</td>
      <td>W06000018</td>
      <td>191369.0000</td>
      <td>0.300000</td>
      <td>4.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>142196</th>
      <td>2024-07-01</td>
      <td>Blaenau Gwent</td>
      <td>W06000019</td>
      <td>131157.0000</td>
      <td>-2.500000</td>
      <td>3.100000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>142197</th>
      <td>2024-07-01</td>
      <td>England and Wales</td>
      <td>K04000001</td>
      <td>301172.0000</td>
      <td>0.200000</td>
      <td>1.600000</td>
      <td>296273.0000</td>
    </tr>
    <tr>
      <th>142198</th>
      <td>2024-07-01</td>
      <td>Great Britain</td>
      <td>K03000001</td>
      <td>292495.0000</td>
      <td>0.600000</td>
      <td>2.200000</td>
      <td>287077.0000</td>
    </tr>
    <tr>
      <th>142199</th>
      <td>2024-07-01</td>
      <td>United Kingdom</td>
      <td>K02000001</td>
      <td>289723.0000</td>
      <td>0.600000</td>
      <td>2.200000</td>
      <td>284433.0000</td>
    </tr>
  </tbody>
</table>
<p>70875 rows × 7 columns</p>
</div>




```python
london = _2010_2024.loc[_2010_2024["Area_Code"].str.startswith("E09")]
```


```python
import matplotlib.pyplot as plt
import seaborn as sns

# Set the figure size
plt.figure(figsize=(12,6))

# Get unique region names
regions = london["Region_Name"].unique()

# Use Seaborn color palette for different regions
colors = sns.color_palette("tab10", len(regions))

# Plot each region separately with a unique color
for i, region in enumerate(regions):
    subset = london[london["Region_Name"] == region]
    plt.scatter(subset["Date"], subset["Average_Price"], color=colors[i], label=region, alpha=0.6)

# Labels and title
plt.xlabel("Year")
plt.ylabel("Average Price (£)")
plt.title("Average House Prices in Inner London Regions (2010-2024)")
plt.xticks(rotation=45)
plt.legend(title="Region", bbox_to_anchor=(1.05, 1), loc='upper left')  # Move legend outside plot
plt.grid(True)

plt.show()

```


    
![png](workout_getting_started_files/workout_getting_started_26_0.png)
    



```python
plt.figure(figsize=(12,6))

# Plot as a line graph
for i, region in enumerate(regions):
    subset = london[london["Region_Name"] == region]
    plt.plot(subset["Date"], subset["Average_Price"], marker='o', color=colors[i], label=region, alpha=0.6)

plt.xlabel("Year")
plt.ylabel("Average Price (£)")
plt.title("Average House Prices in Inner London Regions (2010-2024)")
plt.xticks(rotation=45)
plt.legend(title="Region", bbox_to_anchor=(1.05, 1), loc='upper left')
plt.grid(True)

plt.show()

```


    
![png](workout_getting_started_files/workout_getting_started_27_0.png)
    



```python
# Aggregate data to yearly averages
london["Year"] = london["Date"].dt.year  # Extract year
yearly_avg = london.groupby(["Year", "Region_Name"])["Average_Price"].mean().reset_index()

# Plot
plt.figure(figsize=(12,6))

for i, region in enumerate(regions):
    subset = yearly_avg[yearly_avg["Region_Name"] == region]
    plt.plot(subset["Year"], subset["Average_Price"], marker='o', color=colors[i], label=region, alpha=0.6)

plt.xlabel("Year")
plt.ylabel("Average Price (£)")
plt.title("Yearly Average House Prices in Inner London (2010-2024)")
plt.xticks(rotation=45)
plt.legend(title="Region", bbox_to_anchor=(1.05, 1), loc='upper left')
plt.grid(True)

plt.show()

```

    /tmp/ipykernel_10377/613539015.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      london["Year"] = london["Date"].dt.year  # Extract year



    
![png](workout_getting_started_files/workout_getting_started_28_1.png)
    


## ➕ Step 5: Creating & Renaming Columns

1.  **Create a new column** that is derived from existing columns (e.g., a ratio, difference, or sum).
2.  If your dataset has no numeric columns to combine, try a **string** operation (e.g., combining first and last name).
3.  **Rename columns** with `df.rename(columns={"OldName": "NewName"})`.

```python
# Creating a new column based on a formula
df["NewColumn"] = df["ExistingNumColumn"] * 3.14

# Renaming columns
df = df.rename(columns={"OldColumn": "BetterName"})

## 📊 Step 6: Summary Statistics & Grouping

1.  Calculate basic **aggregations** like `.mean()`, `.median()`, or `.count()` on your numeric columns.
2.  Try **grouping** by a categorical column with `.groupby("SomeCategory").mean()`.
3.  Use `.value_counts()` on a categorical column to see the frequency of each category.

-   Which category has the highest **mean** or **count**?
-   Are there any surprising or interesting **groups** in your data?

## ♻️ Step 7: Reshaping (Pivot, Melt) (If Applicable)

If your dataset is “**wide**” or “**long**” and you want to **reshape** it:

1.  Use `df.pivot()` or `df.pivot_table(...)` to transform your data from long to wide format.
2.  Use `df.melt(...)` to go from wide to long format.
3.  If it doesn’t make sense for your current dataset, just read about it for future reference!

-   `pivot_table` can **aggregate** data if you have duplicates or if you want a group-wise summary.
-   `melt` is great for turning multiple columns into a single “value” column with a new “variable” column.


## 🔗 Step 8: Combining Data (Concat & Merge) (Optional)

If you find a **second** dataset on Google that relates to your first one:

1.  Use `pd.concat([df1, df2])` to stack them vertically if they have the **same columns**.
2.  Use `pd.merge(df1, df2, on="common_column")` to join them on a **shared key**.

-   Could you combine your main dataset with a small **lookup table** or metadata?
-   Check out the differences between `"inner"`, `"left"`, `"right"`, or `"outer"` merges.

## ⏰ Step 9: Time Series Fun (If Applicable)

If your dataset contains **dates**:

1.  Convert the date column to **datetime** using `pd.to_datetime()`.
2.  Set the date column as your index with `df.set_index("DateColumn", inplace=True)`.
3.  Try **resampling** or **grouping by** a time component:
    
    ```python
    df.resample("M").mean()  # monthly frequency
    df.resample("W").sum()   # weekly sum
    
    ```
    
4.  Slice by date range (e.g. `df["2021-01":"2021-03"]`).

## 🔤 Step 10: Text Manipulations

If you have **string columns**, try a few **`.str`** operations:

1.  Convert all text to **lowercase**: `df["TextCol"].str.lower()`.
2.  Check if the column **contains** a specific word: `df["TextCol"].str.contains("keyword")`.
3.  **Split** text on a delimiter: `df["TextCol"].str.split(",")`.
4.  **Replace** certain values or strings using `df.replace({"old": "new"})` or `df["TextCol"].str.replace(...)`.

## 💾 Step 11: Exporting Your Cleaned Data

1.  Save your **DataFrame** to a CSV file:
    
    ```python
    df.to_csv("my_cleaned_data.csv", index=False)
    
    ```
    
2.  Or save to an Excel spreadsheet:
    
    ```python
    df.to_excel("my_cleaned_data.xlsx", sheet_name="Sheet1", index=False)
    

## 🎉 Step 12: Wrap-Up & Reflection

-   **What was the most challenging** aspect of working with your dataset?
-   **Which method** or step do you feel you need more practice with?
-   **Any surprising findings** from your data analysis?

> **Congratulations** on completing this worksheet! By practicing each step, you’ve covered the **core Pandas functionalities**:

1.  **Reading & Writing** data
2.  **Selecting & Filtering** data
3.  **Plotting**
4.  **Creating & Renaming** columns
5.  **Summary Stats & Grouping**
6.  **Reshaping** data (pivot, melt)
7.  **Combining** datasets (concat, merge)
8.  **Handling Datetimes**
9.  **Text manipulations**

Now you have a solid foundation to explore **even more** of Pandas and apply your new skills to real-world data challenges!

## 🙌 Next Steps

-   Consider creating visualizations or dashboards using libraries like **Seaborn**, **Plotly**, or **Matplotlib**.
-   Practice making your analyses **repeatable** and **shareable** in a **Jupyter Notebook** or **GitHub repo**.
-   Keep experimenting with new datasets—**the more variety, the better** your skills become.





```python

```
