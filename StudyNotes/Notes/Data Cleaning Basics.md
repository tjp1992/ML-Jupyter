# Data Cleaning Basics

The following `.md` file is meant for personal recap of the data cleaning procedure and is purely educational. For those who are starting off a new path into machine learning are more than welcome to `fork` the following document. Otherwise just skim though as a reference.

*The Following document was referenced from [dataquest](https://dataquest.io)*

`Data Cleaning` is an essential procedure of machine learning. It is ever so crucial that the data be clean before the analysis procedure, and as such a part of machine learning that takes [over half of the time](https://www.forbes.com/sites/gilpress/2016/03/23/data-preparation-most-time-consuming-least-enjoyable-data-science-task-survey-says/), Analyzing dataset that hasn't been cleaned is both pointless and very dangerous, as the outcome of the prediction does not entail proper data

### Reading `.csv` File using `panda`

Reading csv file can be accomplished by `pandas.read_csv()` function. However, depending on the character sets that exist in the dataset, further parameter `encoding` needs to be specified.

> ---------------------------------------------------------------------------
> UnicodeDecodeError                        Traceback (most recent call last)
> pandas/_libs/parsers.pyx in pandas._libs.parsers.TextReader._convert_tokens()
>
> pandas/_libs/parsers.pyx in pandas._libs.parsers.TextReader._convert_with_dtype()
>
> pandas/_libs/parsers.pyx in pandas._libs.parsers.TextReader._string_convert()
>
> pandas/_libs/parsers.pyx in pandas._libs.parsers._string_box_utf8()
>
> UnicodeDecodeError: 'utf-8' codec can't decode byte 0xe9 in position 4: invalid continuation byte

**Pandas csv read file error**

As shown above, while trying to use `pandas.read_csv()` function, there was decode error due to no `encoding` was specified during reading. Following errors can be fixed by using some of the common encodings:

- UTF-8
- Latin-1(also known as ISO-8859-1)
- windows-1251

As such it is important to look out for dataset encoding before reading the file

### Filtering `Dataframe` Columns

It is important to loop through the columns after importing the `.csv` file. As it is ever more important to have proper column names for data cleaning.

Column names can often include certain character sets that hinder the process of analysis. Some character sets may include `' '`, `','`,`'('`,`')'`... etc.

In order to check for following cases, it is important to go through the column names with the function `DataFrame.info()`. This allows us to go through the column names and to check if certain elements are missing in certain rows of the dataset without having to loop through the dataset.

##### Column names

>  For instance a column name could be `' Operating System(Region) '`, the column name includes a preceding and trailing white space and capital with special characters `'('`, `')'`. 

With the example one can use `DataFrame.columns` attribute to get the column names in a list and loop through the list to use `str.strip()` ,`str.replace()`, `str.lower()` functions to get a clean column names.

```python
# Get the DataFrame column names
old_col = DataFrame.columns

# Define a function to clean the data
def clean_col(col):
    col = col.strip()
    # Shortening column name can expedite the process of Data Analysis
    col = col.replace('Operating System','os')
    col = col.replace("(","")
    col = col.replace(")","")
    col = col.lower()
    return col

# Loop through to clean the column names
cleaned_col = []
for c in old_col:
    cleaned_col.append(clean_col(c))
    
DataFrame.columns = cleaned_col
```

By modifying the column names, we have taken the first step in data cleaning.



### Data Types

Majority of times, datasets do not come in cleanly filtered data. Most of the time, they are `int`, `float` in `str` format making it harder to get unique data of certain columns.

> <class 'pandas.core.frame.DataFrame'>
> RangeIndex: 1303 entries, 0 to 1302
> Data columns (total 13 columns):
>
> | num  | Column                   | Non-Null Count | Dtype  |
> | ---- | ------------------------ | -------------- | ------ |
> | 0    | Manufacturer             | 1303 non-null  | object |
> | 1    | Model Name               | 1303 non-null  | object |
> | 2    | Category                 | 1303 non-null  | object |
> | 3    | Screen Size              | 1303 non-null  | object |
> | 4    | Screen                   | 1303 non-null  | object |
> | 5    | CPU                      | 1303 non-null  | object |
> | 6    | RAM                      | 1303 non-null  | object |
> | 7    | Storage                  | 1303 non-null  | object |
> | 8    | GPU                      | 1303 non-null  | object |
> | 9    | Operating System         | 1303 non-null  | object |
> | 10   | Operating System Version | 1133 non-null  | object |
> | 11   | Weight                   | 1303 non-null  | object |
> | 12   | Price (Euros)            | 1303 non-null  | object |
>
>
> dtypes: object(13)
> memory usage: 132.5+ KB

Above is the output of a certain dataset by using the following function `DataFrame.info()` , it can be seen that most of the `dtype` in the dataframe is an object type, but in reality is a `str` type. This does not make it easy for smooth analysis. *(It can be seen that `Operating System Version` column has less dataset compared to other columns. Following issue will be addressed further down)`*

Pandas library contains dozens of [vectorized string methods]('https://pandas.pydata.org/pandas-docs/stable/user_guide/text.html#method-summary') we can use to manipulate the text data, many of which perform the same operations as Python string methods. Most vectorized string methods are available using the `Series.str` [accessor](http://pandas.pydata.org/pandas-docs/stable/api.html#string-handling). which means we can access them by adding `str` between the series name and the method name:

```python
# Use the following syntax to access string methods available to Series
Series.str.method_name()
```

##### String Data to other `dtype`

There are many instances where certain columns contain data types that are `str` but could easily converted to `int` for `float` type for easier processing. In this section, I will deal with different methods to convert a column of a dataset to a different type, and the preceding steps to be taken before converting the `dtype` of a  dataset.

**Look for Patterns**

The Dataset that needs adjustment in the value will have specific pattern, or in some cases will not have pattern, but by using `DataFrame.unique()` method, we can easily look for patterns.

**Replacing String**

For examples, say that there is a column in a dataset of column `'screen_size'`*(After Column name has been modified)*. The `screen_size` data mostly comprised of sizes of the monitor with the unique sets of `['15.4"', '17.3"', ... , '19.3"']`. The following column could easily be represented in `float` type, but was not possible due to the character `'"'`, we can change replace the string values of the data through `Series.str.replace()` method.

```python
# Replace the string value of the data
DataFrame['screen_size'] = DataFrame['screen_size'].str.replace('"','')
```

**Converting Column `dtype`**

After unnecessary characters have been removed from the data, we can then change the `dtype` of the column for easier processing. As displayed before, `float` type would be a better fit for the column data type as there are decimal points in the data.

```python
# Changing The Data type of a column
DataFrame['screen_size'].astype(float)
```

**Changing Column Name**

We have replaced the `'"'` character from the data and made the column into `float` type, but the `'"'` character has significance, as it shows the unit in which the data is in, it would be advisable to make the column name have a reference to the `unit` that is being used.

We could, potentially use the method used above, by replacing `DataFrame.columns` with an updated `list`, but that would be troublesome as the only column we have to change is 1. In such case, we could use `DataFrame.rename()` function to easily achieve the goal.

```python
# Changing Column name 
DataFrame.rename({'screen_size':'screen_size_inch'}, axis=1, inplace=True)
```

### Creating New Columns

Another example would be if there is a column by the name `'gpu'` . when we get the `DataFrame.unique()` from the table the data contained following data `['Intel Iris Plus 640','Intel HD Graphics 6000', 'Intel HD Graphics 620', 'AMD Radeon Pro 455'...]`. From the data retrieved, we can see that the manufacturer is in the beginning of all the dataset, and we could easily create a new column with the column name `'gpu_manufacturer'`.

This can easily be achieved by using `DataFrame.str.split()` function to split the data by whitespace and getting the first index of the split data by using `.str[index]` attribute. 

```python
# Split the Data and create a new column using the data

DataFrame['gpu_manufacturer'] = DataFrame['gpu'].str.split().str[0]
```



### Replacing Data

In cases when there are certain data that needs to be to changed, and if there are specific data type that needs to be converted, we can achieve that by using `Series.map()`. This method cannot be used on DataFrame and can only be used on `Series` Type. 

For instance, lets say there is typo in the data as such shown below

> ```python
> # Let's say there is a DataFrame 'fruit'
> fruit_name = fruit['fruit_name']
> print(fruit_name)
> ```
>
> 
>
> | 0    | pair   |
> | ---- | ------ |
> | 1    | pair   |
> | 2    | oranje |
> | 3    | oranje |
> | 4    | oranje |
> | 5    | oranje |
>
> dtype: object

Such typo will influence the outcome, as the data is not correct, and the fruit `pair` simply does not exist. In such a scenario, we can use `Series.map()` as explained above to correct the data

```python
# Create a map with correct data
correction = {
    'pair' : 'pear',
    'oranje': 'orange'
}

# Use 'Series.map()' function to correct the data with typo
fruit['fruit_name'] = fruit['fruit_name'].map(correction)
```

*Changing the data values can easily be achieved as above, but as an important side note, it is important that the following method be used only once. `Series.map()`method will look for all the values in data for the `key` of the `dictionary`, but if the value is absent and the data does not match any of the `key`, the method will convert all the data into `NaN` .*

### Detecting`None` and `NaN` Values

In cases when there `None` or `NaN` values, it would be advisable to process the following missing values. We can easily check for `NaN` or `None` values from the data by using [`isnull()` or `notnull()` methods](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.dropna.html)*(By convention, it would be easier to stop missing values by using `isnull()` method*

```python
# 'isnull()' or 'notnull()' can be used on dataframe for 

DataFrame.isnull().sum()
```



**Processing `None` and `NaN` Values**

There are multiple ways to process such data:

- Remove any rows that have missing values.
- Remove any columns that have missing values
- Fill the missing values with some other values
- Leave the missing value as it is

**Removing `Row` or `Column` from Data **

Removing `rows` and `columns` can easily be achieved by [`DataFrame.dropna()`method](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.dropna.html). This method by default has `axis=0` , which deletes the rows that contain the missing values, while if parameter `axis=1` is given, deletes the column.

```python
# Removing Rows with missing Data
DataFrame.dropna()
DataFrame.dropna(axis=0)

# Removing Columns with missing Data
DataFrame.dropna(axis=1)
```

**Fill the missing Values**

Use `boolean comparison` to replace the missing values
