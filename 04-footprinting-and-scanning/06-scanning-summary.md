# Scanning Summary

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 909–918. Examples are lab-specific and need verification.

## **Footprinting & Scanning@**

- Foot printing & Scanning
    1. Wireshark
    2. Arp scan `arp-scan -I eth1 192.168.31.0/24`
    3. Ping `ping 192.168.31.2`
    4. fping `fping -I eth1 -g 192.168.31.0/24 -a`
    5. nmap `nmap -sn 192.168.31.0/24`
    6. Zenmap - GUI of nmap
