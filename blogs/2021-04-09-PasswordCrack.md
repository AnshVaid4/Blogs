---
title: Cracking Passwords
author: Ansh Vaid
date: 2021-04-09 7:10:00 +0530
categories: [Cyber Security and Ethical Hacking]
tags: [CEH, EthicalHacking, CyberSecurity , attack, MITM, mitm, man in the middle, browser, password, crack, john, john the ripper, oph, loph, hydra, hydra-wizrd]
---

<img src="/assets/EthicalHacking/passwordcrackinbanner.PNG" alt="image1" height="375" width="900"/>
<caption>Image taken from <a href="https://www.familysearch.org/blog/en/wp-content/uploads/sites/2/2013/06/Password-Security-Shutterstock-124176472.jpg">here</a></caption>

---

In my last blog I discussed about Man In The Middle attack, also gave you a demo on how your connection can be intercepted and your data can be manipulated by the attacker. As I told in my last two blogs of **Cyber Security and Ethical Hacking** series, this blog will give you the information related to the password cracking techniques. 

**Attention Future Hackers**
It is mandatory to have a Kali Linux (Parrot OS works too). None other linux distro should be used, because the
tools and commands I am going to discuss are installed beforehand in the Kali Linux. In other distros you will
have to additionally download and install the packages from internet and various dependencies too. You are
understanding the concepts of hacking, so it is mandatory for you to have Kali inux at least.

---

**CAUTION: For practicing hacking always try for these two websites:**

---

<ul>
<li><a href="http://certifiedhacker.com/">http://certifiedhacker.com</a></li>
<li><a href="http://testphp.vulnweb.com/">http://testphp.vulnweb.com</a></li>
</ul>

**For practicing purpose there are other resources too, but as a beginner these two sites are recommended, other ways**
**will also be shared by me once you get the basic concepts, in my upcoming blogs. And sice you are practicing hacking,t**
**you should notry on some other websites other than the above two websites I mentioned, because you might end up breaking**
**something in other websites, also there are other security techniques implemented on those website which can keep**
**a track on you for doing malicious things and take some legal actions against you.**

---

**Also this blog on hacking is just for informative purpose. Kindly use the knowledge given below wisely and for ethical purpose only. You are here to learn cyber security, and not to harm people by using your knowledge in unethical way.**

---
<br>

---

# <u>What Is Password Cracking</u>
This is the most important phase of system hacking where you get the access to the hashes of the passwords, or sometimes the passwords are encrypted too, so you need correct algorithm to decrypt the password, to get the access of the user account whose password you got. Now again there are two scenrios, <br>
-> You will use it to recover your password, or your system administrator uses it to recover your passwords if you have forgotten it.<br>
-> Hackers use this to get unauthorized access to your account. And many of the accounts in the present day also have way too easy passwords.

## <u>Password Attacks</u>
There are 4 types of password attacks:
<ol>
<br>
<li><b><u>Non Electronic Attack:</u></b> No need of technical knowledge to crack the password.<br> -Shoulder Surfing<br> -Social Engineering<br> -Dumpster Diving</li>
<br>
<br>
<li><b><u>Active Online Attack:</u></b> Cracking password by continuously hitting to the target to get the hashes.<br> -Dictionary and Bruteforce attack<br> -Phishing<br> -Malwares<br> -Password Guessing <br> -NBT-NS/LLMNR poisoning</li>
<br>
<br>
<li><b><u>Passive Online Attack:</u></b> Just opposite of <b>Active Online Attack</b> where attacker don't have a direct connection to victim to crack passwords.<br> -<a href="https://blog.vulnfreak.org/posts/MITM/">Man In The Middle Attack</a><br> -Wire Sniffing<br> -Replay Attack</li>
<br>
<br>
<li><b><u>Offline Attack:</u></b> Attacker gets the hashes of victim from victim's device and cracks it in his own machine.<br> -Rainbow Table Attack<br> -Distributed Network Attack</li>
</ol>
<br>
<br>

# 1. <u>Non Electronic Attack</u>
## 1.1 <u>Social Engineering</u>
Social engineering is just an attack where the attacker tries to take advantage of human behaviour of trusting anyone easily. But attacker gets the credentials of the victim easily and use them later to access his account. Eg. Phishing, Pharming, Whaling etc.

## 1.2 <u>Shoulder Surfing</u>
Attacker is physically present behind you and is watching you typing you credentials, which he later uses to login to your account

## 1.3 <u>Dumpster Diving</u>
Attacker finds something important like password, pin of you card in the garbage that you threw as a waste.
<br>
<br>

# 2. <u>Active Online Attack</u>
## 2.1 <u>Dictionary Attack</u>
Attacker has a list of wordlist of password that the victim might be using, and tries them one by one to crack password.

## 2.2 <u>Bruteforce Attack</u>
The attacker tries each and every combination of word of each length to crack the password. Success rate is 100% but takes lot of time depending upon the password.

## 2.3 <u>Malwares</u>
The victim installed a malware, spyware or keylogger accidentally, rather they are hidden in some application or exe file, which run in background to share each and every information of victim to the target.

## 2.4 <u>NBT-NS/LLMNR Poisoning</u>
The service running in Windows OS, to share the files in a Local Area Network, when not in use, then stop this service. So the attacker gets the hashes of password by poisoning the service of victim. Usually done in older versions of Windows OS, will show this in some other blog.

