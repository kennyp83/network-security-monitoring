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
 
<h3 align="center" style="bold">
 full content data
</h3>

**Definition:** An *unfiltered* log of all information crossing a network. CIRTs usually review this data in two parts. Part one is looking at a summery of the data, part two is inspecting individual packets.

**Part 1: inspecting the summery**



_Here is a generic example of a full content data using the tool tshark. The tool you use will depend on your machine. If Unix/Linux, use tcpdump, if you are on windows use wireshark's tshark._
```
    1 0.000000000 10.111.72.247 → 217.160.0.187 TCP 66 63091 → 80 [SYN] Seq=0 Win=65535 Len=0 MSS=1460 WS=256 SACK_PERM
    2 0.145644600 217.160.0.187 → 10.111.72.247 TCP 66 80 → 63091 [SYN, ACK] Seq=0 Ack=1 Win=65535 Len=0 MSS=1250 SACK_PERM WS=4096
    3 0.145788900 10.111.72.247 → 217.160.0.187 TCP 54 63091 → 80 [ACK] Seq=1 Ack=1 Win=65280 Len=0
    4 0.146494000 10.111.72.247 → 217.160.0.187 HTTP 212 GET / HTTP/1.1
    5 0.293101100 217.160.0.187 → 10.111.72.247 TCP 54 80 → 63091 [ACK] Seq=1 Ack=159 Win=69632 Len=0
    6 0.306813800 217.160.0.187 → 10.111.72.247 HTTP 411 HTTP/1.1 200 OK  (text/html)
    7 0.353568800 10.111.72.247 → 217.160.0.187 TCP 54 63091 → 80 
```
*My god, what am I looking at right now?*
* **Lines 1-3:** 3-way TCP handshake, unsure what that is? GeeksforGeeks does a great job explaining:https://www.geeksforgeeks.org/computer-networks/tcp-3-way-handshake-process/
*TLDR*
	*  In networking, the requesting client is the very first packet sent. With that in mind when looking at the first packet, you can be sure that the IP of the client visiting the website is ```10.111.72.247```.
	*  the arrow, ->, on this line represents the flow of traffic, the traffic is flowing from the clients IP to ```217.160.0.187```, with this information I know that that IP belongs to the web server that the client is visiting.
* **Line 4:** A HTTP GET request asking the server for it's default webpage.
* **Line 5:** The requested server acknowledges(ACK) the get request.
* **Line 6:** The requested server sends an HTTPS OK, this includes the "HTML payload"/ contents of the website. notice the 411, this is the number of bytes. It is larger than the other lines because it includes the payload.
* **Line 7:** The client's computer acknowledges(ACK) that the payload is received.

**Part 2: inspecting Packets**

- Once someone on a CIRT team has identified a packet they want to get more information on, they can inspect it closer. The above example shows only headers. Once a packet is looked inspected you should be able to view everything available in the headers(MAC addresses, IP's, etc.), along with GET requests, user agent and some HTTP headers.
	- If you want more info on how to actually capture and inspect full content, visit: www.wireshark.org . 

<h3 align="center" style="bold">
 Extracted Content Data
</h3>

**Definition:** High level data transferred between computers. For example, files, images and other media. Unlike full content data, high level data does not focus on MAC addresses or IP.

- *note:*  Like fill content data, www.wireshark.org is going to be your best friend for viewing this content.

- Another tool you **will** find useful is Xplico, www.xplico.org.
	- Xplico allows analysts to *attempt* to reconstruct a web page after it's content is captured in a monitored network.

<h3 align="center" style="bold">
 Session Data
</h3>

**Definition:** The focus of session data is the "conversation" between two computers, more specifically: who spoke, when and how. This can be but is not limited to, timestamps, source IP, source port, destination IP, destination port, protocol, application bytes sent and others. 

- *note:* This data can be seen in full content as well. Session data is valuable if memory is scarce.
- Tools:  If you want to view session data, here are a few options for tool. Again all roads lead to wireshark;
	- Argus 
		- https://qosient.com/argus/faq.shtml
	- Zeek(formerly known as Bro)
		- https://zeek.org/

<h3 align="center" style="bold">
 Transaction Data
</h3>

**Definition:** The requests and replies between two network devices. Transaction data is a nice middle ground between session data and full content data. It is not as detailed as full content, but not as dense as session data.

-  Tools: Zeek can be used here to render transaction data.
- 
<h3 align="center" style="bold">
 Statistical Data
</h3>

**Definition:** The description of traffic resulting from activity in a network.. Key aspects of the traffic, like bytes, data size and start and end times. 

-One tool you can use here is... WIRESHARK.

<h3 align="center" style="bold">
 Meta-Data
</h3>

This one is pretty well known, it is
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MzYxNTA1NjksLTEwMTI0OTYyNzEsLT
EwMTQ0MzQyNjgsLTYyMjUxNTM3MSwtNDcxNzA3OTYsOTg3Nzkw
OTM0LC0xNzIyOTU3NTUwLDE4NTE2NzI2MDAsMzE1MDM0OTcwLD
EzMTM3NDc2MDcsLTE0NjIzMTIyOTAsLTE4NDUyNzU4NTcsMTE4
Njc2MzMxMywxMzMyODQzMzY5XX0=
-->