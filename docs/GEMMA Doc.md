#GEMMA

*(Links to the user manual, and another tutorial are available at the bottom of this page)*

>GEMMA  is  the  software  implementing  the  *G*enome-wide  *E*fficient  *M*ixed  *M*odel  *A*ssociation algorithm for  a  standard  linear  mixed  model  and  some  of  its  close  relatives  for  *G*enome-*W*ide *A*ssociation *S*tudies (GWAS). It fits a univariate *L*inear *M*ixed *M*odel (LMM) for marker association tests with a single phenotype to account for population stratification and sample structure, and for estimating the proportion of variance in phenotypes explained (PVE) by typed genotypes (i.e. "chip heritability").  It fits a multivariate linear mixed model (mvLMM) for testing marker associations with multiple phenotypes simultaneously while controlling for population stratification, and for estimating genetic correlations among complex phenotypes. It fits a Bayesian sparse linear mixed model (BSLMM) using Markov chain Monte Carlo (MCMC) for estimating PVE by typed genotypes, predicting phenotypes, and identifying associated markers by jointly modeling all markers while controlling for population structure.  It is computationally efficient for large scale GWAS and uses freely available open-source numerical libraries--<cite>[GEMMA user manual](http://www.xzlab.org/software/GEMMAmanual.pdf)</cite>

To see all of the possible inputs for GEMMA, simply type this into the terminal:

    gemma -h

To run a basic mixed model analysis with GEMMA, you will need your inputs in either PLINK binary format (BED/BIM/FAM extensions) or BIMBAM formats (with mean genotype, phenotype, and an optional annotation file). Once you have your data in this format, GEMMA also requires a relatedness matrix to run the mixed model; however, GEMMA has a relatedness matrix calculation algorithm built in.

<br>**With PLINK binary files, type your commands in as shown:**</br>

    gemma -bfile <fileset name/prefix> -gk <1 or 2> -o <output prefix>

These file options indicate:

* **-bfile :** A character string.The name of the PLINK binary file set, given without the extension. For example, if your files are names dat.bed, dat.bim, and dat.fam, you would just type in dat after the bfile flag.
* **-gk:** An integer, either 1 or 2. Tells GEMMA the type of relatedness matrix to calculate. Option 1 calculates the centered relatedness matrix, while option 2 calculates the standardized relatedness matrix.
* **-o:** A character string. Your designated name for the analysis output.

<br>**Using the BIMBAM file format, your command line input will look like this instead:**</br>

    gemma -g <filename> -p <filename> -gk <num> -o <output prefix>

These file options indicate:

* **-g:** A character string. Indicates the mean genotype file in your set. The full name, including extension, is required.
* **-p:** A character string. Indicates the phenotype file for your set. Again, the full name is required.
* **-gk and -o options are the same as above.**

Once the relatedness matrix algorithm is finished, GEMMA will create a folder in the current directory called output. Here, you will find the relatedness matrix file: <output name>.CXX.txt.

Now that you have a relatedness matrix, you can use that file in either a univariate mixed model analysis or a multivariate mixed model analysis. 

<br>**To run a univariate analysis with PLINK binary files, type out your commands in the terminal like so:**</br>

    gemma -bfile <fileset name/prefix> -k <filename> -lmm <num, 1-4> -o <output prefix>

These file options indicate:

* **-bfile:** A character string.The PLINK binary file set name. Like previously, only the prefix is required; do not type any of the extensions in for this option
* **-k:** A character string. The name of the previously calculated relatedness matrix file. Full name, including file extension, is required.
* **-lmm:** An integer between 1 and 4 inclusive. Specifies which frequentist test to use and which corresponding p-value to list in the output. Option 1 gives the Wald test, option 2 gives the likelihood ratio test, option 3 gives the score test, and option 4 performs all three tests.
* **-o:** Character string. Specifies your desired output prefix for the analysis file.

Once the analysis is complete, check the output folder in your current directory for your mixed model output: <output name>.assoc.txt. 

<br>**Similarly, for running the univariate mixed model with the BIMBAM formatted data, the terminal commands will look like this:**</br>

    gemma -g <filename> -p <filename> -a <filename> -k <filename> -lmm <num, 1-4> -o <output prefix>

These file options indicate:

* **-g:** Character string; the mean genotype file for your fileset. The full filename, including extension, is required
* **-p:** Character string; the phenotype file for your set. Again, the full name is required.
* **-a:** Character string; the annotation file of the set (optional)
* **-k:** A character string. The name of the previously calculated relatedness matrix file. Full name, including file extension, is required.
* **-lmm:** An integer between 1 and 4 inclusive. Specifies which frequentist test to use and which corresponding p-value to list in the output. Option 1 gives the Wald test, option 2 gives the likelihood ratio test, option 3 gives the score test, and option 4 performs all three tests.
* **-o:** Character string. Specifies your desired output prefix for the analysis file.

For the multivariate mixed model, the only additional command line argument required is...

* **-n:** One or more integers separated by spaces; indicates which phenotype values in the phenotype file (whether PLINK binary or BIMBAM format) are included in the association analysis.

####**Additional information** 
[Tutorial on iPlant confluence Wiki](https://pods.iplantcollaborative.org/wiki/display/atmman/Validate+Workflow+v0.7#ValidateWorkflowv0.7-GEMMA)<br></br>
[User Manual](www.xzlab.org/software/GEMMAmanual.pdf)<br></br>

