> Estimated time to complete this tutorial is ~2 hours

> Prior knowledge needed - Basic bash command familiarity, terminal use familiarity, accessing stampede

> Tools needed - Computer, internet access, TACC allocation or Agave API on local machine


# Tutorial for running Validate using a sample data set.

This guide assumes you will be using Stampede to run the workflow. Validate may be ran on your own hardware by cloning from our github or setting up Agave locally (INSERT LINK TO QUICKERSTART GUIDE WHEN ADDED TO THIS REPOSITORY).

## 1. Accessing Stampede

On a mac or linux system, simply ssh into Stampede using your TACC username and password.

~~~~~
ssh taccuserid@stampede.tacc.utexas.edu
~~~~~

After entering your password you will be placed on a login node on the Stampede system. 

Some basic familiarity with the linux CLI will be helpful. Try to make practice of typing commands rather than copy-pasting them.

Remember, you can type cd at any point to return to your home directory should you get "lost."

For full documentation for Stampede user access, please see [this link](https://portal.tacc.utexas.edu/user-guides/stampede)

## 2. Downloading Validate

Activate Git module
~~~
module load git
~~~

Clone Validate into home directory
~~~~
git clone -b Developing-Release https://github.com/CyVerse-Validate/Validate.git
~~~~


## 3. Accessing Syngenta data set


## 4. Submitting jobs using SLURM

https://portal.tacc.utexas.edu/user-guides/stampede#running

# Using Agave:

The Agave API provides a set of CLI tools for accessing the Cyverse data store and running apps on Stampede. Comprehensive instructions for configuring your client may be found [here](https://github.com/iPlantCollaborativeOpenSource/cyverse-sdk).

Frequently-Used Commands

example of submitting a job w/ syngenta data

Include JSON skeleton



