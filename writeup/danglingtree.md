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

#### Web Enumeration
<img width="1820" height="829" alt="image" src="https://github.com/user-attachments/assets/14325305-3e17-4b43-89c5-b465f09cd145" />
<img width="1271" height="850" alt="image" src="https://github.com/user-attachments/assets/e5bfe800-191a-4499-9f91-a37e1a57cfbd" />
<img width="1824" height="945" alt="image" src="https://github.com/user-attachments/assets/923baea5-adbc-4218-9b22-03a27e6a1124" />

