# Data Aggregation

Extracting meaningful insights from datasets requires cleaning — lots of it. So, it's critical to know how to manipulate data quickly and efficiently.

In this section, we'll learn to aggregate data with `pandas`. Here are a couple of takeaways:

- Different techniques for aggregating data
- Building intuition around the groupby operation

To get the most out of this section, it is important to be familiar with `panda`, `matplotlib` library and be able to filter through Data Frame. 

In this section, **World Happiness Report** will be used for Data Aggregation, which assigns each country with a **happiness score** based on poll results.

- How can aggregating the data give us more insight into happiness scores?
- How did world happiness change from 2015 to 2017?
- Which factors contribute the most to the happiness score?

**Groupby**

In data aggregation process it is important to be able to use the [`df.groupby()` method](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.groupby.html). The following method will create a GroupBy object where we can easily retrieve data from DataFrame faster and not having to loop through the DataFrame individually.

```python
df.groupby('col')
```

Before we start aggregating data, we'll build some intuition around GroupBy objects. We'll start by using the [`GroupBy.get_group()` method](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.get_group.html) to select data for a certain group.

```python
GroupBy.get_group('Group Name')
```

We can also use [`GroupBy.groups` attribute](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.groups.html) to get more information about the GroupBy object:

```python
# I will be using generalized syntax and display the result of an example below
grouped = df.groupby(col)
grouped.groups
```

> {'Australia and New Zealand': Int64Index([8, 9], dtype='int64'),
>  'Central and Eastern Europe': Int64Index([ 30,  43,  44,  51,  53,  54,  55,  58,  59,  61,  63,  68,  69,
>               72,  76,  79,  82,  85,  86,  88,  92,  94,  95, 103, 105, 110, 126, 129, 133], dtype='int64'),
>  'Eastern Asia': Int64Index([37, 45, 46, 71, 83, 99],dtype='int64'),
>  'Latin America and Caribbean': Int64Index([ 11,  13,  15,  22,  24,  26,  29,  31,  32,  39,  40,  41,  42,
>               47,  50,  52,  56,  57,  64,  97, 104, 118], dtype='int64'),
>  'Middle East and Northern Africa': Int64Index([ 10,  19,  21,  27,  34,  38,  48,  62,  67,  75,  81,  91, 
>               102, 106, 107, 109, 111, 134, 135, 155],dtype='int64'),
>  'North America': Int64Index([4, 14], dtype='int64'),
>  ...
>  }

The `GroupBy.groups` attribute shows the index of each group.

There are many [aggregation methods](https://pandas.pydata.org/pandas-docs/stable/user_guide/groupby.html) built into the `pandas` library. The Following are some examples of the commonly used inbuild methods.

| **Methods** | **Description**                          |
| ----------- | ---------------------------------------- |
| **mean()**  | Calculates the mean of groups            |
| **sum()**   | Calculates the sum of group values       |
| **size()**  | Calculates the size of the groups        |
| **count()** | Calculates the count of values in groups |
| **min()**   | Calculates the minimum of group values   |
| **max()**   | Calculates the maximum of group values   |



**Multiple aggregation**

We can do multiple aggregation by using the [`GroupBy.agg()` method](https://pandas.pydata.org/pandas-docs/version/0.22/generated/pandas.core.groupby.DataFrameGroupBy.agg.html), We pass function names as the parameter as a list.

```python
# Both are usable
GroupBy.agg(['mean', 'max'])

GroupBy.agg([np.mean, np.max])

```

**`df.pivot_table()`**

We can use [`DataFrame.pivot_table()` method](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.pivot_table.html) to achieve the same goal as `GroupBy.agg()` method, but the advantage of using `DataFrame.pivot_table()` is to allow easier comprehension of complex aggregations. 

```python
pv_happiness = happiness2015.pivot_table('Happiness Score', 'Region')
pv_happiness.plot(kind='barh', title='Mean Happiness Scores by Region', xlim=(0,10), legend=False)
```

>  ![Mean_happiness](https://s3.amazonaws.com/dq-content/343/mean_happiness.png)

**※When using `groupby()` be clear which will become the `index` and `value` of the new `GroupBy` object**

