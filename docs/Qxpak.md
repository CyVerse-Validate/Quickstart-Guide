(Links to sample data, the user manual, and another tutorial are available at the bottom of this page)

Qxpak v.5

"Qxpak is a package for versatile statistical genomics, specifically designed for sophisticated quantitative trait loci and association analyses. Multiple loci, multiple trait, infinitesimal genetic effects, imprinting, epistasis or sex linked loci can be fitted. The new version (v. 5) allows us, among other new features, to include either relationship matrices obtained with molecular information or user defined matrices that can be read from an input file. This feature can be used for genome selection or - more importantly - to correct for population structure in association studies. In crosses, two parental lines, not necessarily inbred, can be accommodated"

-Qxpak manual. 

###**Inputs**
Qxpak normally requires four files: 

1. parameter file with input details
2. data file containing phenotypes and any effect that may be included in the model
3. pedigree file with genotypes
4.  marker file with genotypes.



**Parameter file**

The parameter file carries the parameters for the program to run, and specifies the files which Qxpak will use. The file will ask for the following files to be defined. 

|      ___  |                |
|:----------|:-------------  |
| $data     | Data file      |
| $pedigree |  Pedigree file |
| $marker   |   Marker file  |
|$userInverse | User direct - user-defined covariance matrix file |
|$userDirect|User direct - user-defined covariance matrix file|
|$haplotype|Haplotype file|
|$output   |Output file |


**Data File**
The data file is a .dat file, a free-format file without a header that always contains the individual in the first column, whether it be numeric or alphanumeric. Record order is not important. Subsequent columns include traits and effects and may include more than are used in the model.
Missing values must be coded as 0. If the actual value is 0, recode it as 0.000001.

**Pedigree File**
A pedigree file is required for quantitative trait locus (QTL) analysis. This file includes the individual, father, mother, sex, and breed. The last two are optional if analyzing non-sex chromosomes or within breed populations. Individuals do not have to be coded; missing parents should be indicated with a 0. Breed is irrelevant unless at least one parent is unknown.

**Marker File**
Two formats are available: “usual” and “transposed”. In the usual format, the first record contains the chromosome name and successive records contain: individual, allele1_mkr1, allele2_mkr1, etc. Missing alleles are specified by 0.
The transposed format is appropriate when there are many more markers than individuals. In this format, the first row is a list of individual codes, and successive rows contain: SNP_name, chr_number, ind1_allele1, ind1_allele2, ind2_allele1, ind2_allele2, etc. Unknown markers should be coded as 0, and chromosomes must have numbers rather than names; markers should be arranged by chromosome 1, 2, etc.

**User-Defined Covariance Matrix Files**
One or two files can be included to allow for the including of random effects distributed as N(0,V), where V can be any positive definite matrix which is stored in the file. The matrix is then invertyed to obtain random effects predictions, and the inverse can also be included to save computation. The parameter file must be modified appropriately to apply the effects to specific columns.
The format of these files is: row, column, value in space-delimited form like the other files.

**Haplotype File**
Contains known haplotypes if any. The first record contains the name of the chromosome. Successive records include individual, order of markers where phases known. If several chromosomes are analyzed, the format should be repeated for each.

###**Outputs**

**q.0**
Contains running output that might be useful for, among other things, checking convergence.

**Primary Output File**
A variety of different results are reported in the same file.

**Haplotype Output File**
If the applicable section in the parameter file is specified, the haplotypes sampled at each MCMC iteration are written. The format is: chromosome, MCMC_iteration, individual, phase, alleles.

**Z Files**
Z files contain the IDB probabilities or SNP configurations.

**Other Output Files**
There are numerous other undocumented output files.

###**Wrapper Script**
There is also a wrapper script available on the iplant wiki page, link.
This allows the user to write in the parameters directly into the command line without having to edit the parameter file repeatedly. 

|      ________  |                |
|:---------------|:-------------  |
| -p|Name of the parameter file using the $ markers above.|
| -d|Name of the data file; the replacement for $data.|
| -g|Name of the pedigree file; the replacement for $pedigree.|
|-m|Name of the marker file; the replacement for $marker.
|-i|Name of the user-defined inverse file; replacement for $userInverse.|
|-t| Name of the user-defined direct file; replacement for $userDirect.|
|-h |Name of the haplotype file; replacement for $haplotype.
|-o|Name of the output file; defaults to result.txt. Several other files may be generated depending upon the parameter file.|

A sample code with the wrapper used would look like… 
 

    qxpakwrapper.py -p parameterFile.par -d dataFile.dat -g pedigreeFile.ped -m markerFile.mkr -i userInverse.inverse -t UserDirect.direct -h haplotypes.haplo -o results.csv

####**Additional information** 
[Tutorial on iPlant confluence Wiki](https://pods.iplantcollaborative.org/wiki/display/DEapps/Qxpak)<br></br>
[User Manual](http://nce.ads.uga.edu/~ignacy/numpub/blupf90/docs/qxpak.pdf)<br></br>
[Sample Data](http://mirrors.iplantcollaborative.org/browse/iplant/home/shared/iplantcollaborative/example_data/qxpak)
