# File path: ./notebook_tutorials_pandas/.ipynb_checkpoints/pandas_worksheet_1-checkpoint.ipynb


Welcome to this **hands-on** Pandas challenge! This worksheet will test and deepen your skills in **data manipulation, exploration, cleaning, and analysis**. By the end, you'll be ready to tackle **real-world** datasets with confidence.

---

## 🔍 **Step 1: Choose and Load Your Dataset**
Pick one of the following famous datasets to work with:
1. **Iris Dataset** 🌸 (Flower measurements)
2. **Wine Dataset** 🍷 (Chemical composition of wines)
3. **Boston Housing Dataset** 🏠 (Housing prices and features)

Each of these datasets is available in `sklearn.datasets`. Load it into a **Pandas `DataFrame`**.

```python
from sklearn.datasets import load_iris, load_wine, load_boston  # Boston may be deprecated in newer sklearn
import pandas as pd

# Uncomment the dataset you want to use
# data = load_iris()
# data = load_wine()
# data = load_boston()  # May require `fetch_openml("boston")` if not available directly

df = pd.DataFrame(data.data, columns=data.feature_names)

# If there's a target, store it separately or add it as a new column
# df['target'] = data.target

# Display first 5 rows
df.head()
```

> **Tip:** If you’re loading the **Boston** dataset via `fetch_openml`, you may need:
> ```python
> from sklearn.datasets import fetch_openml
> data = fetch_openml(name='boston', version=1)
> df = pd.DataFrame(data.data, columns=data.feature_names)
> df['target'] = data.target
> ```



```python

```

# 🏆 Pandas Practice Worksheet: From Fundamentals to Advanced! 🚀

Welcome to this **hands-on** Pandas challenge! This worksheet will test and deepen your skills in **data manipulation, exploration, cleaning, and analysis**. By the end, you'll be ready to tackle **real-world** datasets with confidence.

---

## 🔍 **Step 1: Choose and Load Your Dataset**
Pick one of the following famous datasets to work with:
1. **Iris Dataset** 🌸 (Flower measurements)
2. **Wine Dataset** 🍷 (Chemical composition of wines)
3. **Boston Housing Dataset** 🏠 (Housing prices and features)

Each of these datasets is available in `sklearn.datasets`. Load it into a **Pandas `DataFrame`**.

```python
from sklearn.datasets import load_iris, load_wine, load_boston  # Boston may be deprecated in newer sklearn
import pandas as pd

# Uncomment the dataset you want to use
# data = load_iris()
# data = load_wine()
# data = load_boston()  # May require `fetch_openml("boston")` if not available directly

df = pd.DataFrame(data.data, columns=data.feature_names)

# If there's a target, store it separately or add it as a new column
# df['target'] = data.target

# Display first 5 rows
df.head()
```

> **Tip:** If you’re loading the **Boston** dataset via `fetch_openml`, you may need:
> ```python
> from sklearn.datasets import fetch_openml
> data = fetch_openml(name='boston', version=1)
> df = pd.DataFrame(data.data, columns=data.feature_names)
> df['target'] = data.target
> ```

---

## 🧐 **Step 2: Initial Exploration**
1. Print the **shape** of the dataset (`.shape`).
2. Display the **column names** (`.columns`).
3. Check the **data types** of each column (`.dtypes`).
4. Get a **quick overview** of any **missing values** (e.g., `df.isnull().sum()`).
5. Generate **summary statistics** of numeric columns (`.describe()`).

```python
# Your code here!
```

> **Question:** Are there any columns that are not numeric? If so, how might that affect your analysis?

---

## 👀 **Step 3: Data Selection & Indexing**
1. Select only the **first 10 rows**.
2. Select only the columns that contain **numeric values**.
3. Extract all rows where the **first feature column** has a value **greater than its median**.
4. Find the row with the **maximum value** in the **last numeric column**.
5. Use **boolean indexing** or the **`.query()`** method to filter rows in a more readable way.

```python
# Your code here!
```

> **Challenge:** Practice both **label-based indexing** (`.loc`) and **integer-based indexing** (`.iloc`) to see the difference.

---

## 🔄 **Step 4: Data Cleaning & Transformation**
1. Convert all column names to **lowercase** (or snake_case).
2. Rename at least one column to a more meaningful name (e.g. `petal length (cm)` -> `petal_length`).
3. Add a new column called `"feature_sum"` that contains the **sum of all feature values** for each row.
4. **Normalize** (scale between `0` and `1`) all numeric columns.

```python
# Your code here!
```

> **Tip:** For normalization, consider using:
> ```python
> df_norm = (df - df.min()) / (df.max() - df.min())
> ```

---

