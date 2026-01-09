# COMP3010Assign2
Github repo for COMP3010 Assignment  2 containing  a report about splunk usage

YouTube link: https://youtu.be/LD2ObrhfA5M 

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

 Guided Questions 

Q1: List IAM users accessing the AWS service 

A:  the users of the AWS service were bstoll,  btun, splunk_access, and web_admin. I found this out by querying the dataset with “index=botsv3 earliest=0 sourcetype=asw:cloudtrail  | stats count by userIdentity.userName. I then switched the presentation to verbose mode and clicked on the statistics tab, which gave me this: 

In an SOC context, this is one of the first investigative actions that would be taken by a level 1 member of the team, after finding out what the issue was, in this case, a public s3 bucket on the AWS service. This allows for more focused investigation. 
<img width="2552" height="1431" alt="q1" src="https://github.com/user-attachments/assets/d97cd4df-f21d-43a4-ba4c-2bf732660679" />

 

Q2: What field would you use to alert you that the service has been used without MFA? 

A: the field that you should use is index=”botsv3 “earliest=o sourcetype=aws:cloudtrail userIdentity.sessionContext.attributes.mfaAuthenticated=*false*. This gives you all cloudtrail entries where a user's session has been started without MFA authentication. 

In an SOC context, this would be used after finding out which users have used the service, to further narrow the scope of the investigation, and find out which user could have caused the problem    

 <img width="2553" height="1434" alt="q2" src="https://github.com/user-attachments/assets/bef426a4-74df-48c8-a440-5fb75d70feac" />


 
 

 

l 

Q3: What is the model of processor used on the webserver? 

A: the processor used is the Intel Xeon E5-2676. I found this by using the query index=botsv3 earliest=0 sourcetype=”hardware”. This query displays all the hardware information that has been gathered about connected devices. The only entries displayed were of the webserver. This could be useful in an SOC context because any information could be useful in an investigation. 

<img width="2553" height="1436" alt="q3" src="https://github.com/user-attachments/assets/10e2289d-1bc6-4993-860e-6497c75a693a" />


Q4: What is the event ID of the API call that made the s3 bucket publicly accessible? 

A: the event ID is ab45689d-69cd-41e7-8705-5350402cf7ac.  i  found this by using the query index=botsv3 earlies=0  sourcetype=aws:cloudtrail PutBucketAcl. This query searches for changes to the access control list (ACL) of the s3 bucket. I then looked through the permissions grantees until I found the grantee http[...]groups/global/Allusers (i.e. public).  This is useful in an SOC context because it essentially serves as the start of the timeline of the incident and allows you to identify the user who erroneously (or maliciously) assigned the permissions. 

<img width="2549" height="1432" alt="q4" src="https://github.com/user-attachments/assets/b181cec9-8c57-43e6-8e48-d7636132c517" />


Q5: What is the username of the user who assigned the bucket to be publicly accessible? 

A: Their username is bstoll. I found this by expanding some more of the information fields of the mistaken permissions grant, where it shows the details of the owner, in this case, bstoll. This is useful for an SOC because it will allow them to contact the person that made this mistake and give them extra training or take punitive action. If this came from an external actor, it would allow the team to take actions to remove their access to the systems. 

<img width="2549" height="1434" alt="q5" src="https://github.com/user-attachments/assets/f634ae21-8d08-4192-a2fe-e759f7b616ff" />

Q6: what is the name of the s3 bucket that was made public? 

A: the bucket that was made public was “frothlywebcode”.  This was found from the same entry as the previous 2 questions, but expanding a different field, namely requestParameters, which contains the bucketName field. This is useful to an SOC team because it allows them to triage the damage done by correcting the access policy, and investigating that bucket further to evaluate damage.  

<img width="2554" height="1434" alt="q6" src="https://github.com/user-attachments/assets/345e39cb-1344-4f49-bccd-9c0626b29f7d" />

Q7: What is the name of the text file that was uploaded to the S3 bucket while it was publicly available? 

The name of the file was OPEN_BUCKET_PLEASE_FIX.txt. I found this file by querying “index=botsv3 earliest=0 sourcetype=”aws:s3:accesslogs txt”. This showed   an entry for a HTTP GET request containing the .txt file on the S3 bucket. This is useful because it shows the SOC team what was uploaded to the bucket in this time and that   they need to remove and assess this. This would be done by a higher tier member of the team.  

 

 <img width="2556" height="1434" alt="q7" src="https://github.com/user-attachments/assets/629cf6a0-203b-4c1c-8e42-4bb18f46ecb8" />


Q8: What is the FQDN of the endpoint that is running a different edition of Windows OS? 

A:  I found that the FQDN was BSTOLL-L.froth.ly. I did this by first finding out what the different version of windows was by running the query “index=botsv3 earliest=0 sourcetype=winhostmon | stats count by OS”. This shows me the number of entries by different OS versions, of which the only different one was Windows 10 Enterprise 

<img width="2547" height="1428" alt="q8-1" src="https://github.com/user-attachments/assets/6bdfad5f-b1f1-4baf-bac0-6336b0424c7e" />

I then viewed other events by this device a found that the host was BSTOLL-L 

<img width="2548" height="1433" alt="q8-2" src="https://github.com/user-attachments/assets/027c9c90-96d7-427a-b438-694ac63521ac" />

I then used the query “index=botsv3 earliest=0 sourcetype=aws:cloudtrail | stats count by host” to find the host of the server, which turned out to be “splunk.froth.ly” but we can remove the “splunk”.  
<img width="2553" height="1434" alt="q8-3" src="https://github.com/user-attachments/assets/aa497539-f9ab-43fb-b11f-28939bb4f0f0" />

From here, we can infer that the FQDN of this webserver being run by BSTOLL-l was BSTOLL-l.froth.ly. 

Conclusions 

My findings from this investigation are that there were 4 IAM users within the dataset. API calls had been made without MFA, an S3 bucket was misconfigured, making it public by the user bstoll. There was also a .txt file uploaded to this bucket while it was public. It would also be useful for there to be an automatic alerts system that notifies the team when there is a possible error made, such as setting the S3 bucket to public. This would make response times to these events much quicker and limit any damage that could be done as a result. 

The general lessons learned from this investigation were that MFA needs to be more rigorously enforced, as admin accounts granting permissions should always have this. Additionally, SIEM tools like this are an incredibly powerful and useful part of an SOC’s toolkit for investigation and monitoring networks for suspicious activity. I also learned several personal lessons from this investigation, such as how useful these tools are and what is within their scope. I have also made great strides in their actual use.    



 
