# DNS Zone Transfers

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 554–604. Examples are lab-specific and need verification.

### **DNS Zone Transfers**

- Domain Name System DNS is a protocol that is used to resolve domain names/hostnames to IP addresses
- During the early days of the internet, users would have to remember the IP addresses of the sites that they wanted to visit, DNS resolves this issue by mapping domain names ( easier to recall ) to their respective IP addresses.
- A DNS server (nameserver ) is like a telephone directory that contains domain names and their corresponding IP addresses
- A plethora of public DNS server have been set up by companies like Cloudflare (1.1.1.1) and google (8.8.8.8) . These DNS servers contain the recoreds of almost all domains on the internet.

A-  resolves a hostname or domain to an IPv4 adress

AAAAA - resolves a hostname or domain to an IPv6 address

NS- reference to the domains nameserver

MX —mail server

CNAME — domain aliases

TXT— text record

HINFO — host information

SOA— domain authority

SRV— service records

PTR — resolves an IP address to a hostname

**DNS Interrogation** :: is the process of enumerating DNS record for a  specific domain

**DNS Zone Transfe**r:

ZoneTransfer.me is a website

In DNSdumpster.com (dns recon & research, find & lookup dns records) search Zonetransfer.me

—

>dnsrecon -d zonetransfer.me/hackersploit.org

**>dnsenum zonetransfer.me**

>sudo vim /etc/host     — wifi ip like :: 192.168.1.1 router.admin and search in browser this ip

>whatis dig            —- dns lookup utility

>dig axfr @nsztm1.digi.ninja zonetransfer.me

>fierce  -h       —is a semi light weight scanner that helps locate IP space and hostnames against specified domains

>fierce -dns hackerploit.org
