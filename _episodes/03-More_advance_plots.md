---
title: "More advance plots"
teaching: 5
exercises: 0
questions:
- "What dataset is being used?"
objectives:
- "Briefly describe the dataset."
keypoints:
- "One must know a bit about your data before any machine learning takes place."
---


# Code Example

Here we will import required libraries for the rest of the tutorial.

~~~
import pandas as pd # to store data as dataframe
import numpy as np # for numerical calculations such as histogramming
~~~
{: .language-python}

You can check the version of these packages by checking the `__version__` attribute.

~~~
np.__version__
~~~
{: .language-python}


# Dataset Used

The dataset we will use in this tutorial is ATLAS data. Some events correspond to a Higgs Boson decay (<span style="color:orange">signal</span>) and others do not (<span style="color:blue">background</span>). Various physical quantities such as lepton charge and transverse momentum are recorded for each event. The analysis in this tutorial loosely follows [the discovery of the Higgs Boson](https://www.sciencedirect.com/science/article/pii/S037026931200857X).

# Exploring the Dataset

We need to format the dataset so we can explore! First, we open our data set and read it into pandas DataFrames.

~~~
# get data from files

DataFrames = {} # define empty dictionary to hold dataframes
for s in samples_list: # loop over samples
    DataFrames[s] = pd.read_csv('/kaggle/input/.../'+s+".csv") # read .csv file

DataFrames # print data to take a look
~~~
{: .language-python}

where `...` depends on which dataset you want to read.

Before diving into plotting, there may be things you should do to clean up your data. 

