---
title: Enumeration
author: Ansh Vaid
date: 2021-03-06 7:10:00 +0530
categories: [Cyber Security and Ethical Hacking]
tags: [CEH, EthicalHacking, CyberSecurity , Enumeration, Windows Enumeration, Linux Enumeration, SMTP enumeration, NTP enumeration, SNMP enumeration, LDAP enumeration]
---

<img src="/assets/EthicalHacking/Enumeration.jpeg" alt="image1" height="400" width="900"/>
<caption>Image taken from <a href="https://www.lynda.com/Linux-tutorials/Ethical-Hacking-Enumeration/479403-2.html">here</a></caption>

---

In my last blog I discussed the techniques regarding how to perform scanning. In fact the tools we used in Linux,
the same tools can be used in Windows OS. They are GUI based applications. You can easily install and use in Windows OS
if you are clear how to use in Linux OS. Now let's start with another step after scanning in this series of <b>Cyber Security
and Ethical Hacking</b>.

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

# What is enumeration?

Enumeration is just extraction of extra information regarding the target network, device such as the NetBios name, routing tables, shared resources, user names
group names of the target device. With the help of the attackers could find the pre identified vulnerabilities about the target. Following are the possible scenarios during enumeration:
1. You get an email. Now you can find the username of the person who sent you the email. You can find the domain name and server used by the sender, who sent
you the email. So this is also a type of enumeration.
2. Sometines the routers are configured with default passwords from the company itself, and is remain unchanged. So this makes easier to attack such routers or 
any device which is configured with default passwords.
3. Active Directory enumeration is done. This is a feature in Windows OS, which can be easily bruteforced to get the valid usernames, and their respective
passwords can also be cracked.
4. Usernames,group names and SID can be extracted by the attacker during enumeration.

## <u>Other Enumerations</u>
Some enumeration types I have mentioned above and some are briefly discussed below. The below table is a gist of enumeration types, the important ones are further discussed below this table.<br>

|Enumeration Type|Description|
|-|-|
|**DNS zone transfer**|Generally communication between DNS client and server is done through UDP port 53, but if the size of the message exceeds the limit then the communication is done over TCP port. Some malwares use the same DNS port number 53 to exploit vulnerabilities in DNS server.|
|**NetBios Name Service**|NetBios Name Servers maintain a database of NetBios names for the host and their respective IPs. This service is used when you share the data among Windows OS in LAN, to do name resolutions. That's why attackers are interested in attacking name servers.|
|**NetBios Session Service**|Service is used during the file transfer in a network in Windows OS. Null seesions are established and resources sharing is done with the help of this service. Attackers try to attack this service to get unauthorized access of critical file system resulting to data theft.|
|**Simple Network Management Protocol**|Protocol simply used for network management, attached to the devices such as firewalls, switches, other services etc. So attacker can get useful information if he is able to intercept the requests and rsponse messages.|
|**Lightweight Directory Access Protocol**|This protocol maintains distributed directory information services over an Internet Protocol network. Basically LDAP enumeration is done in Windows OS|
|**Simple Mail Transport Protocol**|This protocol is used in transfering emails over internet. This is a connection oriented protocol.|

<br>

### 1. <u>NetBios Enumeration</u>
NetBios as discussed earlier is a unique name of the device, which is used during the transmission of data in a network. It is of 16 ASCII characters, out of which 15 characters are used to destinguish device
and 16th character is reserved for service or name record type. So during the enumeration of NetBios attacker can get a list of devices belonging to a domain, policies, passwords, services running etc.

<b>Command:</b> nbtstat -[options]<br>
The command is used to see the NetBios name. Just type <b>nbtstat</b> in the command prompt of your windows operating system and you will be able to see various options along with its descriptions. You will surely get the output in terms of netbios names if it is present in your cache. In my case there were no NetBios name present in my cache so I didn't get any output.

![nbtstatoptions](/assets/EthicalHacking/nbtstatoptions.PNG)
<br><br>

![nbtstatcmd](/assets/EthicalHacking/nbtstatcmd.PNG)
<br><br>

Apart from this you can use various tools for NetBios enumeration. One such tool is <b>NetBios Enumerator</b>. This is a simple tool used for NetBios enumeration with simple GUI and options. Following is the output when I scanned with this tool over an IP range.

![enumtool](/assets/EthicalHacking/enumtool.PNG)
<br>
So it displayed me the netbios name of the machine which is in the same network and also it displayed me the MAC address of the machine. So in these two ways you can do NetBios enumeration.

### 2. <u>Enumerating User Accounts</u>
This can be easily done if you can easily connect to the target device. And you just need the PsTools. These are developed by Microsoft, and is a collection of tools that can provide a lot of information about the device.
You can download the tool from <a href="https://docs.microsoft.com/en-us/sysinternals/downloads/pstools">here</a>. Just unzip it and try executing from the command prompt on your computer or similarly the attacker can take the tools in the pendrive and try them on target device by lending the device from the victim for some time.
PsTools contains a set of small utility applications that help in gaing various information regarding the device. Some of these are:<br><br>

