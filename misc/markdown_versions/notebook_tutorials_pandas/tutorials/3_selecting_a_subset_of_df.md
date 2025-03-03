# File path: ./notebook_tutorials_pandas/tutorials/3_selecting_a_subset_of_df.ipynb

import pandas as pd
```

This tutorial uses the Titanic data set, stored as CSV. The data consists of the following data columns:

* PassengerId: Id of every passenger.

* Survived: Indication whether passenger survived. 0 for yes and 1 for no.

* Pclass: One out of the 3 ticket classes: Class 1, Class 2 and Class 3.

* Name: Name of passenger.

* Sex: Gender of passenger.

* Age: Age of passenger in years.

* SibSp: Number of siblings or spouses aboard.

* Parch: Number of parents or children aboard.

* Ticket: Ticket number of passenger.

* Fare: Indicating the fare.

* Cabin: Cabin number of passenger.

* Embarked: Port of embarkation.


```python
titanic = pd.read_csv("../data/titanic.csv")
titanic.head() # note that i have named the DataFrame 'tc' for 'titanic'

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



## How do I select a subset of a DataFrame?
#### How do I select specific columns from a DataFrame?

![image.png](3_selecting_a_subset_of_df_files/ac9535f8-e975-4e4d-bb3d-bf5c4c5d6f42.png)

I’m interested in the age of the Titanic passengers.


```python
ages = titanic["Age"]
print(ages)
```

    0      22.0
    1      38.0
    2      26.0
    3      35.0
    4      35.0
           ... 
    886    27.0
    887    19.0
    888     NaN
    889    26.0
    890    32.0
    Name: Age, Length: 891, dtype: float64


To select a single column, use square brackets [] with the column name of the column of interest. 
Each column in a DataFrame is a Series. As a single column is selected, the returned object is a pandas Series. We can verify this by checking the type of the output:


```python
type(ages)
```




    pandas.core.series.Series



And we can have a look at the shape of the output:


```python
ages.shape
```




    (891,)



`DataFrame.shape` is an attribute of a pandas Series and DataFrame, containing the number of rows and columns (nrows, ncolumns). 

A pandas `Series` is a 1-D data constructand so *only* the number of rows is returned 

I’m interested in the age and sex of the Titanic passengers.


```python
age_sex = titanic[["Age","Sex"]]
```


```python
age_sex.head(7)
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
      <th>Sex</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>22.0</td>
      <td>male</td>
    </tr>
    <tr>
      <th>1</th>
      <td>38.0</td>
      <td>female</td>
    </tr>
    <tr>
      <th>2</th>
      <td>26.0</td>
      <td>female</td>
    </tr>
    <tr>
      <th>3</th>
      <td>35.0</td>
      <td>female</td>
    </tr>
    <tr>
      <th>4</th>
      <td>35.0</td>
      <td>male</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>male</td>
    </tr>
    <tr>
      <th>6</th>
      <td>54.0</td>
      <td>male</td>
    </tr>
  </tbody>
</table>
</div>



To select *multiple columns*, **use a list of column names** within the selection brackets []

Note: The inner square brackets define a Python list with column names, whereas the outer brackets are used to select the data from a pandas DataFrame as seen in the previous example.


```python
type(titanic[["Age", "Sex"]])
```




    pandas.core.frame.DataFrame




```python
titanic[["Age", "Sex"]].shape


```




    (891, 2)



The selection returned a DataFrame with 891 rows and 2 columns. Remember, a DataFrame is 2-dimensional with both a row and column dimension.

## How do I filter specific rows from a DataFrame?

![image.png](3_selecting_a_subset_of_df_files/8b6eba85-a0d4-4529-bfde-9ba597b40918.png)

I’m interested in the passengers older than 35 years.


```python
above_35 = titanic[titanic["Age"]>35]
above_35.head()

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
      <th>6</th>
      <td>7</td>
      <td>0</td>
      <td>1</td>
      <td>McCarthy, Mr. Timothy J</td>
      <td>male</td>
      <td>54.0</td>
      <td>0</td>
      <td>0</td>
      <td>17463</td>
      <td>51.8625</td>
      <td>E46</td>
      <td>S</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12</td>
      <td>1</td>
      <td>1</td>
      <td>Bonnell, Miss Elizabeth</td>
      <td>female</td>
      <td>58.0</td>
      <td>0</td>
      <td>0</td>
      <td>113783</td>
      <td>26.5500</td>
      <td>C103</td>
      <td>S</td>
    </tr>
    <tr>
      <th>13</th>
      <td>14</td>
      <td>0</td>
      <td>3</td>
      <td>Andersson, Mr. Anders Johan</td>
      <td>male</td>
      <td>39.0</td>
      <td>1</td>
      <td>5</td>
      <td>347082</td>
      <td>31.2750</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>1</td>
      <td>2</td>
      <td>Hewlett, Mrs. (Mary D Kingcome)</td>
      <td>female</td>
      <td>55.0</td>
      <td>0</td>
      <td>0</td>
      <td>248706</td>
      <td>16.0000</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>



