# [FiverThirtyEight](https://fivethirtyeight.com/)

So far in this course, we've learned about design and data storytelling. In this lesson, we're going to focus our attention on Matplotlib's pre-defined styles. For this case study, we'll use the `fivethirtyeight` style to build this graph.

>  ![img](https://s3.amazonaws.com/dq-content/528/screen1_1.png)

Matplotlib's pre-defined styles change the default visual properties of graphs. Below, we create a line plot using the `Solarize_Light2` style. To do that, we import the [`matplotlib.style` submodule](https://matplotlib.org/api/style_api.html) and then use the [`style.use()` function](https://matplotlib.org/api/style_api.html#matplotlib.style.use).

```python
import matplotlib.pyplot as plt
import matplotlib.style as style

style.use('Solarize_Light2')
plt.plot([1, 2, 3], [5, 2, 7])
plt.show()
```

>  ![img](https://s3.amazonaws.com/dq-content/528/screen1_2.png)

Note that we must use the `style.use()` function before we create the graph — before calling the `plt.plot()` function.

After we call `style.use('Solarize_Light2')`, all subsequent graphs will inherit this style. To get back to the default settings, we need to use `style.use('default')`.

We can see all the available styles by accessing the [`style.available` attribute](https://matplotlib.org/api/style_api.html#matplotlib.style.matplotlib.style.available).

```python
style.available
```

> ['Solarize_Light2',
> '_classic_test_patch',
> 'bmh',
> 'classic',
> 'dark_background',
> 'fast',
> 'fivethirtyeight',
> 'ggplot',
> 'grayscale',
> 'seaborn',
> 'seaborn-bright',
> 'seaborn-colorblind',
> 'seaborn-dark',
> 'seaborn-dark-palette',
> 'seaborn-darkgrid',
> 'seaborn-deep',
> 'seaborn-muted',
> 'seaborn-notebook',
> 'seaborn-paper',
> 'seaborn-pastel',
> 'seaborn-poster',
> 'seaborn-talk',
> 'seaborn-ticks',
> 'seaborn-white',
> 'seaborn-whitegrid',
> 'tableau-colorblind10']



```python
# 'color' parameter of barh() accepts list as a value, so we find the positive values as list of boolean to set color
positive_white = white_corr >= 0
color_map_white = positive_white.map({True:'#33A1C9', False:'#ffae42'})

positive_red = red_corr >=0
color_map_red = positive_red.map({True:'#33A1C9', False:'#ffae42'})

# matplotlib.style function to set the theme of the graph
style.use('fivethirtyeight')
fig, ax = plt.subplots(figsize=(9, 5))
ax.barh(white_corr.index, white_corr, left=2, height=0.5,
        color=color_map_white)
ax.barh(red_corr.index, red_corr, height=0.5, left=-0.1, color = color_map_red)

ax.grid(b=False)
ax.set_yticklabels([])
ax.set_xticklabels([])

# x_coords for setting the labels in the middle between two graphs
x_coords = {'Alcohol': 0.82, 'Sulphates': 0.77, 'pH': 0.91,
            'Density': 0.80, 'Total Sulfur Dioxide': 0.59,
            'Free Sulfur Dioxide': 0.6, 'Chlorides': 0.77,
            'Residual Sugar': 0.67, 'Citric Acid': 0.76,
            'Volatile Acidity': 0.67, 'Fixed Acidity': 0.71}
y_coord = 9.8

for y_label, x_coord in x_coords.items():
    ax.text(x_coord, y_coord, y_label)
    y_coord -= 1

# Vertical line for left and right of labels
ax.axvline(0.5, c='grey', alpha=0.1, linewidth=1,
           ymin=0.1, ymax=0.9)
ax.axvline(1.45, c='grey', alpha=0.1, linewidth=1,
           ymin=0.1, ymax=0.9)

# Horizontal line on the bottom to set ranges
ax.axhline(-1, color='grey', linewidth=1, alpha=0.5,
          xmin=0.01, xmax=0.32)
ax.text(-0.7, -1.7, '-0.5'+ ' '*31 + '+0.5',
        color='grey', alpha=0.5)

ax.axhline(-1, color='grey', linewidth=1, alpha=0.5,
           xmin=0.67, xmax=0.98)
ax.text(1.43, -1.7, '-0.5'+ ' '*31 + '+0.5',
        color='grey', alpha=0.5)

# Horizontal line and text above the line to show which data the graph is displaying
ax.axhline(11, color='grey', linewidth=1, alpha=0.5,
          xmin=0.01, xmax=0.32)
ax.text(-0.33, 11.2, 'RED WINE', weight='bold')

ax.axhline(11, color='grey', linewidth=1, alpha=0.5,
          xmin=0.67, xmax=0.98)
ax.text(1.75, 11.2, 'WHITE WINE', weight='bold')

# Setting the source, with 'backgroundcolor' parameter of `Axes.text()` function
ax.text(-0.7, -2.9, '©DATAQUEST' + ' '*92 + 'Source: P. Cortez et al.',
        color = '#f0f0f0', backgroundcolor = '#4d4d4d',
       size=12)

# Title of the graph
ax.text(-0.7, 13.5,
        'Wine Quality Most Strongly Correlated With Alcohol Level',
        size=17, weight='bold')
# Subtitle of the graph
ax.text(-0.7, 12.7,
        'Correlation values between wine quality and wine properties (alcohol, pH, etc.)')

plt.show()
```

>  ![DataVisualization(fiveThirtyEight)](C:\Users\tjp19\Desktop\Git\ML-Jupyter\StudyNotes\Notes\img\DataVisualization(fiveThirtyEight).png)
