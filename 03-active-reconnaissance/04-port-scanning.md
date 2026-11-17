# Port Scanning

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 616–664. Examples are lab-specific and need verification.

### **Port Scanning with Nmap**

- command

    ```bash
    nmap -sS -A IP
    ```

    ```bash
    namp -Pn 10.4.19.218      —-just port scan

    namp -Pn -p 80,445, 3389 IP        — specify the port number

    nmap -Pn -p1-1000 ip

    namp -Pn -F ip           __ fast scan

    namp -Pn -sU ip          —— UDP port scan

    namp -Pn -F ip -v        — verbose , what port to be discovered

    namp -Pn -F -sV ip            — service version

    namp -Pn -F -sV -O ip         —- uppercase O means OS

    namp -Pn -F -sV -O -sC ip -v        — script sC get more info about open port

    **A—— -sV -O -sC**

    namp -Pn -F -A ip -v

    man nmap               to know like help

    T0(slow) to T5(faster)

    namp -Pn -F  **-T5** -sV -O -sC ip -v           —-much faster make site slow

    nmap -Pn -F ip -oN test.txt              ————-output in txt formate

    nmap -Pn -F ip -oX test.xml              ====output in xml format
    ```

**Nmap Scan:**

**>nmap -Pn -sC -A -T4 -O ip**

**>nmap -sC -A -p21 ip      //further scan**
