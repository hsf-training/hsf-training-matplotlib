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
> ## Auto-show in jupyter notebooks
>
> The jupyter backends (activated via `%matplotlib inline`, `%matplotlib notebook`, or `%matplotlib widget`), call show() at the end of every cell by default. Thus, you usually don't have to call it explicitly there.
{: .callout}



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
       'mZ1', 'mZ2', 'mllll', 'totalWeight'],
      dtype='object')
~~~
{: .output} 

You can see from the output that we have some kinematic variables for the leptons, as well as the mass of the Z1 and Z2 candidates that form the Higgs boson.  
We will like to make a plot of this two masses ...

### MC stack plot
To do this, we will make first a plot only using the MC samples, and we will plot them using the stack option of the hist function of matplotlib.

The first parameter 'x' of the `plt.hist` function allows us to plot multiple data, we can pass it a list of the variable we would like to plot for the different data frames we have for MC.

The list of the MC distributions is:
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
Let's run the function for the variable 'mZ1' and verify the len of the list.
~~~
var_samples=stack_mc_list('mZ1')
print(len(var_samples))
~~~
{: .language-python}
~~~
3
~~~
{: .output}
We can now work in the function that will make the stack plot giving the previous list.
~~~
def plot_stacklist(stack_samples_list, list_label, var, var_units, range_ab, bins_i):
    #Create a new figure
    fig=plt.figure(figsize=(10,8))
    #Create the histograma for the multiple samples in stack_samples_list, 
    #list_label will be a list with the names of the samples in the same order than stack_samples_list
    h=plt.hist(stack_samples_list, range=range_ab, bins=bins_i, label=list_label, stacked=True)
    #Add the x and y label 
    plt.ylabel('Events', fontsize=18 ,loc='top')
    plt.xlabel(var+var_units, fontsize=18,loc='right')
    #Change the appearance of ticks, inside of the axes, draw right and top thicks. 
    plt.tick_params(which='both', direction='in', top=True, right=True, length=6, width=1)
    #Modify the current tick label size
    plt.yticks(fontsize=16)
    plt.xticks(fontsize=16)
    #Place a legend on the axes and modify the font size of the legend.
    plt.legend(loc='best',fontsize=18,frameon=False)
~~~
{: .language-python}

Let's run the function given an example arguments for the variable 'mZ1':
~~~
plot_stacklist(var_samples, mc_samples,'mZ1','[GeV]',[60,120],50)
~~~
{: .language-python}
![mZ1_hist_0]({{ page.root }}/fig/mZ1_hist0.png)

# Selection criteria



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





# Data vs. MC


{: .language-python}

Before diving into plotting, there may be things you should do to clean up your data. 

