Network Analysis 
===========================================

## Network Packet Analysis 

### Network Packets
- Packets exist in the OSI Layer 3 and are formatted according to IP (Internet protocol) or others. 
- Divided into 2 parts: header contains address information and payload contains the content/data.

#### Packet Header
- Example: contains Ethernet header from L2, IP header from L3, Transmission Control Protocol (TCP) header from L4
- Ethernet header: src and des MAC address 
- IP header: src and des IP address 
- TCP header: src port and des port, sequence number, synchronization bits. Sequence number shows number of packet in the packet sequence. 
- Packet might have UDP header instead of TCP 

**Synchronization bits**
- URG (1bit): means Urgent traffic, but normally people would use the IP precedence bits 
- ACK (1bit): attempt to synchronize communications
- RST (1bit): reset the connection
- SYN (1bit): synchronizes sequence numbers
- FIN (1bit): no more data from sender 
- Sending malformed packets: session hijacking attacks (sending RST packet to reset the connection), and SYN flood (flooding the target with SYN packets but never responding to SYN/ACK). 

**Recon // Types of Port Scan**
- Port scan: sending an ICMP (Internet Control Message Protocol) packet to each port to see if they respond, this is an easy scan but can be bypass. 
- How to tell if it's a potential port scan: inspecing incoming packets destined for well-known ports with certain flags turned on

**Stealth Scanning
- You do a stealth scanning when you don't want to establish a 3 way handshake but you still want to get some kind of response from the target. 
- **FIN scan**: FIN flag indicates communication end. Hacker send packets with FIN flag >> if port is open, error message is generated. 
- **Christmas Tree Scan**: Hacker sends TCP packet to the target with the URG, PUSH and FIN flags >> alternating bits turned on and off in flag bytes
- **Null Scan**: turns off all flags >> creates a lack of TCP flags in the packet 
- Examing TCP packets, look at ports, IP address and bit flags. 

#### Payload
- If packet is fixed length, payload may be padded with blank information or something. 

**Trailer**
- Doesn not exist for layer 3 and 4, but appear in layer 2
- Can be part of Ethernet or PPP (Point to Point Protocol). Ethernet has 96 bits indicating reach the end of the transmission. 

**Error Checking Mechanism of Layer 2 Frame**
- 32 bits redundancy check 
- Sender calculates CRC >> creates 32 bits and stores in the trailer by the sender >> transmit the frame >> receiver receives the frame >> receiver calculates the bits like sender and compares with the trailer >> values match, frame is good >> if not and if it's Ethernet, receiver discards the frame and doesn't send anything. 
- In IP, UDP doesn't request a retransmission, but TCP requests it. 

#### Ports 
- Port is number that identifies a channel in which communication can occur. 
- There re 65,635 possible ports, each of TCP and UDP 
- Socket: an IP address concatenated with a port number, unique for a duration of connection 

**Famous Ports**
- 20/21: FTP, 20 for information, 21 for control
- 22: SSH 
- 23: Telnet 
- 25: SMTP 
- 43: Whois 
- 53: DNS 
- 69: Trivial File Transfer Protocol (TFTP), fast version of FTP
- 80: HTTP
- 88: Kerberos 
- 110: POP3 to receive emails
- 137-139: NetBIOS
- 143: IMAP and 220
- 161/162: SNMP 
- 179: Border Gateway Protocol BGP
- 194: IRC chat rooms
- 389: LDAP Lightweight Directory Access Protocol
- 443: HTTPS
- 445: Active Directory/SMB Server Message Block
- 464: Kerberos change password
- 465: SMTP over SSL
- 636: LDAPS
- 993: Secure IMAP
- 995: POP3 Secure 
- 3389: Remote Desktop
- 31337: Back Orifice (malware)
- 54320 and 54321: BO2K (malware)
- 6666: Beast (malware)
- 23476/23477: Donald Dick (malware)
- 43188: Reachout (malware)
- 407: Timbuktu 

### Network Attacks 

### Denial of Service 
- 3 approaches
1. Damage target's ability to operate
2. Overflow target with too many open connections at the same time
3. Use up bandwidth to the target 

**Ping of death attack**
- Attack sends a large ICMP echo packet than the target machine can accept
-Aftermath: causing OS to lock, crash
- Counter: firewalls blocking incoming ICMP packets with some proper lengths 

**Ping flood**
- Send huge amounts of ICMP packets 
- Counter: doesn't work with modern servers 
- is DDoS

**Teardrop Attack**
- Hacker send fragments of broken packets and then when target tries to assemble it, it makes the system crashes 
- Counter: doesn't work anymore

**SYN flood attack**
- Only send a lots of SYN requests and never respond to SYN-ACK
- Overwhelm target system 
- Counter: most modern firewall can prevent this, firewall can block 10,000 requests of SYN
- Better way: change the address and flood the SYN requests?

**LAND (local area network denial) attack**
- Hacker sends fake TCP SYN packet with same src and des IP addresses and port to target
- Target machine thoughts it sent the message to itself, keeps replying to it

**Smurf attack**
- Amplifying. Generate a large amount of ICMP echo requests from a single request, causing traffic jam in the target network
- Counter: routing devices today barely respond to broadcast requests
- Better: only works for victim on the same network subnet, if one machine responds to that request, it will jam the traffic.

**Fraggle attack**
- Similar to smurf attack, except using spoofed UDP packets instead of ICMP echo requests
- Counter: firewall can stop this

