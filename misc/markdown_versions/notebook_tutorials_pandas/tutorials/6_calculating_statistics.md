# File path: ./notebook_tutorials_pandas/tutorials/6_calculating_statistics.ipynb



```python
import pandas as pd

titanic = pd.read_csv("../data/titanic.csv")

```


```python
titanic.head()
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




## Aggregating statistics
![image.png](6_calculating_statistics_files/97a4c970-90e5-4b58-9408-f19cefaa5a31.png)

Can we find the average (mean) age of the Titanic Passengers?
* simply apply the mean method 


```python
print("the mean age is: ", (titanic["Age"].mean()))
```

    the mean age is:  29.69911764705882


* Different statistics are avaialble and can be applied to columns with numericaldata. 
* Operations *in general* exclude missing data and operate across rows by default.

![image.png](6_calculating_statistics_files/554d8350-12ea-461d-b4a4-02dc9fe6ef6a.png)

### What is the median age and ticket fare price of the Titanic passengers?


```python
titanic[["Age", "Fare"]].median()
```




    Age     28.0000
    Fare    14.4542
    dtype: float64



* The statistic applied to multiple columns of a `DataFrame` (the selection of two columns returns a `DataFrame`, see the subset data tutorial http://127.0.0.1:8888/lab/tree/notebook_tutorials_pandas/selecting_a_subset_of_df.ipynb
* The aggregating statistic can be calculated for mulitple columns at the same time. Remember the `describe` function from the first tutorial? 




```python
titanic[["Age","Fare"]].describe()
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
      <th>Age</th>
      <th>Fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>714.000000</td>
      <td>891.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>29.699118</td>
      <td>32.204208</td>
    </tr>
    <tr>
      <th>std</th>
      <td>14.526497</td>
      <td>49.693429</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.420000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>20.125000</td>
      <td>7.910400</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>28.000000</td>
      <td>14.454200</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>38.000000</td>
      <td>31.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>80.000000</td>
      <td>512.329200</td>
    </tr>
  </tbody>
</table>
</div>



Also, instead of using the predefined stats, we can honein on specific combos of aggregating stats for given columns using DataFrame.agg() method. 



For example: 



```python
titanic.agg(
    {
        "Age":["min","max","median","skew"],
        "Fare":["min","max","median","mean"]
    }
)
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
      <th>Age</th>
      <th>Fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>min</th>
      <td>0.420000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>80.000000</td>
      <td>512.329200</td>
    </tr>
    <tr>
      <th>median</th>
      <td>28.000000</td>
      <td>14.454200</td>
    </tr>
    <tr>
      <th>skew</th>
      <td>0.389108</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>NaN</td>
      <td>32.204208</td>
    </tr>
  </tbody>
</table>
</div>



Details about descriptive statistics are provided in the user guide section on <a href="https://pandas.pydata.org/docs/user_guide/basics.html#basics-stats">  descriptive statistics.</a>

## Aggregating statistics grouped by category
![image.png](6_calculating_statistics_files/177aa726-ce16-430a-bfd5-bfa9fce328bc.png)

### What is the average age for male versus female Titanic passengers?


```python
titanic[["Sex","Age"]].groupby("Sex").mean()
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
      <th>Age</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>27.915709</td>
    </tr>
    <tr>
      <th>male</th>
      <td>30.726645</td>
    </tr>
  </tbody>
</table>
</div>



As our interest is the average age for each gender, a subselection on these two cols is made first:
> `titanic[["Sex","Age"]]`.

Next, the `groupby()` method is applied on the `Sex` column to make a group per category, separated by sex. 
> Then, the average age for each category is calculated and returned.

Calculating a given statistic (e.g. `mean` age) for each category in a column (e.g. male/female in the `Sex` column) is a common pattern. The `groupby` method is used to support these type of operations. This fits in the more general split-apply-combine pattern:

* **Split** the data into groups

* **Apply** a function to each group independently

* **Combine** the results into a data structure

The apply and combine steps are typically done together in pandas.

