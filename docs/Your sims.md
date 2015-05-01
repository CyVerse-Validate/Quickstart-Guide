##Installing your own simulations

Like the other page in this repository regarding [installation of your own functions,](docs/Your functions.md) the Validate Workflow is also adaptable to 
any of your own simulations that you would like to use. 
To install your own simulations, follow the same steps found on the aforementioned page: upload your source code or executable, change the permissions, and set it to the proper format.
For simulations, keep in mind that your final file formats must be compatible with whatever analysis tool you are using; 
therefore, if your analysis tool of choice only takes PLINK format, for example, be sure that your simulation data outputs in PED/MAP or BED/BIM/FAM formats.

##Bringing simulation outputs to Atmosphere

Another option, rather than moving your simulation software directly to the computing environment, 
is to just save the simulation output to the Data Store and send the simulation output to the computing environment instead. There's only one catch: depending on the size of your simulation files,
transporting *everything* may take some time. If you still wish to do so, a number of methods exist, the most prominent are:

1) Using iRODs
2) An SFTP client like WinSCP or Cyberduck
3) Git (only for files < 100 MB and/or repos < 1 GB)

##IRODs

iRODs is one of the programs that integrates the iPlant Collaborative together; it allows for Data Store connectivity to other services like Atmosphere.
To set up iRODs, type `iinit` on Atmosphere (since iRODs is built in) or on Stampede type `module load irods`, then `iinit`. 
Regardless, you will then need to type your iPlant credentials in at the appropriate prompts 
(port number is 1247, by the way; everything else relates back to your account).

Once your iRODS connection is set up, you will find that most commands are very similar to their Linux counterparts, only with 'i' in front. For example, to list the files in your Data Store
directory, type `ils`; if you wish to change your current directory, type `icd`; if you want to see your current location, type `pwd` and so on. To obtain files from a given folder, the command
is `iget <path.to.file>`. Many flag options exist for each of these commands, and if you want to view them in more detail [check out the iRODs wiki.](https://wiki.irods.org/index.php/icommands). 
Most files will take less than 60 seconds to download assuming they are less than 2 GB each.

##SFTP client

Most secure file transfer protocol (SFTP) clients normally have a type of interface which makes file transfer easier. 
For instance, WinSCP has a drag-and-drop interface which allows for transporting files to a secure shell (like Stampede) en masse.
One thing of note regarding SFTP clients is that most may take longer than iRODs when transferring larger files; 
however, nothing beyond the file and the client are needed to actually make the transfer.

##Git

Using Git is perhaps a last resort for transferring files, in part because it requires both a Github account and that your files are less than 100 MB each.
If your simulation output is stored in a Github repository, however, you may use git to clone/copy it into your current location.

On Atmosphere, use a binary installer to install git. For example, most instances use Ubuntu, so `sudo apt-get install git` will suffice. From there, the `git` series
of commands should be useable anywhere on the instance. Go to your desired folder and type `git clone <repo URL>` to create a copy of the repository with the simulation outputs
in your current directory. From here, use the outputs to your heart's content.

On Stampede, type `module load git` then `git clone <repo URL>` to create a copy of the entire repository in your current directory.
Ideally, you will want to move everything to your working directory since it has far more storage space than the home directory.
