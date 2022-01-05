# Relational Plots and Multiple Variables

### Seaborn

The following section handles `seaborn` library which is an extension of `matplotlib` library. `seaborn` allows data to be plotted in a manner that can take in the multiple variable in a single visualized graph.

>  ![img](https://s3.amazonaws.com/dq-content/573/screen1_1.png)

**Importation**

```python
# It is the standard alias to import seaborn as 'sns'
import seaborn as sns
```

**Functions**

`seaborn` library consists of multiple functions to support the `scatter plot` that is being created

- [`sns.relplot()` function](https://seaborn.pydata.org/generated/seaborn.relplot.html)
- [`sns.set_these()` function](https://seaborn.pydata.org/generated/seaborn.set_theme.html)

**`sns.relplot()`**

The following function takes in 3 parameters, `data`, `x`, `y`.

```python
sns.relplot(data = DataFrame, x= Series, y= Series)
plt.show()
```

The code above will produce a graph as following on a certain dataset.

>  ![img](https://s3.amazonaws.com/dq-content/573/screen2_1.png)

**`sns.set_theme()`**

The following function will take the graph above, and make it into `seaborn` themed.

>  ![img](https://s3.amazonaws.com/dq-content/573/screen2_1.png)

**hue**

The following graph shows the plots as blue, but by altering the parameters of `sns.relplot()`, we can change the colors of the plot by providing addition `Series` to the Parameter.

```python
sns.relplot(data= DataFrame, x= Series, y= Series, hue= Series)
```

> ![img](https://s3.amazonaws.com/dq-content/573/screen3_1.png)

The hues can take different color ranges to be customized by the parameter `palette`. It takes in abbreviations of different color palette to achieve the goal. Below are examples of different palettes that can be used and further documentation of color palettes can be seen [here](https://matplotlib.org/tutorials/colors/colormaps.html#miscellaneous).

>  ![img](https://s3.amazonaws.com/dq-content/573/screen3_3.png)

Such palettes can be used like below

```python
sns.relplot(data = DataFrame, x= Series, y= Series, hue= Series, palette= 'RdYlGn')
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/573/screen3_2.png) 

**`size`**

We can display the plots further by emphasizing the size by another variable.

`sns.relplot()` has parameters `size` and `sizes` where `size` takes in a `Series` or a `column` of a `DataFrame` while `sizes` takes in a `tuple` emphasizing the min and max size of the plot size.

```python
sns.relplot(data= DataFram, 
		   x= Series, 
           y= Series,
           hue = Series,
           palette = str,
           size = Series,
           sizes = tuple)
```

>  ![img](https://s3.amazonaws.com/dq-content/573/screen4_2.png)

`sizes` not only takes in a `tuple` to set the min and max, it can also take in `dict` or `list` to allow customization of the sizes `categorically`.

```python
sns.relplot(data = DataFrame,
           x = Series,
           y = Series,
           hue = Series,
           palette = str,
           size = Series,
           sizes = list)
```

>  ![img](https://s3.amazonaws.com/dq-content/573/screen4_3.png) 

**`shape`**

The `markers`(`markers` refers to each of the plots), can take various shapes: circle, triangle, square, etc. 

`Markers` can take the form of other shapes by using the `style` and `marker` parameter of `sns.relplot()` function, and by default the shape will be chosen by `seaborn` otherwise the shape of the `marker` can be chosen from the following [documentation](https://matplotlib.org/3.3.3/api/markers_api.html).

```python
sns.relplot(data = DataFrame,
           x = Series,
           y = Series,
           hue = Series,
           palette = str,
           size = Series,
           sizes = tuple or list,
           style = Series,
           markers = list)
# For example
sns.relplot(data = housing,
           x = 'Gr Liv Area',
           y = 'salePrice',
           hue = 'Overall Qual',
           palette = 'RdYlGn',
           size = 'Garage Area',
           sizes = (1,300),
           style = 'Rooms',
           markers = ['*','v'])
```

>  ![img](https://s3.amazonaws.com/dq-content/573/screen5_2.png)

**`col`**

The data is mixed in a way that is hard to visualize the data, because the data is so clustered, we can use a category to separate the graph by the parameter `col` of `sns.relplot()`.

```python
sns.relplot(data = DataFrame,
           x = Series,
           y = Series,
           hue = Series,
           palette = str,
           size = Series,
           sizes = tuple or list
           style = Series,
           markers = list,
           col = Series
           )
```

>  ![img](https://s3.amazonaws.com/dq-content/573/screen6_1.png) 

