# Subdomain Enumeration

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 231–263. Examples are lab-specific and need verification.

### **Subdomain Enumeration with Sublist3r**

—Passive::: this not actively enum  , here using publicly available sources of information , not using bruteforce (at that point will be actively engaging with the target system)

>sublist3r -d hackersploit.org

.. note: total unique subdomains found:1 ; **forum.hackersploit.org**

>sublist3r -d ine.com

- find unique subdomains: 17

    assets.ine.com
    profiles.assets.ine.com
    careers.ine.com
    certs.ine.com
    checkout.ine.com
    els-cdn.content-api.ine.com
    courses.ine.com
    dashboard.ine.com
    info.ine.com
    assets.labs.ine.com
    learn.ine.com
    legacy-community.ine.com
    my.ine.com
    rentals.ine.com
    security.ine.com
    shop.ine.com
    showcase.ine.com
