---
title: "HackTheBox Alert"
date: "January 6, 2025"
description: "Cross site scripting to Local File Inclusion on Markdown file."
difficulty : "Easy"
opsystem : "Linux"
---

![Alert](https://github.com/user-attachments/assets/bf9126f2-63f5-4d39-b32a-23195cc79374)

# HackTheBox - Alert

### Reconnaisance & Information Gathering

    ┌──(blackcat㉿threatactor)-[~/Desktop/htb-alert]
    └─$ sudo nmap -Pn -sV alert.htb
    [sudo] password for blackcat: 
    Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-06 22:20 WIB
    Nmap scan report for alert.htb (10.10.11.44)
    Host is up (0.080s latency).
    Not shown: 998 closed tcp ports (reset)
    PORT   STATE SERVICE VERSION
    22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
    80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
    Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
    
    Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
    Nmap done: 1 IP address (1 host up) scanned in 8.28 seconds

Scan the machine with nmap to discover open ports and running service. Found two open ports, 22 (ssh) and 80 (http)

    ┌──(blackcat㉿threatactor)-[~/Desktop/htb-alert]
    └─$ dirsearch -u alert.htb       
      _|. _ _  _  _  _ _|_    v0.4.3
     (_||| _) (/_(_|| (_| )
    
    Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25
    Wordlist size: 11460
    
    Target: http://alert.htb/
    
    [22:20:29] Starting: 
    ...
    ...
    [22:20:55] 200 -   24B  - /contact.php
    [22:20:55] 301 -  304B  - /css  ->  http://alert.htb/css/
    [22:21:06] 301 -  309B  - /messages  ->  http://alert.htb/messages/
    [22:21:16] 403 -  274B  - /server-status/
    [22:21:16] 403 -  274B  - /server-status
    [22:21:23] 403 -  274B  - /uploads/
    [22:21:23] 301 -  308B  - /uploads  ->  http://alert.htb/uploads/
    
    Task Completed


Since there is a web service running on this machine, we performed directory enumeration using dirsearch to discover the directories available on the web. We found several directories.

We can access the website to understand how it functions. This website is a markdown viewer website. We can upload a markdown file and view (render) it on this website.

![image](https://github.com/user-attachments/assets/1ed03935-1afb-46c3-bed6-a023cf3bec5a)

> Markdown is a lightweight markup language for creating formatted text using a plain-text editor. John Gruber created Markdown in 2004 as an easy-to-read markup language. Markdown is widely used for blogging and instant messaging, and also used elsewhere in online forums, collaborative software, documentation pages, and readme files. 
>
> source: [wikipedia.org](https://en.wikipedia.org/wiki/Markdown)

Try to upload a markdown file. The website will render the uploaded markdown file and we can obtain a link to the uploaded markdown file by using the 'Share Markdown' button.

    # test
    ## im heker
    
    test markdown

![image](https://github.com/user-attachments/assets/632a1e4d-a017-4c1a-80f7-18035fb28408)

The cool thing about Markdown is that we can include HTML and JavaScript within it, and it will be rendered. Try inserting an XSS payload into the Markdown file and then upload it. If the website is vulnerable to XSS, the payload will be executed.

We'll use `<script>alert('heker')</script>` payload. This payload is commonly used for testing xss vulnerability. This is a javascript code that will display a dialog box (alert) in the browser with the message "heker".

    # test
    ## im heker
    
    test xss payload
    <script>alert('heker')</script>

![image](https://github.com/user-attachments/assets/57d46eaf-63d1-4103-88a6-681e892cfa6e)

> Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts are injected into otherwise benign and trusted websites. XSS attacks occur when an attacker uses a web application to send malicious code, generally in the form of a browser side script, to a different end user. Flaws that allow these attacks to succeed are quite widespread and occur anywhere a web application uses input from a user within the output it generates without validating or encoding it.
>
> An attacker can use XSS to send a malicious script to an unsuspecting user. The end user’s browser has no way to know that the script should not be trusted, and will execute the script. Because it thinks the script came from a trusted source, the malicious script can access any cookies, session tokens, or other sensitive information retained by the browser and used with that site. These scripts can even rewrite the content of the HTML page.
>
> source: [owasp.org](https://owasp.org/www-community/attacks/xss/)


