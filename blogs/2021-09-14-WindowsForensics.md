---
title: Forensics Of Windows Registry
author: Ansh Vaid
date: 2021-09-15 7:10:00 +0530
categories: [Cyber Forensics]
tags: [CHFI, CyberForensics, Cyber, Forensics, Windows, Microsoft, Analysis, Registry, Regedit]
---

<img src="/assets/CyberForensics/bannerreg.jpg" alt="image1" height="400" width="900"/>
<caption>Image taken from <a href="https://legaldesire.com/wp-content/uploads/2020/04/investigatore-milano-investigazioni-forensi-digitali-computer-forensics-digital-disk-1080x675.jpg">here</a></caption>

---

In my last blog I discussed the concept behind how the wallet address in a bitcoin blockchain is created. The conceptual implementation could be found in the CTF challenge **What's My Wallet Address**. If you missed the CTF then you can read the writeup at <a href="https://medium.com/vulnfreak/whats-my-wallet-address-a8c25c8e32b1">https://medium.com/vulnfreak/whats-my-wallet-address-a8c25c8e32b1</a>. <br>
This blog is not related to blockchain concepts. For a change I will discuss an interesting topic of Cyber Forensics. I am going to discuss about the role of registry in cyber forensics investigation, why it is necessary to analyze and also show some important registry hives.

# 1. <u>What Is Windows Registry?</u>
Microsoft Windows OS logs each and every activity performed by the user in the Log File, also known as **Event Viewer** which can be accessed using command **compmgmt.msc** in Run dialogue box using (**Windows button + R**). If the attacker gets into your system and does malicious things, or if any malware enters your OS and does malicious things in background then it gets recorded in the log files of your system. After the attack when the forensic investigator accesses your OS then he creates a dump of those logs and also of windows registry. It depends on the how smart the attacker is, because these registry keys and logs can even be deleted. But a good forensic investigator is the person who analyses each and everything present on the system to get a clue about the attack, as per **Locard's Principal** *a criminal will bring something in the crime scene and leaves behind something in the crime scene*, and that **something** has to be found by a cyber forensic investigator from the **crime scene** which is a digital device here.<br>
Now we know the concept of log files in Windows OS, but the further discussion will be totally revolving around the Windows Registry. Windows Registry is a database which is accessed by various softwares, applications, configuration files, dll files etc. on your system because the actual way and settings related to how the software, application etc... would work on OS is actually defined here. Therefore the updations are done to the Windows Registry by various configuration files, softwares whenever we introduce new changes to them. You can imagine Windows Registry as a central hub, without which nothing could be executed, changed in the Windows environment. Even if you open an image and close it will be reflected in the registry, so understand the power of Windows Registry, what all information can be retrieved on minute analysis of it.<br>
To open Windows registry I prefer using registry editor for now, a default tool to access the registry. There are many other tools which provide automated results from the registry with a single click, but our motive is to understand the concept so I will show via regisry editor. Use trigger keys **Windows + R** to open run dialogue box, and write **regedit** there and press enter.<br>

![hack](/assets/CyberForensics/run.PNG)

<br>

Then it will ask you the permissions, so give it. Also this can only work if you are loggedin using Administrator account of Windows OS, otherwise it will ask for the Admin credentials for accessing.<br>
**IMPORTANT:** I will not be discussing all the registry keys because the list is so big that it will take 5-6 more editions of this blog. Instead I will discuss the usage and importance of each hive, rest is self explainatory from the respective names of hives.

<br>

# 2. <u>Getting Into Windows Registry</u>

After accepting the permissions, the windows registry will open, and it will look like the snap below:<br>

![hack](/assets/CyberForensics/reg1.PNG)

<br>

There are 4 hives in the registry:
<ol>
<li><b>HKEY_CLASSES_ROOT</b></li>
<li><b>HKEY_CURRENT_USER</b></li>
<li><b>HKEY_LOCAL_MACHINE</b></li>
<li><b>HKEY_USERS</b></li>
<li><b>HKEY_CURRENT_CONFIG</b></li>
</ol>

The folders and subfolders in above mentioned folders of registry are known as hives. There are 2 main hives i.e. **HKEY_LOCAL_MACHINE** and **HKEY_USERS** and rest other are derived from these two hives. Now let's discuss for every hive.<br>

# 3. <u>HKEY_CLASSES_ROOT</u>
This hive contains the information regarding files association, what kind of application needed to open file and registration of Component Object Model (COM) unique id. Do not confuse yourself with COM directory of android apk, that's totally different.<br>

![hack](/assets/CyberForensics/reg2.PNG)

<br>

You can find various extensions, and the well known extensions like .doc, .ppt, .xlsx, .pdf etc. are also mentioned here in the form of a directory. This directory has information about what software has to be used to open the respective extension. See the snap below:<br>

![hack](/assets/CyberForensics/reg3.PNG)

<br>

