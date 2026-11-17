# INE Labs2

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 1396–1418. Examples are lab-specific and need verification.

**Importing Nmap Scan Results into MSF**

In this lab environment, you will be provided with GUI access to a Kali machine. The target machines will be accessible at **demo.ine.local** running a vulnerable RDP service.

**Objective:** To import Nmap scan results into MSF.

**Tools: Nmap, msfconsole**

```bash
ping -c 4 demo.ine.local
nmap -sV -Pn -oX myscan.xml demo.ine.local
service postgresql start
msfconsole
db_status
db_import myscan.xml
hosts
services
```

This lab demonstrates the process of importing Nmap scan results into the Metasploit Framework, enabling efficient integration of network discovery and vulnerability exploitation.
