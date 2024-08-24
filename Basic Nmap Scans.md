Windows Firewall will block the ICMP echo request that nmap sends by default to know if the host is up or not, so to dont send the ICMP we have to specify the flag -Pn: Treat all hosts as online -- skip host discovery. You can also specify another echo requests such as ARP requests, or TCP/UDP probes for host discovery, -PS/PA/PU/PY also -PE/PP/PM: ICMP echo, timestamp, and netmask discovery probes.

Note: For host discovery you can specify a port, nmap will do a request to that port and if it gets a response is because the host and that port is up, e.g `nmap -sn -PS 445 192.168.13.6`
-sn: Ping Scan/Ping Sweep.

We have to know that nunning a default nmap with a non-privileged user will do a TCP 3-Way Handshake:
![[Captura de pantalla 2024-08-23 235135.png]]
SYN (Synchronize): This process begins with client sending a TCP segment with the SYN flag set, meaning that the client wants to establish a connection with the server. It includes a initial sequence number (ISN), which is a random generated value.

SYN-ACK (Synchronize-Acknowledge): After receiving the SYN segment, the server responds with a TCP segment that has both flags: SYN and ACK.

ACK (Acknowledge): Finally the client acknowledges the server's response by sending a last TCP segment with the ACK flag set. The acknowledgment number is set to one more than the ISN.

After this process, the TCP 3-Way Handshake is completed and the devices can exchange information in both ways.

![[handshake-1 1.png]]


Running nmap as root or specifying -sS (Stealth Scan) will do a Half-Open Scan, sending TCP SYN packets to a specific
port to check if a host is alive. If the host is alive, it
responds with a TCP SYN-ACK then RST so the 3-Way Handhsake doesnt complete and neither establish a connection between the devices. This technique is stealthier than ICMP ping.
![[Nmap-root-scan.png]]
  Conclusion:
  TCP 3-Way handshake
  `nmap 192.168.22.129` (As non-privileged user)

Half-Open Scan (needs to be runned as root)
`nmap -sS 192.168.22.129`
`nmap 192.168.22.129`
