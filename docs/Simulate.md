#Simulate
Unless you already have simulation data stored or uploaded onto your instance, you may want to start out using *Simulate*, the first step of the workflow. Since Simulate is stored in the /usr/bin directory, either change your location to that folder or use `python /usr/bin/Simulate.py` when running the program. The options for Simulate are:
* **Verbose mode:** `-v` or `--verbose`
* **Population size(s):** `-s` or `--size`*
* **Genome Markers per individual:** `-n` or `--number`
* **Loci with effects:** `-l` or `--loci`*
* **Size of said effects:** `-e` or `--effect`
* **Heritability coefficient** `-i` or `--heritability` (must be decimal value between 0 and 1)
* **Population mean(s):** `-m` or `--mean`*
* **Number of generations to evolve:** `-g` or `--gen`
* **Genetic recombination rate:** `-r` or `--rate` (decimal value between 0 and 1)
* **Output file name:** `-f` or `--filename`
* **Distribution:** `-d` Two options: 0 for normal, 1 for gamma. If the gamma distribution is chosen, you will also need the following arguments for parameters (normal distribution parameters are derived in-program):
  * **Parameter 1:** `-p1` represents the _alpha_ or _shape_ parameter of your gamma distributed population; can be floating point number or integer
  * **Parameter 2:** `-p2` represents the _beta_ or _scale_ parameter of your gamma distributed population; can also be a floating point number or integer 

*If you wish to use more than one argument for these options, separate them by commas with no spaces.

The final output of Simulate is three files: a genome file for the population (CSV format), the known truth of said population (text file in OTE format), and a list of the phenotype values for each generation (TXT format).

One example of running Simulate would look like so:
`python Simulate.py --verbose -s 1000,1000 -n 3000 -l 0,1,2 -e 0.2,0.2,0.2 -m 2.7 -g 100 -i 0.25 -f ~/Desktop/Test`

Note that here we have two subpopulations with 1000 individuals each. These individuals then have 3000 markers and three loci with effects. Those effect sizes are all equal at 0.2, and the population mean for both subpopulations is 2.7 (if no second mean is listed, the program will just duplicate the first mean). These populations will both evolve for 100 generations and the heritabity value of the phenotype is 0.25. Finally, the three output files will be moved to the desktop, all beginning with the word "Test."
At the time of this writing, conversion to different formats will need to be done manually; however, exporting of data to other file formats will be an option in coming updates of the Simulate program.

[Back to Workflow Documentation](./workflow documentation.md) | [Next: FaST-LMM](FaST-LMM Docs.md)
