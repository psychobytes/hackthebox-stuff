---
title: "HackTheBox Heal"
date: "December 17, 2024"
description: "Exploiting Local File Inclusion at Ruby on Rails API, Remote Code Execution on LimeSurvey and Consul by HashiCorp"
difficulty : "Medium"
opsystem : "Linux"
---

![Heal](https://github.com/user-attachments/assets/98f3936b-049d-44de-87ab-3fdb209130fc)

# HackTheBox - Heal

### Reconnaisance & Information Gathering
scan open port / running service using nmap. there are 2 open ports ssh and http.
![image](https://github.com/user-attachments/assets/13cf5298-62a5-4e66-b9e6-0df9378dd252)

we know that there is port 80 (http) open. that means there is a web service running. visit the website heal.htb or machine_ip:80. this website can be used to create a resume. there is a form to login. we can try to sign up, but it's better to enumerate it first to get more information about the target.
![image](https://github.com/user-attachments/assets/2e83da8f-b0af-40e2-af06-ea9b8e2ab428)

enumerate directories and subdomains on the website to obtain more information about targets and expand the attack surface.
![image](https://github.com/user-attachments/assets/4e56067b-91fd-4cd3-808f-29865c875c79)
![image](https://github.com/user-attachments/assets/2e5b44e9-ca03-4440-a397-8a06ef43f247)

we don't get any interesting info from directory enumeration, but we found a subdomain (api.heal.htb). from the index page at the api subdomain, we can see that the web service is Ruby on Rails version 7.1.4.
![image](https://github.com/user-attachments/assets/29b7ce8d-a4e7-4321-a9a4-280254ae9aac)

analyze how the website works and operates to gain more insight about target. we can try various features in it and maybe we can find vulnerabilities. try to sign up on the main website.

we automatically log in after signing up and we are directed to the resume page. On this page there is a resume builder feature. There are profile, survey and logout buttons at the top. At the very bottom of the page there is an export as pdf button which functions to download the resume you have built.
![image](https://github.com/user-attachments/assets/5a893625-93f4-443a-8308-eccac8961a03)

if we do further enumeration on the api.heal.htb subdomain, we can find several api endpoints that match with the features in the main domain (heal.htb). for example, on the heal.htb page there are features for creating a resume, viewing profiles, and downloading resume. and in the api.heal.htb subdomain there are resume, profile, and download endpoints. so we can conclude that the domain heal.htb is the frontend and api.heal.htb is the backend.
![image](https://github.com/user-attachments/assets/5e2c87fc-a8ac-40c7-bef6-cdfe82726209)
![image](https://github.com/user-attachments/assets/9ef737a3-f1e2-4157-af8c-f7400db7172c)

there is other interesting findings. we found other subdomain on the survey page (take-survey.heal.htb). we can access it by pressing the survey button then press take the survey button at survey page.
![image](https://github.com/user-attachments/assets/09563ee6-07a7-45f9-b313-f575bec33016)
![image](https://github.com/user-attachments/assets/3d0c9057-aef0-4d68-bdbc-d1b1c6db4da6)

if we go to the index.php page we can find out that there is an admin user (ralph@heal.htb). we also know that the subdo using LimeSurvey.
![image](https://github.com/user-attachments/assets/dce88738-f6ea-445d-9d9c-6eb29c073b43)

we also found login page if we do directory enumeration using dirsearch.
![image](https://github.com/user-attachments/assets/a62b0eb2-e54b-46c9-a38c-f8a0b251d385)
![image](https://github.com/user-attachments/assets/a81f9816-0057-41c0-82ff-7a25b099f4bd)

after we carried out information gathering and reconnaisance, we got quite a lot of information about the target. with this information we know how the service or target works and the attack surface of the target. with sufficient information about the target, we can carry out analysis and look for vulnerabilities in the target.

> Information that we collected so far :
>
> there are 3 domain on target (heal.htb, api.heal.htb, take-survey.heal.htb)
>
> heal.htb is the frontend, api.heal.htb is the backend (Ruby on Rails 7.1.4)
>
> web feature and api endpoint (resume, download, profile)
>
> take-surver.heal.htb using LimeSurvey
>
> there is an admin named ralph (ralph@heal.htb)

### Initial Access & Foothold
download the resume and intercept the traffic using burpsuite. forward the request until we get request at download endpoint.
![image](https://github.com/user-attachments/assets/75e972c2-39af-41b0-bc75-a23940e05075)

pay attention to the following request. at the request line (the first line of the http request) we make a get request to the /download endpoint with the ?filename= parameter. We can assume that this request aims to retrieve a file in a directory.
![image](https://github.com/user-attachments/assets/16116ce9-ed63-461a-b5be-0f1f73ea9785)

we can abuse this feature to retrieve any file in the server (example: /etc/passwd). we managed to get a response of 200 (ok) and data from /etc/passwd. that means the /download endpoint has a local file inclusion vulnerability.
![image](https://github.com/user-attachments/assets/86068889-e580-48e8-8d10-2b3a5256bdc1)

> Local File Inclusion [LFI]
>
> The File Inclusion vulnerability allows an attacker to include a file, usually exploiting a “dynamic file inclusion” mechanisms implemented in the target application.
>
> Local file inclusion (also known as LFI) is the process of including files, that are already locally present on the server, through the exploiting of vulnerable inclusion procedures implemented in the application. This vulnerability occurs, for example, when a page receives, as input, the path to the file that has to be included and this input is not properly sanitized, allowing directory traversal characters (such as dot-dot-slash) to be injected.
>
> source : [owasp.org](https://owasp.org/www-project-web-security-testing-guide/v42/4-Web_Application_Security_Testing/07-Input_Validation_Testing/11.1-Testing_for_Local_File_Inclusion)

we can ask AI for directory structure of Ruby on Rails and sesitive info inside it. by knowing the directory structure and sensitive files in it, we can look for files that most likely contain credentials in them to gain initial access.
![image](https://github.com/user-attachments/assets/5ceb2783-e70b-43e0-b31c-0cedd16638b8)

database.yml file contain information about the database that being used. we can see there are two databases at /storage directory (test.sqlite3, and development.sqlite3).
![image](https://github.com/user-attachments/assets/37eaf178-52ac-4146-8db6-fbcbeb26da7d)

based on the database.yml file development.sqlite3 is the database used by the target in production. open the file to obtain the credentials. development.sqlite3 seems to contain the credentials for web heal.htb. There is a user that we use when registering and user ralph (web administrator).
![image](https://github.com/user-attachments/assets/5cd16f98-6eeb-444b-88cb-c30b0504e803)

crack ralph password hash to get the password for ralph account. we must identify the type of hashing algorithm used in the hash. to identify hash type we can use hash identifier ([hashes.com](https://hashes.com/en/tools/hash_identifier).
![image](https://github.com/user-attachments/assets/83330b9e-0cc4-4315-b015-262f7bab755d)

crack the hash using hashcat.
![image](https://github.com/user-attachments/assets/f95741d0-175b-40e0-b87f-517dc1c9bf5e)
![image](https://github.com/user-attachments/assets/db866552-4a15-4f2d-866f-5498b2bde297)

based on our finding earlier while doing reconnaisance (at subdo / LimeSurvey) and while we testing LFI vulnerability (get /etc/passwd), we knew that user ralph is exist. try to login via ssh using cracked password.
![image](https://github.com/user-attachments/assets/727ad4a2-14b7-4e72-ad7a-4882e6c6d7f4)

we can't log in as ralph via ssh, maybe the password is wrong or maybe ralph dones't have access to ssh. since ralph is the web admin, we try logging in as ralph on the heal.htb web maybe we can find an additional feature that the admin has. but we didn't find additional feature that admin usually has (example: dashboard).
![image](https://github.com/user-attachments/assets/f1ac9225-b2e3-4c95-96a4-7b7c9b05ad88)

try logging in elsewhere. during recon we find the subdo take-survey.heal.htb. maybe we can try to log in there. and we are logged in.
![image](https://github.com/user-attachments/assets/d708a5c3-aa95-4357-bd8b-698f8dbfeafc)

search for information about limesurvey vulnerabilities or exploits on google.
![image](https://github.com/user-attachments/assets/ceac8352-4363-41f6-8491-3998d467989d)

CVE-2021-44967 allows us to achieve remote code execution via the plugin's upload and install functions. source : [nvd.nist.gov](https://nvd.nist.gov/vuln/detail/CVE-2021-44967)
![image](https://github.com/user-attachments/assets/c855e9f9-0d9f-46b5-859a-bb128014de04)

even though based on information from the nvd.nist.gov website that the vulnerability exists in limesurvey version 5.2.4 and limesurvey at our target using version 6.6.4, we can still exploit this feature because until now there has been no solution for this vulnerability since this vulnerability was disclosed. source : [pentest-tools.com](https://pentest-tools.com/vulnerabilities-exploits/limesurvey-524-rce-vulnerability_13029)
![image](https://github.com/user-attachments/assets/fde537ed-9a43-447e-b68a-aa4754608fad)

we can exploit this vulnerability using exploit from [https://github.com/Y1LD1R1M-1337/Limesurvey-RCE](https://github.com/Y1LD1R1M-1337/Limesurvey-RCE)
![image](https://github.com/user-attachments/assets/1ea6f0c3-7177-41e4-b730-352ce28c470c)

download the exploit, adjust ip address and port at php-rev.php file with listener. add compatibility configuration for version 6 in config.xml.
![image](https://github.com/user-attachments/assets/417db7c1-b559-4167-9717-b16f7e6c8860)
![image](https://github.com/user-attachments/assets/1effc095-24cb-4dc5-a9e2-5cf0a36f6895)

zip config.xml and php-rev.php into one zip file. the zip file name must be the same as the zip file name on github. save the zip file in the same directory as exploit.py.
![image](https://github.com/user-attachments/assets/f1325204-b944-4a18-8769-8eba06b4a77f)

set up netcat listener and run the exploit. we got shell as www-data :3
![image](https://github.com/user-attachments/assets/246388eb-0c80-47a6-8a07-01def3b53e2b)

### Privilege Escalation to User
we got shell access to the server as www-data. user flag is usually located in the user home directory. we need to perform privilege escalation to the user to get user flag. we can use linpeas to look for loopholes that can be exploited for privilege escalation.

> [LinPEAS](https://github.com/peass-ng/PEASS-ng/tree/master/linPEAS)
> LinPEAS is a script that search for possible paths to escalate privileges on Linux/Unix*/MacOS hosts.

move linpeas from host to target via python http server. set the http server at linpeas directory and download linpeas from target server using wget.
![image](https://github.com/user-attachments/assets/e87f864c-f597-4d14-8aa7-a91f0cbe8976)
![image](https://github.com/user-attachments/assets/16cac716-eb57-444d-a2ee-cfb2e32bdf83)

run linpeas.
![image](https://github.com/user-attachments/assets/4570db78-d461-4ee6-af97-97f237967542)

we found a password on a php file.
![image](https://github.com/user-attachments/assets/4ee8727b-bcd8-40f6-a6c5-2e8d858b9bfa)

access the php file and it turns out that the password used for the database.
![image](https://github.com/user-attachments/assets/553b8f8b-6ef9-4162-832b-244d892fb414)

even if it turns out that the password is a database password, there is a possibility that another user will use the same password. try logging in as ralph with that password. login failed. if you look in the home directory, there is a home directory for another user, ron. try logging in as ron with that password. login successful.
![image](https://github.com/user-attachments/assets/3edc1e70-41d8-4d6a-a51c-23ffeee19c0b)

don't forget to grab user's flag.
![image](https://github.com/user-attachments/assets/7aa11013-4b8c-418f-a6f9-1ea51731b6a8)

### Privilege Escalation to Root
first, we need to log in as ron via ssh to get more stable and better shell.
![image](https://github.com/user-attachments/assets/707e8771-d62a-4eef-b9bb-2b53b1ef4f7b)

check for listening port to discover running service using netstat.
![image](https://github.com/user-attachments/assets/6b77e127-7fee-4790-8b46-9b73a4bd01e1)

there is port 8500 listening. use curl to retrieve data from the listening port. we get a response in the form of html file that says moved permanently but there is a href that goes to the /ui/ directory. use curl to retrieve data from /ui/ directory, we got response again with html title consul by hashicorp.
![image](https://github.com/user-attachments/assets/5d3d7883-ee66-4305-8901-cf616e69ae93)

because port 8500 can only be accessed locally, we need to do port forwarding using ssh so we can access that resources.
![image](https://github.com/user-attachments/assets/dd570130-afd3-409b-969f-83dfac615255)

we can access that resources from our host.
![image](https://github.com/user-attachments/assets/5d8f133d-4711-471a-9a3c-ddda81ad1798)

look for information about vulnerabilities in Consul on the internet.
![image](https://github.com/user-attachments/assets/83c7336c-bc5b-458d-9bb8-ca6885860570)

> Consul by Hashicorp RCE
> 
> in a certain configuration of Hashicorp Consul, an unauthentication attacker may be able to archive remote command execution on the server. the necessary conditions that make an agent vulnerable to this attack are:
>
> - the API is available on an interface that can be accessed over the network.
> - script checks are enabled.
> - ACLs are disabled or an ACL token is compromised.
>
> given the above conditions, an attacker can register a check on a remote agent with a malicious payload. By design, script checks allow arbitrary code execution, so allowing service registration with checks enabled via an exposed API presents an RCE (remote code execution) threat.
>
> source: [hashicorp blog](https://www.hashicorp.com/blog/protecting-consul-from-rce-risk-in-specific-configurations)

we can check whether the configuration in the consul on the target are vulnerable and allows us to obtain RCE by visiting the endpoint /v1/check/self. because we access the consul directly from local (not over network, direct access from the server as a user via SSH port forwarding so we can access it from our host) and we can access the consul website, which means we are authorized. so we don't need to fulfill all the requirements above to obtain RCE. the only configuration we need is script checks enabled which is true in this case.
![image](https://github.com/user-attachments/assets/8f8ef186-3e87-4d32-8e86-339ef3b459a0)

we can use this exploit to obtain RCE. source: [exploit-db](https://www.exploit-db.com/exploits/51117)
![image](https://github.com/user-attachments/assets/9eb0c342-edd9-4529-babb-65d1f0e06874)

set a listener and run the exploit. we got root, machine pwned :3
![image](https://github.com/user-attachments/assets/ba6c5cd1-3adc-4e1d-b908-804e423ed3ef)
