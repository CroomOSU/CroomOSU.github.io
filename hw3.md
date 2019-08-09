## Eric Croom’s CS 373 Weekly Write Ups: Homework Edition

## Homework #3
The assignement was to analyze traffic for different patterns within a network.  The data is simulated in csv files with R being a smaller sample set than O.  Additionally, we were given two starter scripts to begin working with.  I chose the python script and modified based on details below.
The main function has been updated (or created since there was no main function) to allow the acceptance of different flags
![hw3s](/images/hw3.png)
 1. Extend your script’s statistics gathering to count the use of all well-known destination port numbers for TCP and UDP (ports 1-1024).  For example, you should be able to look up in your output how many TCP packets have destination port 80 and how many UDP packets have destination port 53.  Run your new script on R and O data.  Enable this function using a ‘-stats’
In the images below you can see how the output differs when using the -stats flag and how the results are different from O and R files.

![hw3a](/images/hw3a.png)

![hw3b](/images/hw3b.png)

![hw3c](/images/hw3c.png)

 2. Based on this information, characterize the main functions on each network.  What kind of a network is it? (e.g., work, home, data center, ISP).  
These are difficult to classify as there is limited information.  Both has http and SMB traiffic with O.csv having some more smtp data.  These could be home, work, anything at this point.
 3. Add to your script an option called “-countip” which creates list of distinct IP addresses with their usage counts.  Sort the list by the usage count, not by the IP address.

![hw3d](/images/hw3d.png)

 4. Run your countip script on R and O data.  Does this inform your answer in [2]?
I’m seeing a lot of hosts within each network.  This leads me to believe that it may not be a home network.  While still possible I would think this is more of a small business.

![hw3e](/images/hw3e.png)

![hw3f](/images/hw3f.png)

 5. Attempt to determine the network number (network prefix) that seems to dominate the traffic.
The main prefixes are 10 for R and 192 for O.  This shows that most of the traffic is internal to the network and that there are a multitude of hosts presiding on each network.
 6. Generate sorted output from ‘-countip’ for the IP protocols to identify all the IP addresses that use:
a.	47 GRE (Generic Routing Encapsulation) – this is used to create tunnels between networks with overlapping address spaces.  It is also the base protocol for PPTP, a remote access mechanism.
b.	50 51 IPSEC – this is the protocol that creates virtual private networks, creating an overlay network structure on top of the Internet.  Most IPSEC is router-router these days.
c.	89 OSPF – Open Shortest Path First routing protocol.  This is the ‘standard’ routing protocol for Internet routers, allowing them to discover the topology and choose the best routing paths as connections between routers appear and disappear.
R does not have any of these protocols:

![hw3g](/images/hw3g.png)

Here is the result from O:

![hw3h](/images/hw3h.png)

 7. Find another network prefix that also seems to be associated with this traffic.
207.182.35 appears to dominate this type of traffic.  This is a company called Opus One.
 8. Does the OSPF information inform your answer to question 2?
This looks to be a networking company or that the traffic is routed through opus 1 which is then using the OSPF protocol
 9. Add an option to your script ‘-connto’, which counts the number of packets sent to each service (ports 1-1024) on the network.  For example, a dictionary maps each ipdst to the tuple <proto, dport>, where proto is tcp or udp, based on the IP protocol (6  or 17) and dport is the value of tcpdport or udpdport.
•	Sort the output by the number of distinct source IP address – source port combinations, so that servers which serve a lot of different connections all cluster at one end of the output.  
•	For output, generate a summary line that shows, for each destination IP address, how many distinct source IP addresses accessed it, and what ports were referenced:
ipdst 1.2.3.4 has 334 distinct ipsrc on ports: udp/53, tcp/80, tcp/443
ipdst 5.6.7.8 has 335 distinct ipsrc on ports: tcp/22, tcp/25
…

![hw3i](/images/hw3i.png)


 10. Run your -connto option on R and O data  (ignore anything that ends in .255 – this is a broadcast address).   Does this suggest a set of servers to you?
d.	Return the top 20 servers from your ‘connto’ output.
e.	For the R data, identify the web servers, the printers, the mail servers, the DNS servers
f.	For the O data, identify the mail servers, the pop/imap servers, the DNS servers

![hw3j](/images/hw3j.png)

![hw3k](/images/hw3k.png)

For the R data the 2 ips with the most source ports are 10.5.63.6 and 10.5.63.7.  6 appears to be a mailsever based on the ports and 7 looks like a webserver.  There are others list that have lower traffic that are utilizing dns and http ports, however, 6 and 7 represent the majority of the sources.

For O data the majority of the des tips are utilizing ports 22 and 25 which represent ssh and smtp.  There are some that have http identified and DNS but the majority are dealing with SMTP.

 11. Update your answer from [5] based on this information.
Based on the data represented in the findings it looks like R data might just be a small office or large home network.  O data is different since it has so many SMTP servers this may be a corporate data center or a small mail service.

<a href="../">Back to Home</a>




