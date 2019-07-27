## Eric Croom’s CS 373 Weekly Write Ups

## Week 5 Write Up
This week we are exploring windows internals, rootkits, and memory manipulation.  The priority is to understand the how malware uses stealth by memory manipulation and the methods by which to debug and explore these stealth implementations.  Additionally, this week there were a few labs and general discussion on how windows works.
### Rootkits
Rootkits take control of a target system and are stealthily hidden.  Rootkits like to be deployed to the kernel instead of the application space since they will have much more authority.  In this space they have the ability to hide themselves by hooking apis within windows allowing them to filter or redirect system queries about their existence.
### Lab:  Agony
In this lab we are directed to use cuckoo or other tools to examine a file called Agony.  As this was meant to hide itself, we are tasked with discovering what information it left behind.
Running Cuckoo I found 3 files as shown in the image below.  Also using Tuluka I was able to identify a file I cannot see, wininit.sys.

![agony1](//images/agony1.png)

Additionally, we were tasked to investigate the three hooked locations.  Setting breakpoints on the infected locations in memory I was able to step through the code execution to determine when the code returned back to the original process.  This is illustrated in the next three images.

![agony2](//images/agony2.png)

![agony3](//images/agony3.png)

![agony4](//images/agony4.png)

The results highlighted above represent the number of bytes for the sections of malware used to hook the data.  By understanding where and how big the infectious pieces are we can use this information to apply patches that bypass the malwares effects.  Though these patches may not remove the infection they can invalidate them by fixing the table that had the api pointers changed.

### Lab 2:  Process Explorer mini clone
This lab was a description of what our homework was for this week.  This will be posted to canvas.  This section also exposed us to a new tool, Process Hacker.  This is very similar to process explorer, but with the ability to view the modules, threads, and memory of the process.  Our goal is replicate some of this functionality.  Listing processes, modules, threads and memory are part of this challenge.  
After some research I found several ways to do this in a few languages.  In python there is a module call psutils that can be used.  C# has a Process class that will do most of the work.  However, displaying the memory values does not seem to be as readily apparent in higher level languages.  I’m opting for a c++ implementation as there is documentation on different ways to do parts of this as well as c++ is better suited for this level of memory manipulation.

 ### Bootkits
Bootkits are a type of malware that is loaded into boot process.  Bootkits can be rootkits if they attempt to hide themselves but they don’t have to do this.  In the boot process there are several steps involved that can have malware loaded.  This allows the bootkit to bypass or modify the os since it hasn’t been loaded yet.  
To combat this Microsoft created secure boot.  This ensures that each step in the boot process is verified by way of digital signature.  This will prevent malware from being injected during the boot process.
### Trends in Stealth Malware
There are many methods for malware to use stealth.  The image below lists out several off the methods described this week.

![stealth](//images/stealth.png)

Stealth is what allows the rootkits to be successful and infect a system.  Without employing these avenues to avoid detection the purpose of the malware goes unfulfilled.  Security software needs to understand these methods and devise ways around the stealth to effectively highlight and disable these types of attacks.

### References
The information above was obtained from the following asset.

Kapoor, Aditya - Defense Against The Dark Arts


<a href="../">Back to Home</a>

