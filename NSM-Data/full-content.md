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

- Once someone on a CIRT team has identified a packet they want to get more information on, they can inspect it closer. The above example shows only headers. Once a packet is looked inspected you should be able to view everything available in the headers(MAC addresses, IP's, etc.), along with GET requests, user agent and some HTTP headers. Inspecting packets usually leads to a closer look at one of the other seven types of data.
	- If you want more info on how to actually capture and inspect full content, visit: [www.wireshark.org](https://www.wireshark.org/), or https://www.tcpdump.org/. 