In the previous example, we explicitly selected the 2 columns first. If not, the `mean` method is applied to each column containing numerical columns by passing `numeric_only=True`:


```python
titanic.groupby("Sex").mean(numeric_only=True)
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Fare</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>431.028662</td>
      <td>0.742038</td>
      <td>2.159236</td>
      <td>27.915709</td>
      <td>0.694268</td>
      <td>0.649682</td>
      <td>44.479818</td>
    </tr>
    <tr>
      <th>male</th>
      <td>454.147314</td>
      <td>0.188908</td>
      <td>2.389948</td>
      <td>30.726645</td>
      <td>0.429809</td>
      <td>0.235702</td>
      <td>25.523893</td>
    </tr>
  </tbody>
</table>
</div>




```python

# Another example. 
titanic[["Age","Sex","Fare","Survived"]].groupby("Sex").mean(numeric_only=True)
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
      <th>Age</th>
      <th>Fare</th>
      <th>Survived</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>27.915709</td>
      <td>44.479818</td>
      <td>0.742038</td>
    </tr>
    <tr>
      <th>male</th>
      <td>30.726645</td>
      <td>25.523893</td>
      <td>0.188908</td>
    </tr>
  </tbody>
</table>
</div>



It does not make much sense to get the average value of the `Pclass`. If we are only interested in the average age for each gender, the selection of columns (rectangular brackets `[]` as usual) is supported on the grouped data as well:


```python
titanic.groupby("Sex")["Age"].mean()
```




    Sex
    female    27.915709
    male      30.726645
    Name: Age, dtype: float64



![image.png](6_calculating_statistics_files/d7055f95-7670-4682-a8d8-85b33eb3c2bf.png)

The `Pclass` column contains numerical data but actually represents 3 categories (or factors) with respectively the labels ‘1’, ‘2’ and ‘3’. Calculating statistics on these does not make much sense. Therefore, pandas provides a `Categorical` data type to handle this type of data. More information is provided in the user guide <a href="https://pandas.pydata.org/docs/user_guide/categorical.html#categorical"> Categorical Data</a> section.

## Now, what is the mean ticket fare price for each of the sex and cabin class combinations?



```python
titanic.groupby(["Sex", "Pclass"])["Fare"].mean()
```




    Sex     Pclass
    female  1         106.125798
            2          21.970121
            3          16.118810
    male    1          67.226127
            2          19.741782
            3          12.661633
    Name: Fare, dtype: float64



##### As you can see, grouping can be done by multiple columns at the same time. Provide the column names as a list to the `groupby()` method.
A full description on the split-apply-combine approach is provided in the user guide section on <a href="https://pandas.pydata.org/docs/user_guide/groupby.html#groupby">groupby operations</a>.

## Count number of records by category

![image.png](6_calculating_statistics_files/d0126f8b-9b83-4a2b-8758-816dec717b75.png)



### What is the number of passengers in each of the cabin classes? 


```python
titanic["Pclass"].value_counts()
```




    Pclass
    3    491
    1    216
    2    184
    Name: count, dtype: int64



##### The `value_counts()` method counts the number of records for each category in a column.

> The function is a shortcut, as it is actually a groupby operation in combination with counting of the number of records within each group:


```python
titanic.groupby("Pclass")["Pclass"].count()
```




    Pclass
    1    216
    2    184
    3    491
    Name: Pclass, dtype: int64



#### Note:
* Both `size` and `count` can be used in combination with `groupby`.
* Whereas, `size` includes  `NaN` values and just provides the number of rows (size of the table)
* `count` excludes the missing values.
* In the `value_count` method, use the `dropna` argument to include or exclude the `NaN` values.

The user guide has a dedicated section on `value_counts` , see the page on <a href="https://pandas.pydata.org/docs/user_guide/basics.html#basics-discretization"> discretization</a>.

# REMEMBER
> * Aggregation statistics can be calculated on entire columns & rows.
> * `groupby` provides the power of the **split-apply-combine** pattern.
> * `value_counts` is a convenient shortcut to count the number of entries in each category of a variable. 


```python

```
