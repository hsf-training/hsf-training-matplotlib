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

We will be using the following [Github Repository](https://github.com/hsf-training/hsf_matplotlib_notebooks) to follow the lesson.

You would only need to look for the [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/hsf-training/hsf_matplotlib_notebooks/main)

Binder is good for live coding sessions and thus has a 10-20 min inactivity timeout. If this occurs during the session follow these steps (they should work most of the time)
- Click on cloud with down arrow
- Close the Binder
- Click on the Binder badge to open a new Binder session
- Create new notebook
- Click on cloud with up arrow to regain your changes



## Plan B: Google Colab

If for whatever reason Binder is not working. All notebooks should have a
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/hsf-training/hsf_matplotlib_notebooks/blob/main/)
Just click and run the cells that say **If on Colab**

This only requires the user to have a Google account but it is much more stable and does not have the inactivity limit like Binder.

Some details on Google Colab:
- Colab allows you to create a copy of the notebook and stores it in your google drive
- Colab comes with some python libraries installed but not the ones required for our workshop. This forces us to run the first cell of the notebook which downloads the materials from Github and installs the necessary packages into your session.
- However, when running this cell for the first time, Colab will not be able to make use of some of the libraries installed unless we click on `Runtime` and then click on `Restart Runtime`. Rerun the first cell and we are good to go!
- The caveat is that this procedure would need to be executed for each notebook in the lesson.

## Plan C: GitHub Codespaces

GitHub Codespaces provides a cloud-based development environment with pre-configured dependencies. This is a modern alternative that works well for educational content.

1. Go to the [notebooks repository](https://github.com/hsf-training/hsf_matplotlib_notebooks)
2. Click the green "Code" button and select "Codespaces"
3. Create a new codespace or use an existing one
4. The environment will be automatically configured with Python and Jupyter

## Plan D: SWAN
SWAN is a CERN based notebook hosting service. It is stable like Colab and setup is easy like Binder.
Simply click on the Badge below and log in to SWAN with your CERN account (CERN account required).

[![SWAN](https://swan.web.cern.ch/sites/swan.web.cern.ch/files/pictures/open_in_swan.svg)](https://cern.ch/swanserver/cgi-bin/go?projurl=https://github.com/hsf-training/hsf_matplotlib_notebooks.git)

## If you want to run locally

We highly recommend you create a virtual environment first. Choose one of the following approaches:

### Option 1: Using conda (recommended for scientific Python)
```bash
conda create --name mpl python=3.11
conda activate mpl
git clone https://github.com/hsf-training/hsf_matplotlib_notebooks.git
cd hsf_matplotlib_notebooks
# Install requirements
conda install -c conda-forge --file requirements.txt
conda install jupyterlab
```

### Option 2: Using pip and venv
```bash
python -m venv mpl-env
source mpl-env/bin/activate  # On Windows: mpl-env\Scripts\activate
git clone https://github.com/hsf-training/hsf_matplotlib_notebooks.git
cd hsf_matplotlib_notebooks
# Install requirements
pip install -r requirements.txt
pip install jupyterlab
```

Now you can launch JupyterLab (recommended) or the classic notebook:
```bash
jupyter lab --no-browser
# Or for classic notebook interface
jupyter notebook --no-browser
```
Then copy one of the URLs printed on the terminal window and paste in your browser.


Your feedback is very welcome! Most helpful for us is if you "[Improve this page on GitHub](https://github.com/hsf-training/hsf-training-matplotlib/edit/gh-pages/setup.md)". If you prefer anonymous feedback, please [fill this form](https://forms.gle/9ge6rkYk6UMUt2WT8).

{% include links.md %}
