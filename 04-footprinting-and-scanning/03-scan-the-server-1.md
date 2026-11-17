# Scan the Server 1

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 740–755. Examples are lab-specific and need verification.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at **demo.ine.local**.

**Objective:** This lab covers the process of performing port scanning and service detection with Nmap.

Tools: Nmap

```bash
ping -c 4 demo.ine.local
nmap demo.ine.local
nmap demo.ine.local -p-
nmap demo.ine.local -p 6421,41288,55413 -sV

```
