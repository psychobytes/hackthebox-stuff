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

Because there is a web service on this machine, do directory enumeration with dirsearch to discover directories that are on the web. We found several directories.

Try accessing the website to find out how this website works.

![image](https://github.com/user-attachments/assets/1ed03935-1afb-46c3-bed6-a023cf3bec5a)

This is Markdowdn Viewer website. There is an upload button on the main page, we can upload a markdown file and view it.

> Markdown is a lightweight markup language for creating formatted text using a plain-text editor. [Wikipedia](https://en.wikipedia.org/wiki/Markdown)

We can try to create a markdown file and upload it. The web will render the markdown file that we uploaded. We also can get a link from the markdown file that we uploaded using the share markdown button.

![image](https://github.com/user-attachments/assets/632a1e4d-a017-4c1a-80f7-18035fb28408)

Cool thing about markdown is, we can put html and js script inside it and it will rendered. Try to put xss payload inside the markdown then upload it. If the web is vuln, xss will triggered.

![image](https://github.com/user-attachments/assets/57d46eaf-63d1-4103-88a6-681e892cfa6e)


