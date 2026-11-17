# Website Recon and Footprinting

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 121–182. Examples are lab-specific and need verification.

## **Website Recon and Footprinting**

- IP Addresses
- Directories hidden from search engine
- Names
- Email address
- Phone numbers
- Physical address
- Web technologies being used

Passive Recon:

>what is host

>host hackersploit.org

### robots.txt:

for example: **https://hackersploit.org/robots.txt**

here, website like google /bing/duckduckgo will crawl the website

.. most website has robots.txt , which website does not have robots.txt which means really doing something wrong . IT specify (robots.txt) what folders or what files you don’t want search engine to index.

crawling: It essentially refine the website and then it indexes it on google.com

### sitemap.xml

for example: **https://hackersploit.org/sitemap.xml**

-access publically if particular page are not linked on the main website/front end of a website this provide or tell us some of the others linked/pages than can be accessed publically… like for wordpress website

**extensions:**

### (Build with) and (wappalyzer)

— tell us what is running on that website/what web technology/ content management system is , like wordpress or IP or version

command in kali linux:

```bash
what web

whatweb hackersploit.rog
```

### HTTrack /HDTrack

You can download teh entire website as is through tools

```bash
sudo apt get install webthttrack
```

### **Whois Enumeration**

**Website Footprinting with Netcraft**

—website recon or footprinting with netcraft

__a. netcraft—b. resources…c. site report
