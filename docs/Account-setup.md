#Setting up your Accounts

Before you can get started analyzing your GWAS tools, you will need to set up a few accounts to get access to all the necessary platforms. These accounts, tools, and functions will be explained in more detail later on. For now it is important that the accounts be setup that way you can access the features we talk about later on. 

First, and most importantly, you will need an iPlant Collaborative account which can be obtained [here.](https://user.iplantcollaborative.org/register/) Please note that iPlant account creation requires some kind of affiliation with a university or company to be completed.

Now that you have created an iPlant account, you have access to both the Data Store and the Discovery Environment! As the name implies, the Data Store is the recommended place to hold most of your data, as each personal folder can hold up to 100 GB by default. If you need more space, you may fill out [this form](http://www.iplantcollaborative.org/content/request-data-store-allocation-increase) to get a personal folder increase of up to 1 TB. From here, you will want to request access to the Atmosphere cloud computing services. To do so, simply email support@iplantcollaborative.org.

To use the Validate Workflow on Stampede, you will need a few more accounts. First, set up an account with the Texas Advanced Computing Center (TACC) [through this page.](https://portal.tacc.utexas.edu/account-request) Like the iPlant account, TACC requires an institution to be named that you are affiliated with. Beyond that, the registration requires the usual information along with an email address. Also, unless you are a professor or in charge of a collaborative project at your company/institution, simply list the PI option near the end of the application as *Ineligible.*

Next, set up an account with the Extreme Science and Engineering Discovery Environment (XSEDE) [through this page.](https://portal.xsede.org/?p_p_id=58&p_p_lifecycle=0&p_p_state=maximized&p_p_mode=view&saveLastPath=0&_58_struts_action=%2Flogin%2Fcreate_account) The only difference among XSEDE account creation and the previous two accounts is that XSEDE does require a .edu address for proper registration. 

Finally, to get access to the Agave API, you must request access to the "iPlant-Collabs" project (this allows you a certain allocation of nodes on Stampede as well). To request access, send a message to support@iplantcollaborative.org. Getting access may take a day or two, but you will know for sure upon trying out Stampede for yourself. **Note that you will not immediately receive a notification upon getting access. The only way to know for sure is to try it out!**

#Accessing Stampede
To access Stampede, you may use a number of different SSH clients, depending on your operating system:

###For Windows:
* [PuTTY:](http://www.putty.org/) a no-frills Unix-esque SSH client
* [WinSCP:](http://winscp.net/eng/index.php) A more user-friendly interface similar to Windows Explorer. Allows integration with PuTTY and drag-and-drop transfer of files from local drive to remote computer.

###For Mac:
* Terminal: Pre-installed command line interface that can be used to access Stampede and other remote computers.
* [Cyberduck](https://cyberduck.io/)

###For Unix/Linux:
* Terminal: The standard Unix terminal may be used to access Stampede through the *ssh* command.
