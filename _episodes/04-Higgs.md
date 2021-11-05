---
title: "Higgs"
teaching: 5
exercises: 5
questions:
- "How might I plot a data vs MC comparison?"
objectives:
- "Provide an example data vs MC comparison plot"
keypoints:
- "Data vs MC comparison plots look nice with matplotlib!"
---

FIXME

plot such as

![m4l](../fig/m4l.jpg){:width="40%"}

from [the ATLAS Higgs discovery paper](https://www.sciencedirect.com/science/article/pii/S037026931200857X#fg0020).

Access the 'Matplotlib Data vs MC' notebook you created in the [Setup page](https://hsf-training.github.io/hsf-training-matplotlib/setup.html)


~~~
plt.hist(DataFrames['ggH125_ZZ4lep']['mllll'])
~~~
{: .language-python}

Did you learn at school that you always need axes labels? Well it's still true! 

~~~
plt.hist(DataFrames['ggH125_ZZ4lep']['mllll'])
plt.xlabel('m4l [GeV]')
plt.ylabel('Events')
~~~
{: .language-python}

Ok ok, but the x-axis values are very different compared to the graph we're aiming to reproduce. The x-axis on the graph we're trying to reproduce starts at 80 and ends at 250 in steps of 5. Notice how this code produces an array of values starting at 80 and ending at 250, in steps of 5. 

~~~
np.arange(start=80, # The interval includes this value
          stop=250+5, # The interval doesn't include this value
          step=5 ) # Spacing between values
~~~
{: .language-python}

Now let's use this.

~~~
bin_edges = np.arange(start=80, # The interval includes this value
                      stop=250+5, # The interval doesn't include this value
                      step=5 ) # Spacing between values
plt.hist(DataFrames['ggH125_ZZ4lep']['mllll'], bins=bin_edges)
plt.xlabel('m4l [GeV]')
plt.ylabel('Events')
~~~
{: .language-python}

But why are our y-axis values so different to that in the paper? It's because we haven't used "weights". So here we go.

~~~
plt.hist(DataFrames['ggH125_ZZ4lep']['mllll'], bins=bin_edges, 
         weights=DataFrames['ggH125_ZZ4lep']['totalWeight'])
plt.xlabel('m4l [GeV]')
plt.ylabel('Events')
~~~
{: .language-python}

Ok nice, but so far we've only used signal. Let's stack signal on top of the backgrounds.

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames['ggH125_ZZ4lep']['mllll'])
    weight_list.append(DataFrames['ggH125_ZZ4lep']['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True)
plt.xlabel('m4l [GeV]')
plt.ylabel('Events')
~~~
{: .language-python}

Another thing you may have learnt at school is to always have a legend. Still true here!

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=samples_list)
plt.xlabel('m4l [GeV]')
plt.ylabel('Events')
plt.legend()
~~~
{: .language-python}

Let's use the same colours as the paper.

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=samples_list, color=colors_list)
plt.xlabel('m4l [GeV]')
plt.ylabel('Events')
plt.legend()
~~~
{: .language-python}

Our x-axis label should really have a superscript. Let's do that now.

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=samples_list, color=colors_list)
plt.xlabel('$m_{4l}$ [GeV]')
plt.ylabel('Events')
plt.legend()
~~~
{: .language-python}

and it'd be even nicer if our label wasn't italicised.

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=samples_list, color=colors_list)
plt.xlabel('$\mathrm{m_{4l}}$ [GeV]')
plt.ylabel('Events')
plt.legend()
~~~
{: .language-python}

Oh and we should also modify the y-axis label to be in line with the paper.

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=samples_list, color=colors_list)
plt.xlabel('$\mathrm{m_{4l}}$ [GeV]')
plt.ylabel('Events/5 GeV')
plt.legend()
~~~
{: .language-python}

Can we move the x-axis label to be on the right, like in the paper?

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=samples_list, color=colors_list)
plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1)
plt.ylabel('Events/5 GeV')
plt.legend()
~~~
{: .language-python}

Ok but that's moved it too far. How about now?

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=samples_list, color=colors_list)
plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV')
plt.legend()
~~~
{: .language-python}

