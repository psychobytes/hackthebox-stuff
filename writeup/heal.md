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

> Information that we collected so far :
>
> there are 3 domain on target (heal.htb, api.heal.htb, take-survey.heal.htb)
>
> heal.htb is the frontend, api.heal.htb is the backend (Ruby on Rails 7.1.4)
>
> web feature and api endpoint (resume, download, profile)

### Initial Access & Foothold
after we carried out information gathering and reconnaisance, we got quite a lot of information about the target. with this information we know how the service or target works and the attack surface of the target. with sufficient information about the target, we can carry out analysis and look for vulnerabilities in the target.

download the resume and intercept the traffic using burpsuite. forward the request until we get request at download endpoint.
![image](https://github.com/user-attachments/assets/75e972c2-39af-41b0-bc75-a23940e05075)

pay attention to the following request. at the request line (the firsr line of the http request) we 
![image](https://github.com/user-attachments/assets/16116ce9-ed63-461a-b5be-0f1f73ea9785)



