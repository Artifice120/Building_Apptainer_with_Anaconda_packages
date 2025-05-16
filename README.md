# Building_Apptainer_with_Anaconda_packages
One way to build your own apptainer containers using anaconda installations

# Base recipe file 

In this example I am using the bootstap ( base OS ) of docker which allows me to build from a base docker image

the ```From: ``` allows me to specify a anaconda3 docker distrobution

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

* %post is a required header that runs the following commands after the inital bootstrap is made
* %environment is a required header if you want to use the export command
* %runscript is a headerused to run a script each time the container is activated

> NOTE: the source command will not work in this recipe and the ```conda init``` will lose effect after the container is made
> Consider adding the neede conda contents of the .bashrc to the  %runscript or in a bash script opened in the container

# Running a bash script in a apptainer container 
Unfortunantley, apptainer does not have the ```SHELL``` option when building a container to get around this a shell script can be run with the following options

```
singularity exec container.sif /bin/sh example.sh
```

source commands will still not be recognized. All uses of conda install from here need to use the prefix option ```-p```