## 2.5 <u>Password Guessing</u>
The attacker creates a list of passwords that the victim might be using and rate them of high to low probability. Checks them by entering them manually. Mainly done by those people who are very close to you.

## 2.6 <u>Password Dumping</u>
Attacker directly interacts with victim machine, and extract all the password hashes stored in the machine.
<br>
<br>

# 3. <u>Passive Online Attack</u>
## 3.1 <u>Wire Sniffing</u>
The attacker uses the tools like wireshark and pwdump to get all your packets being transferred, and analyzes them to get some important information such as passwords and user ID.

## 3.2 <u><a href="https://blog.vulnfreak.org/posts/MITM/">Man In The Middle Attack (MITM)</a></u>
As discussed in the last blog, I was able to see the password and the username of the victim machine. Also I was able to change them in my attacker's machine.

## 3.3 <u>Replay Attack</u>
The attacker gets the session ID OR token of the victim, and then uses the same token to login to the victim's account.
<br>
<br>

# 4. <u>Offline Attack</u>
## 4.1 <u>Creating Rainbow Tables</u>
The rainbow table consistes of the hashes of the dictionary or the bruteforced list, and those hashes are compared by the hashes captured by the attacker.

## 4.2 <u>Distributed Network Attack</u>
The password is cracked by a group of computers in a network, in order to get the speedy crack of the passwords. Each computer tries different word, the list is designed in such a way that there is no clashes in the wordlist. 
<br>
<br>

# <u>What Is SAM database in Windows?</u>
In windows OS, the passwords are stored is SAM database, in the NTLM hashed format. When you login in to your system after booting, the password you entered are matched with this file only. This file cannot be copied or moved or deleted from this path. Neither you can open this file, even if you open it then also the file is encrypted, you will unable to understand it. So the attacker performs the **Active Online Attack** to gets the password. He can dump the hashes from this file using the tool **Pwdump**. <br>

![hack](/assets/EthicalHacking/passwordcrackin1.PNG)

<br>
<br>

# <u>What is Shadow File in Linux?</u>
Just like you had a SAM database in windows to store all the password hashes of the user present on the sytem, in the same way, in linux there is a **Sahadow** file in **/etc/** directory, which stores the password of easch and every user present there. You can edit it unlike SAM file in Windows. Afterall the root user of Linux has more power than the Adminstrator of the Windows.

<br>
<br>

# <u>Password Cracking Tools</u>

## 1. <u>For Windows OS</u>
### 1.1 <u>L0phtCrack 6</u>
This is a vast tool for cracking the passwords from the hashes. You can customize this tool according to you. It provides you the interface where you can select the options to select the type of dictionary attack to perform, whether you need the alpha-numeric or only alphabets to use in dictionary. Also at the end of dictionary it starts with the bruteforce attack. Also it directly detects the hashes and username in the current system you are working, and starts performing the cracking for them. You can change those hashes with the file you got from pwdump tool. Following are the snapshots of L0phtCrack.<br>

![hack](/assets/EthicalHacking/passwordcrackin2.PNG) 

<br>

![hack](/assets/EthicalHacking/passwordcrackin3.PNG)

<br>

### 1.2 <u>Ophcrack</u>
Another great tool which uses the rainbow tables to crack the hashes. You ge the various options regarding what hashes they are, LM or NTLM, or you can directly load the file of pwdump and select the rainbow tables from the **Crack** option in its title bar. And start it to crack the hashes. Following are the snapshots of Ophcrack. <br>

![hack](/assets/EthicalHacking/passwordcrackin5.PNG) 

<br>


![hack](/assets/EthicalHacking/passwordcrackin4.PNG)

<br>
<br>

## 2. <u>For Linux OS</u>
### 2.1 <u>John the ripper</u>
A very famous and most usable tool in the password cracking field. This tool can perform bruteforce as well as dictionary attack on any type of hashes, such as MD5, SHA1, SHA2, LM etc. If password is not cracked from dictionary and bruteforce will surely crack the password. I used this tool in <a href="https://blog.vulnfreak.org/posts/Hacking2/">System Hacking (Linux)</a> blog. Following snapshot shows the same hash cracking that I used in L0ph and Oph crack, but with the help of **John the ripper** tool.<br>

![hack](/assets/EthicalHacking/passwordcrackin6.PNG)

<br>

### 2.2 <u>Hydra-wizard</u>
This is again most usable tool for getting the password of any service such as SSH, FTP, MySql server etc. You just need to enter the IP of target, the username or the file containing the username, the password to try or the file containing the passwords. It will start the dictionary attack. I used this tool in <a href="https://blog.vulnfreak.org/posts/Hacking2/">System Hacking (Linux)</a> blog. Following snapshot shows the hydra-wizrd which is trying to crack the password for ssh service for root user on other deecice.<br>

![hack](/assets/EthicalHacking/passwordcrackin7.PNG)
<br>

### 2.3 <u>Aircrack-ng</u>
The tool which is used to crack the wifi passwords from the .cap file you have got. This tool I will be discussing at the time of wifi-cracking blog.
<br>
<br>
<br>

*In this blog I showed you various password cracking methodologies and their tools. It depends on the password how complex it is, like **p@s$w0Rd** will take a lot of time to be cracked while **password** will be cracked in few minutes during the bruteforce.*

<br><br>

<b><i>In the next blog I will show how NBT-NS/LLMNR poisoning can be done and how the password of victim Windows machine can be cracked after this poisoning. This attack is more prominent in the Local Area Network.</i></b>