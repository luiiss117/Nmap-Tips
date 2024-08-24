We should know that running a default Nmap scan with a non-privileged user will perform a TCP 3-Way Handshake:

SYN (Synchronize): This process begins with the client sending a TCP segment with the SYN flag set, indicating that the client wants to establish a connection with the server. It includes an Initial Sequence Number (ISN), which is a randomly generated value.
SYN-ACK (Synchronize-Acknowledge): After receiving the SYN segment, the server responds with a TCP segment that has both the SYN and ACK flags set.
ACK (Acknowledge): Finally, the client acknowledges the server's response by sending a last TCP segment with the ACK flag set. The acknowledgment number is set to one more than the ISN.
After this process, the TCP 3-Way Handshake is completed, and the devices can exchange information in both directions.

Running Nmap as root or specifying the -sS flag (Stealth Scan) will perform a Half-Open Scan, sending TCP SYN packets to a specific port to check if a host is alive. If the host is alive, it responds with a TCP SYN-ACK, followed by an RST, so the 3-Way Handshake does not complete, and no connection is established between the devices. This technique is stealthier than an ICMP ping.

Conclusion:

TCP 3-Way Handshake (non-privileged user:

`nmap 192.168.22.129`

Half-Open Scan (needs to be run as root):

`nmap -sS 192.168.22.129`
*I highly recommend using Wireshark when you run an Nmap scan, especially if you are a beginner.*
