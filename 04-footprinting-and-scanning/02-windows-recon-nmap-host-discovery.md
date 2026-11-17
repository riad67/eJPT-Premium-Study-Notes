# Windows Recon: Nmap Host Discovery

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 723–739. Examples are lab-specific and need verification.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at demo.ine.local.

**Objective:** Your task is to discover available live hosts and their open ports using Nmap and identify the running services and applications.

Tools: Nmap

```bash
ping -c 5 demo.ine.local
nmap demo.ine.local
nmap -Pn demo.ine.local
nmap -Pn -p 443 demo.ine.local
//We can observe in the Nmap output that the host is up, but port 443 is filtered.
nmap -Pn -sV -p 80 demo.ine.local
```
