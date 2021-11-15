---
title: "More advanced plots"
teaching: 5
exercises: 0
questions:
- "Why we need to explore Data vs. MC distributions?"
objectives:
- "Do some stacked plots with MC."
- "Apply a basic selection criteria."
- "Add error bars to the plot."
- "Perform a Data vs. MC plot comparison."
keypoints:
- "To do."
---


# MC distributions

In the previous episode, you were able to make basic plots of some physical variables using the MC and data samples that we have been working with.

Here we will focus on the principal MC samples that contribute more to the physics that we are looking for, this is 4 leptons final state,  and then we will compare it with real data.

First we need to import matplotlib, pandas and numpy as usual:
~~~
import matplotlib.pyplot as plt
%matplotlib inline
import pandas as pd
import numpy as np
~~~
{: .language-python}

We will work with 3 MC samples, the main backgrounds 'ttbar', 'llll', and the signal 'ggH125_ZZ44lep'.
Additionally, we have the data sample 'data'.

So, we need to start creating a list with the names of the samples:
~~~
samples_list = ['ttbar_lep','llll','ggH125_ZZ4lep', 'data']
~~~
{: .language-python}
and we will use it to open our samples as pandas dataframes.

For this we will write the next function that takes the above list and return a dictionary with the dataframes of the samples:
~~~
def created_dic(samples_list):
  dataFrame_dic = {}
  for s in samples_list: 
    dic_dfsamples[s] = pd.read_csv(path_samples+f'{s}.csv')
  return dataFrame_dic
~~~
{: .language-python}
Let's run the function and verify the keys of the dictionary
~~~
dic_dfSamples=created_dic(samples_list)
print(dic_dfSamples.keys())
~~~
{: .language-python}
~~~
dict_keys(['ttbar_lep', 'llll', 'ggH125_ZZ4lep', 'data'])
~~~
{: .output}
Let's access to the dataframe of our signal and take a look at all the variables that we have available
~~~
dic_dfsamples['ggH125_ZZ4lep'].columns
~~~
{: .language-python}
~~~
Index(['entry', 'lep_pt_0', 'lep_pt_1', 'lep_pt_2', 'lep_pt_3', 'lep_eta_0',
       'lep_eta_1', 'lep_eta_2', 'lep_eta_3', 'lep_phi_0', 'lep_phi_1',
       'lep_phi_2', 'lep_phi_3', 'lep_E_0', 'lep_E_1', 'lep_E_2', 'lep_E_3',
       'lep_charge_0', 'lep_charge_1', 'lep_charge_2', 'lep_charge_3',
       'lep_type_0', 'lep_type_1', 'lep_type_2', 'lep_type_3', 'lep_z0_0',
       'lep_z0_1', 'lep_z0_2', 'lep_z0_3', 'lep_sigd0_0', 'lep_sigd0_1',
       'lep_sigd0_2', 'lep_sigd0_3', 'lep_ptconerel_0', 'lep_ptconerel_1',
       'lep_ptconerel_2', 'lep_ptconerel_3', 'lep_etconerel_0',
       'lep_etconerel_1', 'lep_etconerel_2', 'lep_etconerel_3', 'min_mll',
       'mZ1', 'mZ2', 'mllll'],
      dtype='object')
~~~
{: .output} 

You can see from the output that we have some kinematic variables for the leptons, as well as the mass of the Z1 and Z2 candidates that form the Higgs boson.  
We will like to make a plot of this two masses ...

### MC stack plot
To do this, we will make first a plot only using the MC samples, and we will plot them using the stack option of the hist function of matplotlib.

The first parameter 'x' of the plt.hist function allows us to plot multiple data, we can pass it a list of the different datasets that we would like to plot.
Then the list of the MC distributions is:
~~~
mc_samples=samples_list[:3]
~~~
{: .language-python}

Then, we will define a function that returns a list of the variable we want to plot, for the samples listed in the input list.

~~~
def stack_mc_list(var, mc_samples):
    stack_samples_list=[]
    for s in mc_samples:
        stack_samples_list.append(dic_dfsamples[s][var])
    return stack_samples_list
~~~
{: .language-python}
> ## Exercise
>
> Note
>
> > ## Solution
> >
> > o
> >
> > ~~~
> > len()
> > ~~~
> > {: .language-python}
> > ~~~
> > output
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}


# Selection criteria


# Data vs. MC


{: .language-python}

Before diving into plotting, there may be things you should do to clean up your data. 

