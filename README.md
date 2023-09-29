# Nmap-network-scanning-project
Blog to document my experience with Nmap


## This project was completed in July but I wanted to document what I've learned about Nmap. 

Project purpose: 
  - Verify the Nmap installation and Nmap version that are installed on a system by using the terminal. 
  - Identification of potential vulnerabilities on a network.
  - Exploration of Nmap scanning of a network to discover active hosts, open ports and other running services.

Verifying the installed version!
![image](https://github.com/CertainRisk/Nmap-network-scanning-project/assets/141761181/feb05eb9-ce72-42d6-8dc8-5a3f1c1da220)

### TCP SYN - Stealth Scan (-sS)
I started out with a stealthy scan of my Metasploitable VM. 

While widely used it does have some limitations. 
1) Firewalls for example may detect and block SYN scans.
2) SYN scans can identify open, closed, filtered ports but they provided limited information on the specific services running on those ports.
3) As shown in the picture, performing SYN scans require root or administrator privileges which presents security concerns.
4) SYN scans also don't complete the TCP three-way handshake which limits their ability to show infromation on the full state of a connection.
 ![sS](https://github.com/CertainRisk/Nmap-network-scanning-project/assets/141761181/f02e4b3a-5e3d-483c-a97f-c83b7fe3caa9)

You can switch to -sT option, when you can't use the -sS (SYN) type scan. 
nmap -sT localhost.example.com

I wanted to learn more about how firewalls can detect and block SYN scans and I found out that some firewalls reject packets isntead of dropping them to fool the scan into thinking that the port is closed instead of filtered. I found that pretty creative!

### UDP Scans (-sU) 
- While much less reliable than the other scans due to there be no way of knowing if data transmission was successful or not, one would wonder why anyone would use them. I decided to find out!
- As it turns out UDP scans can be an internet threat. For example, UDP scans are more vulnerable to DoS attacks.
- When it comes to UDP scanning, it will send a packet and wait, in this case if no response is found the port is assumed to be open since a closed port would commonly result in an ICMP error packet being returned.
- After establishing that a UDP port is open, it sends a UDP packet specific to the services on that open port to detect which service it is.
![sU](https://github.com/CertainRisk/Nmap-network-scanning-project/assets/141761181/28223f64-2d6e-4dda-98f3-fb00980ea79c)

![sU](https://github.com/CertainRisk/Nmap-network-scanning-project/assets/141761181/cf9c077f-771d-4902-8801-1174883fe31b)

### TCP NULL Scans (-sN)
Attackers can send a packet to the target with no flags set and the target will be confused and not respond. In this case it will indicate to the attacker that the port is open on the target, because if the port is closed then it will respond with a RST packet.
![sN](https://github.com/CertainRisk/Nmap-network-scanning-project/assets/141761181/d3c9e4e6-03ca-4f24-874b-e818d5c63fe2)

![Wireshark NULL](https://github.com/CertainRisk/Nmap-network-scanning-project/assets/141761181/d73832ee-a94b-40cb-9a95-018944e78269)


### TCP FIN Scans (-sF)
Instead of sending an empty packet with no flag set, in the FIN scan - the FIN flag is set to determine if a port is closed. If a port is closed it will result in the return of a RST packet.
![Wireshark FIN](https://github.com/CertainRisk/Nmap-network-scanning-project/assets/141761181/cc926d92-7423-43f7-9534-f03f2f0b409e)

### TCP Xmas Scans (-sX)
Similar to NULL and FIN scans, except these use TCP packets with the following flags:
- PSH - Push - Flag used to inform the receiving host that the data should be pushed up to the receiving application immediately. 
- URG - Urgent flag to inform receiving station that certain data within a segment should be prioritized.
- FIN - Determines if ports are closed and results in the return of a RST packet.
TCP Xmas scans also expect RST packets for closed ports. 
![sX](https://github.com/CertainRisk/Nmap-network-scanning-project/assets/141761181/ed6f7395-5148-4ecd-898d-556abffd959c)

![Wireshark sX](https://github.com/CertainRisk/Nmap-network-scanning-project/assets/141761181/c40a5e2d-6e0d-4698-a855-05090ab89865)

