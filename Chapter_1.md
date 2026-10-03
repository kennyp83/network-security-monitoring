# **Chapter 1: Network Security Monitoring Rationale**

  *Objective*: This chapter is meant to introduce NSM and tell the reader why it matters.
  
## **Definitions from this chapter** 

 >*Network Security Monitoring(NSM)*
 
 The collection, analysis and escalation of intrusions on a network. NSM is a method of network security. Basically a way to find intruders and do something about them. NSM does *not* involve preventing intrusions. When a network is compromised, the intruders "rarely execute their entire mission in the course of a few minutes". NSM gives you the opportunity to "detect, respond to, and contain intruders".

>*Computer Incident Response Teams (CIRT)*

CIRT can be an individuals or a team of individuals. These are the people who counter digital threats for organizations.

>*Continuous monitoring(CM)*

Continuous monitoring is another method of network security. "A CM operation strives to find an organization's computers, identify vulnerabilities and if possible, patch those holes". This is different than NSM, Cm looks for vulnerabilities in the system. NSM is looking for adversaries in the system and wants to contain them before they do anything harm.

*More on continuous monitoring*: [link]https://www.nist.gov/publications/search?k=Continuously+Monitoring+&t=&a=&ps=All&n=&d%5Bmin%5D=&d%5Bmax%5D=

---
 ### A note on how NSM compares to other approaches
Firewalls, antivirus, whitelisting, data leakage systems and digital rights management work by stopping intruders, often without the need for human intervention beyond setup. NSM works differently, it focuses on visibility, finding when the network is compromised and stopping them "before the intruder accomplishes his mission". This is more successful in cases where threats are trying to undetected remain in a system

## NSM's collected Data.
>Below are the seven types of data collected by a CIRT professionals using NSM. 

### full content data
- An *unfiltered* log of all information crossing a network. CIRTs usually review this data in two parts. Part one is looking at a summery of the data, part two is inspecting individual packets.

_Here is a generic example of a full content data using the tool TCP dump_
12:34:56.789001 IP 192.168.1.10.52344 > 93.184.216.34.80: Flags [S], seq 1234567890, win 65535, options [mss 1460,sackOK,TS val 12345 ecr 0,nop,wscale 7], length 0 12:34:56.789502 IP 93.184.216.34.80 > 192.168.1.10.52344: Flags [S.], seq 987654321, ack 1234567891, win 29200, options [mss 1400,sackOK,TS val 56789 ecr 12345,nop,wscale 7], length 0 12:34:56.790003 IP 192.168.1.10.52344 > 93.184.216.34.80: Flags [.], ack 1, win 512, length 0 12:34:56.790504 IP 192.168.1.10.52344 > 93.184.216.34.80: Flags [P.], seq 1:122, ack 1, win 512, length 121
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg1MTY3MjYwMCwzMTUwMzQ5NzAsMTMxMz
c0NzYwNywtMTQ2MjMxMjI5MCwtMTg0NTI3NTg1NywxMTg2NzYz
MzEzLDEzMzI4NDMzNjldfQ==
-->