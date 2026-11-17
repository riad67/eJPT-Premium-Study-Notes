# Importing Nmap Scan Results Into MSF

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 4146–4163. Examples are lab-specific and need verification.

n this lab environment, you will be provided with GUI access to a Kali machine. The target machines will be accessible at **demo.ine.local** running a vulnerable RDP service.

**Objective:** To import Nmap scan results into MSF

Tools: namp, msfconsole

```bash
nmap -sV -Pn -oX myscan.xml demo.ine.local
service postgresql start
msfconsole
db_status
db_import myscan.xml
hosts
services
```
