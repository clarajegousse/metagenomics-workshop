---
layout: page
title: Setup
---

# Overview

This workshop is designed to be run on pre-imaged Amazon Web Services (AWS)
instances. With the exception of a spreadsheet program, all of the command line software and data used in the workshop are hosted on an Amazon 
Machine Image (AMI). Please follow the instructions below to prepare your computer for the workshop:



## Required  software

This lesson requires a working spreadsheet program. If you don't have a spreadsheet program already, you can use LibreOffice. It's a free, open source spreadsheet program.  Directions to install are included for each Windows, Mac OS X, and Linux systems below. For Windows, you will also need to install Git Bash, PuTTY, or the Ubuntu Subsystem.

> ## Windows
> - Download the [Git for Windows installer](https://git-for-windows.github.io/). Run the installer and follow the steps below:
>   + Click on "Next" four times (two times if you've previously installed Git). You don't need to change anything in the Information, location, components, and start menu screens.
>   + Select "Use the nano editor by default" and click on "Next".
>   + Keep "Use Git from the Windows Command Prompt" selected and click on "Next". If you forgot to do this programs that you need for the workshop will not work properly. If this happens rerun the installer and select the appropriate option.
>   + Click on "Next".
>   + Keep "Checkout Windows-style, commit Unix-style line endings" selected and click on "Next".
>   + Select "Use Windows' default console window" and click on "Next".
>   + Click on "Install".
>   + Click on "Finish".
>   + If your "HOME" environment variable is not set (or you don't know what this is):
>   + Open command prompt (Open Start Menu then type `cmd` and press [Enter])
>   + Type the following line into the command prompt window exactly as shown: `setx HOME "%USERPROFILE%"`
>   + Press [Enter], you should see `SUCCESS: Specified value was saved.`
>   + Quit command prompt by typing `exit` then pressing [Enter]
> - An **alternative option** is to install PuTTY
>  by going to the [the installation page](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html). For most newer computers, click on putty-64bit-X.XX-installer.msi to download the 64-bit version. If you have an older laptop, you may need to get the 32-bit version putty-X.XX-installer.msi. If you aren't sure whether you need the 64 or 32 bit version, you can check your laptop version by following [the instructions here](https://support.microsoft.com/en-us/help/15056/windows-32-64-bit-faq). Once the installer is downloaded, double click on it, and PuTTY should install.
> - **Another alternative option** is to use the Ubuntu Subsystem for Windows. This option is only available for Windows 10 - detailed [instructions are available here](https://docs.microsoft.com/en-us/windows/wsl/install-win10).
{: .solution}

> ## Mac OS X
> -  The default shell in some versions of macOS is Bash, and Bash is available in all versions, so no need to install anything. You access Bash from the Terminal (found in /Applications/Utilities). See the Git [installation video tutorial](https://www.youtube.com/watch?v=9LQhwETCdwY) for an example on how to open the Terminal. You may want to keep Terminal in your dock for this workshop.
{: .solution}

> ## Linux
>  - The default shell is usually Bash and there is usually no need to install anything. To see if your default shell is Bash type echo $SHELL in a terminal and press the Enter key. If the message printed does not end with '/bash' then your default is something else and you can run Bash by typing bash.
{: .solution}


## Option A: Using the lessons with Amazon Web Services (AWS)

If you are signed up to take a Metagenomics Data Carpentry Workshop, you do *not* need to worry about setting up an AMI instance. The Carpentries
staff will create an instance for you and this will be provided to you at no cost. This is true for both self-organized and centrally-organized workshops. Your Instructor will provide instructions for connecting to the AMI instance at the workshop.

If you would like to work through these lessons independently, outside of a workshop, you will need to start your own AMI instance. 
Follow these [instructions on creating an Amazon instance](https://carpentries-incubator.github.io/metagenomics-workshop/AMI-setup/index.html). Use the AMI `ami-0e7fb76a881ab5e09` (Metagenomics - 18 March (The Carpentries Incubator)) listed on the Community AMIs page. Please note that you must set your location as `N. Virginia` in order to access this community AMI. You can change your location in the upper right corner of the main AWS menu bar. The cost of using this AMI for a few days, with the t2.medium instance type is very low (about USD $1.50 per user, per day). Data Carpentry has *no* control over AWS pricing structure and provides this cost estimate with no guarantees. Please read AWS documentation on pricing for up-to-date information. 

If you're an Instructor or Maintainer or want to contribute to these lessons, please get in touch with us [team@carpentries.org](mailto:team@carpentries.org) and we will start instances for you. 

After the basic software of the genomic instace is setup you need to add the metagenomics environment. 
Here is a link to [specifications file](https://github.com/carpentries-incubator/metagenomics/blob/gh-pages/files/spec-file.txt) with the exact versions of each tool in this environment. You can use the spec file as follows:  
> ~~~
> $ conda create --name myenv --file spec-file.txt
> ~~~
>{: .bash}

More information about how to use environments and spec file is available at [conda documentation](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)

This environment can be modified by adding or deleting tools in a file `metagenomics.yml`, 
original metagenomics.yml file had the following content:  
~~~
$ cat metagenomics.yml
~~~
{: .bash}
~~~
name: metagenomics                                                                
dependencies:                                      
  - kraken2 
  - krona             
  - maxbin2
  - spades
  - kraken-biom
  - checkm-genome

~~~
{: .output}

Then you can create your own metagenomics conda environment using the metagenomics.yml file.  
~~~
$ conda env create -f metagenomics.yml
~~~
{: .bash}  

Finally execute some remaining installation scripts.  
~~~
bash /home/dcuser/.miniconda3/envs/metagenomics/opt/krona/updateTaxonomy.sh                                
wget ftp://ftp.ncbi.nih.gov/pub/taxonomy/taxdump.tar.gz 
tar -xzf taxdump.tar.gz 
mkdir .taxonkit
cp names.dmp nodes.dmp delnodes.dmp merged.dmp /home/dcuser/.taxonkit
rm *dmp readme.txt taxdump.tar.gz gc.prt 
~~~
{: .bash}  

### Data

The data used in this workshop are available on Zenodo. Because this workshop works with real data, be aware that file sizes for the data are large. Please read the Zenodo page linked below for information about the data and access to the data files. 
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.4285900.svg)](https://doi.org/10.5281/zenodo.4285900)


More information about these data will be presented in the [first episode of the Data processing and visualization for metagenomics lesson](https://carpentries-incubator.github.io/metagenomics/01-background-metadata/index.html).


## Option B: Using the lessons on your local machine

While not recommended, it is possible to work through the lessons on your local machine (i.e. without using
AWS). To do this, you will need to install all of the software used in the workshop and obtain a copy of the
dataset. Instructions for doing this are below.

### Software

#### Software for Bash:

| Software | Version | Manual | Available for | Description |
| -------- | ------------ | ------ | ------------- | ----------- |
| [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) | 0.11.7 | [Link](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/)| Linux, MacOS, Windows | Quality control tool for high throughput sequence data. |
| [Trimmomatic](http://www.usadellab.org/cms/?page=trimmomatic) | 0.38 | [Link](http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/TrimmomaticManual_V0.32.pdf) | Linux, MacOS, Windows | A flexible read trimming tool for Illumina NGS data. |
|[Kraken](http://ccb.jhu.edu/software/kraken2/)|2.1.1|[Link](https://github.com/DerrickWood/kraken2/wiki/Manual)|Available for|A tool for taxonomic assignation for reads from metagenomics|
|[KronaTools](https://github.com/marbl/Krona/wiki) |2.7.1|help link|A tool for taxonomic visualization in hierarchical pie graphs.|
|[MaxBin2]()|2.2.7|help link|Available for| Tool for MAGs reconstruction|
|[Spades](https://cab.spbu.ru/software/spades/)|v3.14.1 |[Link](https://github.com/ablab/spades/blob/spades_3.15.2/README.md#meta)|Linux & MacOS| Tool for assemblies|
|[Kraken-biom](https://github.com/smdabdoub/kraken-biom)|1.0.1|help link|Available for|Tool to convert kraken reports in R readable files|
|[CheckM-genome](https://ecogenomics.github.io/CheckM/)|v1.1.3 |help link|Available for|Tool to check completeness and contamination in MAGs |

#### R and RStudio:

R and RStudio are two separate pieces of software:

R is a programming language that is especially powerful for data exploration, visualization, and statistical analysis
RStudio is an integrated development environment (IDE) that makes using R easier. In this course we use RStudio to interact with R.

> ## Mac OS X
> -  Download R from the [CRAN website](https://cran.r-project.org/bin/macosx/).
> + Select the .pkg file for the latest R version
> + Double click on the downloaded file to install R
> + It is also a good idea to install [XQuartz](https://www.xquartz.org/) (needed by some packages)
> + Go to the [RStudio download](https://www.rstudio.com/products/rstudio/download/#download) page
> + Under Installers select RStudio x.yy.zzz - Mac OS X 10.6+ (64-bit) (where x, y, and z represent version numbers)
> + Double click the file to install RStudio
> + Once it’s installed, open RStudio to make sure it works and you don’t get any error messages.
{: .solution}

> ## Windows
> -  Download R from the [CRAN website](https://cran.r-project.org/bin/windows/base/release.htm).
> + Run the .exe file that was just downloaded
> + Go to the [RStudio download page](https://www.rstudio.com/products/rstudio/download/#download)
> + Under Installers select RStudio x.yy.zzz - Windows Vista/7/8/10 (where x, y, and z represent version numbers)
> + Double click the file to install it
> + Once it’s installed, open RStudio to make sure it works and you don’t get any error messages.
{: .solution}

> ## Linux
> - Follow the instructions for your distribution from [CRAN](https://cloud.r-project.org/bin/linux), they provide information to get the most recent version of R for common distributions. For most distributions, you could use your package manager (e.g., for Debian/Ubuntu run sudo apt-get install r-base, and for Fedora sudo yum install R), but we don’t recommend this approach as the versions provided by this are usually out of date. In any case, make sure you have at least R 3.3.1.
> + Go to the [RStudio](https://www.rstudio.com/products/rstudio/download/#download) download page
> + Under Installers select the version that matches your distribution, and install it with your preferred method (e.g., with Debian/Ubuntu ´sudo dpkg -i rstudio-x.yy.zzz-amd64.deb´ at the terminal).
> + Once it’s installed, open RStudio to make sure it works and you don’t get any error messages.
{: .solution}

#### Software(packages) for R:

| Software | Version | Manual | Description |
| -------- | ------------ | ------ | ------------- | ----------- |
| [phyloseq](https://github.com/joey711/phyloseq) | 1.36.0 | [Link](https://joey711.github.io/phyloseq/) | Explore, manipulate and analyze microbiome profiles with R |
| [ggplot2](https://cloud.r-project.org/web/packages/ggplot2/index.html) | 3.3.3 | [Link](https://ggplot2.tidyverse.org/) | System for declaratively creating graphics, based on The Grammar of Graphics |

### QuickStart Software Installation Instructions

These are the QuickStart installation instructions. They assume familiarity with the command line and with installation in general. As there are different operating systems and many different versions of operating systems and environments, these may not work on your computer. If an installation doesn't work for you, please refer to the user guide for the tool, listed in the table above.

We have installed software using [miniconda](https://docs.conda.io/en/latest/miniconda.html). Miniconda is a package manager that simplifies the installation process. Please first install miniconda3 (installation instructions below), and then proceed to the installation of individual tools. 

### Miniconda3

> ## MacOS
> 
>To install miniconda3, type:
>
>~~~
>$ curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh
>$ bash Miniconda3-latest-MacOSX-x86_64.sh
>~~~
>{: .bash}
> Then, follow the instructions that you are prompted with on the screen to install Miniconda3. 
{: .solution}


### FastQC

> ## MacOS
>
>To install FastQC, type:
>
> ~~~
> $ conda install -c bioconda fastqc=0.11.7=5
> ~~~
>{: .bash}
{: .solution}

> ## FastQC Source Code Installation
>
> If you prefer to install from source, follow the directions below:
>
> ~~~
> $ cd ~/src
> $ curl -O http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.7.zip
> $ unzip fastqc_v0.11.7.zip
> ~~~
> {: .bash}
>
> Link the fastqc executable to the ~/bin folder that
> you have already added to the path.
>
> ~~~
> $ ln -sf ~/src/FastQC/fastqc ~/bin/fastqc
> ~~~
> {: .bash}
>
> Due to what seems a packaging error
> the executable flag on the fastqc program is not set.
> We need to set it ourselves.
>
> ~~~
> $ chmod +x ~/bin/fastqc
> ~~~
> {: .bash}
{: .solution}

**Test your installation by running:**

~~~
$ fastqc -h
~~~
{: .bash}

### Trimmomatic

> ## MacOS
>
> ~~~
> conda install -c bioconda trimmomatic=0.38=0
> ~~~
>{: .bash}
{: .solution}

> ## Trimmomatic Source Code Installation
>
> If you prefer to install from source, follow the directions below:
>
> ~~~
> $ cd ~/src
> $ curl -O http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.38.zip
> $ unzip Trimmomatic-0.38.zip
> ~~~
> {: .bash}
>
> The program can be invoked via:
>
> ~~~
> $ java -jar ~/src/Trimmomatic-0.38/trimmomatic-0.38.jar
> ~~~
>
> The ~/src/Trimmomatic-0.38/adapters/ directory contains
> Illumina specific adapter sequences.
>
> ~~~
> $ ls ~/src/Trimmomatic-0.38/adapters/
> ~~~
> {: .bash}
{: .solution}

**Test your installation by running:** (assuming things are installed in ~/src)

~~~
$ java -jar ~/src/Trimmomatic-0.38/trimmomatic-0.38.jar
~~~
{: .bash}


> ## Simplify the Invocation, or to Test your installation if you installed with miniconda3:
>
> To simplify the invocation you could also create a script in the ~/bin folder:
>
> ~~~
> $ echo '#!/bin/bash' > ~/bin/trimmomatic
> $ echo 'java -jar ~/src/Trimmomatic-0.36/trimmomatic-0.36.jar $@' >> ~/bin/trimmomatic
> $ chmod +x ~/bin/trimmomatic
> ~~~
> {: .bash}
>
> Test your script by running:
>
> ~~~
> $ trimmomatic
> ~~~
> {: .bash}
{: .solution}

