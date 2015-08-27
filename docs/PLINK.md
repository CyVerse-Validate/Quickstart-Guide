#PLINK: An Open-Source Whole Genome Association Analysis Toolset

*(Links to sample data, the user manual, and another tutorial are available at the bottom of this page)*

-----------

>PLINK is a popular bioinformatics tool designed, "for basic, large-scale analyses in a computationally efficient manner."--<cite>[PLINK documentation](http://nce.ads.uga.edu/~ignacy/numpub/blupf90/docs/qxpak.pdf)</cite> 

In the context of the Validate Workflow, PLINK is useful for handling both linear and logistic regression models and for file format conversion. 
Though PLINK's analysis algorithms may not be quite as thorough as other mixed model software's, 
it is a versatile GWAS (genome wide association studies) tool for handling dosage analysis, genotype-environment interactions, epistasis, and data management.

##Input File Formats

**NOTE:** For most any type of command you run in PLINK, the program will initially try and connect to the Internet to download the latest version of the software. 
Because this process is often unnecessary and time-consuming, we recommend using the `--noweb` flag in each of your commands to tell PLINK not to update.

The file formats PLINK uses for genotype data fall into several different groups:

####**PED/MAP files** 
------
Standard files with .ped and .map extensions detailing the genotype information of an individual or a group of individuals. The PED file is delimited by spaces or tabs, and the first six columns of a PED file must correspond to the following: 
*Family ID*, *Individual ID*, *Paternal ID*, *Maternal ID*, *Sex*, and *Phenotype.* The MAP file is a description of each genetic marker, and this file must have exactly 4 columns:
*Chromosome*, *SNP ID*, *Genetic distance (in morgans)*, and *Base-pair position*.

To run PED/MAP format files, use this command:

  `plink --file <dataset name sans extension>`

Alternatively, if the PED and MAP files have different names, use these commands:

  `plink --ped <PED file> --map <MAP file>`

If certain columns of the PED files are missing, the flags `--no-parents`, `--no-sex`, and `--no-pheno` may be used to denote PED files without the paternal and maternal IDs, sex, or phenotype respectively.

####**BED/BIM/FAM files** 
------
Binary equivalents of the PED/MAP files. Because of the conversion to binary, these files take up far less storage space and can be more efficiently loaded than an equivalent PED/MAP set would. 
Furthermore, do not attempt to read the BED file; it is a compressed file and a text editor will only show strange characters when opening the BED file. 
The BIM and FAM files, however, are still readable in a standard text editor. The BIM file is basically an extended MAP file with two extra columns designating the allele names. 
The FAM file is merely the first six columns of the PED file, and as such displays the mandatory information detailed above.

To run BED/BIM/FAM files, use this commmand:

  `plink --bfile <binary dataset name, sans extension>`

####**TPED/TFAM files** 
------
These files represent a transposed fileset. 
The first 4 columns of a TPED file are the same as a standard 4-column MAP file. Then, all genotypes are listed for all individuals for each particular SNP on each line. 
The TFAM file, like the standard FAM file, is just the first six columns of a standard PED file.

To run the TPED/TFAM files, use this command:

  `plink --tfile <transposed dataset name, sans extension>`

Note that some or all of these file extensions are also usable with other genome wide association studies tools in the Validate Workflow (e.g. FaST-LMM, GEMMA). 

In some cases, PLINK also supports covariates in a given dataset. A covariate file should be formatted with three columns: *Family ID*, *Individual ID*, and *covariate value*. To load said covariate file, type in the command line like so:

  `plink --file <dataset> --covar <covariate file, plus extension>`

##File Format Conversion

Depending on your purpose for your data, occasionally conversion between PLINK formats may be necessary. 
Fortunately, PLINK is very efficient in this regard, and even extremely large datasets can be converted in a reasonable amount of time.

Assuming that you are starting with the standard PED/MAP format, data may be converted into binary format with the command 

  `plink --file <dataset name> --make-bed`. 

The default output name for the new BED/BIM/FAM files will be *plink*; however, the output name can be changed by instead running 

  `plink --file <dataset name> --out <new binary name> --make-bed`

This `--out` option for specifying the new file name may be used with any other type of PLINK file conversion or operation done from the command line. 

To instead create transposed datasets, run the command:

  `plink --file <dataset name> --transpose`

Finally, to convert a binary or transposed file set back to its original PED/MAP format, add the --recode option to the command line like so:

  `plink --bfile or --tfile <dataset name> --recode --out <new dataset name>`

##Data Analysis

PLINK is also capable of running many types of basic quantitative analyses including epistasis, dosage analysis, and meta-analysis. For the purposes of this tutorial, however, we will only focus on the three algorithms for quantitative trait association.<br></br> 
**First**<br></br>
The standard quantitative trait association analysis may be called using the command 

  `plink --file <dataset> --assoc --out <output name>` 

This command will create a new file titled based on whatever name you specified in the command (will be called plink by default). 
Regardless of your chosen file name, the file extension will be *.qassoc* and it will have the following columns:

|           |                |
|:----------|:-------------  |
| CHR   | Chromosome number |
| SNP   | SNP Identifier |
| BP    | Physical position (base-pair) |
| NMISS | Number of missing genotypes |
| BETA  | Regression coefficient |
| SE    | Standard Error |
| R2    | Regression r-squared (coefficient of determination) |
| T     | Wald test (based on a t-distribution) |
| P     | Wald test asymptotic p-value |

**The other two quantitative association methods are regression models**<br></br> 
Both linear and logistic regression are supported, and these models are actually more flexible than the standard quantitative trait association option. 
More specifically, these regression models allow options for the aforementioned covariate files (again using the `--covar` option), 
for the interaction between said covariates and the SNPs (`--interaction`), 
for confidence intervals with each value (`--ci <decimal number between 0 and 1>`), etc. Keep in mind that while these regression models have extra options, they come at the price of increased runtime.

**linear regression models**<br></br>
To run a linear regression model, type the command like so:

  `plink --file <dataset name> --out <output name> --linear` 

This will generate an *.assoc.linear* file with the name specified. 

**logistic regression models**<br></br>
to run a logistic regression model, type 

  `plink --file <dataset name> --out <output name> --logistic`

This command will generate an *.assoc.logistic* file with the output name you specified.
For both of these options, the standard columns in the output files will be the following:

|           |                |
|:----------|:-------------  |
| CHR   | Chromosome number |
| SNP   | SNP Identifier |
| BP    | Physical position (base-pair) |
| A1    | Tested allele (minor allele by default) |
| TEST    | Code for test (ADD for additive effects of allele dosage by default) |
| NMISS | Number of non-missing individuals included in analysis |
| BETA/OR  | Regression coefficient (for linear regression) or odds ratio (for logistic) |
| STAT  | Coefficient t-statistic |
| P     | Asymptotic p-value for coefficient t-statistic |

Any of these analyses outputs may be run through Winnow and therefore are compatible with the rest of the Validate Workflow (so long as a known-truth file is available as well).

[Tutorial on iPlant confluence Wiki](https://pods.iplantcollaborative.org/wiki/display/DEapps/PLINK)<br></br>
[PLINK documentation](http://pngu.mgh.harvard.edu/~purcell/plink/index.shtml)<br></br>
[Sample data](http://mirrors.iplantcollaborative.org/browse/iplant/home/shared/syngenta_sim/PEDMAP_DE) (WARNING: Very large datasets)