Can you do the same for the y-axis?

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=samples_list, color=colors_list)
plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()
~~~
{: .language-python}

Notice how in the graph from the paper, the x-axis really starts and ends at 80 and 250. Whereas for us there's currently a bit of space either side. Can we fix that?

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=samples_list, color=colors_list)
plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()

# set the x-limit of the axes
plt.xlim( left=80, right=250 )
~~~
{: .language-python}

Ok now let's add some text to the plot.

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=samples_list, color=colors_list)
plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data')
~~~
{: .language-python}

and make it bold.

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=samples_list, color=colors_list)
plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold')
~~~
{: .language-python}

and increase the font size a bit.

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=samples_list, color=colors_list)
plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')
~~~
{: .language-python}

How about some more text? We need to place a `r` before the string of text to be able to use the latex `\rightarrow`.

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=samples_list, color=colors_list)
plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$H \rightarrow ZZ^{(*)} \rightarrow 4l$')
~~~
{: .language-python}

Once again, we can de-italicise the latex with `mathrm`:

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=samples_list, color=colors_list)
plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')
~~~
{: .language-python}

One last bit of text...

~~~
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=samples_list, color=colors_list)
plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')
~~~
{: .language-python}

How about we make the legend labels like those in the paper?

~~~
labels_list = ['Background Z+jets,tt', 'Background ZZ$^{(*)}$', 
               r'Signal ($\mathrm{m_{H}}$=125 GeV)']
mllll_list = []
weight_list = []
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
         label=labels_list, color=colors_list)
plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')
~~~
{: .language-python}

Cool. Now let's add uncertainties to the plot.

~~~
bin_centres = np.arange(start=80+5/2, # The interval includes this value
                        stop=250+5/2, # The interval doesn't include this value
                        step=5 ) # Spacing between values

mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list, color=colors_list)

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err) # heights

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')
~~~
{: .language-python}

You might just be able to see some new blue bars at the bottom of your plot. But we want the uncertainty bars to start further up. Let's do that.

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list, color=colors_list)

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err) 

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')
~~~
{: .language-python}

Ok we've moved the uncertainty bars up. Now we want to make them as wide as the other bars.

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list, color=colors_list)

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err, width=5) 

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')
~~~
{: .language-python}

Now let's give them those diagonal line hatches.

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list, color=colors_list)

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err, width=5, hatch="////") 

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')
~~~
{: .language-python}

and we can even make the uncertainty bars transparent.

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list, color=colors_list)

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err, width=5, hatch="////", color='none') 

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')
~~~
{: .language-python}

But of course we need to add a legend label for the uncertainty bars!

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list, color=colors_list)

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err, width=5, hatch="////", color='none', label='Stat. Unc.') 

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')
~~~
{: .language-python}

Nice. But in the paper, the uncertainty bars start at the same height as the light blue signal. So we need to modify a few parts of the code.

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    if s=='ggH125_ZZ4lep': continue # skip if signal
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list[:-1], 
                      color=colors_list[:-1])

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the signal bar
plt.hist(DataFrames['ggH125_ZZ4lep']['mllll'], bins=bin_edges, bottom=mc_x_tot, 
         weights=DataFrames['ggH125_ZZ4lep']['totalWeight'], color=colors_list[-1],
         label=labels_list[-1])

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err, width=5, hatch="////", color='none', label='Stat. Unc.') 

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend()

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')
~~~
{: .language-python}

In the paper, there's no box around the legend. We can do that too! Adding `frameon=False` to `plt.legend`.

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    if s=='ggH125_ZZ4lep': continue # skip if signal
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list[:-1], 
                      color=colors_list[:-1])

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the signal bar
plt.hist(DataFrames['ggH125_ZZ4lep']['mllll'], bins=bin_edges, bottom=mc_x_tot, 
         weights=DataFrames['ggH125_ZZ4lep']['totalWeight'], color=colors_list[-1],
         label=labels_list[-1])

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err, width=5, hatch="////", color='none', label='Stat. Unc.') 

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend(frameon=False)

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')
~~~
{: .language-python}

