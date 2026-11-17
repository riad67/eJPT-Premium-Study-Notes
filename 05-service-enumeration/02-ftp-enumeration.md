# FTP Enumeration

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 936–961. Examples are lab-specific and need verification.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

**Objective:** Your task is to perform FTP enumeration with Metasploit.

Tools: Metasploit Framework , FTP client

```bash
ping -c 4 demo.ine.local
msfconsole
use auxiliary/scanner/ftp/ftp_version
set RHOSTS demo.ine.local
run
use auxiliary/scanner/ftp/ftp_login
set RHOSTS demo.ine.local
set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
run
use auxiliary/scanner/ftp/anonymous
set RHOSTS demo.ine.local
run
ftp demo.ine.local

```
