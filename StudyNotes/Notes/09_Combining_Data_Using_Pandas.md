# Combining Data Using Pandas

**`pd.concat()` Function**

We can use [`pd.concat()` function](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.concat.html) to combine DataFrames.

**Axis=0(Default)**

>  ![Concat_Updated](https://s3.amazonaws.com/dq-content/344/Concat_Updated.svg)

**Axis=1**

>  ![Concat_Axis1](https://s3.amazonaws.com/dq-content/344/Concat_Axis1.svg)

`df.concat()` function will combine the two DataFrames in the axis specified in the parameter, but when using two DataFrames with different sizes, the `df.concat()` function will fill out the empty values with `NaN` .

**Read up on the parameters [`pd.concat()` function](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.concat.html) to utilize the function to it's potential**

**`pd.merge()** 

[`pd.merge()` function](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.merge.html) - a function that can execute high performance database-style joins. Note that unlike the `concat` function, the `merge` function only combines dataframes horizontally (axis=1) and can only combine two dataframes at a time. However, it can be valuable when we need to combine very large dataframes quickly and provides more flexibility in terms of how data can be combined.

