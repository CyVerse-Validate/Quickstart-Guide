# Generating a sample data set using Alphasim

## Running Alphasim through Agave
** Estimated Time ~30min **

Prerequisites: Agave CLI, general knowledge of executing using Agave, Access to Cyverse data store, and Stampede allocation (if you want).

Helpful Documentation

Alphasim: http://www.alphagenes.roslin.ed.ac.uk/wp-content/uploads/AlphaSimManual/AlphaSim.html
Alphasim parameter file: https://github.com/CyVerse-Validate/Stampede-Files/blob/master/AlphaSim-1.04/AlphaSimInputInformation.txt

##Locate / Open parameter file

You can download a sample parameter files from our repository. The parameter file allows you to pass commands into the AlphaSim software.
Once you have access the parameter file, upload it to your Data Store. The default parameter file has specifications for running multiple generations for corn genetics.

Upload with command (where USERNAME is your Cyverse username and FOLDERNAME is where you would like it to be located on the data store): files-upload -S data.iplantcollaborative.org -F AlphaSimSpec.txt USERNAME/FOLDERNAME

* Save the following as a JSON file (This can be saved locally if you have the Agave CLI installed) with username replaced with your CyVerse username and the path to the file to the parameter file within your Data Store.
`{
   "jobName": "testAlphaSim",
   "softwareName": "AlphaSim-1.04",
   "requestedTime": "05:00:00",
   "archive": true,
   "inputs":{
     "specificationFile": "agave://data.iplantcollaborative.org/USERNAME/ALPHASIM_SPEC_PATH"
     }
    }`

* With the following command you can run AlphaSim (publicly available on Agave). This is assuming that you don’t want to change any of the parameters:

`jobs-submit -F [path to json file]`

* After submitting your job there will be a returned message which will list your job-id - This is helpful for looking up the job status and downloading output later.

* The command:

`job-status [yourjobid]`

will allow you to see when your job will be done

* Once this finishes it will save onto your Data Store, if Archive is set to true, under Archive/Jobs in your personal DE folder.

* You can download your outputs from jobs with the general command:

`jobs-output –download –path [path to the desired file relative to the job output folder on the data store] [JOBID]`

* You will download your outputs to your local computer from the Data Store with the following commands:

`jobs-output –download –path AlphaSim/Selection/SelectionFolder1/SnpSolutions.txt [yourjobid] jobs-output –download –path AlphaSim/SimulatedData/Gender.txt [yourjobid] jobs-output –download –path AlphaSim/SimulatedData/PedigreeTbvTdvTpv.txt [yourjobid] jobs-output –download –path AlphaSim/SimulatedData/AllIndividualSnpChips/Chip1Genotype.txt [yourjobid] jobs-output –download –path AlphaSim/Chromosomes/Chromosome1/Chip1SnpInformation.txt [yourjobid]`

* Alternatively, feel free to modify this bash script to your needs to automate pulling in all of the output files:

https://github.com/CyVerse-Validate/Stampede-Files/blob/master/AlphaSim-1.04/getFilesExample.sh

* If you are okay with these outputs they are now useable. You also have the option to convert to pedmap (which is a more standard format) using our merger application:

## Convert to ped/map

1. Download the merger.py from the github repository here (or if you have already installed Validate, it is included): https://github.com/CyVerse-Validate/Validate/tree/master/CurrentReleaseStable/Util_1/Merger

2. Run the merger with the AlphaSim outputs with the following commands from the directory where your AlphaSim output is located, where ALPHASIMPREFIX is the prefix of your job output:

`python PATHTOMERGE/merge.py –output ALPHASIMPREFIX alphasim –snp SimulatedData/Chip1SnpInformation.txt –pedigree SimulatedData/PedigreeTbvTdvTpv.txt –gender SimulatedData/Gender.txt –geno SimulatedData/AllIndividualsSnpChips/Chip1Genotype.txt –sol Selection/SelectionFolder1/SnpSolutions.txt`

This will yield ALPHASIMPREFIX.ped and ALPHASIMPREFIX.map in the directory specified in your above output flag.

* To convert your ped/map files to bed/bim/fam format, required by many applications such as fastlmm, follow these steps:

## Convert to bed/bim/fam

1. Download plink from the github repository here (or if you have already installed Validate, it is included): https://github.com/CyVerse-Validate/Validate/blob/master/CurrentReleaseStable/GWAS_1/plink

2. Run Plink with the following command from the directory where your ped/map files are located:

`PATHTOPLINK/plink –file ALPHASIMPREFIX –out ALPHASIMPREFIX –make-bed`

* At this point, you should have all the original output available to you as well as ped/map files and bed/bim/fam files and can use the appropriate files for your job
