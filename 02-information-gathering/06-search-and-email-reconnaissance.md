# Search and Email Reconnaissance

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 264–533. Examples are lab-specific and need verification.

### **Google Dorks**

Internet Archive : https://web.archive.org/  this is waybackmachine

- google dorks:
    1. site:ine.com          ( where all results ine.com related)
    2. site:ine.com inurl:admin
    3. site:ine.com inurl:forum
    4. site:*.ine.com          ( it will show sub domains for I need)
    5. site:*.ine.com inurl:admin
    6. site:*.ine.com intitle:admin
    7. site:*.ine.com filetype:pdf
    8. site:ine.com employees or instructors
    9. intitle:index of        ( common vul within web servers)
    10. cache:ine.com
    11. inurl:auth_user_file.txt
    12. inurl:passwd.txt

    *** GHDB—google hacking database

**Email Harvesting with theHarvester**

- theHarvester   ( this is passive enum tool works with OSINT )

    >theHarvester -d ine.com -b baidu,bevigil,bing,bingapi,brave,bufferoverun,censys,certspotter,criminalip,crtsh,dehashed,dnsdumpster,duckduckgo,fullhunt,github-code,hackertarget,hunter,hunterhow,intelx

    - output

        ## [*] Hosts found: 95

        - .ine.com

        1pass-scim.ine.com

        1pass-scim.ine.com:35.227.112.188

        admin-api.ine.com:3.209.49.29

        admin.ine.com:75.140.41.9

        admin.showcase.ine.com

        admin.showcase.ine.com:216.239.32.21

        ads.ine.com:64.22.127.46

        apparel.ine.com

        assets.ine.com

        assets.ine.com:18.155.202.85

        b.ine.com

        bid46yz.45160067t.help.ine.com:158.247.19.249

        bid47mj.45160067m.email.ine.com:158.247.23.73

        blog.ine.com:44.199.137.201

        blog.ine.com:75.140.41.19

        bootcamps.ine.com

        bz719.e.ine.com:223.165.116.47

        bz720.billing.ine.com:223.165.117.227

        careers.ine.com

        certs.ine.com

        checkout.ine.com:13.227.74.73

        chef01.ine.com:52.71.19.199

        clicks.ine.com

        clicks.ine.com:108.138.128.48

        community.development.ine.com:3.80.85.11

        compliance.ine.com

        content-api.development.ine.com

        content-api.ine.com

        content-api.ine.com:54.211.233.49

        content-api.staging.ine.com

        courses.ine.com:3.216.42.5

        dashboard.development.ine.com

        dashboard.ine.com

        dashboard.staging.ine.com

        dashboard2.development.ine.com

        development.ine.com

        events.development.ine.com

        events.ine.com

        events.ine.com:18.238.49.129

        feedback.my.ine.com

        feedback.my.ine.com:192.241.183.155

        get.ine.com

        helpdesk.ine.com

        helpdesk.serviceportal.ine.com

        inedid.az.demos.ine.com

        info.ine.com

        internal.ine.com

        labs.ine.com

        learn.ine.com

        legacy-community.ine.com

        live.ine.com:75.140.41.227

        logs.ine.com:50.16.129.90

        marketing.ine.com

        media1.ine.com:75.140.41.39

        members.ine.com:52.44.139.85

        my.development.ine.com:13.227.74.42

        my.ine.com

        my.ine.com:3.169.183.59

        pritunl.ine.com

        pritunl.ine.com:34.206.234.208

        profiles.ine.com:52.201.209.93

        racks.ine.com:24.172.112.44

        racks2.ine.com:24.172.112.44

        racks2.ine.com:75.140.41.68

        rancher-eks.ine.com

        rancher-eks.ine.com:34.234.42.250

        rancher-eks.rancher.ine.com:54.225.200.251

        rancher.ine.com

        rancher.ine.com:34.238.92.57

        releases.ine.com

        rentals.ine.com:54.241.208.226

        scrack-vpn.ine.com:75.140.41.125

        security.ine.com

        security.ine.com:141.193.213.11

        shop.ine.com

        shopify.ine.com:104.236.221.73

        showcase.ine.com

        showcase.ine.com:216.239.34.21

        sonar.my.development.ine.com

        sonar.my.development.ine.com:108.139.10.42

        staging.ine.com

        statistics.ine.com:54.175.128.39

        status.ine.com

        store.ine.com:75.140.41.18

        subscriptions.development.ine.com:18.208.68.251

        subscriptions.ine.com:52.201.209.93

        support.ine.com:75.140.41.26

        try.ine.com

        uaa.development.ine.com:50.17.32.88

        updates.ine.com:23.21.86.19

        vid.ad.demos.ine.com

        vorack-vpn.ine.com:75.140.41.126

        workbooks.ine.com:108.138.246.78

        www2.ine.com

    >theHarvester -d ine.com -b duckduckgo,yahoo,bing,baidu
    **Output:**

    ## [*] Emails found: 7

    [e@hooine.com](mailto:e@hooine.com)

    [eason@ryine.com](mailto:eason@ryine.com)

    [emailthenose@arrowine.com](mailto:emailthenose@arrowine.com)

    [info@presenceafricaine.com](mailto:info@presenceafricaine.com)

    [lasse.rousi@medixine.com](mailto:lasse.rousi@medixine.com)

    [u@hblightshine.com](mailto:u@hblightshine.com)

    [u@hbligine.com](mailto:u@hbligine.com)

    [*] No people found.

    ## [*] Hosts found: 8

    R3.ine.com

    blog.ine.com

    checkout.ine.com

    info.ine.com

    learn.ine.com

    members.ine.com

    my.ine.com

    showcase.ine.com

Free to test this or to perform reconnaissance on this domain zonetransfer.me site

**Leaked Password Databases**

- haveibeenpwned.com site
