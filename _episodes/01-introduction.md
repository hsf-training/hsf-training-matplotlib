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
A with any python code it is always a good practice to import the necessary libraries as a first step.

```python
import matplotlib.pyplot as plt
```

Matplotlib graphs your data on Figures (i.e., windows, Jupyter widgets, etc.), each of which can contain one or more Axes (i.e., an area where points can be specified in terms of x-y coordinates, or theta-r in a polar plot, or x-y-z in a 3D plot, etc.). The simplest way of creating a figure with an axes is using pyplot.subplots. We can then use Axes.plot to draw some data on the axes:

```python
fig, ax = plt.subplots()  # Create a figure containing a single axes.
ax.plot([1, 2, 3, 4], [1, 4, 2, 3])  # Plot some data on the axes.
```
this code produces the following figure

![basic_plot](https://matplotlib.org/stable/_images/sphx_glr_usage_002.png)


> ## Notice
> If you look at the plot and the order of the list of numbers you can clearly see that the order of the arguments is of the form
>
> ~~~
> plot(xpoints,ypoints)
> ~~~
> {: .language-python}
>
>But what is useful is that if we wanted to do more than one plot in the same figure we could do this in two main ways.
> ~~~
> plot(xpoints,ypoints , xpoints_2,ypoints_2, xpoints_3,ypoints_3)
> ~~~
> {: .language-python}
Or the more traditional way
> ```python
> plot(xpoints,ypoints)
> plot(xpoints_2,ypoints_2)
> plot(xpoints_3,ypoints_3)
> ```
> Both methods allow you to produce a plot like the following *(we will later see how to produce them in more detail)*
> > ## See example plot
> >
> > ![3linesplot_ver1](../fig/3linesplot_ver2.png)
> {: .solution}
{: .callout}


# What goes into a plot?

Now, let's have a deeper look at the components of a Matplotlib figure.

![parts of image](https://matplotlib.org/stable/_images/anatomy.png)



{% include links.md %}
