# Pandas Cheat Sheet
1. [Import data](#1-import-data)
2. [Export data](#2-export-data)
3. [Create test objects](#3-create-test-objects)
    - [Build a dataframe from inputted data](#build-a-dataframe-from-inputted-data)
    - [Or create a series from a list](#or-create-a-series-from-a-list)
4. [View/Inspect data](#4-view-or-inspect-data)
    - [head(), tail()](#head-tail)
    - [Add or insert row(s)](#add-or-insert-rows)
    - [Add multiple rows to DataFrame](#add-multiple-rows-to-dataframe)
    - [Or we can add new column(s)](#or-we-can-add-new-columns)
    - [Get DataFrame info](#get-dataframe-info)
    - [Count unique rows](#count-unique-rows)
5. [Selection](#5-selection)
    - [Get a list or series of values for a column](#get-a-list-or-series-of-values-for-a-column)
6. [Data cleaning](#6-data-cleaning)
    - [Rename the columns](#rename-the-columns)
    - [Working with Missing Data in Pandas](#working-with-missing-data-in-pandas)
7. [Filter, Sort, and Groupby](#7-filter-sort-and-groupby)
    - [Filter Pandas DataFrame by row values](#filter-pandas-dataframe-by-row-values)
    - [sort_values()](#sort-values)
    - [groupby()](#groupby)
8. [Statistics](#8-statistics)

## 1. Import data
Convert a CSV directly into a DataFrame using the function `pd.read_csv`
Note: Another similar function also exists called `pd.read_excel` for excel files
```python
# Load data
df = pd.read_csv('filename.csv') # From a CSV file
df = pd.read_excel('filename.xlsx') # From an Excel file
```

## 2. Export data
`to_csv()` dumps to the same directory as the notebook. We can save the first ten row by
`df[:10].to_csv()`. We can also save and write a DataFrame to an Excel File or a specific
Sheet in the Excel file using `df.to_excel()`
```python
df.to_csv('filename.csv', index=False) # Write to a CSV file
df.to_excel('filename.xlsx') # Write to an Excel file
```

## 3. Create test objects
#### Build a dataframe from inputted data
This is useful when we want to manually instantiate simple data to see changes as it flows
through a pipeline.
```python
# Build data frame from inputted data
df = pd.DataFrame(data = {'Name': ['Bob', 'Sally', 'Scott', 'Katie'],
'Physics': [68, 74, 77, 78],
'Chemistry': [84, 100, 73, 90],
'Algebra': [78, 88, 82, 87]})
```

#### Or create a series from a list
```python
# Create a series from an iterable my_list
my_list = [['Bob',78],
['Sally',91],
['Scott',62],
['Katie',78],
['John',100]]
df1 = pd.Series(my_list) # Create a series from an iterable my_list
```

## 4. View or inspect data
#### head(), tail()
`head()` function displays the `first n` records from a DataFrame. I often print the top record
of a DataFrame in my notebook so I can refer back to it if I forget what’s inside.
```python
df.head(3) # First 3 rows of the DataFrame
```

`tail()` function is used to return the `last n` rows. This is useful for quickly verifying data,
especially, after sorting or appending rows.
```python
df.tail(3) # Last 3 rows of the DataFrame
```

#### Add or insert row(s)
To append or add a row to DataFrame, we create the new row as Series and use append()
method.

In this example, the new row is initialized as a python dictionary, and `append()` method is
used to append the row to the DataFrame.

When we are adding a python dictionary to `append()`, make sure we pass `ignore_index=True`, so that the index values are not used along the concatenation axis. The resulting axis will instead be labeled as number series `0, 1, ..., n-1`, which is useful when the concatenation axis does not have meaningful indexing information.

The `append()` method returns the DataFrame with the newly added row.
```python
#Append row to the dataframe, missing data (np.nan)
new_row = {'Name':'Max', 'Physics':67, 'Chemistry':92, 'Algebra':np.nan}
df = df.append(new_row, ignore_index=True)
```

#### Add multiple rows to DataFrame
```python
# List of series
list_of_series = [pd.Series(['Liz', 83, 77, np.nan], index=df.columns),
pd.Series(['Sam', np.nan, 94,70], index=df.columns ),
pd.Series(['Mike', 79,87,90], index=df.columns),
pd.Series(['Scott', np.nan,87,np.nan], index=df.columns),]
# Pass a list of series to the append() to add multiple rows
df = df.append(list_of_series , ignore_index=True)
```

#### Or we can add new column(s)
```python
# Adding a new column to existing DataFrame in Pandas
sex = ['Male','Female','Male','Female','Male','Female','Female','Male','Male']
df['Sex'] = sex
```

#### Get DataFrame info
`info()` function is useful for getting some general information like header, number of
values, and datatype by column. A similar but less useful function is `df.dtypes` which just
gives column data types.
```python
df.info() #Index, Datatype and Memory information
```

```python
df['Chemistry'].dtypes # Check data type in pandas dataframe
>>> dtype('int64')
df['Chemistry'] = df['Chemistry'].astype(float) # Convert Integers to Floats in Pandas DataFrame
df['Chemistry'].dtypes
>>> dtype('float64')
df.shape # Number of rows and columns
>>> (9, 5)
```

#### Count unique rows
The `value_counts()` function is used to get a series containing counts of unique values.
```python
# View unique values and counts of Physics column
df['Physics'].value_counts(dropna=False)
```

## 5. Selection
#### Get a list or series of values for a column
This works if we need to pull the values in columns into `X` and `y` variables so we can fit a
machine learning model.
```python
df['Chemistry'] # Returns column with label 'Chemistry' as Series
```
```python
df[['Name','Algebra']] # Returns columns as a new DataFrame
```
```python
df.iloc[0] # Selection by position
df.iloc[:,1] # Second column 'Name' of data frame
df.iloc[0,1] # First element of Second column
```

## 6. Data cleaning
#### Rename the columns
`rename()` function is quite useful when we need to rename some selected columns
because we need to specify information only for the columns which are to be renamed.
```python
# Rename columns
df = df.rename({'Name':'Student','Algebra':'Math'}, axis='columns')
```

#### Working with Missing Data in Pandas
In DataFrame sometimes many datasets simply arrive with missing data, either because it
exists and was not collected or it never existed.

* **NaN** (an acronym for Not a Number), is a special floating-point value recognized by all
* systems that use the standard IEEE floating-point representation

Pandas treat `NaN` as essentially interchangeable for indicating missing or null values. To
facilitate this convention, there are several useful functions for detecting, removing, and
replacing null values in Pandas DataFrame.
```python
# Checks for null Values, Returns Boolean Arrray
check_for_nan = df.isnull()
```

To check null values in Pandas DataFrame, we use `isnull()` or `notnull()` method.
`isnull()` method returns DataFrame of Boolean values which are True for NaN values. In
the opposite position, `notnull()` method returns DataFrame of Boolean values which are
False for NaN values.
```python
value = df.notnull() # Opposite of df2.isnull()
```

We use `dropna()` function to drop all rows that have any missing values.
```python
drop_null_row = df.dropna() # Drop all rows that contain null values
```

Sometimes, we may just want to drop a column that has some missing values.
```python
# Drop all columns that contain null values
drop_null_col = df.dropna(axis=1)
```

We can fill missing values by `using fillna()`. For example, we may want to replace `NaN` with zeroes.
```python
replace_null = df.fillna(0) # Replace all null values with 0
```

Or we can replace `NaN` with the mean value.
```python
# Replace all null values with the mean (mean can be replaced with almost any function from the statistics module)
df = round(df.fillna(df.mean()),2)
```

`replace()` method can be used to replace values in DataFrame
```python
one = df.replace(100,'A') # Replace all values equal to 100 with 'one'
```

## 7. Filter, Sort, and Groupby
#### Filter Pandas DataFrame by row values
We want to see students who get 80 or higher in Physics
```python
fil_80 = df[df['Physics'] > 80]
```

What if we want to see students who receive 80 or higher grade in Chemistry but less than
90 on Math exam
```python
fil = df[(df['Chemistry'] > 80) & (df['Math'] < 90)]
```

#### sort values
Often we want to sort Pandas DataFrame in a specific way. Typically, one may want to sort
Pandas DataFrame based on the values of one or more columns or sort based on the values
of row index or row names of Pandas DataFrame.

For example, we want to sort values by Student’s name in ascending order.
```python
ascending = df.sort_values('Student')
```

Sorting Chemistry score in descending order.
```python
descending = df.sort_values('Chemistry',ascending=False)
```

More complicated, we want to sort values by Physics scores in ascending order then
Chemistry scores in descending order.
```python
df.sort_values(['Physics','Chemistry'],ascending=[True,False])
```
In this case, a DataFrame will be sorted for Physics and Chemistry column respectively. We
can also pass a list to the ‘ascending’ parameter to tell Pandas which column to sort how.

#### groupby()
Groupby is a pretty simple concept. We can create a grouping of categories and apply a
function to the categories. It is a simple concept but it’s an extremely valuable technique that
we often use. Groupby concept is important because it’s the ability to aggregate data
efficiently, both in performance and the amount code is magnificent.

Let’s group the unique values from the Sex column
```python
group_by = df.groupby(['Sex']) # Returns a groupby object for values from one column
group_by.first() # Print the first value in each group
```

Calculate the average across all columns for every unique Sex group
```python
average = df.groupby(‘Sex’).agg(np.mean)
```

## 8. Statistics
We may be familiar with pivot tables in Excel to generate easy insights into our data.
Similarly, we can create Python pivot tables using the `pivot_table()` function available in
Pandas. The function is quite similar to the `group_by()` function but offers significantly
more customization.

Let’s say we want to group values by Sex and calculate the mean and standard deviation of
Physics and Chemistry columns. We will call the `pivot_table()` function and set the
following arguments:

* `index` to be `'Sex'` since that is the column from `df` that we want to appear as a
unique value in each row
* `values` as `'Physics','Chemistry'` since that's the column we want to apply some
aggregate operation on
* `aggfunc` to `'len','np.mean','np.std` `len` will count the unique distinct values
from the Sex column, `np.mean` and `np.std` will calculate the mean and standard
deviation respectively.

```python
pivot_table = df.pivot_table(index='Sex',
values=['Physics','Chemistry'],
aggfunc=[len, np.mean, np.std])
```

Note: Using `len` assumes we don't have `NaN` values in our datagram.

**describe()** is used to view some basic statistical details like percentile, mean, std, etc. of a
DataFrame or a series of numeric values.
```python
df.describe() # Summary statistics for numerical columns
```

Find the maximum value of each row and column using `max()`
```python
# Get a series containing maximum value of each row
max_row = df.max(axis=1)
# Get a series containing maximum value of each column without skipping NaN
max_col = df.max(skipna=False)
```

Similarly, we can use `df.min()` to find the minimum value of each row or column.

Other useful statistics functions:
* `df.sum()`: Returns the sum of the values for the requested axis. By default, axis is index
(axis=0).
* `df.mean()`: Returns the average value
* `df.median()`: Returns the median of each column
* `df.std()`: Returns the standard deviation of the numerical columns.
* `df.corr()`: Returns the correlation between columns in a DataFrame.
* `df.count()`: Returns the number of non-null values in each column.
