#A Quick Guide to Stampede for Beginning Users

**NOTE:** This guide is intended for users who are unfamiliar with the basics 
of the Stampede supercomputer or only have a cursory knowledge of the system. 
For more advanced documentation, please consult one
of the other pages in this repository or the [TACC User Guide](https://portal.tacc.utexas.edu/user-guides/stampede).

##Intro

For those of you who are new to the [Stampede system](https://portal.tacc.utexas.edu/user-guides/stampede), first of all, congratulations on gaining access to one of the most powerful computers on Earth! 
We hope that Stampede will be useful in whatever research you are conducting. Before you start, please make sure that all your accounts are in place.
To check which accounts you need, refer to the [Accounts Setup page.](https://github.com/UNCW-iPlant/Quickstart-guide/blob/master/docs/Account-setup.md) 
Also, using Stampede requires at least a basic familiarity with Linux commands and the command line interface (CLI), so if you are lacking there, please consult this
[Linux cheat sheet](http://linoxide.com/images/linux-cheat-sheet-612x792.png) or the [Software Carpentry shell tutorials](http://swcarpentry.github.io/shell-novice/)

##Differences from Linux Terminal

While the Stampede shell *does* operate under a Linux operating system (OS) and runs bash commands, Stampede is slightly different from a typical Linux terminal.
How so? In one sense, Stampede has many capabilities beyond what a typical Linux shell can do since it is essentially a large compute cluster rather than a standalone computer; 
however, Stampede is also run by a set of administrators, so it is not an entirely isolated computing environment like the [iPlant Collaborative's Atmosphere computing environment]() is.
Some particular differences are outlined below.

1) **Stampede does not allow for root user access for running commands!** The Stampede cluster hosts thousands of users per day on a not-so-isolated computing environment with high processing power; 
giving everyone access to the `sudo` command or the ability to log in as a root user would inevitably cause disaster on the machine. Hence, only the administrators have root access to most of the files.
While you are able to install and change environmental variables for your particular allocation, universal changes are not allowed. By extension, this means that any programming packages or modules 
(e.g. a Python module or an R package) cannot be installed on a permanent location. These packages can be accessed _on your allocation_, however, by changing the PYTHONPATH environmental variable and installing.

2) **Stampede uses SLURM for batch processing in addition to basic Linux commands.** If there's one thing that will get the TACC admins on your case, it's running time-consuming operations on the login node 
(i.e. your location when you first log in). The login node should only be used for small, basic operations that won't take more than a few minutes. Otherwise the operation will borrow from other compute nodes
to complete, and everyone else's performance will suffer. If you have a job or operation that will take a longer time (say, several hours or a day), then you will want to run a batch job using SLURM. 
To run a batch job, create a shell script with your necessary commands and at the top, write a header like the one below to show SLURM how to run your job:

>``#!/bin/bash`				  # tells Stampede this is a command for the bash shell
>`#SBATCH -J myMPI`           # job name
>`#SBATCH -o myMPI.o%j`       # output and error file name (%j expands to jobID)
>`#SBATCH -n 32`              # total number of mpi tasks requested
>`#SBATCH -p development`     # queue (partition) -- normal, development, etc.
>`#SBATCH -t 01:30:00`        # run time (hh:mm:ss) - 1.5 hours
>`#SBATCH --mail-user=username@tacc.utexas.edu`
>`#SBATCH --mail-type=begin`  # email me when the job starts
>`#SBATCH --mail-type=end`    # email me when the job finishes
>`ibrun ./a.out              # run the MPI executable named a.out

This header will give the computer additional options beyond simply running your job and returning the output. Please keep in mind that because SLURM batch processing is available to everyone, your job may not be started immediately.
If you wish to see where your job is regarding priority and progress, type `squeue -U <your TACC username>`. Another command for running a simple command through SLURM is the `srun` command. Again, this command is more useful for one-time executions
when the login node may not be appropriate. All SLURM commands have a usage menu that can be accessed by typing `<slurm command> -h`.

3) **Stampede also has Agave apps and modules available.** By using the Agave API and additional modules in conjunction with the cluster, Stampede can extend its functionality to include a number of user-made programs for research.
Regarding modules, Stampede supports scientific distributions of some popular programming languages including Python, R, and MATLAB (the MATLAB software includes a "bring your own license" usage model).
To see the modules you currently have installed, just type `module list`, and a numbered list of *Currently Loaded Modules* will appear. If you want to search for a particular module, you can use
the `module spider` command to do so. For example, if you wish to search for a particular Python version, type `module spider python`. Some particularly useful modules include:

* Python: includes most packages found in scientific distributions such as numpy, scipy, pandas, etc.
* R: includes many popular packages used for data visualization and analysis
* iRODS: allows for connectivity across the internet to the iPlant Data Store for transferring or accessing files
* intel/13.0.2.146: Installs the most recent version of the Intel compiler for improved code performance and compilation time.

A series of commands for running iPlant applications are also covered in the next section. 

##Setting Up and Running Apps

Regarding apps, through the Agave API, Stampede provides a number of scientific apps that may be combined with the full power of the supercomputer. Most of the apps deal with life sciences, and to see the full list of applications available, use
the command `apps-list`. If you wish to submit an app of your own, you will need a few things set up in a folder either on Stampede or on the iPlant Data Store beforehand:

* The source code for your application
* A test script and test data to run your application
* A general wrapper script for use with Stampede
* A Javascript Object Notation (JSON) file describing your app (see below for a basic example)

While the former three parts are important for actually running the app, the last part-the JSON description file-acts as metadata for others who wish to use your app in the future. 
It shows all of the possible inputs and their types, links to documentation, the version number of your app, and the execution system the app is running on, among other things. 
The format of the JSON file looks much like other Javascript files with emphasis on attribute-value pairings in your app. All JSON files used in the Agave system have the following format:

'{   "application_metadata":"value",
    "inputs":[],
    "parameters":[],
    "outputs":[]
}'

A sample JSON description, then, [may look like this.](https://github.com/iPlantCollaborativeOpenSource/iplant-agave-sdk/blob/master/examples/samtools-0.1.19/stampede/samtools-sort.json)
Though this may be the hardest part of actually making an app, the staff at TACC and iPlant have helped simplify the process by providing an [App Builder](http://agaveapi.co/app-builder/) with real-time updates of your description and a number of templates borrowed from existing applications.
Once your materials are finished, you may want to test your app on a *private execution system.* Because public apps must first be vetted by the administrators, you will want to make sure your app works in the first place. This is where the private execution system comes in handy.
Upon installing the Agave API, you should have three private systems already loaded. To see the names of these systems, type `systems-list in the command line. The private ones will be those with your username attached. To see only your private systems, add `-Q` after typing `systems-list`.

To run an app on your private execution system, simply change the executionSystem line in your app's JSON description to whatever the name of your private system is. Then, to actually submit the app, type `apps-addupdate -F <path to JSON file>`.
From there, you can type `apps-list -Q` to verify that the app has been added to your private apps list (for future reference: `-P` indicates public and `-Q` indicates private listings).

Now that your app has been submitted, you can run jobs with it. Unfortunately, submitting a job request requires another JSON file; however, this JSON only requires you to fill in variable names and file locations. If you have any input folders on other systems (such as the iPlant Data Store),
you will need to write the full path to the files (for example: `agave://data.iplantcollaborative.org/shared/iplantcollaborative/example_data/Samtools_mpileup/ex1.bam`). Once your job file is done, type `jobs-submit -F <path to job JSON>`. You should get a Job ID number once the command goes through.
To check on the status of your job, type `jobs-status <insert Job ID number here>`. This option can also become verbose by adding the -v flag, giving you more information about the status of the job. 

State progression for Agave V2 jobs is: PENDING, STAGING_INPUTS, CLEANING_UP, ARCHIVING, STAGING_JOB, FINISHED, KILLED, FAILED, STOPPED, RUNNING, PAUSED, QUEUED, SUBMITTING, STAGED, PROCESSING_INPUTS, ARCHIVING_FINISHED, ARCHIVING_FAILED.

In the event something goes wrong with your job, you can check on it through the `jobs-history` command. Type `jobs-history <insert Job ID here>` to see where exactly the error(s) formed.

You may also wish to download or look at certain files from your job output. To list the output, type `jobs-output <insert Job ID here>` and to download a file from the output type `jobs-output --download <insert name of output file here>`.

And that about covers it! You should now be able to navigate the Stampede system and run your own code with little trouble. That said, there are many additional commands and options Stampede has to offer beyond what's listed here.
**To see the full list of resources on Stampede, check out the official TACC users guide here!**

**Also, if you want a list of all available commands on Stampede under a certain umbrella (like apps or jobs), type `compgen -c <search term here>** 

##Using the Workflow on Stampede

While the apps will be available through Agave in the near future, for now you are free to upload them from Github and run through batch processing. To upload from Github, take these steps:

1) Use the `module load git` command to upload the git module onto your login node
2) Clone (i.e. make a copy of) the repository with the source code onto either your work directory or home directory. 
`Git commit https://github.com/UNCW-iPlant/Validate-Master` will do the trick. 
Please note that once the cloning process is done, it will produce a local copy of the Validate-Master repository, along with the source code, in whatever directory you were in when you called the git command.
3) For this, all you would need is the source code in the *Current Release* folder. This is the stable release that is currently available.
Use the command `cd ./Validate-Master/<folder you want>` to get to the programs in the workflow. You may need to start with Simulate to generate some data, but if you already have your desired data in place,
simply move on to the next folder: FaST-LMM. From here, you may move the FaST-LMM executable to be in the same folder with you data or specify the path to your data. 
Either way, you may run analyses through batch processing and SLURM commands. For more information on the programs and what inputs you could use, [check the Quickstart guide here.](https://github.com/UNCW-iPlant/Quickstart-guide)

Once the apps are available through Agave, you can just submit a job description like the example linked above to get things running. To submit your job description and get a job started, just
use the `jobs-submit` command corresponding to whatever app you want to run. Make sure you have all of the outputs directed to the right place, along with the links to whatever input you may be using.