In the paper, the x and y-axis ticks are inside the axes as opposed to outside as we currently have them. But we can change that!

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    if s=='ggH125_ZZ4lep': continue # skip if signal
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list[:-1], 
                      color=colors_list[:-1])

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the signal bar
plt.hist(DataFrames['ggH125_ZZ4lep']['mllll'], bins=bin_edges, bottom=mc_x_tot, 
         weights=DataFrames['ggH125_ZZ4lep']['totalWeight'], color=colors_list[-1],
         label=labels_list[-1])

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err, width=5, hatch="////", color='none', label='Stat. Unc.') 

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend(frameon=False)

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')

# set the axis tick parameters for the main axes
plt.tick_params(which='both', # ticks on both x and y axes
                direction='in') # Put ticks inside and outside the axes
~~~
{: .language-python}

The paper also has ticks on the top axis. So can we!

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    if s=='ggH125_ZZ4lep': continue # skip if signal
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list[:-1], 
                      color=colors_list[:-1])

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the signal bar
plt.hist(DataFrames['ggH125_ZZ4lep']['mllll'], bins=bin_edges, bottom=mc_x_tot, 
         weights=DataFrames['ggH125_ZZ4lep']['totalWeight'], color=colors_list[-1],
         label=labels_list[-1])

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err, width=5, hatch="////", color='none', label='Stat. Unc.') 

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend(frameon=False)

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')

# set the axis tick parameters for the main axes
plt.tick_params(which='both', # ticks on both x and y axes
                direction='in', # Put ticks inside and outside the axes
                top=True) # draw ticks on the top axis
~~~
{: .language-python}

and on the right axis.

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    if s=='ggH125_ZZ4lep': continue # skip if signal
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list[:-1], 
                      color=colors_list[:-1])

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the signal bar
plt.hist(DataFrames['ggH125_ZZ4lep']['mllll'], bins=bin_edges, bottom=mc_x_tot, 
         weights=DataFrames['ggH125_ZZ4lep']['totalWeight'], color=colors_list[-1],
         label=labels_list[-1])

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err, width=5, hatch="////", color='none', label='Stat. Unc.') 

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend(frameon=False)

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')

# set the axis tick parameters for the main axes
plt.tick_params(which='both', # ticks on both x and y axes
                direction='in', # Put ticks inside and outside the axes
                top=True, # draw ticks on the top axis
                right=True ) # draw ticks on right axis
~~~
{: .language-python}

We can also add minor ticks on the x-axis to look more like the paper.

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    if s=='ggH125_ZZ4lep': continue # skip if signal
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list[:-1], 
                      color=colors_list[:-1])

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the signal bar
plt.hist(DataFrames['ggH125_ZZ4lep']['mllll'], bins=bin_edges, bottom=mc_x_tot, 
         weights=DataFrames['ggH125_ZZ4lep']['totalWeight'], color=colors_list[-1],
         label=labels_list[-1])

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err, width=5, hatch="////", color='none', label='Stat. Unc.') 

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend(frameon=False)

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')

# set the axis tick parameters for the main axes
plt.tick_params(which='both', # ticks on both x and y axes
                direction='in', # Put ticks inside and outside the axes
                top=True, # draw ticks on the top axis
                right=True ) # draw ticks on right axis

# separation of x axis minor ticks
plt.gca().xaxis.set_minor_locator( AutoMinorLocator() )
~~~
{: .language-python}

as well as for the y-axis

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    if s=='ggH125_ZZ4lep': continue # skip if signal
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list[:-1], 
                      color=colors_list[:-1])

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the signal bar
plt.hist(DataFrames['ggH125_ZZ4lep']['mllll'], bins=bin_edges, bottom=mc_x_tot, 
         weights=DataFrames['ggH125_ZZ4lep']['totalWeight'], color=colors_list[-1],
         label=labels_list[-1])

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err, width=5, hatch="////", color='none', label='Stat. Unc.') 

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend(frameon=False)

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')

# set the axis tick parameters for the main axes
plt.tick_params(which='both', # ticks on both x and y axes
                direction='in', # Put ticks inside and outside the axes
                top=True, # draw ticks on the top axis
                right=True ) # draw ticks on right axis

