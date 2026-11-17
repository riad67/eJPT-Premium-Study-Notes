# Postfix Recon: Basics

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 4455–4520. Examples are lab-specific and need verification.

An SMTP (Simple Mail Transfer Protocol) server is a mail server that sends and receives emails using the SMTP protocol. It's responsible for sending, receiving, and relaying outgoing mail between email senders and recipients.

In this lab we will look at the basics of Postfix SMTP server reconnaissance.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

**Objective:** Answer the following questions:

1. What is the SMTP server name and banner.
2. Connect to SMTP service using netcat and retrieve the hostname of the server (domain name).
3. Does user “admin” exist on the server machine? Connect to SMTP service using netcat and check manually.
4. Does user “commander” exist on the server machine? Connect to SMTP service using netcat and check manually.
5. What commands can be used to check the supported commands/capabilities? Connect to SMTP service using telnet and check.
6. How many of the common usernames present in the dictionary /usr/share/commix/src/txt/usernames.txt exist on the server. Use smtp-user-enum tool for this task.
7. How many common usernames present in the dictionary /usr/share/metasploit-framework/data/wordlists/unix_users.txt exist on the server. Use suitable metasploit module for this task.
8. Connect to SMTP service using telnet and send a fake mail to root user.
9. Send a fake mail to root user using sendemail command.

**Tools: nmap, telnet, nc msf**

```bash
nmap -sV -script banner demo.ine.local
#port 25 smtp version:Postfix
#Banner: openmailbox.xyz ESMTP Postfix: Welcome to our mail server
#
# Connect to SMTP service using netcat and retrieve the hostname of the server (domain name).
//domain name: openmailbox.xyz
nc demo.ine.local 25
#Does user "admin" exist on the server machine? Connect to SMTP service using netcat and check manually.
answer: yes
VRFY admin@openmailbox.xyz
#What commands can be used to check the supported commands/capabilities? Connect to SMTP service using telnet and check.
telnet demo.ine.local 25
HELO attacker.xyz
EHLO attacker.xyz
#got 8 common username
smtp-user-enum -U /usr/share/commix/src/txt/usernames.txt -t demo.ine.local
#got 22 common username

msfconsole -q
use auxiliary/scanner/smtp/smtp_enum
set RHOSTS demo.ine.local
exploit

#Connect to SMTP service using telnet and send a fake mail to root user.
telnet demo.ine.local 25
HELO attacker.xyz
mail from: admin@attacker.xyz
rcpt to:root@openmailbox.xyz
data
Subject: Hi Root
Hello,
This is a fake mail sent using telnet command.
From,
Admin
.
#Send a fake mail to root user using sendemail command.

sendemail -f admin@attacker.xyz -t root@openmailbox.xyz -s demo.ine.local -u Fakemail -m "Hi root, a fake from admin" -o tls=no

```

In this lab, we looked at the basics of Postfix SMTP server reconnaissance.
