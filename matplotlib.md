# Matplotlib Cheat Sheet

1. [Create Plot](#1-create-plot)
    + [Import Library](#import-library)
    + [Create Figure](#create-figure)
    + [Adjust Figure Size](#adjust-figure-size)
    + [Axes](#axes)
    + [Add Axes](#add-axes)
    + [Add Axes v2](#add-axes-v2)
2. [Plotting (1D)](#2-plotting-1d)
    + [Draw points with lines](#draw-points-with-lines)
    + [Draw scatter points](#draw-scatter-points)
    + [Draw a vertical bar chart](#draw-a-vertical-bar-chart)
    + [Draw a horizontal bar chart](#draw-a-horizontal-bar-chart)
    + [Draw horizontal line](#draw-horizontal-line)
    + [Draw vertical line](#draw-vertical-line)
    + [Draw filled polygon](#draw-filled-polygon)
    + [Draw histogram](#draw-histogram)
    + [Draw boxplot](#draw-boxplot)
    + [Draw violin plot](#draw-violin-plot)
3. [Plotting (2D)](#3-plotting-2d)
4. [Plotting (3D)](#4-plotting-3d)
5. [Customize Plot](#5-customize-plot)
    + [Color](#color)
    + [Transparency](#transparency)
    + [Colormap](#colormap)
    + [Marker](#marker)
    + [Line Width](#line-width)
    + [Line Style](#line-style)
    + [Add Text](#add-text)
    + [Math text(LaTex)](#math-text-latex)
    + [Plot Padding](#plot-padding)
    + [Aspect Ratio to 1](#aspect-ratio-to-1)
    + [Limit Axes](#limit-axes)
    + [Limit x-Axis (or Y-axis)](#limit-x-axis--or-y-axis)
    + [Set Title, x- and y-axis Labels](#set-title--x--and-y-axis-labels)
    + [Set Ticks](#set-ticks)
6. [Save Plot](#6-save-plot)
    + [Save Figures](#save-figures)
    + [Save Transparent Figures](#save-transparent-figures)
7. [Show Plot](#7-show-plot)
8. [Extras](#8-extras)
    + [Clear an Axis](#clear-an-axis)
    + [Clear Figure](#clear-figure)
    + [Close Window](#close-window)

## 1. Create Plot
#### Import Library
```python
import matplotlib.pyplot as plt
```

#### Create Figure
```python
fig = plt.figure()
```

#### Adjust Figure Size
```python
fig2 = plt.figure(figsize=(w,h))
fig2 = plt.figure(figsize=plt.figaspect(2.0)) # Twice the Height
```

#### Axes
All plotting is done with respect to an Axes. A subplot is contained within a figure and a subplot is an axes in a grid system.

#### Add Axes
```python
fig.add_axes() 
ax1 = fig.add_subplot(221) # 2 rows by 2 rows, first subplot
ax3 = fig.add_subplot(212) # 2 rows by 1 row, second subplot
```

#### Add Axes v2
```python
fig3, axes = plt.subplots(nrows=2,ncols=2) # 2 by 2 subplots
fig4, axes2 = plt.subplots(ncols=3) # 1 row by 3 columns
```

## 2. Plotting (1D)
#### Draw points with lines
[docs](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.plot.html)
```python
ax.plot(x,y)
```

#### Draw scatter points
[docs](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.scatter.html?highlight=scatter#matplotlib.pyplot.scatter)
```python
ax.scatter(x,y)
```

#### Draw a vertical bar chart
[docs](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.bar.html?highlight=bar#matplotlib.pyplot.bar)
```python
ax.bar([1,2,3],[3,4,5])
```

#### Draw a horizontal bar chart
[docs](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.barh.html?highlight=barh#matplotlib.pyplot.barh)
```python
ax.barh([0.5,1,2.5],[0,1,2])
```

#### Draw horizontal line
[docs](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.axhline.html?highlight=axhline#matplotlib.pyplot.axhline)
```python
ax.axhline(0.45)
```

#### Draw vertical line
[docs](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.axvline.html?highlight=axvline#matplotlib.pyplot.axvline)
```python
ax.axvline(0.45)
```

#### Draw filled polygon
[docs](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.fill.html?highlight=fill#matplotlib.pyplot.fill)
```python
ax.fill(x,y,color='blue')
```

#### Draw histogram
[docs](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.hist.html?highlight=hist#matplotlib.pyplot.hist)
```python
ax.hist(y)
```

#### Draw boxplot
[docs](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.boxplot.html?highlight=boxplot#matplotlib.pyplot.boxplot)
```python
ax.boxplot(y)
```

#### Draw violin plot
[docs](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.violinplot.html?highlight=violinplot#matplotlib.pyplot.violinplot)
```python
ax.violinplot(z)
```

## 3. Plotting (2D)
[docs](https://matplotlib.org/stable/api/image_api.html)
```python
ax.imread(img) # read stored image/array
ax.imshow(img, cmap='gist_earth', interpolation='nearest',  vmin=-2, vmax=2) # show image
```

## 4. Plotting (3D)
[docs](https://matplotlib.org/stable/tutorials/toolkits/mplot3d.html#toolkit-mplot3d-tutorial)
```python
fig = plt.figure()
ax = fig.add_subplot(projection='3d')
```

## 5. Customize Plot
#### Color
[list of colors](https://matplotlib.org/stable/gallery/color/named_colors.html)
```python
ax.plot(x, y, c='yellow')
```

#### Transparency
```python
ax.plot(x, y, alpha=0.4)
```

#### Colormap
[list of colormaps](https://matplotlib.org/stable/tutorials/colors/colormaps.html)
```python
ax.imshow(img, cmap='seismic')
```

#### Marker
[list of markers](https://matplotlib.org/stable/api/markers_api.html)
```python
ax.scatter(x, y, marker=".")
ax.scatter(x, y, marker="o")
```

#### Line Width
```python
ax.plot(x, y,linewidth=4.0)
```

#### Line Style
[list of linestyles](https://matplotlib.org/stable/gallery/lines_bars_and_markers/linestyles.html)
```python
ax.plot(x, y, ls='solid')
ax.plot(x, y, ls='--')
```

#### Add Text
```python
x_pos, y_pos = 1, 10
ax.text(x_pos, y_pos, 'Example Graph', style='italic')
```

#### Math text(LaTex)
[docs](https://matplotlib.org/stable/tutorials/text/usetex.html)
```python
plt.title(r'$sigma_i=15$', fontsize=20)
```

#### Plot Padding
```python
ax.margins(x=0.0,y=0.1)
```

#### Aspect Ratio to 1
```python
ax.axis('equal')
```

#### Limit Axes
[docs](https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.set_xlim.html)
```python
ax.set(xlim=[0,10.5],ylim=[-1.5,1.5])
```

#### Limit x-Axis (or Y-axis)
```python
ax.set_xlim(0,10.5)
ax.set_ylim(-1.5,1.5)
```

#### Set Title, x- and y-axis Labels
```python
ax.set(title='An Example Axes', ylabel='Y', xlabel='X')
```

#### Set Ticks
```python
ax.xaxis.set(ticks=range(1,5), ticklabels=[3, 100, "foo"])
ax.yaxis.set(ticks=range(1,5), ticklabels=[1, 200, "bar"])
```

## 6. Save Plot
#### Save Figures
```python
plt.savefig('foo.png')
```

#### Save Transparent Figures
```python
plt.savefig('foo.png', transparent=True)
```

## 7. Show Plot
```python
plt.show()
```

## 8. Extras
#### Clear an Axis
```python
plt.cla()
```

#### Clear Figure
```python
plt.clf()
```

#### Close Window
```python
plt.close()
```