# separation of x axis minor ticks
plt.gca().xaxis.set_minor_locator( AutoMinorLocator() )

# separation of y axis minor ticks
plt.gca().yaxis.set_minor_locator( AutoMinorLocator() )
~~~
{: .language-python}

Ok now for experimental data. Let's add a line before `plt.xlabel` to plot experimental data.

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    if s=='ggH125_ZZ4lep': continue # skip if signal
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list[:-1], 
                      color=colors_list[:-1])

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the signal bar
plt.hist(DataFrames['ggH125_ZZ4lep']['mllll'], bins=bin_edges, bottom=mc_x_tot, 
         weights=DataFrames['ggH125_ZZ4lep']['totalWeight'], color=colors_list[-1],
         label=labels_list[-1])

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err, width=5, hatch="////", color='none', label='Stat. Unc.') 

plt.hist(DataFrames['data']['mllll'], bins=bin_edges)

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend(frameon=False)

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')

# set the axis tick parameters for the main axes
plt.tick_params(which='both', # ticks on both x and y axes
                direction='in', # Put ticks inside and outside the axes
                top=True, # draw ticks on the top axis
                right=True ) # draw ticks on right axis

# separation of x axis minor ticks
plt.gca().xaxis.set_minor_locator( AutoMinorLocator() )

# separation of y axis minor ticks
plt.gca().yaxis.set_minor_locator( AutoMinorLocator() )
~~~
{: .language-python}

Doesn't quite look how we want... Let's use `plt.errorbar` instead.

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    if s=='ggH125_ZZ4lep': continue # skip if signal
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list[:-1], 
                      color=colors_list[:-1])

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the signal bar
plt.hist(DataFrames['ggH125_ZZ4lep']['mllll'], bins=bin_edges, bottom=mc_x_tot, 
         weights=DataFrames['ggH125_ZZ4lep']['totalWeight'], color=colors_list[-1],
         label=labels_list[-1])

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err, width=5, hatch="////", color='none', label='Stat. Unc.') 

data_x,_ = np.histogram(DataFrames['data']['mllll'], bins=bin_edges ) # histogram the data
data_x_errors = np.sqrt( data_x ) # statistical error on the data

# plot the data points
plt.errorbar(x=bin_centres, y=data_x, yerr=data_x_errors)

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend(frameon=False)

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')

# set the axis tick parameters for the main axes
plt.tick_params(which='both', # ticks on both x and y axes
                direction='in', # Put ticks inside and outside the axes
                top=True, # draw ticks on the top axis
                right=True ) # draw ticks on right axis

# separation of x axis minor ticks
plt.gca().xaxis.set_minor_locator( AutoMinorLocator() )

# separation of y axis minor ticks
plt.gca().yaxis.set_minor_locator( AutoMinorLocator() )
~~~
{: .language-python}

and of course we need a legend label!

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    if s=='ggH125_ZZ4lep': continue # skip if signal
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list[:-1], 
                      color=colors_list[:-1])

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the signal bar
plt.hist(DataFrames['ggH125_ZZ4lep']['mllll'], bins=bin_edges, bottom=mc_x_tot, 
         weights=DataFrames['ggH125_ZZ4lep']['totalWeight'], color=colors_list[-1],
         label=labels_list[-1])

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err, width=5, hatch="////", color='none', label='Stat. Unc.') 

data_x,_ = np.histogram(DataFrames['data']['mllll'], bins=bin_edges ) # histogram the data
data_x_errors = np.sqrt( data_x ) # statistical error on the data

# plot the data points
plt.errorbar(x=bin_centres, y=data_x, yerr=data_x_errors, label='Data')

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend(frameon=False)

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')

# set the axis tick parameters for the main axes
plt.tick_params(which='both', # ticks on both x and y axes
                direction='in', # Put ticks inside and outside the axes
                top=True, # draw ticks on the top axis
                right=True ) # draw ticks on right axis

# separation of x axis minor ticks
plt.gca().xaxis.set_minor_locator( AutoMinorLocator() )

# separation of y axis minor ticks
plt.gca().yaxis.set_minor_locator( AutoMinorLocator() )
~~~
{: .language-python}

