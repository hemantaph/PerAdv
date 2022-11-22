# PerAdv
Eccentric wave model development and playground

# Install git-lfs
for linux: sudo apt-get install git-lfs \
for mac: brew install git-lfs \
for ligo-cluster: it should be already install \

# git clone 
git clone https://github.com/hemantaph/PerAdv.git
or 
git clone git@github.com:hemantaph/PerAdv.git
then
$ cd PerAdv
$ git lfs pull

# unzip files
$ unzip bilby.zip
$ unzip lalsuite.zip

# create an evironment with the right dependencies
Make sure you are already in anaconda (base) environment
### create an env using lalsuite yml file
Go to cloned repository, PerAdv. Then, change the env name in the yml file to something simple like 'lal' 
$ nano lalsuite/common/conda/environment.yml
or 
$ vim lalsuite/common/conda/environment.yml

After changing the name, create the env named 'lal'
$ conda env create -f lalsuite/common/conda/environment.yml

Now, open the env
$ conda activate lal

# Intalling Bilby
this bilby contain chages in bilby/gw/source.py file
$ cd bilby 
$ pip install -r requirements.txt
$ pip install .

# installing lalsuite
$ ./00boot
$ ./configure --prefix=${HOME}/lalsuite-install 
$ make clean && make && make install
This will create a folder in your home directory. Link lalsuite to your env.
$ . ${HOME}/lalsuite-install/etc/lalsuite-user-env.sh
$ export C_INCLUDE_PATH="${HOME}/lalsuite-install/include:$C_INCLUDE_PATH"

## error handling in installing lalsuite
It there is c or c++ dependency problem add these lines in bashrc
$ nano 
or 
$ vim 

add these lines,

export CC=gcc
export CXX=g++
export LC_ALL=C

LC_CTYPE=en_US.UTF-8
LC_ALL=en_US.UTF-8

# testing lalsimulation and bilby
Check your python is from the right env
$ which python

Now open python 
$ python
>>> import lalsimulation as lal
>>> lal.__file__

you should see file location of lalsimulation and it should be inside the created lalsuite-install directory.
Now call a custom waveform from bilby, 
>>> import bilby
>>> import numpy as np
>>> bilby.gw.source.lal_PerAdvFD(np.array([20,30,40]), 6.5, 5.8, 0.1, 200, 0.4, 1.3)

if it doesn't run go back to the bilby folder and install it again
$ pip install .

# Test folder
Acess the test folder and use the files for various testing with the custom waveform model.



