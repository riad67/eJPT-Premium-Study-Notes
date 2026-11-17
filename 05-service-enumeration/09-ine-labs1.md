# INE Labs1

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 1372–1395. Examples are lab-specific and need verification.

**windows recon: Nmap host discovery**

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at demo.ine.local.

**Objective:** Your task is to discover available live hosts and their open ports using Nmap and identify the running services and applications.

Tools: Nmap

```bash
ping -c 5 demo.ine.local       //ping the target machine to see if it's alive or not
nmap demo.ine.local
nmap -Pn demo.ine.local
nmap -Pn -p 443 demo.ine.local     //check for close port

//We can observe in the Nmap output that the host is up, but port 443 is filtered

nmap -Pn -sV -p 80 demo.ine.local

```

In this lab, we saw a standard method to discover hosts using Nmap, which is behind a firewall.