and now to make them black circles.

~~~
mllll_list = []
weight_list = []
mc_stat_err_squared = np.zeros(len(bin_centres)) # array to hold MC stat uncertainties
for s in samples_list:
    if s=='ggH125_ZZ4lep': continue # skip if signal
    mllll_list.append(DataFrames[s]['mllll'])
    weight_list.append(DataFrames[s]['totalWeight'])
    weights_squared,_ = np.histogram(DataFrames[s]['mllll'], bins=bin_edges,
                                     weights=DataFrames[s]['totalWeight']**2) # square the totalWeights
    mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s
mc_heights = plt.hist(mllll_list, bins=bin_edges, weights=weight_list, stacked=True, 
                      label=labels_list[:-1], 
                      color=colors_list[:-1])

mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars

# plot the signal bar
plt.hist(DataFrames['ggH125_ZZ4lep']['mllll'], bins=bin_edges, bottom=mc_x_tot, 
         weights=DataFrames['ggH125_ZZ4lep']['totalWeight'], color=colors_list[-1],
         label=labels_list[-1])

# plot the statistical uncertainty
plt.bar(bin_centres, # x
        2*mc_x_err, # heights
        bottom=mc_x_tot-mc_x_err, width=5, hatch="////", color='none', label='Stat. Unc.') 

data_x,_ = np.histogram(DataFrames['data']['mllll'], bins=bin_edges ) # histogram the data
data_x_errors = np.sqrt( data_x ) # statistical error on the data

# plot the data points
plt.errorbar(x=bin_centres, y=data_x, yerr=data_x_errors, label='Data', 
             fmt='ko') # # 'k' means black and 'o' is for circles

plt.xlabel('$\mathrm{m_{4l}}$ [GeV]', x=1, horizontalalignment='right')
plt.ylabel('Events/5 GeV', y=1, horizontalalignment='right')
plt.legend(frameon=False)

# set the x-limit of the axes
plt.xlim( left=80, right=250 )

plt.text(100, # x
         20, # y
         'ATLAS Open Data',
         weight='bold',
         fontsize='13')

plt.text(100, # x
         18, # y
         r'$\mathrm{H \rightarrow ZZ^{(*)} \rightarrow 4l}$')

plt.text(100, # x
         16, # y
         '$\sqrt{s}$=13 TeV: $\int$Ldt = 10 fb$^{-1}$')

# set the axis tick parameters for the main axes
plt.tick_params(which='both', # ticks on both x and y axes
                direction='in', # Put ticks inside and outside the axes
                top=True, # draw ticks on the top axis
                right=True ) # draw ticks on right axis

# separation of x axis minor ticks
plt.gca().xaxis.set_minor_locator( AutoMinorLocator() )

# separation of y axis minor ticks
plt.gca().yaxis.set_minor_locator( AutoMinorLocator() )
~~~
{: .language-python}

Looking good!



