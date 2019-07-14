## Eric Croom’s CS 373 Weekly Write Ups

## Week 3 Write Up
Week 3 is our introduction to Malware Defense.  The series of lectures details some of the modus operandi of the malware methods of defense.  This week a hands-on discussion was held for the tools introduced.  Yara was explained and Cuckoo was also introduced.  Labs to show usage of these tools were also accomplished.  I was able to follow along with these labs and have documented that below.

### Malware Defense
To be able to defend against malware we must understand the methods by which it will attack a user.  The presenter demonstrated this with an attack graph (displayed below) and walked through the descriptions of the four sections within the graph.

![Attack Graph](/images/attack.png)

1. First Contact
This is the method by which the attackers will gain access to the targets.  There can be many methods by which the attacker can attempt to infiltrate the target system.  The targets can be addressed directly through email or instant messaging.  More indirect methods could be from Malvertising, poisoned search results, and watering hole pollution.  The last aspect that can be overlooked is physical access.  
2. Local Execution
Local Execution refers to how the malicious software gets executed on the target system.  There are several methods to accomplish this.  The attacker could employ social engineering to entice users to execute their code.  Exploitation of software problem in pdf, java, scripting can be used.  Also, the attacker could use features built into operating systems to ensure execution, like autorun.  The end goal of this execution is to “harvest data”.
3. Establish Presence
Generally, malware will either try to hide itself like in a bootkit or rootkit, or blend in.  To blend in malware can change its file name to be more like the operating system (svchest as we saw in previous weeks), have a valid signature, or modify file properties.  
Malware must also persist in the system.  After a reboot the malware needs to become active again.  There are several locations throughout windows where this can happen.  This persistence could be representative in a file, but also hidden in places that are generally not targeted by file threat detection systems.  One example would be a script located in the registry.  In the image below we can see the various places that malware can persist.

![Persistence](/images/persist.png)

4. Malicious Activity
The activity itself is anything that the malware uses to manipulate the target.  This would be data gathering, ransomware, or any other method of disruption to the target.

#### Defenses
The defense against malware is multi layered.  If we can prevent malware at the various levels attack vectors we will have better coverage and make it less likely that malware can take hold of the system.  The image below shows the layers as well as technologies associated to the layers.

![Defense layers](/images/layers.png)

The lecturer listed several methods of defense that are used within the layers to defend against malware.  While there was a lot of McAfee specific names thrown around there was a good generic list provided of the types of features anti-malware would contain:

![Anti malware](/images/anti.png)

### Yara
Yara is a language that allows for pattern matching with specific rules.  This is used by malware researchers.  Since some vendors are closed people needed a better way to determine if threats were present on their machines.  When a researcher needs to define rules for searching within files or memory yara is the tool to use when you don’t have access to a scan engine.
#### Lab 1
The purpose of this lab was to get us used to using yara rules.  We were given a sample folder that had some potential malware in it.  I examined each file with fileinsight to try to find a common string(s).  Upon inspection I found that the following was the most promising:

![packedV](/images/jampack.png)

This appears to be a packed version of a longer string.  After further inspection of the remaining files I found a more robust string.

![unpackedV](/images/jamunpack.png)

Using the yara editor I was able to create a yara rule that will cover the files in the sample and not pull false positives off of the system files.

![yara1](/images/yara1.png)

![yara2](/images/yara2.png)

![ yaraSYSRun](/images/yaraSYSRun.png)

#### Lab 2
This is a continuation of the previous lab.  Here we are to look at the other two sample groups and provide yara rules for these as well.
Group 2:  Working through these sample there are a lot of commonality as these are html files.  One thing that stood out was the javascript to basically inject new html that is to be decoded.

![ decode](/images/decode.png)

In this I noticed an Active X control, however, here is where I got stumped.  After watching more of the video I am beginning to understand the logic of what was being done.  I was not familiar with these controls before nor that they had class id’s associated with them.  The lecture shows the completed yara signature which has the class id spelled out in hex.  I had the first part but that is apparently too broad.  The second part took some more understanding of the proposed exploit to further complete the signature.

![ lab 2 yara](/images/lab2yara.png)

Group 3:  This one I had a bit more trouble working out.  I was using fileinsight to try to find some interesting strings to use to generate my rules however when compared to the lecture I’m not finding these strings when extracting from the files.  I understand the explanation and rational behind the lecture, but I am not sure how they got to the point of where they were choosing the strings.  Perhaps I missed something but it seems like this part was glossed over.  Either way the image below shows the final form of the rule from the lecture.

![ lab 3 yara](/images/yara3.png)

### Cuckoo
Cuckoo is an automated analysis system that will run vms with malware and report back the status.	
For the last lab for this week we are to use Cuckoo to determine if a threat exists and analyze with the tools as appropriate and provide a generic yara signature.
Lab:  Sample 2 chosen

![ week 3 last lab 1](/images/w3_lastLab_1.png)

I began by running the file through Cuckoo to extract the logs about what the process was doing.  I found that it created three files qusla.exe, text.txt, and dx.bat.  Along with these files there appears to be some registry manipulation along with the manipulation of internet explorer.

![ week 3 last lab 2](/images/w3_lastLab_2.png)

At this point I thought it might be appropriate to investigate the strings in the file itself to see if anything really stands out to me.  After extraction of the strings I found the references to internet explorer and a CurrentVersion\Run reg key.  IE is now on the desktop and the reg key that was changed references aimsn with a value of c:\qusla.exe.  

![ week 3 last lab 3](/images/w3_lastLab_3.png)

Scrolling down the list of strings I noticed something interesting.

![ week 3 last lab 4](/images/w3_lastLab_4.png)

There might an internal name listed within the file.  So here I ran strings all which will pull them all in order and found the internal name of hau.

![ week 3 last lab 5](/images/w3_lastLab_5.png)

So the yara signature I would suggest for this file would be oring the current file name with the internal  file name:

![ week 3 last lab 6](/images/w3_lastLab_6.png)

### References
The information above was obtained from the following asset.

Schmugar, Craig - Defense Against The Dark Arts


<a href="../">Back to Home</a>