## 🚰 **Step 5: Handling Missing Data & Outliers**
1. Check again if there are **missing values**. If so, **decide** whether to drop or fill them.
2. For numeric columns, consider detecting **outliers** (e.g., using **IQR** or **Z-scores**):
   - Calculate the IQR (`Q3 - Q1`).
   - Identify outliers that fall below `(Q1 - 1.5 * IQR)` or above `(Q3 + 1.5 * IQR)`.
3. Decide how to handle outliers (remove them, cap them, or leave as is).

```python
# Your code here!
```

> **Question:** What impact do outliers have on **mean** vs **median**? Which measure is more **robust** to outliers?

---

## 📈 **Step 6: Exploratory Data Analysis (EDA)**
1. **Group** the data by the target variable (if you have one) and calculate the **mean** for each group.
2. Create a **box plot** of one (or more) numeric columns.
3. Generate a **histogram** of the target variable (if categorical) or of any numeric column (if the target is numeric).
4. Use `.value_counts()` on any **categorical** columns (like `target`) to understand class distribution.

```python
# Your code here!
```

> **Challenge:** Try a **scatter plot** or **pairplot** to see the relationships between features. For a quick pairplot:
> ```python
> import seaborn as sns
> sns.pairplot(df, hue='target')
> ```

---

## 🔗 **Step 7: Combining & Merging Data**
1. Create a **second DataFrame** with **random values** (same number of rows) and a matching index. Merge it with your original dataset using:
   - An **inner join**.
   - A **left join**.
2. Experiment with **joining** on the target column (if applicable) or on an **artificial key**.

```python
# Your code here!
```

> **Tip:** When merging, watch out for duplicates or mismatched keys that could affect your row counts.

---

## 🔄 **Step 8: Reshaping Data (Pivot, Melt, and More)**
1. If you have a **long** dataset, try to **pivot** it to get a **wide** format using `pd.pivot_table` or `df.pivot`.
2. Conversely, if you have a **wide** dataset, practice using `.melt()` to make it **long** again.
3. Create a **pivot table** that summarizes at least one numeric feature grouped by a **categorical** variable (e.g., `target`).

```python
# Your code here!
```

> **Challenge:** Experiment with **multi-level** pivot tables or apply multiple aggregate functions (like `mean`, `std`, etc.) in one pivot.

---

## 🎛️ **Step 9: Advanced GroupBy & Apply**
1. Use **`.groupby()`** to compute **multiple aggregates** (e.g., `mean`, `median`, `std`) for each group.
2. Create a **custom function** that transforms or summarizes your data, and apply it group-wise with `.apply()`.
3. Explore **`.agg()`** and **`.transform()`** to see how they differ from **`.apply()`**.

```python
# Your code here!
```

> **Question:** When would you prefer `.apply()` over `.agg()` or `.transform()`?

---

## 🎯 **Step 10: Final Challenge**
1. Write a function that returns the **top 5 rows** where the sum of all numeric columns is **above the 75th percentile** of the overall dataset.
2. **Sort** these rows in descending order based on that sum.
3. Save your final **cleaned dataset** as a `.csv` file.

```python
# Your code here!
```

---

## 🚀 **Bonus Challenges**
1. **Correlation Heatmap:** Use Seaborn or Matplotlib to show correlations between features.
   ```python
   import seaborn as sns
   import matplotlib.pyplot as plt

   plt.figure(figsize=(10, 6))
   sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
   plt.title("Feature Correlation Heatmap")
   plt.show()
   ```
2. **Pairplot Analysis:** Create a pairplot colored by target (if applicable) to see pairwise relationships.
3. **Feature Engineering:** Create new features (e.g., polynomial terms, interaction terms) and see if they reveal new insights.
4. **Time for Stats/ML:** If your dataset is suitable, try a **basic regression or classification** with `sklearn`.

---

## 🎉 **Well Done!**
If you completed this worksheet, you're **well on your way** to mastering Pandas! Try applying these concepts to **real-world datasets** or integrate **machine learning** with `sklearn`.

---
### 📝 **Final Thought:** 
- Write down one topic you still find tricky in Pandas. 
- Identify **one** new function or method you want to explore further. 
- **Action Plan:** Outline **two** specific steps you’ll take to master that function.

> Remember, **practice** is the key to excellence. Keep exploring, keep coding, and have fun! 🚀
```

---

### Suggested Next Steps
- Explore real-world datasets from [Kaggle](https://www.kaggle.com/datasets).
- Practice more advanced **data visualization** with Plotly or Seaborn.
- Dive into **time-series** data if it interests you (e.g., stock prices, weather data).
- Use **GitHub** or **personal projects** to showcase your newfound skills.

**Good luck** on your journey to becoming a Pandas pro! Feel free to modify any tasks based on your interests or the nature of your chosen dataset. Enjoy the learning process!


```python

```
