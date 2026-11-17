# Passive Information Gathering

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 80–120. Examples are lab-specific and need verification.

# Passive Information Gathering

## **Passive Information Gathering@**

- Passive Information Gathering
    1. `host hackersploit.org`
    2. robots file - ****https://hackersploit.org/robots.txt
    3. site map - https://hackersploit.org/sitemap_index.xml
    4. Web tech - **Wappalyzer, built with** extensions
    5. `whatweb hackersploit.org`
    6. Download whole website - **HTTrack**
    7. **Who is**
    - `whois hackersploit.org`
    - `whois 172.64.32.93`
    - Sites : who.is domaintools.com
    1. Website footprinting with **Netcraft** - **https://sitereport.netcraft.com/?url=https%3A%2F%2Fhackersploit.org**
    2. **Dnsrecon**
    - `dnsrecon -d hackersploit.org`
    - Site: dnsdumpster.com
    1. **WAF**
    - Download : https://github.com/EnableSecurity/wafw00f
    - `wafw00f hackertube.net -a`
    1. Subdomain Enumeration - **Sublist3r**
    - `sublist3r -d hackersploit.com -o hs_sub_enum.txt`
    1. **Google dorks**
    - site:ine.com
    - site:ine.com employees
    - site:ine.com inurl:forum
    - site:*.ine.com
    - site:*.ine.com intitle:forum
    - site:*.ine.com filetype:pdf
    - inurl:auth_user_file.txt
    - inurl:passwd.txt
    - inurl:wp-config.bak
    1. waybackmachine
    2. **Email Harvesting**
    - `theHarvester -d hackersploit.org`
    - `theHarvester -d hackersploit.org -b google,linkedin,dnsdumpster,duckduckgo,crtsh`
    - `theHarvester -d zonetransfer.me -b all`
    1. Leaked Passwords database : https://haveibeenpwned.com/
