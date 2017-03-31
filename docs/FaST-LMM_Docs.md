# FaST-LMM

*(Links to sample data, the user manual, and another tutorial are available at the bottom of this page)*

>The main genome wide association studies tool that we have used, FaST-LMM stands for *Fa*ctored *S*pectrally *T*ransformed *L*inear *M*ixed *M*odels. It is a tool from Microsoft Research designed for analyses of very large data sets, and has been tested on data sets with over 120,000 individuals.

## Running the Program

**The program requires a minimum of three files to function:** 

1. A [PEDMAP](http://pngu.mgh.harvard.edu/~purcell/plink/data.shtml) set of files
2. A phenotype file corresponding to the PEDMAP set
3. A set of [PLINK](http://pngu.mgh.harvard.edu/~purcell/plink/index.shtml) formatted files to compute the genetic similarity matrix decomposition. This does not need to be different from number 1. 

**The input flags you would use are as follows:**
* **-file :** Denotes the file name for the PLINK .ped/.map files
* **-bfile :** Denotes the name for PLINK .bed/.bim/.fam files
* **-tfile :** Denotes the name for PLINK .tped/.tfam files
* **-pheno :** Denotes the name of the phenotype file (including extension)
* **-covar :** Denotes the name of the covariate file (including file extension)
* **-out :** The name of your final output file, which is placed into the same directory as your program and data unless otherwise specified

**These are the bare minimum options needed to run FaST-LMM; however, some other options for considerations are...**
* **-verboseOutput :** use this flag to show more complex and detailed output; does not require a file to be named
* **-fileSim :** The name of the PLINK set used for computing the genetic similarity matrix and its decomposition
* **-pValuePrintThreshold :** Restricts the output file to only include SNPs with a p-value less than or equal to the specified threshold

An example of executing the FaST-LMM program might look like so:
`fastlmmc -verboseOutput -bfile toydata -pheno toydata.phe.txt -covar toydata.covar.txt -out MyResults.csv`

#### **Additional information** 
[Tutorial on iPlant confluence Wiki](https://pods.iplantcollaborative.org/wiki/display/TUT/FaST-LMM)  

[User Manual](http://nbviewer.ipython.org/github/MicrosoftGenomics/FaST-LMM/blob/master/doc/ipynb/FaST-LMM.ipynb)  

[Sample Data](http://mirrors.iplantcollaborative.org/browse/iplant/home/shared/iplantcollaborative/example_data/fastlmm)  

[Back to Workflow Documentation](workflow\ documentation.md) | [Next: GEMMA](GEMMA\ Doc.md)
