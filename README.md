# COMP3010Assign2
Github repo for COMP3010 Assignment  2 containing  a report about splunk usage


COMP 3010 Assignment  2 report 

Introduction 

An SOC (Security Operations Centre) is a department within an organisation that handles monitoring of their IT systems, and the detection and response to security incidents. This can be done with a type of software called an SIEM (Security Information and Event Management) platform that it used to investigate these incidents. 

BOTSv3 is a dataset produced by Splunk to be used with their SIEM software to train and test the skills of users. This is done with a series of guided questions that I have answered and will explain in this report. I will also cover the general roles and tiers within an SOC team in relation to the exercise, and discuss the prevention, detection, response, and recovery actions the team would take. I will also cover the process of installing Splunk and preparing the BOTSv3 dataset for use. Finally, I will cover the key lessons I learned during this assignment. 

SOC Roles and Incident Handling 

An SOC makes use of different tiers to effectively make use of the time and different levels of skills of its members. The lowest level is tier 1, usually the most junior members of the team and they would be responsible for day-to-day monitoring of systems, triage, and basic investigation of alerts and, if necessary, escalation of these alerts. Tier 2 members would take charge of the in-depth investigation of an incident, similarly my own role in this BOTSv3 exercise. They would map out a timeline of events, identify root causes such as misconfiguration of permissions, intrusion points, and impact, attempt to contain damage and recommend remediation to higher tiers. Tier 3 would handle the most complex of tasks such as digital forensics, reverse engineering malware, and creating detection and prevention methods. Tier 4, usually the final tier, is responsible for the leadership of the team such as coordinating response to attacks, holistic improvement of practices, and communication with the executive team about any incidents. They would also approve or recommend actions to be taken to recover from the incident. 

Splunk installation and data preparation 

The first stage of installing Splunk was to prepare the environment for it. The environment  i chose was Ubuntu 24.04.3 running within a VMware virtual machine and then gave it the necessary resources to run Splunk.  

For installing Splunk itself, the first step was to go to Splunk’s website and create an account, filling in all necessary fields. 
![splunk signup](https://github.com/user-attachments/assets/9ad1b2cb-52a2-42c5-87bb-b849574946fe)

After this, I navigated to the downloads page, and chose the Linux installs tag, and from there got copied the wget link for the .tgz  version. I chose this one because it includes all the necessary libraries and tools to be able to use it in the way I needed to. I then proceeded to copy that link into my terminal within Linux.
<img width="2550" height="1429" alt="wget" src="https://github.com/user-attachments/assets/f959bc72-4d13-4ffe-85c4-de3e6b8977ae" />

This command downloads the file onto my machine. 

 

The next step was to, firstly, make sure that the file was downloaded and I used the command “ls” to verify this. Having done this, the next step was to extract the file using the “sudo tar xvzf <filename> -C /opt” command. Sudo gives the user administrator privileges, needed to extract into “/opt”, tar is used to create or extract “.tar” archives. The line “xvzf” gives the commands on how to extract the file and tells the machine to decompress, extract, show the filename, from the filename in the argument. The “-C /opt” section tells the machine the to extract the file in the –C directory, in the folder /opt. It then asks for my password as it is needed to grant administrator privileges. 

 <img width="2545" height="1425" alt="sudo tar" src="https://github.com/user-attachments/assets/0e4eabd8-9382-40c1-8690-1da9cdf5659d" />


 

 

 

 

 

 

 

 

 

The next step is to navigate into my desired  filepath  to start Splunk, and I do this by running the command “cd /opt/splunk/bin”. Now that I am there, I use the command “sudo  ./splunk start --accept-license" to start the program, and accept the license agreement. After this, i then have to input a username and password to use Splunk.  
<img width="2552" height="1431" alt="splunk start" src="https://github.com/user-attachments/assets/d481ea97-d748-4c76-8010-fb41578fe1d0" />

Following this, i am given the link for the splunk web interface. I simply open this link in the browser, and then the splunk web application opens and I am prompted to enter the username and password that I created earlier. 

 <img width="2550" height="1429" alt="splunk  login" src="https://github.com/user-attachments/assets/42f8e23b-197d-4736-bcdb-9a8e8f184bc5" />


I then enter the username and password, click login and am then greeted with the Splunk homepage. 
<img width="2543" height="1424" alt="splunk  gome" src="https://github.com/user-attachments/assets/03d4614c-27ee-4f69-ba2a-5ecc76177cc4" />

Now that the splunk installation process is complete, I now need to load Botsv3. First, I go to the Boss of the SOC GitHub and download the dataset 
<img width="2543" height="1424" alt="botsv3 github" src="https://github.com/user-attachments/assets/f28ed8af-d3a6-4914-a03b-1af821c63213" />

After this I then open my downloads folder and extract the file, making sure that all the components of the file are as expected.
<img width="2552" height="1431" alt="bbotsv3 file" src="https://github.com/user-attachments/assets/6733d94b-0415-4286-93b2-02fcf0eb90f6" />

After this, I reopen my terminal into a new instance. I then do “sudo su” for root access, open the downloads folder with “cd Downloads” and do  “ls” to check what is there. Following this i run cp –r botsv3_data_set /opt/splunk/etc/apps”. This command recursively copies the dataset into the following filepath so that it can be used by Splunk. After this i  check that everything is in the files as it should be, i then navigate back through the filepath  to get to the bin section of splunk and run ./splunk  start. 
<img width="2554" height="1431" alt="botsv3  opened" src="https://github.com/user-attachments/assets/85a86bb3-9bac-4c81-9eda-302301a69f99" />
<img width="2549" height="1429" alt="splunksatrt2" src="https://github.com/user-attachments/assets/fb732a80-1720-4de3-9795-cb2f37548b7d" />

I then open the link given and sign in same as earlier, and  i am greeted by the dataset in splunk after searching the botsv3 index. 
 <img width="2553" height="1432" alt="botsv3 splunk" src="https://github.com/user-attachments/assets/b762c6d8-7e7f-48e7-88dd-cc2ae4f0c91e" />


 
