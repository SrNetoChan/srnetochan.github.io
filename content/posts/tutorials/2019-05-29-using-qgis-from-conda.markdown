---

date: 2019-05-29 22:46:23+00:00
title: Using QGIS from conda-forge
categories:
- Sem categoria
tags:
- conda
- QGIS
- conda-forge
- mamba
---

QGIS recipes have been available on Conda-forge for a while, but now, that they work for the three main operating systems, installing QGIS from Conda is s starting to become a very reliable alternative to other QGIS distributions. Anyway, let's rewind a bit...

What is Conda?

<blockquote>Conda is an open source package management system and environment management system that runs on Windows, macOS and Linux. Conda quickly installs, runs and updates packages and all their dependencies. Conda easily creates, saves, loads and switches between environments on your local computer. It was created for Python packages, but it can package and distribute software for any language.</blockquote>

What is Conda-forge?

Conda-forge is a community driven channel that builds and enable hundreads of packages.

Why is that of any relevance?

Conda provides a similar way to build, package and install QGIS (or any other software) in Linux, Windows, and Mac. It also provides builds for Linux aarch64 and Mac arm64. You can also choose what version of python you want to use with it.

As a user, it's the installation part that I enjoy the most. I am a Linux user, and one of the significant limitations is not having an easy way to install more than one version of QGIS on my machine (for example the latest stable version and the Long Term Release version). I was able to work around that limitation by compiling QGIS myself, but with Conda, I can install as many versions as I want in a very convenient way.

The following paragraphs explain how to install QGIS using Conda. The instructions and Conda commands should be quite similar for all the operating systems.

## Anaconda, miniconda or mambaforge?

First thing you need to do is to install the Conda packaging system. Two distributions install Conda: **Anaconda** and **Miniconda**. There's is also an alternative called **Mambaforge** that also installs Mamba.

**TL;DR** Anaconda is big (3Gb?) and installs the packaging system and a lot of useful tools, python packages, libraries, etc... . Miniconda is much smaller and installs just the packaging system, which is the bare minimum that you need to work with Conda and will allow you to selectively install the tools and packages you need. Finally, my current favorite, **Mambaforge**. It is as small as miniconda, it uses conda-forge channel as default, and allow you to use [mamba](https://mamba.readthedocs.io/en/latest/index.html) instead of conda, which has the exact same commands, but it is blasing fast!

For more information, check this stack exchange answer on [anaconda vs miniconda.](https://stackoverflow.com/a/45421527/1918685)

Download [anaconda](https://www.anaconda.com/distribution/) or [miniconda](https://docs.conda.io/en/latest/miniconda.html) or [mambaforge](https://github.com/conda-forge/miniforge#mambaforge) installers for your system and follow the instructions to install it.

Windows installer is an executable, you should run it as administrator. The OSX and Linux installers are bash scripts, which means that, once downloaded, you need to run something like this to install:


    bash Miniconda3-latest-Linux-x86_64.sh

## Installing QGIS


Notice that the Conda (or mamba) tools are used in a command line terminal. Besides, on Windows, you need to use the specific command prompt that is installed with miniconda.


### Using environments


Conda works with environments, which are similar to [Python virtual environments](https://virtualenv.pypa.io/en/latest/) but not limited only to python. Basically, it allows isolating different installations or setups without interfering with the rest of the system. I recommend that you always use environments. If, like me, you want to have more that one version of QGIS installed, then the use of environments is mandatory.

Creating an environment is as easy as entering the following command on the terminal:


    conda create --name <name_of_the_environment>


For example,


    conda create --name qgis_stable


You can choose the version of python to use in your environment by adding the option `python=<version>`. Currently versions of QGIS run on python 3.8, 3.9, 3.10 and 3.11.

conda create --name qgis_stable python=3.10

To use an environment, you need to activate it.


    conda activate qgis_stable


Your terminal prompt will show you the active environment.


    (qgis_stable) aneto@oryx:~/miniconda3$


To deactivate the current environment, you run


    conda deactivate




### Installing packages


Installing packages using Conda is as simples as:


    conda install <package_name>


Because conda packages can be stored in different channels, and because the default channels (from the anaconda service) do not contain QGIS (and are actually free), we may need to specify the channel we want to get the package from. [conda-forge](https://conda-forge.org/) is a community-driven repository of conda recipes and includes updated QGIS packages. Make sure to activate the  environment first.


    conda install qgis --channel conda-forge

If we use mambaforge, we can simply do:

    mamba install qgis


Conda will download the latest available version of QGIS and all its dependencies installing it on the active environment.

Note: Because conda always try to install the latest version, if you want to use the QGIS LTR version, you must specify the QGIS version.

    conda install qgis=3.28.8 --channel conda-forge

or

    mamba install qgis=3.28.8
    


### Uninstalling packages


Uninstalling QGIS is also easy. The quickest option is to delete the entire environment where QGIS was installed. Make sure you deactivate it first.

`conda deactivate
conda env remove --name qgis_stable`

Another option is to remove QGIS package manually. This is useful if you have other packages installed that you want to keep.


    conda activate qgis_stable
    conda remove qgis -c conda-forge


This only removes the QGIS package and will leave all other packages that were installed with it. Note that you need to specify the conda-forge channel. Otherwise, Conda will try to update some packages from the default channels during the removal process, and things may get messy.


## **Running QGIS**


To run QGIS, in the terminal, activate the environment (if not activated already) and run the qgis command


    conda activate qgis_stable
    qgis


## Updating QGIS


To update QGIS to the most recent version, you need to run the following command with the respective environment active


    conda update qgis -c conda-forge

or 

    mamba update qgis


To update a patch release for the QGIS LTR version you run the install command again with the new version:


    conda install qgis=3.28.8 -c conda-forge

or 

    mamba install qgis=3.28.8


## Some notes and caveats


Please be aware that QGIS packages on Conda do not provide the same level of user experience as the official Linux, Windows, and Mac installer from the QGIS.org distribution. For example, there are no desktop icons or file association, it does not include GRASS and SAGA, etc ...

On the other hand, QGIS installations on Conda it will share user configurations, installed plugins, with any other QGIS installations on your system.
