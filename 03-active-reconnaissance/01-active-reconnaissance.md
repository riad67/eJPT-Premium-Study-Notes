# Active Reconnaissance

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 534–553. Examples are lab-specific and need verification.

# Active Information Gathering

## Active Information Gathering@

- Active Information Gathering
    1. DNS record & Zone Transfer `dnsenum zonetransfer.me`
    2. Host discovery with Nmap
    - `cat /etc/hosts`
    - `nmap -sn 192.168.2.0/24`
    - `netdiscover -i eth0 -r 192.168.2.0/24`
    1. Port Scanning with nmap
    - `nmap 192.168.2.3`
    - `nmap -Pn 192.168.2.3`
    - `nmap -Pn -p- 192.168.2.3`
    - `nmap -Pn -p- -F -sU 192.168.2.3`
    - `nmap -p 80,44 192.168.2.3`
    - `nmap -p- -sV 192.168.2.3`
    - `nmap -sV -p- -O 192.168.2.3`
    - `nmap -Pn -F 192.168.2.3 -oN outputfile.txt`
