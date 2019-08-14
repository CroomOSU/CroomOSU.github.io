## Eric Croom’s CS 373 Weekly Write Ups

## Week 8 Write Up
This week is all about messaging security.  Email is major part of the internet and securing it is as important as any other aspect of a network or system.  These lectures dive into all aspects of messaging security, discussing the terminology, technology, tools, and techniques involved.  There is also discussion on social engineering and data manipulation.  
I have one note on the labs discussed during this weeks lectures.  There appears to be data missing or instructions that were not given.  In the first set of videos there are slides that indicate a lab was discussed as well as the end of the lecture stating it was about to be discussed but this information is missing.  Additionally, the classification lab at the end of the second lecture did not provide any instructions what we were to do.  Through some trial and error I was able to access the data base through the command line interface for postgres, however, clear direction or documentation was lacking for what to do or how to proceed.
### Messaging Security
There are various terms that are used throughout the discussion on messaging security in the industry.  The following image gives a list general terms associated with this topic.

![wk8a](/images/wk8a.png)

While all of these are important the main concept is the difference between spam and ham.  Ham is the representation of good email while spam is bad or unwanted email.  Know the difference between the two is the goal of messaging security.
There are two main technology vectors that deal with message security, reputation engines and content engines.  Reputation engines based off of ip addresses, urls, and potentially the message itself.  This is contrast to content engines which rely on the content of the message and pattern matching to help clarify the difference between a spam and ham message.
While the number of potential tools that could be used for these endeavors is abundant the image below indicates some of the major ones in use for spam identification.  Note that while databases are listed as a tool this is very generic.  I would say that they ways in which databases are used, storing the data, and the methodologies involved are the real tools.

![wk8b](/images/wk8b.png)

The methodology around what is described as research techniques are fairly common when dealing with data classification.  Grouping, parsing, aggregation, and outlier identification are standard practice when trying to evaluate data sets.  All of these techniques are invaluable when combing through large amounts of data to understand patterns and extract tokens to represent potential positive hits for spam messages.
As discussed, the methods around data examination are consistent with data discovery in general.  Having a good understanding of SQL and data manipulation is key to understanding spam and classifying it as such and allowing ham to be processed and pushed through to the client.  One of the important points made during this discussion was around the “data scientific method”.  This image below details this concept and as a data analyst / ETL technician / or any of the other titles I have worked under I can attest that these are invaluable in understanding and processing data.

![wk8c](/images/wk8c.png)

Another relevant area to understand when evaluating messages for security is the header data for the emails.  Within the data section from addresses and other data can be spoofed.  While not explicitly stated this can be very useful when sending email from systems and wanting the data to be directed to specific return address.  Even through SMTP is not designed to be secure some of the flaws do have real world benefits.  By using header data as seen below an analyst can trace back the information regarding the handoffs and history of the message to help determine legitimacy.

![wk8d](/images/wk8d.png)

### References
The information above was obtained from the following asset.

Peterson, Eric - Defense Against The Dark Arts

<a href="../">Back to Home</a>
