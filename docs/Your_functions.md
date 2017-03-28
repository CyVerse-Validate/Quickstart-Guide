#Installing your own functions

Though the Validate Workflow—on both Atmosphere and Stampede—provides a number of options for GWAS analysis tools, you are
also able to bring your own methods in for use. As long as the output from your function is in the proper style (*not* necessarily file format),
then you can easily integrate it into the workflow.

##Bringing in your own functions

On Atmosphere and Stampede both, bringing in your own methods are not terribly difficult. 
All you need is the source code, a terminal, and access to the rest of the Workflow.

1) Upload either the source code of your analysis tool or the compiled executable of your tool to the Atmosphere instance or Stampede node.
To do so, we recommend [VNC Viewer](http://www.realvnc.com/download/viewer/) and [WinSCP](http://winscp.net/eng/index.php), respectively. 
If you have a Mac, simply use the built in Terminal or [Cyberduck](https://cyberduck.io/?l=en).

2) Be sure to set the permissions on your main code or executable such that you will be able to execute it. 
Once you have successfully uploaded your code, simply use the `chmod` command to change the permissions on your code.
For example, `chmod 777 <filename>` changes the permissions such that anyone may execute the file if desired. (Don't worry,
no one else will have access to your particular instance or node, so allowing open access causes no problems when doing personal research.)

3) Run the code as usual. Please keep in mind, however, that your code's output must adhere to the [output style standards]
to be compatible with the rest of the workflow:

*	Data must be arranged into columns, not rows
* Spreadsheet format (more specifically, CSV) is preferred, but not required
* The following columns are the minimum required for any file format:
  * A column denoting the particular SNP being analyzed
  * A column with the significance score indicating whether or not a SNP is statistically significant (e.g. a p-value column)

Another column that may be included is:
*	A column indicating the effect size or weight of a given SNP for determining a phenotype value 

4) If you are aiming to make permanent your source code either on an Atmosphere instance or on Stampede, 
you'll need to do another few things:

###If on Atmosphere:
The key thing you will need to do is move your source code/executable to a permanent location on the instance. 
**Do not leave anything you want to save on the Desktop or your personal directory!** 
Instead, it's recommended that you move everything either to the `usr` or `usr/bin` folder for imaging. 
In particular, move any executables to the `usr/bin/` directory; that way, one can launch the executable from any location simply by typing its name.
Once you have everything moved to a permanent directory, simply go back to the Atmosphere page, hit the "Image" button, fill out the necessary information, and you're done!

**NOTE:** Even after you fill out the image forms, do not terminate the instance immediately! Atmosphere will need to "take a picture" of your instance, which may take a few minutes.
During that time, please keep your instance either *active* or *suspended.*

##If on Stampede
Getting your app permanently, formally recognized on Stampede involves a bit more effort. 
To list an app on Stampede, you'll need to go through the Agave API and the app submission process there. 
To get started, you'll need to [set up the necessary accounts](Account-setup.md). 
From there, in addition to the source code, you will need a Javascript Object Notation (JSON) file description of your app, test data, and a wrapper shell script for your app. 
For a more in-depth explanation of the requirements, please consult [this tutorial](https://github.com/iPlantCollaborativeOpenSource/iplant-agave-sdk)


[Back to Read Me](../README.md) | [Next: Installing your simulations](Your sims.md)
