---
jupyter:
  jupytext:
    cell_metadata_filter: code,-all
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.19.3
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

This tutorial is based on the pandas official website: [pandas getting started](https://pandas.pydata.org/docs/getting_started/index.html)

# Getting Started
## Overview
pandas is a package that provides fast, flexible, and expressive data structures designed to make working with “relational” or “labeled” data both easy and intuitive.

The two primary data structures of pandas, `Series` (1-dimensional) and `DataFrame` (2-dimensional), handle the vast majority of typical use cases in finance, statistics, social science, and many areas of engineering.

pandas is **fast**. Many of the low-level algorithmic bits have been extensively tweaked in Cython code.

### Mutability and copying of data
All pandas data structures are value-mutable (the values they contain can be altered) but not always size-mutable. The length of a Series cannot be changed, but, for example, columns can be inserted into a DataFrame. However, the vast majority of methods produce new objects and leave the input data untouched.


## What kind of data does pandas handle?

![[Pandas-20260518055632445.webp]]

```python
import pandas as pd
df = pd.DataFrame(
    {
        "Name": [
            "Braund, Mr. Owen Harris",
            "Allen, Mr. William Henry",
            "Bonnell, Miss Elizabeth",
        ],
        "Age": [22, 35, 58],
        "Sex": ["male", "male", "female"],
    }
)
print(df)
```

To manually store data in a table, create a `DataFrame`. When using a Python dictionary of lists, the dictionary keys will be used as column headers and the values in each list as columns of the `DataFrame`.

![[Pandas-20260612101435480.webp]]

When selecting a single column of a pandas `DataFrame, the result is a pandas `series.

```python
print(df["Age"])
```

You can create a `Series` from scratch as well:
```python
ages = pd.Series([22, 35, 58], name="Age")
print(ages)
```

Pandas has provided some methods to its DataFrames and Series.
Methods like `max()`, `min()`, `describe()`, and etc.

```python
print(df["Age"])
print(df["Age"].max())
```

```python
print(df.describe())
```

## How to read and write tabular data?

![[Pandas-20260612103103287.webp]] 
Pandas provides the `read_csv()` function to read data stored as a csv file into a pandas `DataFrame`. pandas supports many different file formats or data sources out of the box (csv, excel, sql, json, parquet, …), each of them with the prefix `read_*`.

We can view the first or last N rows of a DataFrame by `head(N)` or `tail(N)` methods.

We can also check the data types of a DataFrame like this:
```python
print(df.dtypes)
```

We can use `to_excel()` method to create an excel file from an DataFrame.

We can get a technical summary of a DataFrame by `info()` method like this:
```python
print(df.info())
```


## How to select a subset of a DataFrame?

#### Filtering columns
We can select multiple columns of a DataFrame like this:
```python
import pandas as pd
df = pd.DataFrame(
    {
        "Name": [
            "Braund, Mr. Owen Harris",
            "Allen, Mr. William Henry",
            "Bonnell, Miss Elizabeth",
        ],
        "Age": [22, 35, 58],
        "Sex": ["male", "male", "female"],
    }
)

print(df[["Name", "Sex"]])
```

#### Filtering rows
To select rows based on a conditional expression, use a condition inside the selection brackets `[]`.
```python
above_30 = df[df["Age"]> 30]
print(above_30)
```

>The output of the conditional expression (`>`, but also `==`, `!=`, `<`, `<=`,… would work) is actually a pandas `Series` of boolean values (either `True` or `False`) with the same number of rows as the original `DataFrame`. Such a `Series` of boolean values can be used to filter the `DataFrame` by putting it in between the selection brackets `[]`. Only rows for which the value is `True` will be selected.


```python
males = df[df["Sex"].isin(["male"])]
print(males)
```
Similar to the conditional expression, the `isin()` conditional function returns a `True` for each row the values are in the provided list. To filter the rows based on such a function, use the conditional function inside the selection brackets `[]`.

we can use `|`, `&` operators too:
```python
age_range_30_36= df[(df["Age"] > 30) & (df["Age"] < 39)]
print(age_range_30_36)
print(age_range_30_36.shape)
```

#### Filtering rows and columns
```python
print(df)
adult_names = df.loc[df["Age"] > 34, "Name"]
print("\n")
print(adult_names)
```

In this case, a subset of both rows and columns is made in one go and just using selection brackets `[]` is not sufficient anymore. The `loc`/`iloc` operators are required in front of the selection brackets `[]`. When using `loc`/`iloc`, the part before the comma is the rows you want, and the part after the comma is the columns you want to select.

When using column names, row labels or a condition expression, use the `loc` operator in front of the selection brackets `[]`. For both the part before and after the comma, you can use a single label, a list of labels, a slice of labels, a conditional expression or a colon. Using a colon specifies you want to select all rows or columns.

```python
print(df.iloc[0:2, 0:1])
```
When specifically interested in certain rows and/or columns based on their position in the table, use the `iloc` operator in front of the selection brackets `[]`.

When selecting specific rows and/or columns with `loc` or `iloc`, new values can be assigned to the selected data.
```python
df.iloc[0:2, 0] = "Anonymous"
print(df)
```

## How to create plots in pandas?
We can create plots from pandas DataFrames.

#### Line plots
example:
```python
import pandas as pd
import matplotlib.pyplot as plt
air_quality = pd.read_csv("air_quality_no2.csv", index_col=0, parse_dates=True)
air_quality.plot()
plt.show()
```

Output:
![[Pandas-20260613152146185.webp]]

>The `index_col=0` and `parse_dates=True` parameters passed to the `read_csv` function define the first (0th) column as index of the resulting `DataFrame` and convert the dates in the column to `Timestamp` objects, respectively.

With a `DataFrame`, pandas creates by default one line plot for each of the columns with numeric data.

We can also plot only an specific column like this: `air_quality["station_paris"].plot()`.

#### Scatter Plots
```python
air_quality.plot.scatter(x="station_paris", y="station_london", alpha=0.5)
plt.show()
```
Output:
![[Pandas-20260613153330924.webp]]

There are other plot methods too.

#### Area plots
We can create area plots in a subplot visualization.
```python
air_quality.plot.area(figsize=(12, 4), subplots=True)
plt.show()
```
Output:
![[Pandas-20260613160341371.webp]]

We can also use matplotlib methods here:
```python
fig, axs = plt.subplots(figsize=(12, 4)) #Create an empty Matplotlib Figure and Axes
axs.set_ylabel("NO$_2$ concentration")
air_quality.plot.area(ax=axs) #Use pandas to put the area plot on the prepared Figure/Axes
plt.show()
```
Output:
![[Pandas-20260613160559251.webp]]

## How to create new columns derived from existing columns
We can create new columns in a DataFrame derived from existing columns like this:
```python
import pandas as pd
df = pd.DataFrame(
    {
        "Name": [
            "Braund, Mr. Owen Harris",
            "Allen, Mr. William Henry",
            "Bonnell, Miss Elizabeth",
        ],
        "Age": [22, 35, 58],
        "Sex": ["male", "male", "female"],
    }
)

print(df)

df["new_age"] = df["Age"]*2
print()
print("new df:")
print(df)
```

We can also use the `rename()` method.
>By this method we can rename column names or indexes.

```python
df_renamed = df.rename(columns={
    "Age": "renamed_Age",
    "Sex": "renamed_Sex",
})

print(df_renamed)
```

We can also use mapping functions instead of fixed names, like the example below:
```python
df_renamed = df.rename(columns=str.lower)
print(df_renamed)
```

## How to calculate summary statistics

#### Aggregating statistics
Different statistics are available and can be applied to columns with numerical data. Operations in general exclude missing data and operate across rows by default.
```python
import pandas as pd
df = pd.DataFrame(
    {
        "Name": [
            "Braund, Mr. Owen Harris",
            "Allen, Mr. William Henry",
            "Bonnell, Miss Elizabeth",
        ],
        "Age": [22, 35, 58],
        "Sex": ["male", "male", "female"],
    }
)

print(df["Age"].mean())
print()
print(df["Age"].describe())
```

Instead of the predefined statistics, specific combinations of aggregating statistics for given columns can be defined using the `DataFrame.agg()` method:
```python
res = df.agg(
    {
        "Age": ["min", "max", "median", "mean"]
    }
)
print(res)
```

#### Aggregating statistics grouped by category
What should we do inorder to know What is the average age for male versus female?
As our interest is the average age for each gender, a subselection on these two columns is made first: `df[["Sex", "Age"]]`. Next, the `groupby()` method is applied on the `Sex` column to make a group per category. The average age for each gender is calculated and returned.
```python
print(df[["Sex", "Age"]].groupby("Sex").mean())
```
We can also not select any columns and calculate the mean for every column with numeric data like this:
```python
print(df.groupby("Sex").mean(numeric_only=True))
```

If we are only interested in the average age for each gender, the selection of columns (square brackets `[]` as usual) is supported on the grouped data as well:
```python
print(df.groupby("Sex")["Age"].mean())
```

![[Pandas-20260628114850657.webp]]

Grouping can be done by multiple columns at the same time. Provide the column names as a list to the `groupby()` method.
```python
df = pd.DataFrame({
    "Name": ["Ali", "Reza", "Akbar", "Json", "Sara", "Sweetie", "Negar", "Negin", "Tatiana"],
    "Sex": ["male", "male", "male", "male", "female", "female", "female", "female", "female"],
    "weight": ["fat", "normal", "fat", "fat", "normal", "fat", "normal", "fat", "fat"],
    "Age": [23,19,23, 35, 32, 29, 24, 31, 51],
    "height": [156, 189, 170, 160, 157, 190, 157, 173, 171]
})

print(df.groupby(["Sex", "weight"])[["height", "Age"]].mean())
```

#### Count number of records by category
We can use the `value_counts()` method to count the number of records for each category in a column.
```python
print(df["Sex"].value_counts())
```

```python
print(df.groupby("Sex")["Sex.count())
```

>Both `size` and `count` can be used in combination with `groupby`. Whereas `size` includes `NaN` values and just provides the number of rows (size of the table), `count` excludes the missing values. In the `value_counts` method, use the `dropna` argument to include or exclude the `NaN` values.

## How to reshape the layout of tables?

#### Sort table rows
```python
import pandas as pd
df = pd.DataFrame({
    "Name": ["Ali", "Reza", "Akbar", "Json", "Sara", "Sweetie", "Negar", "Negin", "Tatiana"],
    "Sex": ["male", "male", "male", "male", "female", "female", "female", "female", "female"],
    "weight": ["fat", "normal", "fat", "fat", "normal", "fat", "normal", "fat", "fat"],
    "Age": [23,19,23, 35, 32, 29, 24, 31, 51],
    "height": [156, 189, 170, 160, 157, 190, 157, 173, 171]
})

print(df.sort_values(by="Age", ascending=False))
```

#### Long to wide table format
![[Pandas-20260629141830613.webp]]
The `pivot()` function is purely reshaping of the data: a single value for each index/column combination is required.

```python
print(df)
print()
dfWeightAge = df.pivot(columns="weight", values="Age", index="Name")
print(dfWeightAge)
df.plot.bar(x="Name", y="Age")
print()
```

We can also use aggregation functions by `pivot_table()` method for multiple values that we have for each index/column combination.

```python
meanAges = df.pivot_table(
    values="Age", index="Sex", columns="weight", aggfunc="mean"
)
print(meanAges)
```

We can do the same by `groupby()` method:
```python
print(df.groupby(["Sex", "weight"])[["Age", "height"]].mean())
```

#### Wide to long format
The `pandas.melt()` method on a `DataFrame` converts the data table from wide format to long format.
The method will _melt_ all columns NOT mentioned in `id_vars` together into two columns: A column with the column header names and a column with the values itself. The latter column gets by default the name `value`.
```python
df_pivoted = df.pivot(columns="Sex", values="Age")
print(f"df_pivoted:\n{df_pivoted}\n")
tmp = df_pivoted.melt(
    value_vars=["female", "male"],
    value_name="Age",
    var_name="Gendre"
)
print(tmp)
```

The additional parameters have the following effects:
- `value_vars` defines which columns to _melt_ together
- `value_name` provides a custom column name for the values column instead of the default column name `value`
- `var_name` provides a custom column name for the column collecting the column header names. Otherwise it takes the index name or a default `variable`
Hence, the arguments `value_name` and `var_name` are just user-defined names for the two generated columns. The columns to melt are defined by `id_vars` and `value_vars`.

## How to combine data from multiple tables

We can concatenate two dataframes with the same columns like this:
```python
import pandas as pd
df1 = pd.DataFrame({
    "Name": ["Ali", "Reza", "Akbar", "Json", "Sara", "Sweetie", "Negar", "Negin", "Tatiana"],
    "Sex": ["male", "male", "male", "male", "female", "female", "female", "female", "female"],
    "weight": ["fat", "normal", "fat", "fat", "normal", "fat", "normal", "fat", "fat"],
    "Age": [23,19,23, 35, 32, 29, 24, 31, 51],
    "height": [156, 189, 170, 160, 157, 190, 157, 173, 171]
})

df2 = pd.DataFrame({
    "Name": ["Thomas", "Ragnar"],
    "Sex": ["male", "male"],
    "weight": ["fat", "normal"],
    "Age": [56,51],
    "height": [170, 177]
})

print(pd.concat([df1, df2], axis=0, keys=["df1", "df2"]))
```

>The `concat()` function performs concatenation operations of multiple tables along one of the axes (row-wise or column-wise).

The `concat` function provides a convenient solution with the `keys` argument, adding an additional (hierarchical) row index.

We can also reset the indexes and delete whatever level we want from the hierarchical index:
```python
print(pd.concat([df1, df2], axis=0, keys=["df1", "df2"]).reset_index(level=0, drop=True))
print()
print(pd.concat([df1, df2], axis=0, keys=["df1", "df2"]).reset_index(drop=True))
```

#### Join tables using a common identifier
![[Pandas-20260702134530461.webp]]
We can merge dataframes together in a behavior like database join.
For example consider the below example:
```python
import pandas as pd

df1 = pd.DataFrame(
    {
        "id": [2, 4, 5, 6, 9],
        "Name": ["Ali", "Hossein", "Mohammad", "Soheil", "Emad"],
        "Salary": [1200, 3220, 5430, 2500, 6000],
    }
)

df2 = pd.DataFrame(
    {
        "id": [2, 3, 4, 5, 6, 1],
        "Name": ["Ali", "Ehsan", "Hossein", "Mohammad", "Soheil", "Reza"],
        "Married": [1, 0, 1, 0, 0, 1],
        "Age": [23, 41, 21, 32, 26, 25]
    }
)

print(pd.merge(df1, df2, how="inner", on="id"))
print()
print(pd.merge(df1, df2, how="left", on="id"))
print()
print(pd.merge(df1, df2, how="right", on="id"))
```

When there is no common key (column name) between two dataframes that we tend to join, we can use `left_on` and `right_on` paramteres to make the link between the two tables.
```python
import pandas as pd

df1 = pd.DataFrame(
    {
        "id": [2, 4, 5, 6, 9],
        "Name": ["Ali", "Hossein", "Mohammad", "Soheil", "Emad"],
        "Salary": [1200, 3220, 5430, 2500, 6000],
    }
)

df2 = pd.DataFrame(
    {
        "idnum": [2, 3, 4, 5, 6, 1],
        "Name": ["Ali", "Ehsan", "Hossein", "Mohammad", "Soheil", "Reza"],
        "Married": [1, 0, 1, 0, 0, 1],
        "Age": [23, 41, 21, 32, 26, 25]
    }
)

print(pd.merge(df1, df2, how="inner", left_on="id", right_on="idnum"))
print()
print(pd.merge(df1, df2, how="left", left_on="id", right_on="idnum"))
print()
print(pd.merge(df1, df2, how="right", left_on="id", right_on="idnum"))
```

## How to handle time series data with ease
We may have datetime coulmns in our dataframe that are just texts, and doesn't support any time operation.
We can change that column's data to `datetime` objects in order to work with them.
```python
air_quality["datetime"] = pd.to_datetime(air_quality["datetime"])
```

Initially, the values in `datetime` are character strings and do not provide any datetime operations (e.g. extract the year, day of the week, …). By applying the `to_datetime` function, pandas interprets the strings and convert these to datetime (i.e. `datetime64[ns, UTC]`) objects. In pandas we call these datetime objects that are similar to `datetime.datetime` from the standard library as `pandas.Timestamp`.

As many data sets do contain datetime information in one of the columns, pandas input function like `pandas.read_csv()` and `pandas.read_json()` can do the transformation to dates when reading the data using the `parse_dates` parameter with a list of the columns to read as Timestamp:
```python
pd.read_csv("../data/air_quality_no2_long.csv", parse_dates=["datetime"])
```

Why using `pandas.Timestamp`?
Let's see some of it's benefits:
```python
In [9]: air_quality["datetime"].min(), air_quality["datetime"].max()
Out[9]: 
(Timestamp('2019-05-07 01:00:00+0000', tz='UTC'),
 Timestamp('2019-06-21 00:00:00+0000', tz='UTC'))
```

```python
In [11]: air_quality["month"] = air_quality["datetime"].dt.month

In [12]: air_quality.head()
```
```
Out[12]: 
    city country                  datetime  ... value   unit  month
0  Paris      FR 2019-06-21 00:00:00+00:00  ...  20.0  µg/m³      6
1  Paris      FR 2019-06-20 23:00:00+00:00  ...  21.8  µg/m³      6
2  Paris      FR 2019-06-20 22:00:00+00:00  ...  26.5  µg/m³      6
3  Paris      FR 2019-06-20 21:00:00+00:00  ...  24.9  µg/m³      6
4  Paris      FR 2019-06-20 20:00:00+00:00  ...  21.4  µg/m³      6

[5 rows x 8 columns]
```
>By using `Timestamp` objects for dates, a lot of time-related properties are provided by pandas. For example the `month`, but also `year`, `quarter`,… All of these properties are accessible by the `dt` accessor.

#### Datetime as index
Working with a datetime index (i.e. `DatetimeIndex`) provides powerful functionalities. For example, we do not need the `dt` accessor to get the time series properties, but have these properties available on the index directly:
```python
air_quality = pd.read_csv("air_quality_no2_long.csv", parse_dates=["date.utc"])
pivoted = air_quality.pivot(index="date.utc", columns="location", values="value")
print(pivoted)
print()
pivoted.index.year
pivoted.index.month
```
Output:
```
location                   BETR801  FR04014  London Westminster
date.utc                                                       
2019-05-07 01:00:00+00:00     50.5     25.0                23.0
2019-05-07 02:00:00+00:00     45.0     27.7                19.0
2019-05-07 03:00:00+00:00      NaN     50.4                19.0
2019-05-07 04:00:00+00:00      NaN     61.9                16.0
2019-05-07 05:00:00+00:00      NaN     72.4                 NaN
...                            ...      ...                 ...
2019-06-20 20:00:00+00:00      NaN     21.4                 NaN
2019-06-20 21:00:00+00:00      NaN     24.9                 NaN
2019-06-20 22:00:00+00:00      NaN     26.5                 NaN
2019-06-20 23:00:00+00:00      NaN     21.8                 NaN
2019-06-21 00:00:00+00:00      NaN     20.0                 NaN

[1033 rows x 3 columns]

Index([2019, 2019, 2019, 2019, 2019, 2019, 2019, 2019, 2019, 2019,
       ...
       2019, 2019, 2019, 2019, 2019, 2019, 2019, 2019, 2019, 2019],
      dtype='int32', name='date.utc', length=1033)
Index([5, 5, 5, 5, 5, 5, 5, 5, 5, 5,
       ...
       6, 6, 6, 6, 6, 6, 6, 6, 6, 6],
      dtype='int32', name='date.utc', length=1033)
```

By providing a **string that parses to a datetime**, a specific subset of the data can be selected on a `DatetimeIndex`.

```python
pivoted["2019-05-20":"2019-05-21"].plot()
```
Output:
![[Pandas-20260702230809598.webp]]

#### Resampling a time series to another frequency
A very powerful method on time series data with a datetime index, is the ability to `resample()` time series to another frequency (e.g., converting secondly data into 5-minutely data).

The `resample()`method is similar to a groupby operation:
- it provides a time-based grouping, by using a string (e.g. `M`, `5H`, …) that defines the target frequency
- it requires an aggregation function such as `mean`, `max`,…
```python
print(pivoted)
print()
resampled = pivoted.resample("ME").max()
print("resampled data: \n\n", resampled)
```
Output:
```
location                   BETR801  FR04014  London Westminster
date.utc                                                       
2019-05-07 01:00:00+00:00     50.5     25.0                23.0
2019-05-07 02:00:00+00:00     45.0     27.7                19.0
2019-05-07 03:00:00+00:00      NaN     50.4                19.0
2019-05-07 04:00:00+00:00      NaN     61.9                16.0
2019-05-07 05:00:00+00:00      NaN     72.4                 NaN
...                            ...      ...                 ...
2019-06-20 20:00:00+00:00      NaN     21.4                 NaN
2019-06-20 21:00:00+00:00      NaN     24.9                 NaN
2019-06-20 22:00:00+00:00      NaN     26.5                 NaN
2019-06-20 23:00:00+00:00      NaN     21.8                 NaN
2019-06-21 00:00:00+00:00      NaN     20.0                 NaN

[1033 rows x 3 columns]

resampled data: 

 location                   BETR801  FR04014  London Westminster
date.utc                                                       
2019-05-31 00:00:00+00:00     74.5     97.0                97.0
2019-06-30 00:00:00+00:00     52.5     84.7                52.0
```

for example we can Make a plot of the daily mean 𝑁⁢𝑂2 value in each of the stations of the example:
```python
pivoted.resample("D").mean().plot(marker="o", figsize=(12, 5))
```
Output:
![[Pandas-20260703001431195.webp]]


## How to manipulate textual data
Similar to datetime having a `dt` accessor, a number of specialized string methods are available when using the `str` accessor. These methods have in general matching names with the equivalent built-in string methods for single elements, but are applied element-wise on each of the values of the columns.