To select rows based on a conditional expression, use a condition inside the selection brackets []

The condition inside the selection brackets titanic["Age"] > 35 checks for which rows the Age column has a value larger than 35:


```python
titanic["Age"] > 35
```




    0      False
    1       True
    2      False
    3      False
    4      False
           ...  
    886    False
    887    False
    888    False
    889    False
    890    False
    Name: Age, Length: 891, dtype: bool



The output of the conditional expression (>, but also ==, !=, <, <=,… would work) is actually a pandas Series of boolean values (either True or False) with the same number of rows as the original DataFrame. Such a Series of boolean values can be used to filter the DataFrame by putting it in between the selection brackets []. Only rows for which the value is True will be selected.

We know from before that the original Titanic DataFrame consists of 891 rows. Let’s have a look at the number of rows which satisfy the condition by checking the shape attribute of the resulting DataFrame above_35:


```python
above_35.shape

```




    (217, 12)



Let's say now that we're interested in only the Titanic passengers from cabin class 2 and 3.



```python
class_23 = titanic[titanic["Pclass"].isin([2,3])]
class_23.head()
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
    <tr>
      <th>5</th>
      <td>6</td>
      <td>0</td>
      <td>3</td>
      <td>Moran, Mr. James</td>
      <td>male</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>330877</td>
      <td>8.4583</td>
      <td>NaN</td>
      <td>Q</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>0</td>
      <td>3</td>
      <td>Palsson, Master Gosta Leonard</td>
      <td>male</td>
      <td>2.0</td>
      <td>3</td>
      <td>1</td>
      <td>349909</td>
      <td>21.0750</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>



##### Like the conditional expression before, `isin()` is a **conditional function** that returns `True` for each row row in the specified Series or list. 
- To filter the rows based on the `conditional function`, use the conditional function *inside* the selection brackets `[]`.
- Here, the condition inside the selection brackets `titanic["Pclass"].isin([2,3])` checks for which rows the `Pclass` column is either 2 or 3.
- This is the same as filtering by rows for which the class is either 2 or 3 and combining the two statements with an `|` (or) operator


```python
# i.e.
class_23 = titanic[(titanic["Pclass"] == 2) | (titanic["Pclass"] == 3)]
```


```python
class_23.head()
class_23.shape
```




    (675, 12)



**NOTE**: When combining multiple conditions, each condition must be wrapped in parentheses `()`. 
            AND we cannot use the standard python `or/and` operators but instead must use the `|` / `&` operators


###### Now, let's imagine we want only the passenger data for which the age is known...


```python
age_no_na = titanic[titanic["Age"].notna()]
age_no_na.head()
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



The `notna()` is another conditional pandas function. 
* it returns `True` for each row where the specified column values are not `Null`.
* Thus, it can be combined with selection brackets `[]` to filter the data table

Since the data displayed by the `head()` method looks very similar, one way we can check if it has actually changed is by checking the shape. 


```python
age_no_na.shape

```




    (714, 12)



### How do I select specific rows and columns from a DataFrame?

![image.png](3_selecting_a_subset_of_df_files/fdd27809-1143-4cdb-9daa-31a4e11bcb29.png)

Now, we are interested in only the names of passengers who are *older than 35 years*...


