# Windows Recon: SMB Nmap Scripts

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 794–908. Examples are lab-specific and need verification.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

**Objective:** Your task is to fingerprint the service using the tools available on the Kali machine and run Nmap scripts to enumerate the Windows target machine's SMB service.

1. Identify SMB(server message block) Protocol Dialects
2. Find SMB security level information
3. Enumerate active sessions, shares, Windows users, domains, services, etc.

**The following username and password may be used to access the service:**

| Username | Password | | administrator | smbserver_771 |

Tools: Nmap

```bash

ping -c 5 demo.ine.local
nmap demo.ine.local
nmap -p445 --script smb-protocols demo.ine.local
nmap -p445 --script smb-security-mode demo.ine.local
nmap -p445 --script smb-enum-sessions demo.ine.local
nmap -p445 --script smb-enum-sessions --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local
nmap -p445 --script smb-enum-shares demo.ine.local
nmap -p445 --script smb-enum-shares --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local
nmap -p445 --script smb-enum-users --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local
nmap -p445 --script smb-server-stats --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local
nmap -p445 --script smb-enum-domains --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local
nmap -p445 --script smb-enum-groups --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local
nmap -p445 --script smb-enum-services --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local
nmap -p445 --script smb-enum-shares,smb-ls --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local

```

- **Objectives**
1. you will have a solid understanding of the importance of network mapping and port scanning.
2. you will have a basic understanding of the OSI model and transport layer protocols like **TCP and UDP**
3. you will be able to comprehensively map out a network and discover different host on a target network with Nmap
4. you will be able to identify open port on target hosts and identify the services running on them
5. you will be able to perform OS and service fingerprinting with Nmap
6. you will have an understanding of how to detect and evade firewalls with Nmap
7. you will be able to speed up or slow down Nmap scans depending on the target environment
- Introduction

Penetration Testing Methodology

- Networking Primer
- Networking Fundamentals

    Network protocols

    **Packets**

    structure: Header , Payload(actual data, contain sources and destination)

    **OSI (open systems interconnection ) Model**

    OSI Layer

    1. Physical layer —- usb, ethernet cables, coax, fiber , hub etc —-**attack:: cable tapping, wire tapping, singal jamming, usb type deye attack**
    2. Data link layer——- ethernet ,ppp, switches:   **arp spoofing, mac spoofing, mimt**
    3. Network layer ——- ip, icmp , IPSec  : **ip spoofing, dos ddos,**
    4. Transport layer ——-tcp, udp ::  **tcp synflood, udp flooding, port scanning**
    5. Session layer ——APIs, NetBios, RPC ::: session **hyjacking , man in the middle attack**
    6. Presentation layer — SSL/TLS, JPEG, GIF, SSH, IMAP:::: **ssl triping attack (encryption) pinon , buffer overflow attack, data injection**
    7. Application layer ——HTTP, FTP, IRC, SSH, DNS ::: **fishing , sql , xss**

    TCP: reliable(if data lost, you can again send data, take time(diff diff segment e ) , gradually data transfer)

    UDP: not reliable , so fast, directly send, **Live streaming , online gaming**

**IP Internet Protocol Functionality**

ICMP Internet Control Message Protocol

DHCP Dynamic Host Configuration Protocol

**IP Header Format**

**Demo: IP Header Analysis**

**Important Port(well known 0-1023)**

Standardized by IANA(Internet Assigned Numbers Authority)

| **Port Number** | **Services** | **Descriptions** |
| --- | --- | --- |
| 80 | HTTP | Hypertext Transfer Protocol |
| 443 | HTTPS | HTTP Secure |
| 21 | FTP | File Transfer Protocol |
| 22 | SSH | Secure Shell |
| 25 | SMTP | Simple Mail Transfer Protocol |
| 110 | POP3 | Post Office Protocol version 3 |

| **Ports** | **Descriptions** |
| --- | --- |
| 3389 | RDP Remote Desktop Protocol |
| 3306 | MySQL Database |
| 8080 | HTTP alternative port |
| 27017 | MongoDB Database |

## **Transport Layer -Part2**

# netstat

```bash
netstat -antp
```
