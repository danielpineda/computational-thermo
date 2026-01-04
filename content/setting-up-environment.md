---
kernelspec:
  name: python3
  display_name: 'Python 3'
---

# Setting up your computing environment

You have a few options for running these examples and solving other problems using the approaches shown:
- Install and use Python and a text editor or integrated development environment (IDE), like [Spyder](https://www.spyder-ide.org), on your computer
- Install and use Jupyter Notebooks on your computer
- Use a (free) cloud Jupyter Notebook environment like [Google Colab](https://colab.research.google.com), [Microsoft Azure Notebooks](https://notebooks.azure.com), or [Binder](https://mybinder.org)

Using Python and Jupyter Notebooks on your computer require essentially the same setup, which is slightly different for different operating systems. The steps following this assume you are planning to use Jupyter Notebook.

:::{tip} miniforge,
Rather than installing the full Anaconda distribution, you could choose to install [Miniconda](https://docs.conda.io/en/latest/miniconda.html), which is a minimal installer for conda. In this case, you would need to explicitly install all the packages you need.
:::


:::{important}
**Important:** You will need to reactivate your environment every time you restart Anaconda.
:::

## Installing Jupyter

1. I recommend you [install Anaconda](https://docs.anaconda.com/anaconda/install/) to manage your Python environment—it makes installing and managing packages very easy, and works on macOS, Linux, and Windows.
2. Create and activate an environment (for example, called `thermo`) for Jupyter with Python 3.13. From the command line for Linux and macOS, or the Anaconda Prompt on Windows, run:
```bash
$ conda create -vv --name thermo --channel cantera --channel conda-forge python=3.13 cantera pint coolprop jupyter numpy scipy matplotlib

$ conda activate thermo
```

Before the second command, you may need to tell your shell (e.g., bash, zsh) about conda, by doing `conda init zsh` for example. If you get an error with the `conda activate` command, your terminal should tell you to do this.

You should activate this environment whenever you want to use these packages.

4. Run Jupyter Notebook:

```bash
$ jupyter notebook
```

and create a new Python 3 notebook with "New" then "Python 3" under "Notebook:"

## Cloud Jupyter Notebook Environments

If you cannot or prefer not to install Anaconda/Python/Jupyter on your computer, you can use one of a number of cloud Jupyter Notebook environments to run these examples and do your work. Major options include:
 - [Google Colab](#google-colab)
 - [Binder](#binder)
 - [Microsoft Azure Notebooks](#microsoft-azure-notebooks)
 - [DataLore](#datalore)


(google-colab)=
### Google Colab

[Google Colab](https://colab.research.google.com) (Colaboratory) is a nice, newer service connected to your Google account that offers free computation time.

In a new notebook, you need to first install Cantera:
```bash
!apt-get -qq update -y
!apt-get -qq install -y python3-software-properties
!apt-add-repository -y ppa:speth/cantera > /dev/null 2>&1
!apt-get -qq install -y cantera-python3
```

and then additional packages like Pint and CoolProp:

```bash
!pip install -q pint coolprop
```

Or, click this link to open a notebook that includes these commands: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/kyleniemeyer/computational-thermo/blob/master/colab-demo.ipynb)

Other common packages like NumPy and SciPy should already be available.

(binder)=
### Binder

[Binder](https://mybinder.org) is a service that runs Jupyter Notebooks online, and can automatically create an environment based on a configuration file:

1. Visit https://mybinder.org
2. Enter the URL for this textbook: https://github.com/kyleniemeyer/computational-thermo
3. Click the \"launch\" button.

Or, just use this link: [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/kyleniemeyer/computational-thermo/master)

(microsoft-azure-notebooks)=
### Microsoft Azure Notebooks

With [Microsoft Azure Notebooks](https://notebooks.azure.com/), after signing in with your Microsoft or Outlook account, you can create a "project" which contains one or more notebooks, text files, data, etc.

In a new Python 3 notebook, you can install Cantera, Pint, and CoolProp in the first cell using:
```bash
!pip install cantera pint coolprop
```
(This may take some time.

(datalore)=
### DataLore

[DataLore](https://datalore.io) is a new and slightly different service that is still under development. Rather than support Jupyter Notebooks directly, they have developed their own implementation of a Python-based notebook.

Although DataLore workbooks come with many common packages installed (e.g., NumPy, SciPy, Matplotlib), it is a bit more challenging to install other packages:

 1. Go to "Tools" → "Library Manager"
 2. In "All Libraries", search for the package you want to install. For example, you can install `pint` and `coolprop`.
 3. In the search results, choose the correct package, then from the dropdown next to the "Install" button choose the latest version available (this should already be selected).
 4. Click the "Install" button. After a few moments, the package should be accessible in your workbook.
 5. Repeat for other packages as needed.

To solve thermodynamics problems, you'll need to install CoolProp at minimum.

Unfortunately, it is not clear how to install Cantera at the moment, so DataLore may be limited. The behavior is also a bit different than expected with Jupyter notebooks regarding work between different cells, since DataLore is more strict about executing cells in order and tracking dependency—it automatically updates any cells that depend on variables that change in the current cell.

This information will be updated as DataLore evolves and more documentation is available.

