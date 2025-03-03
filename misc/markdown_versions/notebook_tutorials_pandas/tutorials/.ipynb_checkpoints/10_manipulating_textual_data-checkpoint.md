# File path: ./notebook_tutorials_pandas/tutorials/.ipynb_checkpoints/10_manipulating_textual_data-checkpoint.ipynb



```python
import pandas as pd

```


```python
titanic = pd.read_csv("../data/titanic.csv")

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



Let's make all the name characters lowercase:



```python
titanic["Name"].str.lower()
```




    0                                braund, mr. owen harris
    1      cumings, mrs. john bradley (florence briggs th...
    2                                  heikkinen, miss laina
    3           futrelle, mrs. jacques heath (lily may peel)
    4                               allen, mr. william henry
                                 ...                        
    886                                montvila, rev. juozas
    887                          graham, miss margaret edith
    888              johnston, miss catherine helen "carrie"
    889                                behr, mr. karl howell
    890                                  dooley, mr. patrick
    Name: Name, Length: 891, dtype: object



To make each of the strings in the `Name` column lowercase, select the `Name` column, add the `str` accessor and apply the `lower` method. As such, each of the strings is converted element-wise.

Similar to datetime objects in the time series tutorial, having a `dt` accessor, a number of specialized string methods are available when using the `str` accessor. These methods have in general matching names with the equivalent built-in string methods for single elements, but are applied element-wise (remember element-wise calculations?) on each of the values of the columns.

> ❓ **Create a new column `Surname`** that contains the surname of the passengers by extracting the part before the comma.



```python
titanic["Name"].str.split(",")
```




    0                             [Braund,  Mr. Owen Harris]
    1      [Cumings,  Mrs. John Bradley (Florence Briggs ...
    2                               [Heikkinen,  Miss Laina]
    3        [Futrelle,  Mrs. Jacques Heath (Lily May Peel)]
    4                            [Allen,  Mr. William Henry]
                                 ...                        
    886                             [Montvila,  Rev. Juozas]
    887                       [Graham,  Miss Margaret Edith]
    888           [Johnston,  Miss Catherine Helen "Carrie"]
    889                             [Behr,  Mr. Karl Howell]
    890                               [Dooley,  Mr. Patrick]
    Name: Name, Length: 891, dtype: object



Using the `Series.str.split()` method, each of the values is returned as a list of 2 elements. 
* The *first element* is the part before the comma
* The *second element* is the part after the comma.


```python
titanic["Surname"] = titanic["Name"].str.split(",").str.get(0)
```


```python
titanic["Surname"]
```




    0         Braund
    1        Cumings
    2      Heikkinen
    3       Futrelle
    4          Allen
             ...    
    886     Montvila
    887       Graham
    888     Johnston
    889         Behr
    890       Dooley
    Name: Surname, Length: 891, dtype: object



As we are only interested in the first part representing the surname (element 0), we can again use the str accessor and apply `Series.str.get()` to extract the relevant part. Indeed, these string functions can be concatenated to combine multiple functions at once!

More information on extracting parts of strings is available in the user guide section on splitting and replacing strings.<br>

https://pandas.pydata.org/docs/user_guide/text.html#text-split

#### Extract the passenger data about the countesses on board of the Titanic.


```python
titanic["Name"].str.contains("Countess")
```




    0      False
    1      False
    2      False
    3      False
    4      False
           ...  
    886    False
    887    False
    888    False
    889    False
    890    False
    Name: Name, Length: 891, dtype: bool




```python
titanic[titanic["Name"].str.contains("Countess")]
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
      <th>Surname</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>759</th>
      <td>760</td>
      <td>1</td>
      <td>1</td>
      <td>Rothes, the Countess. of (Lucy Noel Martha Dye...</td>
      <td>female</td>
      <td>33.0</td>
      <td>0</td>
      <td>0</td>
      <td>110152</td>
      <td>86.5</td>
      <td>B77</td>
      <td>S</td>
      <td>Rothes</td>
    </tr>
  </tbody>
</table>
</div>



The string method `Series.str.contains()` checks for each of the values in the column `Name` if the string contains the word 'Countess' and returns for each of the values `True` (Countess is part of the name) or `False` (Countess is not part of the name). This output can be used to subselect the data using conditional (boolean) indexing introduced in the subsetting of data tutorial. As there was only one countess on the Titanic, we get one row as a result.

> #### **ℹ️ Note**  
> More powerful extractions on strings are supported, as the `Series.str.contains()` and `Series.str.extract()` methods accept [regular expressions](#), but out of scope of this tutorial.

More information on extracting parts of strings is available in the user guide section on regular expressions. <br>
https://docs.python.org/3/library/re.html 

> ❓ **Which passenger of the Titanic has the longest name?**



```python
titanic["Name"].str.len()
```




    0      23
    1      51
    2      21
    3      44
    4      24
           ..
    886    21
    887    27
    888    39
    889    21
    890    19
    Name: Name, Length: 891, dtype: int64



* To get the longest name, we first have to get the lengths of each of the names in the `Name` column.
* By using pandas string methods, the `Series.str.len()` function is applied to each of the names individually, element-wise.

Next, we need to get the corresponding location, preferably the index label, in the table for which the name length is the largest. 
* The `idxmax()` method does exactly that. 

* It is not a string method and is applied to integers, so no str is used.



```python
titanic["Name"].str.len().idxmax()
```




    307



* Based on the index name of the row (`307`) and the column (`Name`), we can do a selection using the `loc` operator, introduced in the tutorial on subsetting.


```python
titanic.loc[titanic["Name"].str.len().idxmax(), "Name"]
```




    'Penasco y Castellana, Mrs. Victor de Satode (Maria Josefa Perez de Soto y Vallejo)'



> ❓ **In the "Sex" column, replace values of "male" by "M" and values of "female" by "F".**




```python
titanic["Sex_short"] = titanic["Sex"].replace({"male":"M","female":"F"})
titanic["Sex_short"]
```




    0      M
    1      F
    2      F
    3      F
    4      M
          ..
    886    M
    887    F
    888    F
    889    M
    890    M
    Name: Sex_short, Length: 891, dtype: object



> * Although `replace()` is not a string method, it provides a convenient way to use mappings or vocabularies to translate certain values.
> * It requires a `dictionary` to define the mapping `{from : to}`.


> **⚠️ Warning**  
> There is also a `replace()` method available to replace a specific set of characters. However, when having a mapping of multiple values, this would become:
> 
> ```python
> titanic["Sex_short"] = titanic["Sex"].str.replace("female", "F")
> titanic["Sex_short"] = titanic["Sex_short"].str.replace("male", "M")
> ```
> 
> This would become cumbersome and easily lead to mistakes. Just think (or try out yourself) what would happen if those two statements are applied in the opposite order...

---

## REMEMBER  
- String methods are available using the `str` accessor.  
- String methods work element-wise and can be used for conditional indexing.  
- The `replace` method is a convenient method to convert values according to a given dictionary.


```python

```