~~~
def plot_data_vs_MC(data, x_variable='mllll', xmin=80, xmax=250, step_size=5, signal_label='ggH125_ZZ4lep', 
                    xlabel=r'$\mathrm{m_{4l}}$', x_units = 'GeV', experiment_label='ATLAS', 
                    process_label=r'$H \rightarrow ZZ^* \rightarrow 4\ell$', cme='13 TeV', lumi='10 fb', mc_weight='totalWeight'):

    bin_edges = np.arange(start=xmin, # The interval includes this value
                          stop=xmax+step_size, # The interval doesn't include this value
                          step=step_size ) # Spacing between values
    bin_centres = np.arange(start=xmin+step_size/2, # The interval includes this value
                            stop=xmax+step_size/2, # The interval doesn't include this value
                            step=step_size ) # Spacing between values

    data_x,_ = np.histogram(data['data'][x_variable], bins=bin_edges ) # histogram the data
    data_x_errors = np.sqrt( data_x ) # statistical error on the data

    signal_x = data[signal_label][x_variable] # histogram the signal
    signal_weights = data[signal_label][mc_weight] # get the weights of the signal events
    signal_color = colors_list[-1] # get the colour for the signal bar

    mc_x = [] # define list to hold the Monte Carlo histogram entries
    mc_weights = [] # define list to hold the Monte Carlo weights
    mc_colors = colors_list[:-1] # define list to hold the colors of the Monte Carlo bars
    mc_labels = [] # define list to hold the legend labels of the Monte Carlo bars

    mc_stat_err_squared = np.zeros(len(bin_centres)) # define array to hold the MC statistical uncertainties
    for s in samples_list: # loop over samples
        if s not in ['data', signal_label]: # if not data nor signal
            mc_x.append( data[s][x_variable] ) # append to the list of Monte Carlo histogram entries
            mc_weights.append( data[s][mc_weight] ) # append to the list of Monte Carlo weights
            mc_labels.append( s ) # append to the list of Monte Carlo legend labels
            weights_squared,_ = np.histogram(data[s][x_variable], bins=bin_edges,
                                             weights=data[s][mc_weight]**2) # square the totalWeights
            mc_stat_err_squared = np.add(mc_stat_err_squared,weights_squared) # add weights_squared for s 
    


    # *************
    # Main plot 
    # *************
    main_axes = plt.gca() # get current axes
    
    # plot the data points
    plt.errorbar(x=bin_centres, y=data_x, yerr=data_x_errors,
                 fmt='ko', # 'k' means black and 'o' is for circles 
                 label='Data') 
    
    # plot the Monte Carlo bars
    mc_heights = plt.hist(mc_x, bins=bin_edges, 
                          weights=mc_weights, stacked=True, 
                          color=mc_colors, label=mc_labels )
    print(mc_heights)
    
    mc_x_tot = mc_heights[0][-1] # stacked background MC y-axis value
    mc_x_err = np.sqrt( mc_stat_err_squared ) # statistical error on the MC bars
    
    # plot the signal bar
    plt.hist(signal_x, bins=bin_edges, bottom=mc_x_tot, 
             weights=signal_weights, color=signal_color,
             label=signal_label)
    
    # plot the statistical uncertainty
    plt.bar(bin_centres, # x
            2*mc_x_err, # heights
            alpha=0.5, # half transparency
            bottom=mc_x_tot-mc_x_err, color='none', 
            hatch="////", width=step_size, label='Stat. Unc.' )
    

    # set the x-limit of the main axes
    plt.xlim( left=xmin, right=xmax ) 
    
    # separation of x axis minor ticks
    main_axes.xaxis.set_minor_locator( AutoMinorLocator() ) 
    
    # set the axis tick parameters for the main axes
    plt.tick_params(which='both', # ticks on both x and y axes
                    direction='in', # Put ticks inside and outside the axes
                    top=True, # draw ticks on the top axis
                    right=True ) # draw ticks on right axis
    
    # x-axis label
    plt.xlabel(xlabel+' ['+x_units+']',
                         x=1, horizontalalignment='right' )
    
    # write y-axis label for main axes
    plt.ylabel('Events / '+str(step_size)+' '+x_units,
                         y=1, horizontalalignment='right') 
    
    # set y-axis limits for main axes
    plt.ylim( bottom=0, top=np.amax(data_x)*1.6 )
    
    # add minor ticks on y-axis for main axes
    main_axes.yaxis.set_minor_locator( AutoMinorLocator() ) 

    # Add text 'ATLAS Open Data' on plot
    plt.text(0.05, # x
             0.93, # y
             experiment_label, # text
             transform=main_axes.transAxes, # coordinate system used is that of main_axes
             weight='bold',
             fontsize=13 ) 
    
    # Add a label for the analysis carried out
    plt.text(0.05, # x
             0.88, # y
             process_label, # text 
             transform=main_axes.transAxes ) # coordinate system used is that of main_axes
    
    # Add energy and luminosity
    plt.text(0.05, # x
             0.82, # y
             '$\sqrt{s}$='+cme+': $\int$Ldt = '+lumi+'$^{-1}$', # text
             transform=main_axes.transAxes ) # coordinate system used is that of main_axes

    # draw the legend
    plt.legend( frameon=False ) # no box around the legend
~~~
{: .language-python}

{% include links.md %}

