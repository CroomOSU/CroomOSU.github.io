## Eric Croom’s CS 373 Weekly Write Ups

## Week 7 Write Up
The week the topic is Web Security.  Since this topic is so large this is just an introduction to the topic due to its depth and breadth.  Different threats and prevention methods are discussed along with a few labs that were presented.  There is also a warning noting that some of the techniques and processes can be considered illegal if performed on systems you don’t own or have permission to.
One other thing to note is this is a fast paced ever changing environment.  As the content is worked through it should be noted that due to updates and patches to browsers and security some content that may have worked in the past should not work now.
### Web Delivery Mechanism
Malware is largely delivered through the web.  Historically the landscape of delivery methods has changed as security becomes better and new attack vectors are exposed.  Below is a timeline of the type of delivery methods through age of internet.

![wk7a](/images/wk7a.png)

As JavaScript can be a major attack vector and the web has developed in sub a way that JavaScript is integrated into the browser from the protocol level into the UI representation there is potential for attack at any of these levels.  There are injections points from the HTTP network layer all the way up to the browser and extensions.
### User Level
#### Attacks
The majority of attacks are based around social engineering.  The concept is to get users to do something wither by tricking, lying, etc. for the purpose of benefitting the attacker.  There are various types of these attacks which could include:  phishing, SEO poisoning, Fake AV, Social Media link insertions, forum link insertion, and malvertising. 
-	Phishing:  getting users to enter their criteria for logging on by faking site UI or emails
-	SEO poisoning:  getting into the top search results so this is the first thing users click on
-	Fake AV:  software that poses as antivirus but is really malware
-	link insertions:  either in Social Media or in Forums disguising links as one thing but taking the target to another malicious site.  This can be done with kerning or other methods like url shortening.
-	Malvertising: this is the method of inserting malicious adds into ad networks that have an established reputation.  Users click on the ad thinking they are trusted ads or local content and have malicious content delivered.
#### Defenses
The following image lists out some of the different ways to defend against these attacks.  The big take away from this is that no matter how good the security can be made the best defense is an educated user.  Teaching the user not to expose their systems is the best way to ensure security on the network. 

![wk7b](/images/wk7b.png)

### Browser Level
There are many attack vectors on the browser that malicious actors can exploit.  The following is a list of potential vectors that could be used to infect a target system.
-	Browser exploits:  when there are issues with the browser itself they can be exploited to run malicious code
-	Obfuscation:  to prevent being filtered out code used the attackers can be obfuscated so that scanners don’t identify it
-	Man in the middle / man in the browser:  These are attacks where the attacker must be between the user the end point.  This can be done by hijacking the equipment along the route. MITB attacks are similar in that they are between points but use the browser as the attack vector.
-	DNS Spoofing:  Impersonating the DNS server will have the browser requested the correct site but accept a faulty one from the spoofed dns
-	Click Jacking:  This is a way that through visual elements an attacker can present malicious information hidden in legitimate information.  Layering an invisible form or link over content to be clicked and perceived as normal to the user.
-	SQL injection:  uses the sql language implementation and the lax security on the part of the developer to gain information about a target database or cause harm to the database.  If the developer does not secure the method of sql statement generations an attacker can gain a lot of information about the system or even compromise it.  One way that I prevent this type of attack is to parameterize queries.  This can remove a lot of the sql injection that is prevalent in using dynamic queries.
-	Same Origin:  this is great in concept but not useful in the modern web.  Resources are now shared and hosted all over.  Implementing same origin would prevent this and make the host provide all of the information locally. CORS needs to be setup correctly to handle data from different areas.
-	Cross Site Scripting:  XSS is when malicious data is added to a resource and is run against host.  Examples would be posting data that has a script tag in it.  This is read back to the browser by another user and the script is run.
-	Cross Site Request Forgery:  this is when the attacker uses the user’s identity (logged in user) to request or post data to other entities as that user.

While HTML5 is great for the developer and has a feature set the users want / enjoy the following two images represent the benefits HTML5 bestows on malicious actors:

![wk7c](/images/wk7c.png)

![wk7d](/images/wk7d.png)

Homework Discussion
While it wasn’t requested that we complete the homework mentioned at the end of the first series of lectures I have done this many times in the past.  After I created many CRUD applications, I would run them through security scanners to test for vulnerabilities.  At first, I would always get flagged with XSS issues.  It could be as simple as adding a script tag with an alert in it to a form field and hitting submit.  This data may be returned to the screen and executed.  I learned that I needed to do validation on the user input and escape data where it really needed to be freeform.  When data wasn’t as open and could be restricted, I would filter out malicious tags and information that was not required to be present in the form data.
### Lab 1 Attack the Web Goat
After some effort I was able to get webgoat transferred from the share.  After some set up I was able to get it running.  Trying to follow along during the lectures proved difficult.  There was suggesting that we should be following PDF’s, however, no one appears to know where these are.  Questions were raised on slack without response.  I was able to watch the demonstration of the walkthrough and found it interesting but without the proper instruction or the associated files I was unable to work through the lab.  
It feels like there are missing data / instructions / lectures that would fill in the gaps or better explain what should be accomplished here.  Overall this week has been a bit scattered and material appears to be missing.
### Web Tool Box
The last topic covered included a discussion on the various tools available to combat malware within the web space.  The following are a list of examples of these tools.
-	Alexa:  shows site popularity.  Domain based
-	Archive.org:  shows the history of site and can help determine long term changes
-	IPVOID:  checks ips against a blacklist
-	Checkshorturl:  expand shortened urls
-	Site Dossier:  general information around the site
-	Webutation:  reputation from trusted sources, AV, Google, etc
-	Web inspector:  online scanning tools similar to webutation.  Uses various classification techniques
-	Virus Total:  aggregator of information and repository of threat management 
-	Linux Tools:  JWHOIS is a domain registration data client and DIG is DNS resolver utility
Additionally, the following list are examples of client-side research tools:

![wk7e](/images/wk7e.png)


### References
The information above was obtained from the following asset.

Cochin, Cedric - Defense Against The Dark Arts


<a href="../">Back to Home</a>


