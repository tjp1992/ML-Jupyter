# Data Visualization(Exploratory)

### Library Importation

```python
# submodule 'pyplot' of 'matplotlib' is imported as 'plt' as convention dictates

import matplotlib.pyplot as plt
```

The `pyplot` submodule is a collection of high-level functions we can use to generate graphs very quickly. 

## Line Graphs and Time Series

### Plotting 

To create our line graph above following steps have to be taken:

- Add the data to the [`plt.plot()` function](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.plot.html#matplotlib-pyplot-plot)
- Display the plot using the [`plt.show()` function](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.show.html)

For instance

```python
# x axis
month_number = [1,2,3,4,5,6,7]
# 6-axis
new_cases [9926, 76246, 681488, 2336640,
             2835147, 4226655, 6942042]

plt.plot(mont_number, new_cases)
plt.show()
```

>   ![img](https://s3.amazonaws.com/dq-content/520/screen4_1.png)

### Modifying Axis Unit

As Shown above, the graph is displayed with x and y axis as month_number, new_cases, but on top of `y-axis` you can see `1e6`. This is a scientific notation indicating $10^6$ is multiplied to the value on the `y-axis`. In order to display the `y-axis` is a plain number, you can use [`plt.ticklabel_format(axis,style) function`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.ticklabel_format.html#matplotlib-pyplot-ticklabel-format).

```python
plt.plot(month_number, new_cases)
plt.ticklabel_format(axis='y', style='plain')
plt.show()
```

Displays the following:

>   ![img](https://s3.amazonaws.com/dq-content/520/screen3_4.png)

The `axis` parameter defines which axis to configure — its arguments are the strings `'x'`, `'y'`, and `'both'`.

The `style` parameter controls the notation style (plain or scientific). Its arguments are `'sci'`, `'scientific'`, and `'plain'`.

### Setting Title

The next is setting a title to the graph. It can be achieved by using the [`plt.title() function`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.title.html#matplotlib-pyplot-title) to add a title to our line graph.

```python
plt.plot(month_number, new_cases)
plt.ticklabel_format(aixs='y', style='plain')
plt.title('New Reported Cases by Month - Globally')
plt.show()
```

> ![img](https://s3.amazonaws.com/dq-content/520/screen5_1.png)

### Labeling Axis

The x-axis shows the month number, and the y-axis shows the number of new reported cases. We can show this on our graph by adding a **label** to each axis — a y-label and an x-label. To add axis labels, we use [`plt.xlabel()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.xlabel.html#matplotlib-pyplot-xlabel) and [`plt.ylabel()`](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.ylabel.html#matplotlib-pyplot-ylabel).

```python
plt.plot(month_number, new_cases)
plt.ticklabel_format(axis='y', style='plain')
plt.title('New Reported Cases By Month (Globally)')
plt.xlabel('Month Number')
plt.ylabel('Number of Cases')
plt.show()
```

> ![img](https://s3.amazonaws.com/dq-content/520/screen5_2.png)

### Plotting With DataFrame

Working with Pandas DataFrame as an example we have imported data collected from [World Health Organization.](https://covid19.who.int/)

```python
import pandas as pd
who_time_series = pd.read_csv('WHO_time_series.csv')
print(who_time_series.head())
```

> ![image-20220102145544803](C:\Users\tjp19\AppData\Roaming\Typora\typora-user-images\image-20220102145544803.png)

The Dataset of the first column contains the `'Date_reported'` column which we can use to create `time series`.

```python
who_time_series['Date_reported'] = pd.to_datetime(who_time_series['Date_reported'])
plt.plot(who_time_series['Date_reported'], who_time_series[who_time_series['Country'] == country_name])
plt.show()
```

##### Graph Patterns

It is important to identify the different patterns in data, and one is by looking for the graph patterns with different  types of growth(`linear`,`exponential`,`logarithmic`)

**Exponential Growth**

> Graph of India
>
>  ![img](https://s3.amazonaws.com/dq-content/520/screen7_2.png)

**Logarithmic Growth**

>  Graph of Italy
>
>  ![img](https://s3.amazonaws.com/dq-content/520/screen7_1.png)

**Linear Growth**

>  Graph of Poland
>
>  ![img](https://s3.amazonaws.com/dq-content/520/screen7_3.png)

### Comparing Graphs

We can have multiple `time series` in a single graph to show comparison of different datasets. This can be achieved by using multiple `plt.plot()` functions before closing off with `plt.show()`. `plt.show()` will close the datasets from accepting more datasets and will create a new graph.

```python
france = who_time_series[who_time_series['Country'] == 'France']
uk = who_time_series[who_time_series['Country'] == 'The United Kingdom']
plt.plot(france['Date_reported'],france['Cumulative_cases'])
plt.plot(uk['Date_reported'], uk['Cumulative_cases'])
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/520/screen9_1.png)

The graph shows two different datasets, but does not indicate the country for which the line represents. This can be achieved by adding a `label` argument to the `plt.plot()` function and using the [`plt.legend()` function](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.legend.html#matplotlib-pyplot-legend).

```python
france = who_time_series[who_time_series['Country'] == 'France']
uk = who_time_series[who_time_series['Country'] == 'The United Kingdom']
plt.plot(france['Date_reported'],france['Cumulative_cases'], label='France')
plt.plot(uk['Date_reported'], uk['Cumulative_cases'], label='The United Kingdom')
plt.legend()
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/520/screen9_2.png) 

When we use `plt.plot()` the first time, Matplotlib creates a line graph. When we use `plt.plot()` again, Matplotlib creates another line graph that shares the same x- and y-axis as the first graph. If we want Matplotlib to draw the second line graph separately, we need to close the first graph with the [`plt.show()` function](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.show.html).

### x and y Axis Ticks

After importing a certain data using `pandas` and using `plt.plot()` and `plt.show()` plotting a certain time plot gave the following result.

>  ![img](https://s3.amazonaws.com/dq-content/521/m2_screen2_1.png)

As seen on the graph above, the `x-axis` label is displayed with a thick black lines. This is due to plotting the data without converting the date type object in the data

With pandas, we can use the [`pd.to_datetime()` function](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.to_datetime.html) to make the conversion:

```python
DataFrame[column] = pd.to_datetime(DataFrame[column])
```

After making the conversion, the graph was displayed as following:

>  ![img](https://s3.amazonaws.com/dq-content/521/m2_screen2_2.png)

The `x-axis` was displayed overlapped on one another. This can be solved by using the [`plt.xticks()` function](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.xticks.html). The function has a `rotation` parameter which can be used to control the angle of rotation

```python
plt.plot(DataFrame[column], DataFrame[column])
plt.xticks(rotation=45)
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/521/m2_screen2_3.png)

## Seasonality, Scatter plots, and correlation

**Seasonality**

On a certain dataset concerning bike rentals, we see spikes in rental at certain specific times, and decrease in specific time zones. Mostly portrayed by using `time series`.

>  ![img](https://s3.amazonaws.com/dq-content/521/m2_screen2_3.png)

This signifies a seasonal trend shown by the graph. As bike riding is an outdoor activity which is heavily influenced by the `temperature`, during cold months, bike rentals can be seen decreased while an increase is visible during warm seasons.

Identifying the seasonal trends can be useful for businesses:

- Planning marketing campaigns at the right time.
- They don't need to panic needlessly when the sales are decreasing as a result of seasonality.
- They can hire extra employees right before the beginning period of high activity.

**Scatter Plot**

Scatter plot can be used to better visualize the relationship between two different datasets. Similar to `bike rental` dataset used for **Seasonality**. This section will also be using the similar dataset to better understand how to use scatter plot and further analyze the importance of scatter plots.

By plotting `time series` in the **Seasonality** section, we see that the hypothesis of 'Correlation between Temperature and Rental'

>  ![img](https://s3.amazonaws.com/dq-content/521/m2_screen4_1.png) 

However, such correlation can be visualized easier by using **Scatter Plots**. Scatter Plots can be plotted by using the [`plt.scatter()` function](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.scatter.html)

```python
plt.scatter(DataFrame[column1], DataFrame[column2])
plt.xlabel('Temperature')
plt.ylabel('Bike Rentals')
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/521/m2_screen4_2.png)

Each point on the scatter plot has an x-coordinate and y-coordinate. Seen from the Scatter plot, we can visualize the relationship between `Temperature` and `Bike Rentals` much easier.

>  ![img](https://s3.amazonaws.com/dq-content/521/correlation_viz.svg)

**Pearson's r(Pearsons correlation coefficient)**

We can measure how well the points fit on a straight line by using the **Pearson correlation coefficient** — also known as **Pearson's r**.

Pearson's r values lie between -1.00 and +1.00. When the positive correlation is perfect, the Pearson's r is equal to +1.00. When the negative correlation is perfect, the Pearson's r is equal to -1.00. A value of 0.0 shows no correlation.

>  ![img](https://s3.amazonaws.com/dq-content/521/pos_nul_neg_r.svg)

Below, we see various scatter plot shapes along with their corresponding Pearson's r.

>  ![img](https://s3.amazonaws.com/dq-content/521/m2_screen6_1.png)

If columns X and Y have *r = +0.8*, and columns X and Z have *r = -0.8*, then the strength of these two correlations is equal. The minus sign only tells us that the correlation is negative, not that it is weaker.

For example, even though the number +0.2 is greater than -0.6, a -0.6 correlation is stronger compared to a +0.2 correlation.

When we compare correlation strengths, we need to ignore the signs and only look at the absolute *r* values. The sign only gives us the correlation's direction, not its strength.

**Calculating `Pearson's r` using function**

To calculate the Pearson's r between any two columns, we can use the [`Series.corr()` method](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.corr.html). For instance, this is how we can calculate the two correlations above:

```python
DataFrame[column].corr(DataFrame[column])
# or
Series.corr(Series)
```

**※`Series.corr()` function only supports numerical data types, *Meaning using correlation function on `str`,`datetime` data types will result in error* **

we can also get overview of correlations using the [`DataFrame.corr()`method]('https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.corr.html'), which calculates the Pearson's r between all pairs of numerical columns.

```python
DataFrame.corr()
```



### Bar Plots, Histograms and Distributions

**Bar Plots**

Bar plots are also a way to visualize correlation when there is a categorical differentiation in the dataset. As used before, the bike dataset can be displayed using the [`plt.bar()` function](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.bar.html).

```python
# Importation to implementation of plt.bar() function
import matplotlib.pyplot as plt

working_days = ['Non-Working Day', 'Working Day']
casual_avg = [1371, 607]

plt.bar(working_days, casual_avg)
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/522/m3_screen2_1.png)

As Shown above, the `working_days` is used for `x-axis` while the `casual_avg` was used as the `y-axis`.

**Bar Plot Ticks Labels**

While using bar plot, we can also use [`plt.xticks()` function](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.xticks.html) to better visualize the dataset.

For instance when using the dataset provided above(Bike Rental), if we want to see a bar plot of the rental counts using the days of the week, the function above will come in handy when visualizing the data.

```python
plt.bar(DataFrame[column1], DataFrame[column2])

plt.xticks(ticks=list, labels=list, rotation=45)
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/522/m3_screen3_3.png)

**Horizontal bar plot**

The example used above can also be portrayed horizontally using [`plt.barh(y, width)` function](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.barh.html) along with `plt.yticks()` to Change the labels on the y-axis ticks.

```python
plt.barh(DataFrame[column], DataFrame[column])
plt.yticks(ticks = list, labels = list)
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/522/m3_screen3_4.png)

**Histogram**

Histogram is useful when visualizing a grouped frequency table.

Grouped frequency table can be extracted by adding `bins` Parameter to the `pd.count_values()` parameter. The `bins` parameter Rather than count values, group them into half-open bins, a convenience for `pd.cut`, only works with numeric data. **Bins is given 10 for a good balance between information and comprehension.**

Histogram can be plotted by using [`plt.hist()` function](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.hist.html).

```python
plt.hist(pd[col])
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/522/m3_screen6_1.png)

Behind the curtains, the `plt.hist()` function did the following:

- Generated a grouped frequency table with ten equal intervals for the `cnt` column.
- Plotted a bar for each interval (ten intervals means ten bars). The height of each bar corresponds to the frequency of its corresponding interval.

A histogram is a modified bar plot — the main visual difference is that there are no gaps between bars.

>  ![img](https://s3.amazonaws.com/dq-content/522/m3_screen7_1.png)

Another equally-important difference is that each bar represents an interval, not a single value.

It's useful to examine the shape of a histogram because it shows us the distribution of the values.

We often see histograms with a shape that is more or less symmetrical. If we draw a vertical line exactly in the middle of a symmetrical histogram, then we divide the histogram in two halves that are mirror images of one another.

A histogram shows the distribution of the values, and if its shape is symmetrical, then we say we have a **symmetrical distribution**.

One common symmetrical distribution is the **normal distribution** (also called Gaussian distribution).

>  ![img](https://s3.amazonaws.com/dq-content/286/s1m4_normal.svg)

Another symmetrical distribution we can see in practice is the **uniform distribution** — the values are *uniformly distributed*. The bars have equal height because the intervals have equal frequencies.

>  ![img](https://s3.amazonaws.com/dq-content/286/s1m4_uniform.svg)

The following histogram shows a **skewed distribution**. In a skewed distribution, we see the following:

- The values pile up toward the end or the starting point of the range, making up the *body* of the distribution.
  - In the case of the `casual` histogram, the values pile up toward the starting point of the range.
- Then the values decrease in frequency towards the opposite end, forming the *tail* of the distribution.

>  ![img](https://s3.amazonaws.com/dq-content/286/s1m4_body_tail.svg)

If the tail points to the right, then the distribution is right skewed (the distribution of the `casual` column is right skewed). If the tail points to the left, then the distribution is said to be left skewed.

>  ![img](https://s3.amazonaws.com/dq-content/522/m3_0.png)

When the tail points to the left, it also points in the direction of negative numbers (on the x-axis, the numbers decrease from right to left). For this reason, a left-skewed distribution is sometimes also said to have a negative skew.

When the tail points to the right, it also points in the direction of positive numbers. As a consequence, right-skewed distributions are also said to have a positive skew.

### Pandas Visualization and Grid Charts

Pandas support visualization with methods within the library for expedited visualization of various graphs.

Certain methods include:

- [`Series.plot.hist()` ](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.plot.hist.html)
- `Series.plot.bar()`
- `Series.plot.barh()`
- `DataFrame.plot.line(x= Series, y= Series)`
- `DataFrame.plot.scatter(x= Series, y= Series)`

This section involves using `pandas` to do exploration of dataset visually.

**Grid Charts**

When there are multiple `line plots` that needs to be analyzed `separately` and `collectively` , it is advisable to use the `Grid Charts` to display the data. `Grid Charts` can be displayed by using the following functions: 

- [`plt.figure()` function](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.figure.html)
- [`plt.subplot()` function](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.subplot.html)

`plt.figure()` will create a frame for which the graphs will be displayed.

`plt.subplot()` will create the graphs within the frame and can be made in the following manner

>  ![img](https://s3.amazonaws.com/dq-content/523/grid_chart_row_col.svg)

```python
# First Create the Frame using plt.figure(), and set the parameters so that the figures can fit in a screen and not overlap
plt.figure(figsize = (10,12))

# Create a graph for different index using plt.subplot()
# The Parameters should be only positional arguments and not a keyword argument
plt.subplot(nrows, ncols, index)
# The Following Equates to creating a empty graph of 3 rows 2 columns at the position index (1)
plt.subplot(3,2,1)

# After creating the graph to fill the contents of the empty graph, plot the graph
plt.plot(Series, Series)

```

