# DNS Recon

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 183–230. Examples are lab-specific and need verification.

### **DNS Recon**

Tool: google dns recon ( is a python scripts enum general dns records of  domain)

site:: [**https://dnsdumpster.com/](https://dnsdumpster.com/)    ( good site for dns recon) , for this I can identify subdomain also.**

- commands

    ```bash
    dnsrecon —help

    dnsrecon -d hackersploit.org       — where d for specify the domain name

    dnsrecon -d zonetransfer.me
    ```

**WAF with wafw00f**

- WAFW00F

    The web application firewall fingerprinting tool

    sends normal http request and get normal response

    ** quickly identifying whether a website or web app is being protected by a web app firewall**

    -identify what firewall will show what next steps are…

    >waf00f -h

    >waf00f -l ( l for list)

    >waf00f hackersploit.org

    note: The site https://hackersploit.org is behind Cloudflare (Cloudflare Inc.)

    >waf00f zonetransfer.me

    note: no waf detected by the generic detection , so what is actually mean by this? this is not protected.

    … with dns dumpster in the previous could possibly be the IP address of the server that’s could possibly actually hosting that website.

    >wafw00f https://hackertube.net    ( this does not change the output, it will same as previous command)

    >wafw00f https://hackertube.net -a    ( a for all possible waf instances)
