> Estimated time to complete this tutorial is ~1 hours

> Prior knowledge needed - Basic computer usage

> Tools needed - Computer, internet access, some accounts may require a institutional email

#Setting up your Accounts

Before you can get started analyzing your [GWAS tools](https://en.wikipedia.org/wiki/Genome-wide_association_study), you will need to set up a few accounts to get access to all the necessary platforms. These accounts, tools, and functions will be explained in more detail later on. For now it is important that the accounts be setup that way you can access the features we talk about later on. 

First, and most importantly, you will need an CyVerse account which can be obtained [here.](https://user.cyverse.org/register/) Please note that the CyVerse account creation requires some kind of affiliation with a university or company to be completed.

Now that you have created an CyVerse account, you have access to both the Data Store and the Discovery Environment! As the name implies, the Data Store is the recommended place to hold most of your data, as each personal folder can hold up to 100 GB by default. If you need more space, you may fill out [this form](http://www.cyverse.org/content/increase-your-data-store-allocation) To get a personal folder increase of up to 1 TB. 

From here, you will want to request access to the Atmosphere cloud computing services. To do so, simply email support@CyVerse.org. Somethiong along the lines of "I would like access to atmosphere for [your login]" should do just fine.

To use the Validate Workflow on Stampede, you will need a few more accounts. First, set up an account with the Texas Advanced Computing Center (TACC) [through this page.](https://portal.tacc.utexas.edu/account-request) Like the CyVerse account, TACC requires an institution to be named that you are affiliated with. Beyond that, the registration requires the usual information along with an email address. Also, unless you are a professor or in charge of a collaborative project at your company/institution, simply list the PI option near the end of the application as *Ineligible.* If you are a staff member at CyVerse, or need shell access to stampede, send a message to support@CyVerse.org to request access to the "CyVerse" allocation. Getting access may take a day or two, but you will know for sure upon trying out Stampede for yourself. **Note that you will not immediately receive a notification upon getting access. The only way to know for sure is to try it out!**

Next, set up an account with the Extreme Science and Engineering Discovery Environment (XSEDE) [through this page.](https://portal.xsede.org/?p_p_id=58&p_p_lifecycle=0&p_p_state=maximized&p_p_mode=view&saveLastPath=0&_58_struts_action=%2Flogin%2Fcreate_account) The only difference among XSEDE account creation and the previous two accounts is that XSEDE does require a .edu address for proper registration. 

Finally, request an [allocation from XSEDE.](https://www.xsede.org/allocations) This allocation will give you access to the actual compute resources on [Stampede](https://portal.xsede.org/tacc-stampede) and give the Stampede system to "bill" you, so to speak, for any jobs run on said system. For example, staff at CyVerse have access to the "CyVerse" project. To request a standard XSEDE allocation, follow [the step-by-step instructions found here.](https://web.archive.org/web/20160409190018/https://portal.xsede.org/allocation-request-steps) **Note this may not be necessary in most cases, however, it is worth doing if you are planning to do intensive app creation/design.**

<a name="Windows">
###Note to access Agave or Stampede you will need a terminal which can pose a problem if you are running a Windows operating system
To solve this problem you should follow the tutorials for accessing a virtual machine we have setup for the validate workflow i.e. an [atmosphere image](Validate on Atmosphere.md) which will grant you access to a terminal and allow you to follow along with these tutorials for the validate workflow.</a>


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

[Back to Read Me](../README.md) | [Next: Accessing Atmosphere](Validate on Atmosphere.md)
