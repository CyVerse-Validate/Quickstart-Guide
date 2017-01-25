#Validate on Atmosphere

##Atmosphere Basics
For a brief tour and overview of Atmosphere, you can watch [this series](https://www.youtube.com/watch?v=8SCE1Vpm9CI&list=PL-0S9LiUi0vhXEADveTYEoKb8ua1aYIby) of YouTube videos (roughly ten minutes of total watch time). Afterwards, or in lieu of, there is also a well written quickstart guide available on the CyVerse website, found [here.](http://www.cyverse.org/atmosphere)

##Terminal Basics
If you are using Atmosphere to access the Validate Workflow you will need to have a basic knowledge 
of the Linux terminal commands. To familiarize yourself with these commands or refresh your knowledge, please consult either of the following links:
  - [This tutorial](http://swcarpentry.github.io/shell-novice/) gives a brief, but comprehensive overview of the Unix Shell. Each lesson in the tutorial has an approximate read length, and the entirety should take roughly an hour and a half.
  - [This cheat sheet](http://linoxide.com/guide/linux-cheat-sheet.png) provides a thorough breakdown of common Linux commands, detailing the command, parameters, and descriptions. 

##VNC Remote Access
Finally, to remotely access individual instances, you will need to download [VNC Viewer software](http://www.realvnc.com/download/viewer/), a secure remote access program. Simply choose the option that matches your operating system, and follow the on-screen instructions.

##Accessing Atmosphere
To access our Atmosphere image, follow the steps below:
  - Click the link [here](https://atmo.cyverse.org/application/images/1194) for a direct link to the image. Alternatively:
    - Login to [Atmosphere](https://atmo.cyverse.org/application/images)
    - Enter "Validate 0.9" in the search box under "Image Search"
  - Click launch. It will take a moment to setup and will eventually say ready.
  - When ready enter the IP address into VNC (or your SSH emulator of choice) followed by a ":1" 
      - For example: "123.456.78.910:1"
  - Click connect and you will be prompted for your CyVerse username and password.
  - Once logged in you will have access to a terminal and a virtual machine with all the software for the Valide project installed.

[Back to Read Me](../README.md) | [Next: Accessing Stampede](Stampede-guide.md)
