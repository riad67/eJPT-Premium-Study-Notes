# Samba Recon: Basics(SMB Enumeration)

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 962–999. Examples are lab-specific and need verification.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

**Objective:** Answer the following questions:

1. Find the default tcp ports used by smbd.
2. Find the default udp ports used by nmbd.
3. What is the workgroup name of samba server?
4. Find the exact version of samba server by using appropriate nmap script.
5. Find the exact version of samba server by using smb_version metasploit module.
6. What is the NetBIOS computer name of samba server? Use appropriate nmap scripts.
7. Find the NetBIOS computer name of samba server using nmblookup
8. Using smbclient determine whether anonymous connection (null session) is allowed on the samba server or not.
9. Using rpcclient determine whether anonymous connection (null session) is allowed on the samba server or not.

Tools: Nmap, Metasploit, nmblookup, smbclient, rpcclient

```bash
nmap demo.ine.local
nmap -sU --top-ports 25 demo.ine.local
nmap -sV -p 445 demo.ine.local
nmap --script smb-os-discovery.nse -p 445 demo.ine.local

msfconsole -q
use auxiliary/scanner/smb/smb_version
set RHOSTS demo.ine.local
exploit

nmap --script smb-os-discovery.nse -p 445 demo.ine.local
nmblookup -A demo.ine.local
// Find the NetBIOS computer name of samba server using nmblookup.
smbclient -L demo.ine.local -N
//Using smbclient determine whether anonymous connection (null session) is allowed on the samba server or not
rpcclient -U "" -N demo.ine.local
//Using rpcclient determine whether anonymous connection (null session) is allowed on the samba server or not.
```
