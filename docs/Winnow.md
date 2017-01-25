#Winnow
*(Links to sample data, and another tutorial are available at the bottom of this page)*

>The bread-and-butter of the workflow, Winnow (formerly the eponymous Validate), is a Python-compatible known truth testing tool for genome wide association studies. Quite simply, Winnow is a tool that evaluates other tools. 
Winnow requires output from a GWAS tool after analyzing a data set. Given the "known truth" of the original data set, Winnow outputs a series of fit statistics to determine the validity of the GWAS tool and whether or not it was truly useful in analyzing the data.

###Winnow Guide

On the _Validate Workflow v0.5_ Atmosphere instance, the main Winnow program, `winnow.py`, is located in the `/usr/bin` directory along with its modules. To see all of the possible options, type this command into the terminal/command line:

`python winnow.py --help`

Though there are quite a few possible options, the following are the only _required_ arguments: 
* **--folder** (or **-F**) which denotes the folder of aggregated GWAS results
* **--class** (or **-C**) to specify the “known-truth” file
* **--snp** (or **-S**) to specify a string/name for the SNP column in the input file
* **--score** (or **-P**) to specify a string/name for the name of the scoring column in results file (e.g., P-value)
* **--filename** (or **-f**) to specify the desired filename for the Validate output file (without file extension); defaults to Results.txt as output filename
* **--kttype** (or **-k**) to specify the type of known-truth file for --class (either OTE or FGS, see below for more details)

Other possible arguments include:
* **--analysis** (or **-a**) to specify the type of analysis, “GWAS” or “prediction” (currently, only GWAS is available and if left blank, Winnow assumes GWAS)
* **--threshold** (or **-t**) to specify a desired threshold for classification metrics where necessary (default is 0.05)
* **--verbose** (or **-v**) to trigger verbose mode
* **--seper** (or **-s**) to indicate how values are separated in the output file (comma or whitespace)
* **--kttypeseper** (or **-r**) to specify the delimination in the known-truth file (comma or whitespace)
* **--beta** (or **-b**) to specify a string for the name of the estimated SNP effect column in results folder
* **--pvaladjust** (or **-p**) to specify the type of P-value adjustment (Currently only BH is supported)
* **--savep** (or **-o**) to save a file containing the SNP ID, P-value, and the adjusted P-value if applicable

For the --kttype argument, the two possible options are "OTE" or "FGS." The "OTE" format represents "Only Truth and Effect," meaning that only those SNPs with significant effects along with the effect size of those significant SNPs are included in the known-truth file. The "FGS" format means "Full Genome Set," meaning that all SNPs and effects are included.  

####**Additional information** 
[Tutorial on iPlant confluence Wiki](https://pods.iplantcollaborative.org/wiki/display/TUT/Winnow)<br></br>
[Sample Data](http://datacommons.cyverse.org/browse/iplant/home/shared/iplantcollaborative/example_data/Validate/Validate_Test_Data)<br></br>


[Back to PLINK](PLINK.md) | [Additional: Winnow Development](Winnow develop.md) | [Next: Demonstrate](Demonstrate.md)
