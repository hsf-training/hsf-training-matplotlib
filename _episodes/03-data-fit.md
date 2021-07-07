---
title: "Data fit"
teaching: 5
exercises: 5
questions:
- "How might I plot a data fit?"
objectives:
- "Provide an example data fit plot"
keypoints:
- "Data fit plots look nice with matplotlib!"
---

FIXME

plot such as

![myy](../fig/myy.jpg){:width="40%"}

from [the ATLAS Higgs discovery paper](https://www.sciencedirect.com/science/article/pii/S037026931200857X#fg0040)

Using your version of the 'Matplotlib Data fit' notebook you created in the [Setup page](https://hsf-training.github.io/hsf-training-matplotlib/setup.html)

~~~
def plot_data_fit(df, # data as a dataframe
                  xmin=100, # x-axis minimum
                  xmax=160, # x-axis maximum
                  step_size=2, # x-axis difference between data points
                  signal_label='Sig+Bkg Fit ($m_H=125$ GeV)', # legend label for signal
                  background_label='Bkg (4th order polynomial)', # legend label for background
                  xlabel=r'$\mathrm{m_{\gamma\gamma}}$', # x-axis label
                  x_units = 'GeV', # x-axis units
                  experiment_label='ATLAS', # experiment label
                  process_label=r'$H \rightarrow \gamma\gamma$', # label for the process 
                  cme='13 TeV', # centre-mass-energy
                  lumi='10 fb' # luminosity (in inverse units)
                 ):   
    
    bin_edges = np.arange(start=xmin, # The interval includes this value
                          stop=xmax+step_size, # The interval doesn't include this value
                          step=step_size ) # Spacing between values
    bin_centres = np.arange(start=xmin+step_size/2, # The interval includes this value
                            stop=xmax+step_size/2, # The interval doesn't include this value
                            step=step_size ) # Spacing between values

    data,_ = np.histogram(df['myy'], bins=bin_edges ) # histogram the data
    errors = np.sqrt( data ) # statistical error on the data

    # data fit
    popt,_ = curve_fit(func, # function to fit
                       bin_centres, # x
                       data, # y
                       p0=[data.max(),0,0,0,0,91.7,125,2.4], # initial guesses for the fit parameters
                       sigma=errors) # errors on y

    # background part of fit
    a = popt[0] # a of a + b*x + c*x^2 + d*x^3 + e*x^4
    b = popt[1] # b of a + b*x + c*x^2 + d*x^3 + e*x^4
    c = popt[2] # c of a + b*x + c*x^2 + d*x^3 + e*x^4
    d = popt[3] # d of a + b*x + c*x^2 + d*x^3 + e*x^4
    e = popt[4] # e of a + b*x + c*x^2 + d*x^3 + e*x^4
    # get the background only part of the fit to data
    background = a + b*bin_centres + c*bin_centres**2 + d*bin_centres**3 + e*bin_centres**4

    A = popt[5] # amplitude of Gaussian
    mu = popt[6] # centre of Gaussian
    sigma = popt[7] # width of Gaussian
    fit = func(bin_centres,a,b,c,d,e,A,mu,sigma) # call func with fitted parameters

    # data fit - background fit = signal fit
    signal = data - background 


    # *************
    # Main plot 
    # *************
    plt.axes([0.1,0.3,0.85,0.65]) # left, bottom, width, height 
    main_axes = plt.gca() # get current axes
    
    # plot the data points
    main_axes.errorbar(x=bin_centres, y=data, yerr=errors, 
                       fmt='ko', # 'k' means black and 'o' means circles
                       label='Data' ) 
    
    # plot the signal + background fit
    main_axes.plot(bin_centres, # x
                   fit, # y
                   '-r', # single red line
                   label=signal_label )
    
    # plot the background only fit
    main_axes.plot(bin_centres, # x
                   background, # y
                   '--r', # dashed red line
                   label=background_label )

    # set the x-limit of the main axes
    main_axes.set_xlim( left=xmin, right=xmax ) 
    
    # separation of x-axis minor ticks
    main_axes.xaxis.set_minor_locator( AutoMinorLocator() ) 
    
    # set the axis tick parameters for the main axes
    main_axes.tick_params(which='both', # ticks on both x and y axes
                          direction='in', # Put ticks inside and outside the axes
                          top=True, # draw ticks on the top axis
                          labelbottom=False, # don't draw tick labels on bottom axis
                          right=True ) # draw ticks on right axis
    
    # write y-axis label for main axes
    main_axes.set_ylabel('Events / '+str(step_size)+' '+x_units, 
                         horizontalalignment='right') 
    
    # set the y-axis limit for the main axes
    main_axes.set_ylim( bottom=0, top=np.amax(data)*1.1 ) 
    
    # set minor ticks on the y-axis of the main axes
    main_axes.yaxis.set_minor_locator( AutoMinorLocator() ) 
    
    # avoid displaying y=0 on the main axes
    main_axes.yaxis.get_major_ticks()[0].set_visible(False) 

    # Add text 'ATLAS Open Data' on plot
    plt.text(0.2, # x
             0.92, # y
             experiment_label, # text
             transform=main_axes.transAxes, # coordinate system used is that of main_axes
             weight='bold',
             fontsize=13 )  
    
    # Add energy and luminosity
    plt.text(0.05, # x
             0.1, # y
             '$\sqrt{s}$='+cme+': $\int$Ldt = '+lumi+'$^{-1}$', # text
             transform=main_axes.transAxes ) # coordinate system used is that of main_axes 
    
    # Add a label for the analysis carried out
    plt.text(0.5, # x
             0.1, # y
             process_label, # text 
             transform=main_axes.transAxes ) # coordinate system used is that of main_axes

    # draw the legend
    main_axes.legend(frameon=False) # no box around the legend


    # *************
    # Data-Bkg plot 
    # *************
    plt.axes([0.1,0.1,0.85,0.2]) # left, bottom, width, height
    sub_axes = plt.gca() # get the current axes
    
    # set the y axis to be symmetric about Data-Background=0
    sub_axes.yaxis.set_major_locator( MaxNLocator(nbins='auto', 
                                                  symmetric=True) )
    
    # plot Data-Background
    sub_axes.errorbar(x=bin_centres, y=signal, yerr=errors,
                      fmt='ko' ) # 'k' means black and 'o' means circles
    
    # draw the fit to data
    sub_axes.plot(bin_centres, # x
                  fit-background, # y
                  '-r' ) # single red line
    
    # draw the background only fit
    sub_axes.plot(bin_centres, # x
                  background-background, # y
                  '--r' )  # dashed red line
    
    # set the x-axis limits on the sub axes
    sub_axes.set_xlim( left=xmin, right=xmax ) 
    
    # separation of x-axis minor ticks
    sub_axes.xaxis.set_minor_locator( AutoMinorLocator() ) 
    
    # x-axis label
    sub_axes.set_xlabel(xlabel+' ['+x_units+']',
                         x=1, horizontalalignment='right' ) 
    
    # set the tick parameters for the sub axes
    sub_axes.tick_params(which='both', # ticks on both x and y axes
                         direction='in', # Put ticks inside and outside the axes
                         top=True, # draw ticks on the top axis
                         right=True ) # draw ticks on right axis 
    
    # separation of y-axis minor ticks
    sub_axes.yaxis.set_minor_locator( AutoMinorLocator() ) 
    
    # y-axis label on the sub axes
    sub_axes.set_ylabel( 'Events-Bkg' ) 


    # Generic features for both plots
    main_axes.yaxis.set_label_coords( -0.09, 1 ) # x,y coordinates of the y-axis label on the main axes
    sub_axes.yaxis.set_label_coords( -0.09, 0.5 ) # x,y coordinates of the y-axis label on the sub axes
~~~
{: .language-python}

{% include links.md %}

