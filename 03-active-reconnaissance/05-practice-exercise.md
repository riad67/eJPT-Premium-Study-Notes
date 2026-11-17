# Practice Exercise

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 665–718. Examples are lab-specific and need verification.

### CTF_01 :

**Q.1 This tells search engines what to and what not to avoid.**

**Solution: target_url/robots.txt**

**Q.2 What website is running on the target, and what is its version?**

Solution: ****

```bash
**nmap** target.ine.local -sC -sV
```

**Q.3 Directory browsing might reveal where files are stored.\**

Solution:

```bash
**dirb** http://target.ine.local
```

              browser: target.ine.local/wp-content/uploads/

               flag.txt

**Q.4 An overlooked backup file in the webroot can be problematic if it reveals sensitive configuration details.**

Solution:

```bash
**dirb http://target.ine.local -w /usr/share/dirb/wordlists/big.txt -X**
```

 **.bak,.tar.gz,.zip,.sql,.bak.zip**

```bash
**curl http://target.ine.local/wp-config.bak**
```

**Q.5 Certain files may reveal something interesting when mirrored.**

Solution:

```bash
httrack http://target.ine.local -O target.html
```

  where we need to mirror the website to  find this flag, to mirror use httrack command

>cd target.html >cd target.ine.local >cat smlrpc0db0.php