| Tool Name | Description |
|-|-|
| PsGetSid | Display the SID of user |
| PsFile | Shows remotely opened files |
| PsInfo | Provides various information about the system | 
| PsPasswd | Changes the password of account |
| PsList | Provides details of processes running in the system |
| PsKill | Kills any process with process ID |
| PsLoggedOn | Provides information regarding who are logged on locally and via resource sharing |

<br>

### 2. <u>SNMP Enumeration</u>
By this, the attacker tries enumerating user accounts and devices on a target device using SNMP. SNMP holds two passwords to access and configure the SNMP agent from management station. Also the information regarding the hosts, routers, devices, ARP tables etc. can be extracted by enumeration.<br>
<b><u>Working of SNMP</u></b>
``` code
1. GET request                      [SNMP manager requests SNMP agent]
2. GET next request       [SNMP manager keeps on retrieving data stored in array]
3. GET response             [SNMP agent resolves request made by SNMP manager]
4. SET request      [SNMP manager tries to modify parameter within SNMP agent's Management Information Base]     
5. Trap                    [SNMP agent informs SNMP manager of a certain event]
```

The SNMP enumeration tools are easily available in the internet, some of them are as follows:
1. OpUtils
2. Engineer's Toolset
3. NetScan Tools Pro
4. SNScan
5. SNMP Informant

### 3. <u>LDAP Enumeration</u>
LDAP protocol is used to access distributed directory services, mainly done in Windows operating system. Client createds a connection oriented LDAP session with Directory System Agent.
Communication is done between client and server using Basic Encoding Rules. Through LDAP enumeration, attacker can get valid user names, addresses etc.<br>
The LDAP enumeration can be done with the following tools, and these are present in internet:
1. LDAP admin tool.
2. LDAP account manager
3. Softerra LDAP administrator
4. LDAP search
5. Active directory explore

![ldapenum](/assets/EthicalHacking/ldapenum.PNG)

### 4. <u>NTP Enumeration</u>
Network Time Protocol is a UDP protocol which is used to synchronize the time of devices over a etwork. Attacker can get the information about a network through NTP enumeration.
The information like:
1. List of hosts connected to NTP server.
2. IP addresses of clientsin a network.
3. Device names and OS of devices connected in a network.

There are certain commands in linux, which could help in NTP enumeration:
1. <b>ntptrace:</b> Traces the chain of NTP servers.
2. <b>ntpdc:</b> Monitors operation of ntpd.
3. <b>ntpdate:</b> Collects number of time samples from a number of time sources.

**Syntax:** The above commands can be used with various options, which you will easily get by just typing the command and pressing enter key.
Your linux machine might not have some of ntp commands installed, so you can install them using *apt-get install [command to install]*.

![ntpdateinstall](/assets/EthicalHacking/ntpdateinstall.PNG) <br>
![ntpdate](/assets/EthicalHacking/ntpdate.PNG) <br>
![ntpdate2](/assets/EthicalHacking/ntpdate2.PNG) <br>

The various tools to do NTP enumeration are:
1. PRTG network monitor
2. NTP time server monitor

### 4. <u>SMTP Enumeration</u>
The protocol is used to send the emails, that too in plain text. There is no encryption method. The enumeration helps the attackers to get the list of valid userson SMTP servers. There are three built-in commands for SMTP-
``` code
1. VRFY                   [Validates users]
2. EXPN                   [Tells actual delivery addresses of alliases and mailing lists]
3. RCPT TO                [Defines the recipients of the message]
```
Following are the tools for SMTP enumeration:
1. NetScan Tools pro
2. SMTP-USER-ENUM

---

The basic aim of enumeration is to get some extra information about the device or network or service. So it is a bit different from the footprinting. Nowadays there are many different ways of getting such enumeraion, so this step is not difficult as it seems to be. You might get this step a bit boring, but when once you start getting some extra information you will find it interesting. Again it's just a way of extracting some extra information about the target.

---
---

This blog was all about different types of enumeration, how it can be done, different tools that could be used in enumeration. So till now we are able to gain as much information possible about the target by footprinting, scanning and enumeration.<br>
Now in the next blog I will start how to get into the system by exploiting the vulnerabilities of the target system.

<!-- Credits for header pic https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.lynda.com%2FLinux-tutorials%2FEthical-Hacking-Enumeration%2F479403-2.html&psig=AOvVaw3UB3Y7h5wCGfZlRCmMDSMx&ust=1615482234889000&source=images&cd=vfe&ved=0CAIQjRxqFwoTCLiO3Lqapu8CFQAAAAAdAAAAABAE -->