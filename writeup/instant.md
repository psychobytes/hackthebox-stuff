---
title: "HackTheBox Instant"
date: "December 21, 2024"
description: "Reverse Engineering APK file to obtain jwt token and uncover api endpoint, exploit LFI in API via swagger to gain full access to server"
difficulty : "Medium"
opsystem : "Linux"
---

![Instant](https://github.com/user-attachments/assets/a1ce74dd-6b94-44f5-b213-5819df962d6e)

# HackTheBox - Instant

### Reconnaisance & Information Gathering
```
┌──(blackcat㉿threatactor)-[~/Desktop/htb-instant]
└─$ sudo nmap -Pn -sV instant.htb
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-30 14:56 WIB
Nmap scan report for instant.htb (10.10.11.37)
Host is up (0.058s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 9.6p1 Ubuntu 3ubuntu13.5 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.58
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.61 seconds
```
First, we scan the machine with nmap to discover open ports and running services. There are two open ports in this machine, 22 (ssh) and 80 (http).

![image](https://github.com/user-attachments/assets/f16a1c1f-7ee6-443f-9383-04e4cc8c6f03)

Visiting the website on port 80 reveals that this website is a landing page to download Instant app. In this box, Instant is a mobile application for transferring funds to various banks and crypto wallets. If we click download now button, instant.apk automatically downloaded.

#### Reversing instant.apk using jadx
We can do reverse engineering to disassemble instant application. With reverse engineering we can find out how the application works, the vulnerabilities in it, the resources that app used (sometimes mobile applications use API), hardcoded credentials (API key), and so on. We can do mobile app reverse engineering with jadx-gui.

> JADX GUI is an open-source tool designed for decompiling Android applications, allowing users to convert APK files into readable Java code. It is widely used by security researchers and developers for analyzing and understanding the inner workings of Android apps.

We can run jadx with command :
```
$ jadx-gui
```

![image](https://github.com/user-attachments/assets/3d2561d8-3f90-44e7-90d6-c5f244ffb30d)

Select instant.apk file on jadx and the app is automatically decompiled.

> Decompilation is the process of converting compiled code (such as bytecode or machine code) back into a higher-level programming language that is more understandable to humans. This is often done to analyze, understand, or modify software when the original source code is not available.

After instant.apk has been decompiled, the next step is that we can look for interesting information in the instant application. We can find api endpoints used by the app, hardcoded credentials and so on.

