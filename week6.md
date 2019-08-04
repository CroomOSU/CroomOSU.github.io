## Eric Croom’s CS 373 Weekly Write Ups

## Week 6 Write Up
This week’s discussion was on network security and the threats and preventative measures associated with the network.  There were several small labs and take-home assignments discussed throughout the lectures.  The main ideas represented were detection, prevention, and the use of wireshark to analyze network traffic data.  There was some ambiguity on what was presented in the lectures and what needs to be completed as homework.  I will do my best in the discussion below to accommodate these recommendations/requirements.
### Robustness Principle and Firewall
The Robustness Principle simply states:
“Be liberal in what you accept, and conservative in what you send” 
In essence I do not agree with this principle.  This is the general interpretation that everyone on the internet is working in good faith.  This was later expanded to say:
“assume that the network is filled with malevolent entities that will send in packets designed to have the worst possible effect" (From Wikipedia:  https://en.wikipedia.org/wiki/Robustness_principle)
It is clear that being liberal in what is accepted can lead to malicious actors infiltrating systems and infecting their target systems.  Better precautions and proper updating to the implementation must be made to quarantine unexpected results rather than accept them without reservation.  The last part of the statement, however, still holds true.  Being conversation in what is sent and acting in the best faith towards the recipient will lead to better communication and cooperation between systems.

The firewall was to fill in data to a spreadsheet about zone to zone policy ideas.  I worked through some of this, however, I was unable to complete all of the items.  There was insufficient description of how this is supposed to work and it appears that these answers would be entirely conditional to the network that they reside in.  It seems that this exercies is to just make up what we thing would be the best fit without any context.  Below represents a start to identifying what the rules would be.  However, without understanding the network itself and the business requirements for how the network should perform one can only guess as to the proper implementation.

![zone](/images//zone.png)

### Network Protection Strategies
Protecting the network is just as important as protecting the end systems.  If the vulnerabilities cannot pass through the network they cannot get to the hosts.  Implementing this strategy will allow for more robust defenses. The following is a list of strategies to help protect the network:
- Positive policy – this type of strategy allows for whitelisting or allowing only certain things to gain access to the network.  This ensures that only what is permissible (defined limit) to interact with the network and the downstream hosts.
- Firewalls / Security Zones – this is another type of policy that defines the zones are allowable to accessed or interacted with.  An example consists of allowing Intranet to be completely allowable between itself while restricting certain protocols between the internet and end user.  Or determining what protocols are acceptable between different types of data centers.
- Defense in Depth – this concept represents rings of security.  Each ring consists of a different level or type of security.  If malicious actors can get past one layer there is another layer in place for defense.  As it goes deeper it becomes more difficult for an attacker to reach their end goal in the system
- Intrusion Detection – this technique uses signatures of known attacks to catch and rectify attacks.  There is a downside to this in that zero-day attacks and false positives can bypass the system.  Zero-day attacks can be unavoidable as they are unknown, however, false positives can be due to alert fatigue or improper monitoring.
- Honeynets / Intrusion Deception – here the defense is to trick or divert attackers into an area that will not affect the system waste the time of the attacker on diversions.  This can be difficult to implement as it is time consuming with setup and configuration.
- Quarantine – this concept will move suspect or malicious intent into an area where they cannot do any harm.  Blacklisting or the identification of bad actors / behavior can be utilized to implement a quarantine.
- Reputation (also host-based) – this is similar to the concept of white / black listing.  This is a method of identifying the good and the bad in all forms identifiable which is then pushed to a central source (cloud hosting) for ingestion by the network for use in defense.
The following chart represents network security technologies by Detection, Products, and Protection Methods.

![nst](/images/nst.png)

### Threats
There are many different types of threats that face networks.  In the sections that follow there is a discussion around these threats.  Additionally, there was a lab assigned in this section.  This lab was moved from a lecture lab to a homework assignment.  This will assignment that deals with scanning and understanding data packet data from csv files will be posted in separate entry.
#### Man in the Middle
This approach positions an attacker or security between the source and destination.  In terms of security this is where a proxy for web traffic would be installed.  This protects the user from malicious activity by detecting and preventing it to moved on to the user.  However, attackers can position themselves between two parties to do damage that may be undetectable.  Examples of this include ARP Poisoning and TCP Hijacking.
#### Hidden Data Transmissions
This threat is hiding data through the use of existing channels of transmission but not used in the traditional or intended way.  Hiding or injecting data into legitimate processes may allow for malicious activity to pass through the network on to the users.
#### Recon
Reconnaissance is the gathering of information about a network or target machine.  This can be done actively by scanning the target or passively by directly connecting to the network (physical connection).
#### Spoofing
Spoofing is when an attacker will change their identity within the network to overcome defenses.  Spoofing can be done to many aspects of the network and the transmissions within it.  There are however some valid use cases for spoofing such as load testing.
#### Resource Consumption Attacks
This type of threat is generally represented by a DOS (Denial of Service) or DDOS (distributed DOS) attack.  This attack will use up the resources of a target system.  In a distributed type of attack multiple hosts attack the target which allows for minimal effort on the attacker’s side and maximum impact to the attacked system.
#### Bugs and Back Doors
Both of these threats are similar in that they compromise the security of the system by allowing ways that should not be permitted.  Backdoors are put in place intentionally while bugs are accidental, but both are dangerous due to the access they can provide.
### Defense
Since all of these threats exists it is necessary to create defenses that will help protect the network and the end user.  Defenses are important as incoming threats are constantly changing, and the malware landscape changes.
#### Packet Filtering, NAT, and Proxying
Packet filtering allows the network to route out problematic packets and drop them before they can read the intended targets.  NAT or Network Address Translation hides the end ip from the outside world.  This was needed due to the relatively small number or ipv4 addresses to allow sharing among the network but turned out to be a good defensive measure.  Proxying allows for a positive man in the middle where the content coming in and going out can be monitored and dropped or redirected when needed.
#### NIPS
NIPS or Network Intrusion Prevention Systems typically used signature or anomaly-based detection strategies.  Signatures check for known patterns of attack while anomalous detection uses out of the norm patters to divert suspect traffic.  Next Gen IPS uses old implementations as well as new to protect systems.  The slide below shows information about NGIPS:

![ ngips](/images/ngips.png)

### Lab
The lab consists of three questions.  The first question is asking us to find the day and time of the meeting between the people in the tcp data.  I was able to do this by searching for the term “Betty” and following the conversation.  There was some encoded data that I decoded using the python script.  The day is Wednesday and the time is 2pm.

![ w6L1](/images/w6L1.png)

For questions 2 and 3 I was able to get the correct answers eventually but needed to search the web for assistance.  For question 2 I was stuck with finding the password.  Once found it still wouldn’t work since I had extracted the hold conversation as the truecrypt file instead of just the one that was sent.  I found the proper conversation by the same port used by both sender and receiver as was hinted at in the hints page.  Eventually, for question 3 I need to search out some resources.  I didn’t know where to start.  I found the pop3 traffic but didn’t know how to tie that to the http protocol where the payload was.  With some google assistance I was able to determine that Las Vegas was the destination and 3113 bytes of data were downloaded as malware.

### References
The information above was obtained from the following asset.

Venugopalan, Ram & Cooper, Geoffrey - Defense Against The Dark Arts


<a href="../">Back to Home</a>


