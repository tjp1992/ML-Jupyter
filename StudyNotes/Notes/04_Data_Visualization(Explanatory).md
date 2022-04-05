# Explanatory Data Visualization

Explanatory Data Visualization, unlike Exploratory Data Visualization is meant for the public, and for people to fully take in the data, it is good to use a graph that the audience can easily understand.

Ease of understanding often comes from familiarity.

In order to make a graph that is easy for the audience to take in, we can utilize `matplotlib`'s `object-oriented interface`. `Matplotlib` has two interfaces:

- A Functional Interface: we use functions to create and modify plots
- An object-oriented (OO) interface: we use methods to create and modify plots.

To create a graph using `OO` interface, we use [`plt.subplots()` function](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.subplots.html), which generates an empty plot and returns a `tuple` of two objects:

```python
# plt.subplots() returns a tuple and can be used as the following
fig, ax = plt.subplots()
# 'fig' would be `matplotlib.figure.Figure` object and can be seen as the canvas on which we can add one or more plots.
# 'ax' would be `matplotlib.axes._subplots.AxesSubplot` object which is the actual plot
ax.bar(['A','B','C'],[2,4,6])
```

>   ![img](https://s3.amazonaws.com/dq-content/525/screen3_4.png)

We know that a large part of our audience will read the article on a mobile device. This means our graph needs to have mobile-friendly proportions: small width, larger height. Our graph currently has a small height and a larger width.

As such, we can use `figsize` parameter inside the `plt.subplots(figsize=(width,height))`function to adjust the proportions.

```python
fig, ax = plt.subplots(figsize=(3, 5))
ax.barh(['A', 'B', 'C'],
        [2, 4, 16])
plt.show()
```

>   ![img](https://s3.amazonaws.com/dq-content/525/screen4_2.png)

When we design graphs (and anything in general), we need design principles to guide us. Design principles help us in two ways:

- They generate design options.
- They help us choose among those options.

One design principle we've already covered is familiarity. For example, if we need to visually present a frequency distribution, familiarity gives us a few options: a histogram and a box plot (let's assume our audience is only familiar with these two). Our audience, however, is more familiar with histograms, so we choose a histogram for our presentation.

The next design principle we're going to learn has to do with maximizing data elements on a graph. Generally, a graph has three elements:

- Data elements: the numbers and the categories visually represented and the relationships between them.
- Structural elements: the axes, the ticks, the legend, the grid, etc.
- Decorations: extra colors, shapes, artistic drawings etc.

Maximizing the data elements ensures the audience's attention is on the data — not on structure or decorations. Below, we see how removing structural elements and decorations can maximize data elements (GIF source: Darkhorse Analytics):

>  ![img](https://s3.amazonaws.com/dq-content/525/data-ink.gif)

Edward Tufte theorized the principle of maximizing data elements in his book *The Visual Display of Quantitative Information* (1983). From the total amount of ink used for printing a graph, some of the ink goes to show the data — that is the **data-ink**. As a sidenote, Tufte worked on his book in the 1980s, when most graphs were printed on paper using ink.

Tufte named the principle of maximizing data elements as **maximizing the data-ink ratio**. The data-ink ratio is the proportion of data-ink from the total ink:
$$
Data-ink~ratio = \frac{data-ink}{total~ink~used~to~print~the~graph}
$$
A graph with many decorations and structural parts has a low data-ink ratio. A graph where data-ink prevails has a greater data-ink ratio. Below, we see two theoretical examples:
$$
Data-ink~ratio = \frac{15}{100} = 0.15
$$

$$
Data-ink~ratio = \frac{75}{100}=0.75
$$

We should try to maximize the data-ink ratio within reason. Some structural elements are necessary; otherwise, the graph can become unreadable. Decorations are optional by definition, but they can help prove a point in some cases. 

Long story short, it is stating that the amount of extras aside from the information should be reduced to the minimum to fully portray the information in a easily comprehensible manner.

**Maximize Data Ink**

To maximize data ink, we can do the following:

- Erase non-data ink
- Erase redundant data-ink

In a bar graphs case, it would be the following:

- The axes
- The ticks(x and y ticks)

>  ![img](https://s3.amazonaws.com/dq-content/525/m1_2.png)

**Removing Axes(Spines)**

To remove the axes(also called **Spines**), we can use the [`Axes.spines[position].set_visible(bool)` method](https://matplotlib.org/api/_as_gen/matplotlib.artist.Artist.set_visible.html), where `position` is a string indicating the locations of the axies: `'left'`,`'right'`, `'top'`, and `'bottom'`. 

```python
fig, ax = plt.subplots()
ax.bar(['A','B','C'],[2,4,16])
ax.spines['left'].set_visible(False)
ax.spines['bottom'].set_visible(False)
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/525/screen6_2.png)

The top removed the axes(spines) on the `bottom` and `left` which left the `top` and the `right` still visible. To remove all the axes, we can `loop` a `list` to remove all the `spines` in a shorter code.

```python
fig, ax = plt.subplots()
ax.bar(['A','B','C'],[2,4,16])

for loc in ['top','bottom','left','right']:
    ax.spines[loc].set_visible(False)
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/525/screen6_3.png)

**Removing Ticks**

To remove ticks, we can use the [`Axes.tick_params(bottom,top,left,right)`method](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.tick_params.html)

```python
fig,ax = plt.subplots()
ax.bar(['A','B','C'],[2,4,16])
ax.tick_params(left=False,bottom=False)
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/525/screen6_4.png)

**Bar Thickness**

We can reduce the size of the bar depending on which type of bar graph it is. For horizontal bar graph(`barh`), we can use `height` parameter of the `Axes.barh()` method. For regular bar graph, we can use the `width` parameter of the `Axes.bar()` method.

```python
fig, ax = plt.subplots()
ax.barh(Series, Series, height=0.1)
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/525/screen7_2.png)

**X-tick Labels**

We can also reduce the non-data ink by reducing the number of ticks on the graph by using the [`Axes.set_xticks` method](![img](https://s3.amazonaws.com/dq-content/525/screen7_2.png)). 

```python
fig, ax = plt.subplots()
ax.barh(Series, Series)
ax.set_xticks([0, 100000, 200000, 300000])
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/525/screen7_3.png)

**Moving X ticks to Top**

When scrolling through an article with the graph, the reader will automatically see the countries and the bar in the graph, but because the quantity is on the bottom, it may confuse the readers. To resolve such an issue, we can use the [`Axes.xaxis.tick_top()` method](https://matplotlib.org/api/_as_gen/matplotlib.axis.XAxis.tick_top.html).

```python
# Assume the rest of the code is written
ax.xaxis.tick_top()
```

>  ![img](https://s3.amazonaws.com/dq-content/525/screen8_1.png)

**Axis Label Colors**

Aside from changing the location of the `x-label` , we can further change the color of the labels by using the [`Axes.tick_params()` method](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.tick_params.html) like we did before.

```python
# Assume the rest of the code is written
ax.xaxis.tick_top()
ax.tick_params(top=False, left=False)
ax.tick_params(axis='x', colors='grey')
```

>  ![img](https://s3.amazonaws.com/dq-content/525/screen8_3.png)

**Bar Colors**

We can change the color of the bar in the bar graph by using `color` parameter of the `Axes.barh(color)` method. This parameter accepts Hex color values.

```python
# Assuming the rest of the code is the same as above
ax.barh(Series, Series, height = 0.45, color = '#af0ble')
```

>  ![img](https://s3.amazonaws.com/dq-content/525/screen8_4.png)

**Title and Subtitle**

Aside from arrange and changing the colors of the axis, we can add title to the graph which sums up the data for the viewer to take in the information more comprehensibly. We can achieve the goal by using the [`Axes.text()` method](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.text.html).

The following method requires at least 3 arguments.

- `x` and `y` : the coordinates that give the position to the text
- `s`: the text

additional arguments to further change the text would be:

- `size`: Controls the text size
- `weight`: Controls the emphasis on the text(bold,italic, etc.)

```python
fig, ax = plt.subplots()
ax.bar(['A','B','C'],[2,4,16])
ax.text(x=0.5, y=18, s='Title example', size=15, weight='bold')
ax.text(x=0.5, y=17, s='Subtitle example', size=12)
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/525/screen9_3.png)

**`x-tick` labels**

The `x-ticks` if without proper comma can make it harder for the viewer to take in the information to fully grasp the gravity of the data. We can use the [`Axes.set_xticklabels()` method](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.set_xticklabels.html).

```python
# Assume the rest of the code is written
ax.set_xticklabels(['0', '150,000', '300,000'])
```

>  ![img](https://s3.amazonaws.com/dq-content/525/screen10_2.png)

**`y-axis` labels**

We can also change the `y-tick` labels so that it is easier for the viewers to read. in order to do so, we'll first clear the `y-axis` labels by using the [`Axes.set_yticklabels()` method](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.set_yticklabels.html). Followed by `Axes.text()` to set the `y-axis` labels again.

```python
# Code is same as above
# First clear the y-tick labels
ax.set_yticklabels([])
# Replace the y-tick labels by using 'Axes.text()'
for i,ele in zip(range(20), Series):
    ax.text(x=-80000, y=i-0.15, s= ele)
```

>  ![img](https://s3.amazonaws.com/dq-content/525/screen10_3.png)

**`axvline`**

Readers who explore the graph will try to determine the approximate death toll for each country. To help them, we're going to draw a vertical line below the 150,000 value. To do that, we use the [`Axes.axvline(x)` method](https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.axvline.html), where `x` is the x-coordinate where the line begins:

```python
# Assume the rest of the code is written
ax.axvline(x=150000)
```

>  ![img](https://s3.amazonaws.com/dq-content/525/screen10_4.png)

The color of the vertical line is too bright and stands out more than we want. Moreover, the line spans too far vertically and isn't on the same line with the `Turkey` label. To fix these problems, we're going to use the following:

- The `ymin` parameter to make it shorter — where `0` is the bottom of the plot, and `1` is the top of the plot.
- The `c` parameter to change the color to `'grey'`.
- The `alpha` parameter to add transparency to the line.

```python
# Assume the rest of the code is written
ax.axvline(x=150000, ymin=0.045, c='grey', alpha=0.5)
```

