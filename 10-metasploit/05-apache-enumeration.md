# Apache Enumeration

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 4279–4373. Examples are lab-specific and need verification.

Apache enumeration is a crucial step in the reconnaissance phase of a penetration test, where the goal is to gather as much information as possible about the Apache web server being targeted. This information can help in identifying potential vulnerabilities or misconfigurations that can be exploited later in the test. In this lab, we will learn about Apache enumeration using the Metasploit framework modules.

In this lab environment, you will be provided with GUI access to a Kali machine. The target machine will be accessible at "victim-1".

**Objective:** Run the following auxiliary modules against the target (victim-1):

- auxiliary/scanner/http/apache_userdir_enum
- auxiliary/scanner/http/brute_dirs
- auxiliary/scanner/http/dir_scanner
- auxiliary/scanner/http/dir_listing
- auxiliary/scanner/http/http_put
- auxiliary/scanner/http/files_dir
- auxiliary/scanner/http/http_login
- auxiliary/scanner/http/http_header
- auxiliary/scanner/http/http_version
- auxiliary/scanner/http/robots_txt

**Tools: msf**

```bash
ping -c 5 victim-1
msfconsole -q
use auxiliary/scanner/http/http_version
set RHOSTS victim-1
run

use auxiliary/scanner/http/robots_txt
set RHOSTS victim-1
run

use auxiliary/scanner/http/http_header
set RHOSTS victim-1
run

use auxiliary/scanner/http/http_header
set RHOSTS victim-1
set TARGETURI /secure
run

use auxiliary/scanner/http/brute_dirs
set RHOSTS victim-1
run

use auxiliary/scanner/http/dir_scanner
set RHOSTS victim-1
set DICTIONARY /usr/share/metasploit-framework/data/wordlists/directory.txt
run

use auxiliary/scanner/http/dir_listing
set RHOSTS victim-1
set PATH /data
run

use auxiliary/scanner/http/files_dir
set RHOSTS victim-1
set VERBOSE false
run

use auxiliary/scanner/http/http_put
set RHOSTS victim-1
set PATH /data
set FILENAME test.txt
set FILEDATA "Welcome To AttackDefense"
run

wget http://victim-1:80/data/test.txt
cat test.txt

use auxiliary/scanner/http/http_put
set RHOSTS victim-1
set PATH /data
set FILENAME test.txt
set ACTION DELETE
run

wget http://victim-1:80/data/test.txt

use auxiliary/scanner/http/http_login
set RHOSTS victim-1
set AUTH_URI /secure/
set VERBOSE false
run

use auxiliary/scanner/http/apache_userdir_enum
set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt
set RHOSTS victim-1
set VERBOSE false
run

```

In this lab, we learned about Apache enumeration using the Metasploit framework modules.
