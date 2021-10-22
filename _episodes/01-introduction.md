---
title: "Introduction"
teaching: 5
exercises: 0
questions:
- "Why use matplotlib for HEP?"
objectives:
- "Understand why matplotlib is useful for HEP"
keypoints:
- "Matplotlib is great for HEP!"
---
The example-based nature of [Matplotlib documentation](https://matplotlib.org/) is GREAT.

Matplotlib is the standard when it comes to making plots in Python. It is versatile and allows for lots of functionality and different ways to produce many plots.
We will be focusing on using matplotlib for High Energy Physics.

# A simple example

Matplotlib graphs your data on Figures (i.e., windows, Jupyter widgets, etc.), each of which can contain one or more Axes (i.e., an area where points can be specified in terms of x-y coordinates, or theta-r in a polar plot, or x-y-z in a 3D plot, etc.). The simplest way of creating a figure with an axes is using pyplot.subplots. We can then use Axes.plot to draw some data on the axes:

```python
fig, ax = plt.subplots()  # Create a figure containing a single axes.
ax.plot([1, 2, 3, 4], [1, 4, 2, 3])  # Plot some data on the axes.
```
this code produces the following figure

![basic_plot](https://matplotlib.org/stable/_images/sphx_glr_usage_002.png)

# What goes into a plot?

Now, let's have a deeper look at the components of a Matplotlib figure.

![parts of image](https://matplotlib.org/stable/_images/anatomy.png)



{% include links.md %}