```python
adult_names = titanic.loc[titanic["Age"]> 35, "Name"]
adult_names.head()
```




    1     Cumings, Mrs. John Bradley (Florence Briggs Th...
    6                               McCarthy, Mr. Timothy J
    11                              Bonnell, Miss Elizabeth
    13                          Andersson, Mr. Anders Johan
    15                     Hewlett, Mrs. (Mary D Kingcome) 
    Name: Name, dtype: object



Here, a **subset** of both rows and columns is created, and just using selection brackets `[]` is not sufficient.

The `loc/iloc` operators are required **in front** of the selection brackets `[]`. 

When using `loc` & `iloc`, the e.g. `loc[a, b]`:
- a = rows desired
- b = columns desired
- when using column names, use `loc` (locate)
    - for `a` and `b`, you can use:
        - single string label
        - a list of string labels
        - conditional expression
        - a colon (specifies that you want to select **all** *rows or columns*.

Now, i'm interested in rows 10 to 25 & 3 to 5. 


```python
titanic.iloc[9:25, 2:5] # as standard in python, the selection range is end-exclusive i.e. only up to the 24th row and 4 column will be displayed 
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
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9</th>
      <td>2</td>
      <td>Nasser, Mrs. Nicholas (Adele Achem)</td>
      <td>female</td>
    </tr>
    <tr>
      <th>10</th>
      <td>3</td>
      <td>Sandstrom, Miss Marguerite Rut</td>
      <td>female</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1</td>
      <td>Bonnell, Miss Elizabeth</td>
      <td>female</td>
    </tr>
    <tr>
      <th>12</th>
      <td>3</td>
      <td>Saundercock, Mr. William Henry</td>
      <td>male</td>
    </tr>
    <tr>
      <th>13</th>
      <td>3</td>
      <td>Andersson, Mr. Anders Johan</td>
      <td>male</td>
    </tr>
    <tr>
      <th>14</th>
      <td>3</td>
      <td>Vestrom, Miss Hulda Amanda Adolfina</td>
      <td>female</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2</td>
      <td>Hewlett, Mrs. (Mary D Kingcome)</td>
      <td>female</td>
    </tr>
    <tr>
      <th>16</th>
      <td>3</td>
      <td>Rice, Master Eugene</td>
      <td>male</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2</td>
      <td>Williams, Mr. Charles Eugene</td>
      <td>male</td>
    </tr>
    <tr>
      <th>18</th>
      <td>3</td>
      <td>Vander Planke, Mrs. Julius (Emelia Maria Vande...</td>
      <td>female</td>
    </tr>
    <tr>
      <th>19</th>
      <td>3</td>
      <td>Masselmani, Mrs. Fatima</td>
      <td>female</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2</td>
      <td>Fynney, Mr. Joseph J</td>
      <td>male</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2</td>
      <td>Beesley, Mr. Lawrence</td>
      <td>male</td>
    </tr>
    <tr>
      <th>22</th>
      <td>3</td>
      <td>McGowan, Miss Anna "Annie"</td>
      <td>female</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1</td>
      <td>Sloper, Mr. William Thompson</td>
      <td>male</td>
    </tr>
    <tr>
      <th>24</th>
      <td>3</td>
      <td>Palsson, Miss Torborg Danira</td>
      <td>female</td>
    </tr>
  </tbody>
</table>
</div>



Again, a **subset** of both rows and columns has been created in one go, but just using `[]` for selection is not enough. 

When specifically interested in rows or columns based on position within the data set/table, use `iloc` -- think of `iloc` as *integer-locate* or *index-locate*

And, when selecting specific rows and/or columns with `iloc` or `iloc`, new values can be assigned to the selected data. 

E.g. let's assign `anonymous` to the first 3 elements of the fourth column


```python
titanic.iloc[0:3, 3] = "anonymous"
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
      <td>anonymous</td>
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
      <td>anonymous</td>
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
      <td>anonymous</td>
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



#### A Recap of `loc` and `iloc`:


```python
# df.iloc[500]
# returns the 501st row (indexing starts from 0). Note that specifying a dimension for the columns is optional.
# df.iloc[500, 3]
# retrieves the 501st row, column number 3. Multiple columns can also be specified:
# df.iloc[500, [0,1,3]]
# This is done using a list within the column dimension.

# Slicing is also possible.
# df.iloc[:500, [0,1,3]]
# shows the first 500 rows for columns 0, 1, and 3. Note: Observations with row number 501 are excluded because slicing excludes the last number (i.e.,
# :500
# means from 0 to 499).

 

# The distinction with
# loc
# lies in its use of indexes.
# df.loc[:500]
# could yield the same results as
# df.iloc[:500]
# if indexes are integers in ascending order. However, if any index differs from the integer ordering, the results will not match. Dates can also be used as indexes.

 

# Note: Slicing with
# loc
# includes both the starting and ending points (unlike
# iloc
# , which excludes the ending point).
```

#### REMEMBER: 
* When selecting *subsets* of data, `[]` are used
    * Inside these brackets, we can use single col/row label
    * A list of col/row labels
    * A slice of labels
    * A conditional expression
    * A colon.
* Select specific rows and columns using `loc` with their specific `string` names
* Select specififc rows and columns using `iloc` with their positions in the table
* You can assign new `values` to a seelction with `iloc`/`loc`


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```
