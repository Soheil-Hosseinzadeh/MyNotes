---
jupyter:
  jupytext:
    cell_metadata_filter: -all
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

In this quick tutorial we tend to learn some basics of **matplot** library and the way to use it in data analysis.

### What is Matplotlib.pyplot ?
Pyplot is a collection of commands and functions by which we can create charts or make changes in them.

### Drawing lines in matplotlib
- create x and y in seperate lists
- plotting the points by `plot` function
- naming x-axis and y-axis by `.xlabel` and `.ylablel`
- giving a title by `.title`
- showing the plot by `.show` function
```python
import matplotlib.pyplot as plt
x = [1, 4, 7]
y = [4, 2, 9]
plt.plot(x, y)
plt.xlabel("x axis")
plt.ylabel("y axis")
plt.title("test")
plt.show()
```

>Another example with 2 lines and a legend info box:
```python
import matplotlib.pyplot as plt 
# line 1 points 
x1 = [1,2,3] 
y1 = [2,4,1] 
# plotting the line 1 points 
plt.plot(x1, y1, label = "line 1") 
# line 2 points 
x2 = [1,2,3] 
y2 = [4,1,3] 
# plotting the line 2 points 
plt.plot(x2, y2, label = "line 2") 
# naming the x axis 
plt.xlabel('x - axis') 
# naming the y axis 
plt.ylabel('y - axis') 
# giving a title to my graph 
plt.title('Two lines on same graph!') 
# show a legend on the plot 
plt.legend() 
# function to show the plot 
plt.show()
```

>Some more custom example:
```python
import matplotlib.pyplot as plt 
# x axis values 
x = [1,2,3,4,5,6] 
# corresponding y axis values 
y = [2,4,1,5,2,6] 
# plotting the points 
plt.plot(x, y, color='green', linestyle='dashed', linewidth = 3, 
		marker='o', markerfacecolor='blue', markersize=12) 
# setting x and y axis range 
plt.ylim(1,8) 
plt.xlim(1,8) 
# naming the x axis 
plt.xlabel('x - axis') 
# naming the y axis 
plt.ylabel('y - axis') 
# giving a title to my graph 
plt.title('Some cool customizations!') 
# function to show the plot 
plt.show()
```

### Creating Bar Plot
```python
import matplotlib.pyplot as plt   
# x-coordinates of left sides of bars   
left = [1, 2, 3, 4, 5]   
# heights of bars   
height = [10, 20, 30, 40, 50]   
# labels for bars   
tick_label = ['one', 'two', 'three', 'four', 'five']   
# plotting a bar chart   
plt.bar(left, height,  = tick_label,   
        width = 0.8, color = ['blue', 'green', 'red','yellow','black'])   
# naming the x-axis   
plt.xlabel('x - axis')   
# naming the y-axis   
plt.ylabel('y - axis')   
# plot title   
plt.title('bar chart!')   
# function to show the plot   
plt.show()
```

### Plotting Histogram
```python
import matplotlib.pyplot as plt   
# frequencies   
ages = [2,5,70,40,30,45,50,45,43,40,44,   
        60,7,13,57,18,90,77,32,21,20,40]   
# setting the ranges and no. of intervals   
range = (0, 100)   
bins = 5
# plotting a histogram   
plt.hist(ages, bins, range, color ='green',   
        histtype = 'bar', rwidth = 0.8)   
# x-axis label   
plt.xlabel('age')   
# frequency label   
plt.ylabel('No. of people')   
# plot title   
plt.title('My histogram')   
# function to show the plot   
plt.show()
```

### Plotting Scatter Plot
```python
import matplotlib.pyplot as plt
import numpy.random as rnd
x = rnd.randint(1, 21, 100)
y = rnd.randint(4, 30, 100)

plt.scatter(x, y, label="stars", marker=".", color="red")
plt.xlabel("x-axis")
plt.ylabel("y-axis")
plt.legend()
plt.show()
```

### Plotting Pie-Chart
```python
import matplotlib.pyplot as plt

# defining labels
activities = ["eat", "sleep", "work", "play"]
# portion covered by each label
slices = [3, 7, 8, 6]
# color for each label
colors = ["r", "y", "g", "b"]
# plotting the pie chart
plt.pie(
    slices,
    labels=activities,
    colors=colors,
    startangle=90,
    shadow=True,
    explode=(0, 0, 0.06, 0),
    radius=1.2,
    autopct="%1.1f%%",
)
# plotting legend
plt.legend(loc=(1, 1))
# showing the plot
plt.show()
```

### Plotting the figure of a function
```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(0.001, 100, 0.01)
y = np.log10(x)

plt.plot(x, y)
plt.xlabel("x")
plt.ylabel("log10(x)")

plt.show()
```