**Packet mistreating attack**
- When a compromised router mishandles packets resulting in congestion in some part of the network 

## Network Traffic Analysis Tools 
- Sniffer: intercept and log traffic passing over a digital network 

### Wireshark
- Captured data is shown in 2 forms: hexadecimal and ASCII, or encrypted image files. 

### HTTPSniffer
- Enable you to see all HTTP commands going to the server and the responses from the server 
- Needs you to understand HTTP commands: GET, HEAD, PUT, POST and response codes like 404 

#### Nmap
- Enable you to see which ports are open on a target system and which services are running 

### Snort
- Is an IDS, but can also be a packet sniffer with lots of config options 

### RSA NetWitness 

## Network Traffic Analysis 

### Using Logs As Evidence 
- Everything has logs 
- A device's log contains the primary records of a personal activities on a system or network 
- Authentication logs contain accounts and authenticated IP address
- Application logs contain time, date, application id
- OS system logs contain events (use of devices, errors, reboots) >> can be used to analyze to identify pattern of activity and unusual events 
- Network device logs contain information about activities that take place in the network 
- IDS contains attack signatures
- Problems with logs: They change rapidly and getting permission to collect evidence from some sources takes time, hacker can change log information 

### Wireless 

Basic wireless networks
- 802.11a: first widely used Wifi standard, operates at 5GHz and pretty slow
- 802.11b: standard operated at 2.4 GHz, indoor range of 125 ft with bandwidth of 11 Mbps
- 802.11g: does not exist in market anymore, includes backward compability with 802.11b, indoor range of 125 ft and bandwidth of 54Mbps 
- 802.11n: bandwidth 100-140 Mbps, frequencies of 2.4 or 5.0 GHz and indoor range 230 ft
- 802.11n-2009: bandwidth up to 600 Mbps with use of 4 spatial streams at a channel width of 40 Mhz. Uses multiple input multiple output (MIMO) 
- MIMO is a wireless technology that supports the use of multiple users at the same time 
- 802.11ac: throughput up to 1Gbps with at least 500 Mbps, 8 MIMO
- 802.11 ad: supports data transmission rates up to 7 Mbps, 10 times faster than 802.11n rate

Finding evidences in wireless storage device like wireless digital, video cameras, wireless printers with storage capabilities, wireless network-attached storage (NAS), tablets and smartphones

## Router Forensics 

**Why?** When you want to trace a path back to the attacker, you can look at the router because the router forwards packets across network to a destination 
- Router contains: read-only memory with power-on self test code, flash memory container the router's os, non-volatile RAM containing config information, volatile RAM containing routing tables and log information. 

### Router Basics

**Network card**
- NIC is an expansion board that is part of mounted motherboard
- What it does? allowing the computer to be connected to a network 
- Handling signal encoding, decoding, data buffering and trasmission, Media Access Control, data encapsulation, building frame around the data 

**Hub**
- Connecting computers on Ethernet LAN 
- Has traffic jam because it takes all receiving packets and sends a copy of it to all ports 

**Switch**
- No more traffic jam because it makes sure that data goes straight from src to des 
- Remembers the address of every node on the network and anticipate where data needs to go 
- Only operates on LAn, does not work with Internet and WAN
- Needs a router

**Router**
- Connects different logical networks, enables traffic passes through 
- Improved security funtions from a switch: records IP addresses (route table), Network Layer 
- Determines where to send information from 1 machine to another 
- Routing table: keeping track of connections or routes. How routing table was created? router examines the incoming packets and if the IP is strange, it adds that to the routing table 
- Modern routers can filter, shape, give priority to traffic according to company or customer needs. 
- Home router also act as firewall and issues IP addresses by DHCP 

#### Router Attacks
- Routing table poisoning: to create errors in routing table, hackers change the routing data update packets that the routing protocols need 

#### Getting Evidence from Router
- Do not shut down the router
1. Connect the router to run certain commands. Use tool like HyperTerminal 
2. Run commands (depends on versions of routers) like "show version", "show version" returns hardware and software information about the router like the platform, os version, system image file, interfaces, amount of RAM the router has, number of network and voice interfaces there are. 
- "show running-config" provides the currently executing config
- "show startup-config" provides system start-up config
- "show ip route command" shows the routing table 
- Cisco IOS 11.2 introduced show tech-support, allows collection of multiple sources of information concerning the router in a single command. 

## Firewall Forensics 

### Firewall Basics 
- 2 types of firewall: packet filtering and stateful packet inspection 

#### Packet Filter 
- Filters incoming packets >> allow entrance or deny based on a set of rules 
- Filter packets based on size, protocol, source IP

#### Stateful Packet Inspection
- Examines all packetsa and takes previous packets into consideration. 
- Less susceptible to ping flood, SYN flood and spoofing because this firewall is aware of the context of a stream of packets. 

#### Application Filter
- Combining stateful packet inspection with scanning for specific application issues 

### Collecting Data 
- 3 ranges of port numbers
1. Well-known ports: 0-1023
2. Registered ports: 1024-49151
3. Dynamic ports: 49152-65535
- Decoy scan: mixing attacker's IP address among a huge batch and using them to scan the target 
- Ping each the system and match them with the TTL in the responses with the connection attempts. **TTL is the number of routers between a source and destination**. So if the TTL of the captured traffic and TTL of test does not match, it indicates that the addresses are spoofed by an attacker. 


