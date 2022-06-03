---
title: Setup
---

  <iframe
      src="https://indico.cern.ch/event/1058838/attachments/2427696/4157672/HSF%20Matplotlib%20Setup.mp4"
      title= "HSF Matplotlib Setup"
      width="100%"
      height="500"
      frameborder="0"
      allowfullscreen="">
  </iframe>

## Binder setup
For this tutorial we will be using [Binder](https://mybinder.org/). It offers a no setup, click and ready to go Jupyter Notebook environment.

We will be using the following [Github Repository](https://github.com/plttraining/hsf_matplotlib_notebooks) to follow the lesson.

You would only need to look for the [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/plttraining/hsf_matplotlib_notebooks/main)

## Plan b : Google Colab

If for whatever reason Binder is not working. All notebooks should have a
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)]()
Just click and run the cells that say **If on Colab**

## If you want to run locally

We highly recommend you create a virtual enviroment first. Open your terminal and do


```bash
conda create --name mpl
conda activate mpl
git clone https://github.com/plttraining/hsf_matplotlib_notebooks.git
cd hsf_matplotlib_notebooks
# Now install the requirements
conda install -c conda-forge --file requirements.txt
conda install notebook jupyter-lab
```
Now you can launch your jupyter notebook or jupyter-lab session
```bash
jupyter notebook --no-browser
# Or
jupyter lab --no-browser
```

Your feedback is very welcome! Most helpful for us is if you "[Improve this page on GitHub](https://github.com/hsf-training/hsf-training-matplotlib/edit/gh-pages/setup.md)". If you prefer anonymous feedback, please [fill this form](https://forms.gle/9ge6rkYk6UMUt2WT8).

{% include links.md %}
