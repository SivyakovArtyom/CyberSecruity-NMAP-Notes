# CyberSecruity-NMAP-Notes

MAP DISCOVERY
first step - host is up
second step - host is running

nmap 192.168.1.1-10
if no host discovery options:Nmap sends an
+ ICMP echo request (ping)
+ TCP SYN packet to port 443
+ TCP ACK packet to port 80
+ ICMP timestamp request
exceptions:
ARP (for ipv4) and Neighboor discovery (for ipv6) scans which are used for any targets on local ethernet network
Default scan without parametrs - syn scan

#Increase level of verbocity
>nmap [ip] -v 

#No scan at all. Do a reverse DNS resolution to learn their names. You can find interestin g information just from their name
>nmap [ip] -sL

#Randomize discovery 
>nmap iR 300 -sL

#Disable port scan 
>nmap iR 300 -sn

#Skip host discovery
>nmap iR 10 -Pn -v

#Types of discovery: SYN discovery
>nmap [ip] -PS22-25, 80, 113, 1050, 35000 -v

#Types of discovery: ACK discovery
>nmap [ip] -PA22-25, 80, 113, 1050, 35000 -v

#Types of discovery: UDP discovery
>nmap [ip] -PU53 -v

#IP protocol pings. By default discover 1,2,4 IP protocol
>nmap [ip] -PO1,2,4

#ARP scan only. Generally use for local scanning. Much faster then IP discovery
>nmap [ip] -PR 

#Use DNS servers for reverse resolving
>nmap [ip] -sL --dns-server [ip1,ip2...]

#Use OS's DNS resolver
>nmap [ip] -sL --system-dns [ip1,ip2...]

#Show tracerout 
>nmap [ip] -sn --tracerout


SCAN TECHNIQUES:
Start after discovery stage. Use when needed port scan and know what kind of services are used. Most of scan types are available to privileged users.

#SYN scan. Never complete TCP scan. Often referred to as a half open scan, because don't open a full TCP connection. If no response is received after several retransmissions, the port is marked as filtered. Work against any compliante TCP stack
>nmap [ip] -sS -v

#TCP connect scan. More noisy
>nmap [ip] -sT -v

#UDP connect scan. Use in combination with SYN scan. 
DNS 53
ICMP 161/162
DHCP 67/68
Generally slower and difficult. UDP scans work by sending a UDP packet to every targeted port
>nmap [ip] -sU -v
-With combination
>nmap [ip] -sU -v -sS

>nmap [ip] -sU -v -sV

#ACK SCAN. Its never determines open or even open filtered port. Out firewall rules
>nmap [ip] -sA -v

#WINDOW SCAN. Same as ACK SCAN except that it exploits an implementation detail of certain systems
>nmap [ip] -sW -v

#NULL, FIN and Xmas SCAN. Advantage to these scan types is that they can possibly sneak through certain non stateful firewalls
>nmap [ip] -s.. -v

#Protocol scanning
>nmap [ip] -sO -v

PORT SPECIFICATION: