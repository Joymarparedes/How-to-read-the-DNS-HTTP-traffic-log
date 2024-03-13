<h1>How to read the DNS & HTTP traffic log</h1>

This reading explains how to identify the brute force attack using tcpdump.
<br />

<img src="https://i.imgur.com/nqn1s6D.png" height="80%" width="80%" alt="Create Virtual Machine"/>
<br />

The first section of the DNS & HTTP traffic log file shows the source computer (your.machine.52444) using port 52444 to send a DNS resolution request to the DNS server (dns.google.domain) for the destination URL (yummyrecipesforme.com). Then the reply comes back from the DNS server to the source computer with the IP address of the destination URL (203.0.113.22). 


<img src="https://i.imgur.com/e1nrTvw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

The next section shows the source computer sending a connection request (Flags [S]) from the source computer (your.machine.36086) using port 36086 directly to the destination (yummyrecipesforme.com.http). The .http suffix is the port number; http is commonly associated with port 80. The reply shows the destination acknowledging it received the connection request (Flags [S.]). The communication between the source and the intended destination continues for about 2 minutes, according to the timestamps between this block (14:18) and the next DNS resolution request (see below for the 14:20 timestamp). 



<h2>TCP Flag codes include:</h2>

- Flags [S]  - Connection Start 
- Flags [F]  - Connection Finish 
- Flags [P]  - Data Push
- Flags [R]  - Connection Reset
- Flags [.]  - Acknowledgment



<img src="https://i.imgur.com/s5AC5m1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

The log entry with the code HTTP: GET / HTTP/1.1 shows the browser is requesting data from yummyrecipesforme.com with the HTTP: GET method using HTTP protocol version 1.1. This could be the download request for the malicious file. 


<br/>
<img src="https://i.imgur.com/qUoNYcC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<br />
Then, a sudden change happens in the logs. The traffic is routed from the source computer to the DNS server again using port .52444 (your.machine.52444 > dns.google.domain) to make another DNS resolution request. This time, the DNS server routes the traffic to a new IP address (192.0.2.172) and its associated URL (greatrecipesforme.com.http). The traffic changes to a route between the source computer and the spoofed website (outgoing traffic: IP your.machine.56378 > greatrecipesforme.com.http and incoming traffic: greatrecipesforme.com.http > IP your.machine.56378). Note that the port number (.56378) on the source computer has changed again when redirected to a new website.

<br />

</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
