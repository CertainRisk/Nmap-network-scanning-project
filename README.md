# Nmap-network-scanning-project
Blog to document my experience with Nmap


## This project was completed in July but I wanted to document what I've learned about Nmap. 

Project purpose: 
  - Verify the Nmap installation and Nmap version that are installed on a system by using the terminal. 
  - Identification of potential vulnerabilities on a network.
  - Exploration of Nmap scanning of a network to discover active hosts, open ports and other running services.

Verifying the installed version!
![image](https://github.com/CertainRisk/Nmap-network-scanning-project/assets/141761181/feb05eb9-ce72-42d6-8dc8-5a3f1c1da220)

TCP SYN - Stealth Scan -sS
I started out with a stealthy scan of my Metasploitable VM. 

While widely used it does have some limitations. 
1) Firewalls for example may detect and block SYN scans.
2) SYN scans can identify open, closed, filtered ports but they provided limited information on the specific services running on those ports.
3) As shown in the picture, performing SYN scans require root or administrator privileges which presents security concerns.
4) SYN scans also don't complete the TCP three-way handshake which limits their ability to show infromation on the full state of a connection.
   
*Picture here*

I wanted to know more about the Firewalls being able to detect and block SYN scans and I found out that some firewalls reject packets isntead of dropping them to fool the scan into thinking that the port is closed instead of filtered. I found that pretty creative!
