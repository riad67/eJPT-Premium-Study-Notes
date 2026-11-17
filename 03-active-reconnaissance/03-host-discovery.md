# Host Discovery

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 605–615. Examples are lab-specific and need verification.

### **Host Discovery with Nmap**

- command

    ```bash
    sudo nmap -sn 192.168.2.0/24

    sudo netdiscover -i eth0 -r 192.168.2.0/24
    ```
