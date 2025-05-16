# Building_Apptainer_with_Anaconda_packages
One way to build your own apptainer containers using anaconda installations

# Base recipe file 

In this example I am using the bootstap ( base OS ) of docker which allows me to build from a base docker image

the ```From: ``` allows me to specify a anaconda3 docker distro

```
Bootstrap: docker

From: continuumio/anaconda3

Stage: CHOOSE A NAME

%labels

PLACEHOLDER

%post

su -  root # USER root

apt-get update \
    && apt-get install -y build-essential \
    && apt-get install -y wget \
    && apt-get install -y git bzip cmake libboost-all-dev parallel zlib1g-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

conda --version

conda install -n base -c conda-forge mamba

mkdir -p /snakey

cd /snakey

PROJECT_DIR=/snakey
```
