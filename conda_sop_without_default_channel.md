#Installing Conda and Disabling the Default Channel

## Purpose
This document outlines the steps to install conda and configuring it to exclude the default Anaconda channel, which requires a commercial license in enterprise settings.


---

## Installation Procedure

### 1. Installing conda
There is an installation script `Miniconda3_Install.sh`, and running it will install Miniconda3 in your account. If you want the most recent version of the installer, you can use google to find it.

The installer will prompt you to agree to the license and will ask you to specify the path for the installation. Selecting the default path is recommended at this step. It will then install the miniconda package and will prompt to make conda the default environment to log into.

### 2. Activating conda 
If you chose not to activate conda at the startup following methods can be used to activate it as needed. Note that the assumption is that conda has been installed in the default location given by the installer. 

#### Method 1 - Using an Alias
you can add the alias 
```bash
alias conda-init='eval "$($HOME/miniconda3/bin/conda shell.bash hook)"'
```
to your `~/.bashrc` file. You can now activate conda by just typing conda-init


#### Method 2 - Using a Script
You can altenatively create a script `conda-init.sh` with the code

```bash
#!/bin/bash
eval "$($HOME/miniconda3/bin/conda shell.bash hook)"
```
You can run this script with the command
```bash
source conda-init.sh
```
Note that you must use source command or the dot command to execute the script in the current shell. Adding execution permission and running it directly will not work.
```bash
eval "$($HOME/miniconda3/bin/conda shell.bash hook)"
```
into the terminal.

#### Method 3 - Direct Running 
You can also activate conda by directly typing


## Deactivating the Default Channel 


### 1. Remove the Default Channel

By default, `conda` includes the `defaults` channel. You must explicitly remove it.

```bash
conda config --remove channels defaults
```
After running this command, open the `~/.condarc` file and add the following lines:

```bash
default_channels: []
custom_channels: {}
```

### 2. Add Approved Channels

You should now add trusted and license-compliant channels like `conda-forge` and `bioconda`.

```bash
conda config --add channels conda-forge 
conda config --add channels bioconda
```

---

### 3. Sample `.condarc` File
Below is a sample `~/.condarc` file you can directly create to do all of the above steps.
```yaml
channels:
  - bioconda
  - conda-forge
default_channels: []
custom_channels: {}
```
The HPC has a script `disable-conda-default.sh` that can be run to create this file.

---
