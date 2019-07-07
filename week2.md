## Eric Croom’s CS 373 Weekly Write Ups

## Week 2 Write Up
This week we explored more Advanced Forensics and additional tooling used to investigate a subjects system for information.  The main focus was on understanding what forensics is and how to access the data on a system for investigation without modifying the data.  Additionally, there were several labs to follow along with during the lectures and a challenge provided at the end.

### Forensics
The discussion revolved around three key aspects of forensics:  Evidence acquisition, Investigation and analysis, and Reporting results.  From the lecture Forensics is “the process of unearthing data of probative value from information systems”.
- Evidence Acquisition:  Evidence or data obtained from a target system or systems is used to identify facts of the incident and prove or disprove those facts/assumptions.  This data can be wide ranging and obtain from of a variety of sources throughout the target system.
- Investigation and Analysis:  Once the evidence has been captured the investigation is performed.  Data integrity must be maintained to support any conclusions being drawn from the analysis.  The various tools and processes described over the past 2 weeks of lectures allow for this investigation to take place.
- Reporting Results:  Throughout the whole process the security analyst must be taking notes on their process and procedures to ensure validity of the process.  If issues arise where data is missing/invalid it must be noted in the report so that the proper authorities are aware of these issues and do not call into question the remaining conclusions.

The next topic to be discussed revolved around Locard’s Exchange Prinicple and volatility.  This principle states that when objects come in contact with each other material is transferred.  In relation to the topic of forensics this is a good concept to keep in mind as we attempt to gather data on a system while not affecting its contents.

Interacting with a live system can be delicate as we do not want to lose power.  This can cause volatile resources to be lost and not be recovered in the investigation.  In the evidence acquisition phase, any relevant data that is the most volatile should be collected first before it is lost.  From the lecture the listing below represents volatile sources from most to least.
![Volatility List](/images/volList.png)

### Tools and Labs
Throughout the lectures the labs consisted of demonstrations of new tools and what they are able to do.  Following along I was able to replicate what was demonstrated.  
**FTK Imager**
This tool is very useful for creating and analyzing images of a drive or disk.  Using this tool you can also investigate the contents of the data.  In the image below you can see that I was able to recreate the process from the Lab to load my current disk and examine files.  I did not create a new image of the disk for this exercise.
![FTK Imager](/images/ftk.png)

**Volatility **
Following along with the lectures for this lab I was able to demonstrate how I was able to extract information from a memory dump using the volatility tool.  The images below are me working through the lab to identify the different data contained in the memory dump.
![Volatility 1](/images/vol1.png)

![Volatility 2](/images/vol2.png)
![Volatility 3](/images/vol3.png)
![Volatility 4](/images/vol4.png)
Volatility has many different plugins that can be used to investigate the data.  One example is timeliner.  This can create a timeline view of the processes captured in the memory dump.

**Yara**
Yara was mentioned briefly in the lectures and can be used in conjunction with volatility.  It has rules and signatures associated with malware that can be used to identify infection of a suspect system.

**Recovering Data with OSFMount and PhotoRec**
OSFMount allows us to mount an image so that it is then accessible to the file system.  From here we can run photorec on the image to restore deleted files.  Below is an image that contains the recovered files, command line window for using photorec and the mounting of the disk.
![Carving Data](/images/carve.png)

**Challenge**
The last part of this series of lectures was a challenge to extract data out of an image of a usb stick.  Here we are looking for targets, malware, username/passwords, and deleted files.  From the results discovered we are asked on how we would advise the targets.  I took the hints provided by the lecture and got to work dissecting the image.
First I mounted the file:
![Challenge 1](/images/challenge1.png)
From here I was able to see the files on the image.
![Challenge 2](/images/challenge2.png)
I recovered data from the image that was deleted.
![Challenge 3](/images/challenge3.png)
Based off of the hints I investigated the files on the image with file insite and found a password using the strings function.
![Challenge 4](/images/challenge4.png)
Applying this password to the zipped file I was able to determine the targets in the csv
![Challenge 5](/images/challenge5.png)
Looking at the other files present it appears to be a root kit intended for the target.

I would contact the targets and advise them that their systems may be compromised from this attack.


### References
The information above was obtained from the following asset.

Beek, Christiaan Defense Against The Dark Arts


<a href="../">Back to Home</a>


