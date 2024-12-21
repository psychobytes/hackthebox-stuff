---
title: "HackTheBox Greenhorn"
date: "December 7, 2024"
description: "Utilize information disclosure in Gitea to get credentials, Exploiting vulnerability at pluck import module, and Privesc by depixelizing redacted credentials in a document."
difficulty : "Easy"
opsystem : "Linux"
---

![image](https://github.com/user-attachments/assets/47e26060-f0dc-4dec-8334-b50c8f4075ff)

# HackTheBox - Greenhorn

### Reconnaisance & Information Gathering
scan open port / running service using nmap. there are 3 open ports, ssh and web (port 80 and 3000).

![image](https://github.com/user-attachments/assets/1f54d4da-e8c3-44d0-b659-ab23c80d7b4a)

check the first site (port 80). it says powered by pluck at the bottom of the website. thats mean the web using pluck.

![image](https://github.com/user-attachments/assets/75b7ae72-a0ab-4e02-a756-143ed9b0b708)

enumerate first web (pluck) dir using dirsearch. there is login.php page.
   
![image](https://github.com/user-attachments/assets/48653684-a296-4a0a-8d09-b547d4bc7b98)
   
![image](https://github.com/user-attachments/assets/29611688-ec15-431c-b1d6-55bae2db9c9b)

on the login page it says pluck 4.7.18. we get the version of pluck used on that web. there is a vulnerability on that version. but for now let's skip it and try the second web enumeration.

![image](https://github.com/user-attachments/assets/b807854e-a56a-4a4a-93b0-b4b368dad98d)
   
check the second site (port 3000). it is the gitea web (used for version control system / repository).

![image](https://github.com/user-attachments/assets/7f1342c2-80d5-44cf-8a8e-bc6857eb4d56)

check the explore page to see public repos, there is a repo with the name "greenadmin / greenhorn".

![image](https://github.com/user-attachments/assets/d3660bc5-fc08-465a-b181-7e28ef22a292)

look around at the repo, there is hash at "/data/settings/pass.php". crack the hash using crackstation.net. hash cracked, use that pass for login at the first site.

![image](https://github.com/user-attachments/assets/b02df3c8-a5fa-4f9b-b093-ba03d447ef1c)

![image](https://github.com/user-attachments/assets/8b61de4a-5a22-4a12-a3e6-ba3c109482e1)

![image](https://github.com/user-attachments/assets/84a60c4e-05d1-4424-85d7-cc76510a2e1d)


### Initial Access & Foothold
we're in. remember the previous vulnerability at pluck that we found ? based on packetstorm website, we can upload fake module to the site and execute it. try uploading revshell and gaining foothold. we can use php revshell from pentestmonkey, zip it, and upload it to install modules page (options >> manage modules >> install modules). don't forget to change the ip and port at revshell php file and set up a listener.

![image](https://github.com/user-attachments/assets/d759a563-f84a-4468-8275-8f84a7357b28)

![image](https://github.com/user-attachments/assets/6a141f74-5851-4acf-bbd3-4b76d302f445)

![image](https://github.com/user-attachments/assets/67eac8b6-2330-483b-bb18-bee6fa74b2b3)

we got shell :3

![image](https://github.com/user-attachments/assets/f60ace1b-4239-47cb-a379-0ebb05b8daa0)

we got foothold at www-data user, try using the same password to login as user. to figure out who is the user we can simply ls the home dir. don't forget to grab the flag.
    
![image](https://github.com/user-attachments/assets/0ad98ca5-54c2-470a-a781-12ebaa7df161)


### Privilege Escalation
now time to privesc. try to get more stable shell via ssh.

![image](https://github.com/user-attachments/assets/c752c5ac-d2a7-4885-88a1-c6dbbb321408)
    
we can't login via ssh, there is no .ssh dir on user so there is no ssh key to log in. we stuck in this shell.

![image](https://github.com/user-attachments/assets/c54a578a-8a74-44a4-9fab-46007f17aab0)

there is a pdf in user dir. maybe that's a hint, but we can't transfer it since we stuck in pentestmonkey shell and can't use ssh. we can transfer the pdf file using netcat.

![image](https://github.com/user-attachments/assets/19771717-c019-47f8-9ec2-176054fdc450)

![image](https://github.com/user-attachments/assets/3d0d2660-82e3-47dc-a77c-1c98be0e49c7)

open the pdf file, there is password but blurred like JAV lol.

![image](https://github.com/user-attachments/assets/b86896ff-501e-47b0-a0f5-6b99efaca65c)

If you often watch JAV, maybe you know the term decensored, we can use similiar technique here. [thehackernews.com](https://thehackernews.com/2022/02/this-new-tool-can-retrieve-pixelated.html)

![image](https://github.com/user-attachments/assets/654f980e-bd7f-4e60-aa6c-48058a3032a6)

extract the image from pdf using pdfimages.

![image](https://github.com/user-attachments/assets/89b25b41-c18d-4507-aeff-fb55089d20d3)

use depix to depixelize the image and we got the password.

![image](https://github.com/user-attachments/assets/f2617f46-aed3-4ad8-b7b3-3f57426365f6)

![image](https://github.com/user-attachments/assets/28337574-aaf6-4698-8e13-161e5f2e59de)

switch to root user and grab the root flag. machine pwnd :3

![image](https://github.com/user-attachments/assets/668c206c-0065-4178-a95e-bc710294e1e3)
