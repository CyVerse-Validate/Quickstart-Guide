#A Small Guide to Further Winnow Development

Because of the structure of the Winnow program, it is easy to add in any 
additional performance metrics that you may wish to include in your final analysis. This documentation is intended to provide a comprehensive manual of how to add to Validate and/or alter Validate in any way to provide a more useful way to test genotype to phenotype association methods with known-truth data sets. 
More specifically, this manual is supposed to work in conjunction with the doc strings and other documentation within the code itself. 

As previous documentation will attest, Winnow is the known-truth testing program in the Validate Workflow and the central piece to said workflow.
What is known-truth testing? Known-truth testing is quite simply, a method of creating realistic data sets where we "know the truth" and then seeing how well our methods identify this "truth." 
Simulate covers the former part of this definition, and Winnow covers the latter part.

The code for Winnow is written in Python. This was chosen because it is an easy-to-understand language. And since validation metrics may change over the years, this manual was written to effectively tell tool developers and others how to alter the code so that it can appropriately do what they need it to do.

Although, in many ways, this documentation may reflect what you would expect from an API developer doc, Validate is more of an open-source script than an API. 
However, we have worked hard to make the scripts easily modifiable and understandable by others. Beyond the use of the ubiquitous Python language, 
we have included well-known scientific modules in the source code. By doing so, we hope to encourage the vast usage of these modules in writing additional functions and classes for Validate.

|          |                                                              |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| winnow.py        | This file contains and initiates the main function of the application.  It also makes all necessary calls to other files.                                                              |
| checkhidden.py   | This file does not need to be modified.  It simply provides functions for checking for hidden files within a directory to insure those are not,included in any analysis.               |
| data.py          | This file contains a class named "Data" which transforms a delimited file in to useable data.                                                                                          |
| fileimport.py    | This file provides functions to import data.  Currently, white space and comma delimitation are the only formats supported.                                                            |
| commandline.py   | This file contains functions for retrieving command line arguments.                                                                                                                    |
| gwas.py          | This file contains functions for executing analysis of a GWAS,application.  For a prediction application, additional functions will,need to be made.                                   |
| performetrics.py | This file contains all individualized functions for performance metrics,used in validation of an application.  This is the file we expect will be most heavily modified in the future. 
| adjustments.py   | This file contains all functions for adjusting P-values before running the analysis. |

You will also need to understand the following five objects from the program to effectively modify the code:

| Object Name   | Object Definition                                                                                                                                                                                                                                                                                                                 |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| betaColumn    | The generated list or vector of SNP weights                                                                                                                                                                                                                                                                                       |
| betaTrueFalse | The "truth" about the betas expressed numerically. This is generated from truth files that are specified during execution (files with an *.ote extension. Generally, this list has the same length as betaColumn, except it contains zeros for SNPs with no effect, and then the explicit quantitative effect for all other SNPs. |
| snpTrueFalse  | This "truth" list is equivalent to betaTrueFalse but expressed categorically with booleans rather than quantitatively.                                                                                                                                                                                                            |
| scoreColumn   | This list is the list of generated "scores" reflecting the score assigned to that SNP from the GWAS application. For example, this is the column that would be generally indicated for P-values                                                                                                                                   |
| threshold     | This is a scalar quantity designed for some metrics that require a threshold such as True Positive Rate, for example.                                                                                                                                                                                                             |

##Adding a performance metric

Adding an additional fit statistic to the list of outputs is fortunately very straightforward. As a basic example, if we wanted to include a correlation value:

1) No sense in reinventing the wheel here. We can import the function from an existing Python package: 
`from scipy import stats`

2) Now we implement it in relation to our objects. This will take place in the `performetrics.py` file. 
In this case, we would use the betaTrueFalse and betaColumn objects to produce a function like this:
``` python
def r(betaColumn, betaTrueFalse):
  betaColumn = np.array(betaColumn)
  betaTrueFalse = np.array(betaTrueFalse)
  return stats.stats.pearsonr(betaColumn, betaTrueFalse)[0]
```

3) Finally, be sure to include your new function in the list of GWAS functions in the `gwas.py` file. 
You will need to include the function name—"r" in this case—and the function call—r(betaColumn, betaTrueFalse)—in the file. 
Remember also that we are only changing the gwaswithBeta function, as we could not analyze a GWAS application that did not include SNP weights.

##Adding a P-value adjustment function

If we wanted to include a Benjamini-Hochberg FDR adjustment:

1) The adjustment functions are located in the `adjustments.py` file.

2) For the BH method, p-values are ordered from largest to smallest and adjusted based on their position or the adjusted value of the previous p-value: whichever is less. The adjusted values are then returned in their original order.

``` python
def fdr_bh(score_col):
  # List for p-vals in order from largest to smallest
  ordered_scores = list()
  # Copy of list of p-vals so the original is not modified
  score_col_copy = list(score_col)
  # List of adjusted p-vals in original order to be returned
  new_pval = [None] * len(score_col)
  # Copies the original list of p-vals into score_col_copy as a tuple (p, index(p)) so we can save the original          order
  for each in score_col_copy:
      ordered_scores.append((each, score_col_copy.index(each)))
      # Removes each p-val from the copy list to ensure that indexes are accurate in case of duplicate p-cals
      score_col_copy[score_col_copy.index(each)] = None
  # Sorts p-vals smallest to largest, then reverses so they are ordered largest to smallest
  ordered_scores.sort()
  ordered_scores.reverse()
  # Solves for the adjusted p-val of the first (largest) original p-val
  adjusted = len(ordered_scores)*ordered_scores[0][0]/len(ordered_scores)
  # Iterates through all ordered p-vals, sets val to the minimum of the previous adjustment and current adjustment
  for each in ordered_scores:
      val = min(adjusted, float(len(ordered_scores)) * float(each[0]) /
                float(len(ordered_scores) - ordered_scores.index(each)))
      # Sets the index of new_pval(from the tuple in ordered_scores) to the adjusted p-val
      new_pval[each[1]] = val
      # Updates the adjusted value so the minimum function will work on the next iteration
      adjusted = val
  # Returns the list of adjusted p-vals in the original order
  return new_pval
```

3) We then must add fdr_bh into the `winnow.py` file by adding the import `from adjustments import fdr_bh`

4) Lastly you must add your new method to the `adjust_score` function in `winnow.py` 

```python
  def adjust_score(self, score):
      if 'pvaladjust' not in self.args_dict.keys():
          return score
      elif self.args_dict['pvaladjust'] == 'BH':
          return fdr_bh(score)
      # Add other adjustments here
      else:
          print 'Currently only BH (Benjamini-Hochberg) is supported, the original P-values will be used'
          return score
```

5) You can add other adjustments with an elif statement. For example, you added the BY adjustment function so before `else` you would add:

```python
elif self.args_dict['pvaladjust'] == 'BY'
  # Return the function you created
  return fdr_by(score)
```

6) You can then use your adjustment in winnow by passing the parameter --pvaladust BY or -p BY; where BY is the value that you set in the above step.

*Definitions and example originally from iPlant wiki page: [A Quick Guide for Further Developing Validate](https://pods.iplantcollaborative.org/wiki/display/docs/A+Quick+Guide+for+Further+Developing+Validate)*

[Back to Read Me](../README.md)