And if you scroll down more, you will get other hives, clicking upon which you will find the folders with names **CurVer** or **CLSID** or sometimes both. CurVer, as the name suggets, would tell you about the current version of the respective software, application etc. CLSID is the Class Identifier, which is added whenever you install a software or update, to maitain the entry of version which is installed. Nowadays the softwares are adding this CLSID in there exe file rather that in registry to limit the use of registry. The CLSID is a unique identifier of alphanumeric string for a particular version of a software, so it's not a big deal to have same CLSID on two or more different devices.<br>

![hack](/assets/CyberForensics/reg4.PNG)

<br>

# 4. <u>HKEY_CURRENT_USER</u>
This hive contains the information related to the current logged in user, derived from **HKEY_USERS** hive.<br>

![hack](/assets/CyberForensics/reg5.PNG)

<br>

There are several hives in it:
<ol>
<li><b>AppEvents</b></li>
<li><b>Console</b></li>
<li><b>Control Panel</b></li>
<li><b>Environment</b></li>
<li><b>Microsoft</b></li>
<li><b>Network</b></li>
<li><b>System</b></li>
<li><b>Volatile Environment</b></li>
</ol>

These all hives contain the configuration settings which he has set for his account. These get loaded as soon as the user enters the password of his account and enters his account. The names themselves are self descriptive about what kind of information they contain in them.<br>
The interesting hive out of all of these is **AppEvents**, which contains the settings related to the alert sounds which are played by the Windows OS.<br>

![hack](/assets/CyberForensics/reg6.PNG)

<br>

# 5. <u>HKEY_LOCAL_MACHINE</u>
This hive contains the information related to the system, right from booting, to the Access Control List of various SYSTEM files, which even the administrator can't access. Event the ACLs can't be access by the administrator due to less privileges.<br>

![hack](/assets/CyberForensics/reg7.PNG)

<br>

There are several hives in it:
<ol>
<li><b>BCD00000000</b></li>
<li><b>HARDWARE</b></li>
<li><b>SAM</b></li>
<li><b>SECURITY</b></li>
<li><b>SOFTWARE</b></li>
<li><b>SYSTEM</b></li>
</ol>

The hive **BCD00000000** is containing the information/configuration regarding the booting process of your system, what all files to be included and other stuffis maintained by this hive. SAM hive is same as SAM file in config folder of System32 folder, having all the usernames and the password hashes of the Windows OS. You cannot access it, because it needs SYSTEM level permissions. Rest the name of hives define what all data they contain.<br>

# 6. <u>HKEY_USERS</u>
This registry hive contains the information, configuration settings related to all the accounts present in the system, no matter if it is an administrator, SYSTEM or guest user.<br>

![hack](/assets/CyberForensics/reg8.PNG)

<br>

There are several hives in it:
<ol>
<li><b>.DEFAULT</b></li>
<li><b>S-1-5-18</b></li>
<li><b>S-1-5-19</b></li>
<li><b>S-1-5-20</b></li>
<li><b>S-1-5-21</b></li>
</ol>

.DEFAULT hive contains the settings before any user logs into the system. S-1-5-18 is the SID, and this hive is dedicated to the local system used by OS. S-1-5-19 hive is for NT authority for local services, S-1-5-20 is for NT authority but for network services and at the end there are two hives with SID S-1-5-21, it's for domain users, i.e. the users which we create in the system. That's why the hive **HKEY_CURRENT_USER** is derived from this, so that the current user configuration settings could be loaded.<br>

# 7. <u>HKEY_CURRENT_CONFIG</u>
This registry consists of various configuration settings of your system, as the name suggests.<br>

![hack](/assets/CyberForensics/reg9.PNG)

<br>

**IMPORTANT:** The registry consists of so many data in an organized manner so it would be difficult to discuss all the keys present in various hives. Each key is unique in itself. But, there are some common paths in all the hives, which you could traverse and get a lot of data, and would give you a sense of why registry is so unique. Out of them the two most common paths are:

<b>
<ol>
<li>[PARENT HIVE]\SOFTWARE\Microsoft\Windows\[TRY VARIOUS HIVES HERE]</li>
<li>[PARENT HIVE]\HARDWARE\Description\[TRY VARIOUS HIVES HERE]</li>
</ol>
</b><br>

**One of them is shown in below snapshot. This registry key shows the name of all the softwares that you have explicitly installed in the system. Since I have installed FTK Imager software in my system, so the same is being displayed here.** <br>

![hack](/assets/CyberForensics/reg10.PNG)

<br>

I have created a tool implementing the same things for Windows Registry Forensics, so that you don't have to remember the complex registry paths: <a href="https://github.com/AnshVaid4/Python/tree/master/Forensics">https://github.com/AnshVaid4/Python/tree/master/Forensics</a><br><br>
If you have not gone through the concepts of use of FTK Imager in forensics, then you can read my blog from <a href="https://blog.vulnfreak.org/2021-06-09-Forensics_with_FTK_Image_%20part_2/">https://blog.vulnfreak.org/2021-06-09-Forensics_with_FTK_Image_%20part_2/</a>.<br><br><br>

In this blog I have discussed about the use of Windows Registry in cyber forensic investigation, various hives in the registry and their respective roles, which hives have derived and which are independent etc.