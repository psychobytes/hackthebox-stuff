---
title: "HackTheBox LinkVortex"
date: "December 11, 2024"
description: "Information Disclosure (.git) to get admin credentials, Exploiting Ghost CMS vulnerability to Arbitrary File Read (Upload Symlinks), Use symlinks again to privilege escalation"
difficulty : "Easy"
opsystem : "Linux"
---

![LinkVortex](https://github.com/user-attachments/assets/0c38056e-9a54-40cd-b60b-da6e316eea64)

# HackTheBox LinkVortex Writeup

## Reconnaisance
- port scanning using nmap to discover open ports / running service. found 2 running service, web & ssh.
  ![image](https://github.com/user-attachments/assets/f65c40eb-a4ee-4899-9589-9834fabd9eb9)

- open the web, check tech stack & version of the web using wappalyzer. web using ghost cms (5.58).
  ![image](https://github.com/user-attachments/assets/622c607d-31a6-47f8-be3c-f1b1b22f4efa)
  ![image](https://github.com/user-attachments/assets/b13c4134-3771-477d-9af1-19a0b7a3d1b4)

- googling to find vulnerability on that service. found cve but require authenticated user to exploit.
  ![image](https://github.com/user-attachments/assets/ca3a7e38-e17e-4b24-8611-6efc35038e8d)
  ![image](https://github.com/user-attachments/assets/f6404e0d-2f7a-44a6-ad83-a437f9b7debc)
  
- recon again, use dirsearch to enumerate directories on the website. found robots.txt and sitemap.xml. 
  ![image](https://github.com/user-attachments/assets/6c9ce417-96e3-41e2-b700-ae1f743fc424)
  ![image](https://github.com/user-attachments/assets/84501c53-34f3-4e68-b901-ba43908e5ecc)

- we also found login page (from robots.txt) and admin username (author) from sitemap.xml
  ![image](https://github.com/user-attachments/assets/18d0a081-be62-44cc-b988-6ce3197579b0)
  ![image](https://github.com/user-attachments/assets/d2a967fd-7e41-4ff0-bbec-7c193c78a034)
  ![image](https://github.com/user-attachments/assets/4dc869e7-e143-4c59-9983-c21e01c1fbef)
  ![image](https://github.com/user-attachments/assets/f8015556-80ad-4d24-bda3-8c6072b965d8)

- enumerate subdomain using ffuf. found dev subdomain.
  ![image](https://github.com/user-attachments/assets/0b0e4007-406a-4bcb-bb27-79ef45208ca0)

- emumerate directory on dev subdomain, found .git directory.
  ![image](https://github.com/user-attachments/assets/506800bf-75b9-4575-95dc-b56c0728c7f2)

- dump .git directory using git-dumper.
  ![image](https://github.com/user-attachments/assets/fec4ad9e-0c4e-4176-8f7e-6b70f284ad0a)

- look around for credentials, we found password on /ghost/core/test/regression/api/admin/authentication.test.js. based on previous finding (author name from sitemap.xml) we can make assumption that email for admin is admin@linkvortex.htb and the password is 'OctopiFociPi*****'.
  ![image](https://github.com/user-attachments/assets/b9ca2a12-c86e-4592-b8ce-8427fe9f52b5)

- try logging in to check the credentials that were previously found. we're logged in, time to exploit the vulnerability we found previously (CVE-2023-40028).
  ![image](https://github.com/user-attachments/assets/2a6f2417-c815-439c-a399-8ab0be483ac6)


## Initial Access / Gaining Foothold
- use this PoC to exploit the vulnerability (https://github.com/0xyassine/CVE-2023-40028/). don't forget to change the target on the script and make it executable.
  ![image](https://github.com/user-attachments/assets/9ef95e33-b406-4b45-80aa-ad4e2b87433f)
  
- we can read all files on the system as long as the user that running the web has access to those files. try to read /etc/passwd to enumerate user but we didn't find the user.
  ![image](https://github.com/user-attachments/assets/117277e9-1c46-4cb8-99a3-87f7fc1619d1)
  
- we can look for credentials elsewhere. remember the dockerfile that we found in .git earlier? there is a config file directory location inside it.
  ![image](https://github.com/user-attachments/assets/fbe5db24-1e6d-4a38-9a3e-e2b16b5a108d)

- open the config file with the cve shell that we used before.
  ![image](https://github.com/user-attachments/assets/1ef3ce80-8936-44bf-85da-208a9984be81)

- login via ssh using that credentials. we're in and we can grab the user's flag.
  ![image](https://github.com/user-attachments/assets/e12f6fb8-0bc1-435f-82d5-add508fa97c4)


## Privilege Escalation to Root
- try to run "sudo -l" to see what bob can execute using sudo. we can run /opt/ghost/clean_symlink.sh as root but only with *.png argument.
  ![image](https://github.com/user-attachments/assets/64dca601-2de1-4501-b489-24f990059e82)

- read the script to figure out what it does and how it works.
  ![image](https://github.com/user-attachments/assets/6a8a4b0f-d244-47a7-ad50-2e23a7cb6eb7)

- we can use AI to explain how it works.
  ![image](https://github.com/user-attachments/assets/4b03870d-71c1-4e98-9fd0-892a84bcc5dc)

- so, the script is designed to manage symlinks that point to png files and there is some filter to etc and root files.