### SubPlots
```python
import numpy as np
import matplotlib.pyplot as plt


def create_plot(ptype):
    # setting the x-axis vaues
    x = np.arange(-10, 10, 0.01)
    # setting the y-axis values
    if ptype == "linear":
        y = x
    elif ptype == "quadratic":
        y = x**2
    elif ptype == "cubic":
        y = x**3
    elif ptype == "quartic":
        y = x**4
    return (x, y)

fig = plt.figure()

plt1 = fig.add_subplot(2, 2, (1, 2))
plt2 = fig.add_subplot(2, 2, 3)
plt3 = fig.add_subplot(224)

x, y = create_plot("cubic")
plt1.plot(x, y, color="red")
plt1.set_title("$y_1=x^3$")

x, y = create_plot("quadratic")
plt2.plot(x, y, color = "g")
plt2.set_title("$y_2=x^2$")

x, y = create_plot("linear")
plt3.plot(x, y)
plt3.set_title("$y_3=x$")

fig.tight_layout(pad=1.1)
plt.show()
```

>In the `add_subplot` method we give three integers as input: `nrows`, `ncols`, `subplotIndex` by which specify the index of the subplot in a grid with `nrows` rows and `ncols` columns.
>The index start from the upper left and continues to the right.

```python
import matplotlib.pyplot as plt
import numpy as np

def create_plot(ptype):
    # setting the x-axis vaues
    x = np.arange(0.5, 20, 0.01)
    # setting the y-axis values
    if ptype == "sin":
        y = np.sin(x)
    elif ptype == "tan":
        y = np.sin(x)/np.cos(x)
    elif ptype == "damped":
        y = (x**(-1/2))*np.sin(x)
    return (x, y)

plt1 = plt.subplot2grid((14, 1), (0, 0), rowspan=3, colspan=1)
plt2 = plt.subplot2grid((14, 1), (5, 0), rowspan=3, colspan=1)
plt3 = plt.subplot2grid((14, 1), (10, 0), rowspan=3, colspan=1)

x, y = create_plot("damped")
plt1.plot(x, y, color="g")
# plt1.set_ylim(-1, 1)

x, y = create_plot("sin")
plt2.plot(x, y, color="b")

x, y = create_plot("tan")
plt3.plot(x, y, color="r")
plt3.set_ylim(-5, 5)

plt.show()
```

in the above code:
`plt1 = plt.subplot2grid((14, 1), (0, 0), rowspan=3, colspan=1)`
`(14, 1)`: the size of the grid that contains the subplots
`(0, 0)`: the location of the subplot
`rowspan`: subplot rows
`colspan`: subplot columns

### Plotting 3D lines and dots
We first need to create 3D axes by `plt.axes(projection="3d")` then we use `ax.plot3D` and `ax.scatter3D` to create 3D lines and dots.
Let's see some example:
```python
# import mpl_toolkits.mplot3d
import numpy as np
import matplotlib.pyplot as plt

ax = plt.axes(projection="3d")

z = np.arange(0, 15, 0.1)
x = np.sin(z)
y = np.cos(z)

ax.plot3D(x, y, z, "gray", linewidth=1)
ax.set_xlabel("x")
ax.set_ylabel("y")

zData = 15 * np.random.rand(100)
xData = np.sin(zData) + 0.1 * np.random.rand(100)
yData = np.cos(zData) + 0.1 * np.random.rand(100)

ax.scatter3D(xData, yData, zData, c=zData, cmap="Blues", edgecolor='black')
plt.show()
```

### Plotting 3D contours
>While using methods like `ax.contour`, `ax.plot_surface` and ... we usually have to have to give `X`, `Y` and `Z` inputs by `np.meshgrid` method with `xy` indexing order.
```python
import matplotlib.pyplot as plt
import numpy as np

def f(x, y):
    return np.sin(np.sqrt(x**2 + y**2))

x = np.arange(-15, 15, 0.1)
y = np.arange(-15, 15, 0.1)

X, Y = np.meshgrid(x, y)
Z = f(X, Y)

ax = plt.axes(projection="3d")
ax.contour3D(X, Y, Z, levels=70, cmap="viridis")
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.set_zlabel("z")

plt.show()
```

### Plotting wireframes and surfaces
```python
ax = plt.axes(projection="3d")

def f(x, y):
    return np.sin(np.sqrt(x**2 + y**2))

x = np.arange(-6, 6, 0.4)
y = np.arange(-6, 6, 0.4)

X, Y = np.meshgrid(x, y)
Z = f(X, Y)

ax.plot_wireframe(X, Y, Z, color="darkRed")
ax.set_title("wireframe")
plt.show()
```


```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(-5, 5, 0.05)
y = np.arange(-5, 5, 0.05)

X, Y = np.meshgrid(x, y)
Z = f(X, Y)

ax = plt.axes(projection="3d")
ax.plot_surface(X, Y, Z, cmap="viridis")
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.set_title("surface")

plt.show()
```
