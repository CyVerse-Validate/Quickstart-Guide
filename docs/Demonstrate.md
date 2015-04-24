#Demonstrate

Demonstrate is the final step in the Validate known-truth pipeline for iPlant Collaborative. 
Using output from Winnow, it produces a set of graphics showing differences in a GWAS/QTL applications performance under varying heritability and population structure. However,
Demonstrate also functions without the need for heritability or population structure, but different graphics will be produced in that case.

The function you will want to use depends on what type of data you have:

###Data with Heritability and Population Structure Specified 
If you want to visualize differences in your data based on heritability or population structure, you'll want to use the
original function Demonstrate. To run Demonstrate, type `R` on your terminal or command line to open the R console. From there use:

`library(Demonstrate)`
If nothing happens, then you did it correctly! Now the Demonstrate package is loaded. Here are the options to run the function:

`Demonstrate(dir, make.AUC.plot=TRUE, AUC.plot.title="Mean AUC By Population Structure and Heritability",
	make.MAE.plot=TRUE, MAE.plot.title="Mean MAE By Population Structure and Heritability",herit.strings=list("_03_","_04_","_06_")
	,herit.values=list(0.3,0.4,0.6),struct.strings=list("PheHasStruct","PheNPStruct"),struct.values=list(TRUE,FALSE))`
	
In this function, dir represents the directory where all Winnow output is stored. These default values are based on the sample data found within this repository. Once run, the function will create two graphs
on the mean absolute error (MAE) and area under the receiver operator curve (AUC) across varying levels of heritability and/or population structure.
The graphs are in pdf format.

###Other data from Winnow
For other types of data, or if you're more interested in comparing GWAS tools than comparing data, you will want to use the Demonstrate2 function. 
Before running it though, you will need to include the function in your global environment:

`source("<path to>/Demonstrate2.R")`

Then run the function:

`Demonstrate2(dir, make.pos.plot=TRUE, pos.plot.title="True Positives by False Positives",
                       make.error.plot=TRUE, error.plot.title="Plot of AUC by MAE", extra.plots=TRUE, 
                       AUC.axis.min=0, AUC.axis.max=1.0, MAE.axis.min=0, MAE.axis.max=2.0)`

Assuming all outputs are kept, Demonstrate2 will output five files in total. First, two frequency histograms illustrating the distribution of both true and false positives 
(if multiple Winnow files were in the original directory, the pdf files will have multiple pages). Second, a .csv file detailing the average sensitivity, specificity, and precision of each  
file. Finally, two plots based on true vs. false positives and mean absolute error vs. area under the curve will be produced. Demonstrate2 will color the points based on the file they came from, so you
can compare multiple GWAS analysis results on the same plot.
