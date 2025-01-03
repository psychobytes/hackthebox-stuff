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

Best way to start mobile app reversing (in context of pentesting) is looking for interesting string like "http://, authorization, auth, key, password, etc.". Search "http://" string using text search button in jadx. We can find various api endpoints or resources used by the application.

![image](https://github.com/user-attachments/assets/24bf5f4d-dd9b-4d87-af97-7e9cd81caef6)

We found some api endpoints and that api is a subdomain to our target (instant.htb). Add that subdo to /etc/hosts in our machine and we can access that api.

![image](https://github.com/user-attachments/assets/84d9b880-ffa0-485a-9080-bc872b114ad0)

We had 401 error (Unauthorized) when accessing the api endpoint. In API usually there are three methods to authenticate, basic auth, jwt, and api key. Search "authorization" in jadx and we found that auth token. (btw if you pay attention, you actually don't need to do this step since we already got that auth token by searching "http://")

![image](https://github.com/user-attachments/assets/e816caac-3d6a-4f7f-b0f7-cae671fa39e8)

The auth token is a string with random letter and separated by dots. That is a sign that token is a JWT token.

> JWT, which stands for JSON Web Token, is an open standard for securely sharing JSON data between parties. The data is encoded and digitally signed, which ensures its authenticity. JWT is widely used in API authentication and authorization workflows, as well as for data transfer between clients and servers. source: [https://blog.postman.com/what-is-jwt/](https://blog.postman.com/what-is-jwt/)

![image](https://github.com/user-attachments/assets/d862023d-635c-443c-a6a8-c96060f17a74)

Use jwt.io website to decode the token. As we can see that token is actually admin token, that means we can use that token to interact with the api as admin.

![image](https://github.com/user-attachments/assets/96cb07c5-a14f-4de7-9510-914c7db9bfc0)

We got 500 Internal Server Error response. The response is no longer 401 unauthorized, that means the token is valid and we are authenticated.

Another approach is by looking at AndroidManifest.xml file. In this case, we don't need to do this because we will get the same results as before (only api endpoint and jwt token).

> AndroidManifest.xml file describes essential information about your app to the Android build tools, the Android operating system, and Google Play. The manifest file is required to declare the components of the app (including all **activities**, services, broadcast receivers, and content providers), permissions that the app needs in order to access protected parts of the system or other apps, and the hardware and software features the app requires.
>
> Activities is a single, focused thing that the user can do (function). Almost all activities interact with the user.
>
> source: [https://developer.android.com/guide/topics/manifest/manifest-intro](https://developer.android.com/guide/topics/manifest/manifest-intro)

Look at the configuration file in the application. Config files are usually located at res directories, usually in subdirectories like res/xml or res/values. 

![image](https://github.com/user-attachments/assets/fe6da44d-ad96-489b-8ac0-ddd6e07d1f77)

There is network_security_config.xml file in res/xml directories. We found another subdomain (swagger-ui.instant.htb). Add the subdomain to /etc/hosts files in our machine, and access it via web browser.

![image](https://github.com/user-attachments/assets/149929ec-f30f-4e52-9de3-37b8a85a463a)

> Swagger is a set of open-source tools built around the OpenAPI Specification that can help to design, build, document, and consume REST APIs. Swagger-UI is an interactive api documentation with the visual documentation making it easy for back end implementation and client side consumption.
> source: [https://swagger.io/docs/specification/v3_0/about/](https://swagger.io/docs/specification/v3_0/about/)

Use the JWT token that we found earlier to authenticate at swagger. After authenticated, we can use the swagger.

![image](https://github.com/user-attachments/assets/a5f9b6d0-7456-40d2-9852-8ed30a79ecad)

### Foothold

There are several api endpoints in the swagger. Endpoint logs are quite interesting to me. We can list all available logs (/view/logs) and we can also read the contents of the log files (/read/log).

![image](https://github.com/user-attachments/assets/7b4df2b5-63c8-4f82-aa72-34cae2e30968)

Try /view/logs endpoint to list all available logs. This endpoint doesn't require parameters so we can execute it straight away.

![image](https://github.com/user-attachments/assets/7d6a7e47-2939-49a3-bd76-e95684a88d5d)


```
{
  "Files": [
    "1.log"
  ],
  "Path": "/home/shirohige/logs/",
  "Status": 201
}
```

There is 1.log file on /home/shirohige/logs. We can read the content of 1.log file using /read/log endpoint. Fill the log_file_name parameter with the log file name that we obtained previously (1.log)

![image](https://github.com/user-attachments/assets/b29bb5c3-3b2a-4444-a94b-a9e40f428a26)

```
{
  "/home/shirohige/logs/1.log": [
    "This is a sample log testing\n"
  ],
  "Status": 201
}
```

The /read/log endpoint works by reading log files in the /home/shirohige/logs/ directory. Then we need to enter the log name parameter (1.log) to read the log file. So enpoint will read the file /home/shirohige/logs/1.log.

What if we try to use this endpoint to read another file. Because this endpoint reads files in the /home/shirohige/logs/ directory, maybe we can do path traversal to read files in other directories. We can try reading the /etc/passwd file by replacing the log name parameter with ../../../../../../etc/passwd.

![image](https://github.com/user-attachments/assets/46ae5bd7-aefc-47c5-a29b-be52bc6a1576)

Boom! it works haha :D This endpoint has a Local File Inclusion (LFI) vulnerability.

> Local File Inclusion [LFI]
>
> The File Inclusion vulnerability allows an attacker to include a file, usually exploiting a “dynamic file inclusion” mechanisms implemented in the target application.
>
> Local file inclusion (also known as LFI) is the process of including files, that are already locally present on the server, through the exploiting of vulnerable inclusion procedures implemented in the application. This vulnerability occurs, for example, when a page receives, as input, the path to the file that has to be included and this input is not properly sanitized, allowing directory traversal characters (such as dot-dot-slash) to be injected.
>
> source : [owasp.org](https://owasp.org/www-project-web-security-testing-guide/v42/4-Web_Application_Security_Testing/07-Input_Validation_Testing/11.1-Testing_for_Local_File_Inclusion)

We can abuse the LFI vulnerability in this endpoint to read any file on the server as long as we know the name of the file and as long as this application is running with the same or above privileges with the file we want to read.

Try to grab the id_rsa file in shirohige home directory so we can log in via ssh as shirohige.

![image](https://github.com/user-attachments/assets/1c351fca-a379-4998-9015-4571624df9e0)

```
{
  "/home/shirohige/logs/../.ssh/id_rsa": [
    "-----BEGIN OPENSSH PRIVATE KEY-----\n",
    "b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcn\n",
    ....
    "5VNy/4CNnMdXALx0OMVNNoY1wPTAb0x/Pgvm24KcQn/7WCms865is11BwYYPaig5F5Zo1r\n",
    "bhd6Uh7ofGRW/5AAAAEXNoaXJvaGlnZUBpbnN0YW50AQ==\n",
    "-----END OPENSSH PRIVATE KEY-----\n"
  ],
  "Status": 201
}
```
