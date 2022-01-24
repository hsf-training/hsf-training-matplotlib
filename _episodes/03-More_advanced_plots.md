---
title: "More advanced plots"
teaching: 5
exercises: 0
questions:
- "Why do we need to explore Data vs. MC distributions?"
objectives:
- "Do some stacked plots with MC."
- "Apply a basic selection criteria."
- "Add error bars to the plot."
- "Perform a Data vs. MC plot comparison."
keypoints:
- "To do."
---


# MC distributions

In the previous episode, you were able to make basic plots of some physical variables using a few data samples from the Atlas open data dataset that we are using.

Here we will use all the 4 leptons final state samples that we have available for this tutorial, these are MC and data.

The goal is to discover the Higgs component in data comparing the final distributions of MC and data in the mass of the 4 leptons variable.

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



In the following dictionary, we have classified the samples we will work on, starting with the "data" samples, 
followed by the "higgs" MC samples and at the end the zz" and "others" MC background components.
~~~
samples_dic= {'data': [['data', 'data_A'], 
                       ['data', 'data_B'], 
                       ['data', 'data_C'], 
                       ['data', 'data_D']],
              'higgs': [['mc', 'mc_345060.ggH125_ZZ4lep'], 
                        ['mc', 'mc_344235.VBFH125_ZZ4lep']], 
              'zz': [['mc', 'mc_363490.llll']], 
              'other': [['mc', 'mc_361106.Zee'], 
                        ['mc', 'mc_361107.Zmumu']]}
~~~
{: .language-python}
We will use uproot to read the content of our samples that are in ROOT format. 
~~~
import uproot3 as uproot
~~~
{: .language-python}
> ## Uproot tutorial
>
> If you want to lear more of the Uproot python Module you can take a look to the tutorial also given by the HEP software foundation in the following link
> <https://hsf-training.github.io/hsf-training-uproot-webpage/index.html>
{: .callout}

For this we will write the next function that takes the above list and return a dictionary with the dataframes of the samples:
~~~
processes = samples_dic.keys()
Tuples={}
samples=[]
for p in processes:
    for d in samples_dic[p]:
        # Load the dataframes
        sample = d[1] # Sample name
        samples.append(sample)
        DataUproot = uproot.open(f'/kaggle/input/reducehiggs4lep/samples_FilterGem_{sample}.root')
        Tuples[sample] = DataUproot['myTree']
~~~
{: .language-python}
Let's take a look to the variables stored in out data samples, taking "data_A" as example
~~~
list(Tuples['data_A'].allkeys())
~~~
{: .language-python}
~~~
[b'trigM',
 b'm4l',
 b'lep_pt',
 b'sum_good_lep',
 b'lep_charge',
 b'lep_type',
 b'trigE',
 b'sum_lep_charge',
 b'channelNumber',
 b'goodlep_sumtypes',
 b'eventNumber',
 b'XSection',
 b'good_lep',
 b'lep_n',
 b'lep_z0',
 b'weight',
 b'lep_phi',
 b'runNumber',
 b'lep_eta',
 b'lep_E']
 ~~~
{: .output}
Let's access to the variables or branches as we normally called, and make a simple plot 
~~~
branches={}
for s in samples:
    branches[s] = Tuples[s].arrays(namedecode='utf-8')
~~~
{: .language-python}

Using the hist method we can visualize the distribution the mass of the 4 leptons "m4l" for this "data_A" sample. 
~~~
plt.hist(branches['data_A']['m4l'])

~~~
{: .language-python}

~~~
(array([ 3., 13.,  3.,  5.,  4.,  2.,  0.,  0.,  1.,  1.]),
 array([ 19.312525,  82.30848 , 145.30444 , 208.3004  , 271.29636 ,
        334.2923  , 397.28827 , 460.2842  , 523.28015 , 586.2761  ,
        649.2721  ], dtype=float32),
 <BarContainer object of 10 artists>)
~~~
{: .output} 

![nMuon_hist_1]({{ page.root }}/fig/m4lep_hist_1.png)

# Selection criteria
Is very important to include some selection criteria in our histograms that we are analyzing. 
These selections are commonly know as "cuts".
With these cuts we are able to select only events of our interest, this is, we will have a subset of our original samples and the distribution are going to change after this cuts.
This will help out to do some physics analysis and start to search for the physics process in which we are interested.
In this case is the 4 lepton final state.

To do this, we will select from all samples that the following:

- the leptons needed to activate either the muon or electron trigger,
- number of leptons in the final state should be 4,
- the total net charge should be zero,
- the sum of the types (11:e, 13:mu) can be 44 (eeee), 52 (mumumumu) or 48 (eemumu),
- good leptons with high transverse momentum

Let's visualize some of these requirements TO DO

Finally, we will apply all the requirements mentioned above to all samples as follows:
~~~
selection_events={}
for s in samples:
    trigger = ((branches[s]['trigM'] == True) | (branches[s]['trigE'] == True))
    sum_leptons = branches[s]['sum_good_lep'] == 4
    sum_charge = branches[s]['sum_lep_charge'] == 0
    sum_types_ee = branches[s]['goodlep_sumtypes'] == 44
    sum_types_mm = branches[s]['goodlep_sumtypes'] == 52
    sum_types_em = branches[s]['goodlep_sumtypes'] == 48
    sum_types_goodlep = (sum_types_ee | sum_types_mm | sum_types_em)
    sum_lep_selection = (sum_leptons & sum_charge & sum_types_goodlep)
    # Select good leptons with high transverse momentum
    pt_0_selection = ((branches[s]['lep_pt'][:,0] > 25000) & (branches[s]['good_lep'][:,0] == 1))
    pt_1_selection = ((branches[s]['lep_pt'][:,1] > 15000) & (branches[s]['good_lep'][:,1] == 1))
    pt_2_selection = ((branches[s]['lep_pt'][:,2] > 10000) & (branches[s]['good_lep'][:,2] == 1))
    high_pt_selection = (pt_0_selection & pt_1_selection & pt_2_selection)
    final_selection = trigger & sum_types_goodlep & sum_lep_selection & high_pt_selection
    selection_events[s] = final_selection
~~~
{: .language-python}



Additionally,  


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

