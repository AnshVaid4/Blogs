---
title: Getting Started With Cyber Forensics
author: Ansh Vaid
date: 2021-04-06 7:10:00 +0530
categories: [Cyber Forensics]
tags: [CHFI, CyberForensics, Cyber, Forensics, StrorageDevice, FTK, PSTools, hex]
---

<img src="/assets/CyberForensics/forensic.jpg" alt="image1" height="325" width="900"/>
<caption>Image taken from <a href="https://www.mbis-inc.net/image.jpg?v=fca8addf769f2f2037a8bf9">here</a></caption>

---

This is the another series besides **Cyber Security and Ethical Hacking** where I will be discussing about need of cyber forensics and various tools used in cyber forensics and how to use them. Like the series of **Cyber Security and Ethical Hacking**, this will also going to be an interesting series and very informative about the another domain of Cyber Security.

**Attention Future Hackers** <br>
This series comprises of various tools and some of them would be engaged in changing some system configurations and changes in registry of Windows OS also. So my advice is to you all is to have a virtual machine of Windows 7 OR Windows 8, Kali Linux installed in your host machines, rather than changing the configurations of host OS. You can also download Santoku linux as well, we might be needing that also.
<br>

---

# <u>Need of Cyber Forensics</u>
We all come across various articles about some server got hacked, data breach occured; recently the data of Facebook was compromised, also the data breach case of Mobikwik was also into news highlights. Specially this thing increased along with the social engineering attacks during the lockdown period where most of the people were losing their jobs and most have to work with less salaries. Ultimately it was a great opportunity for the hackers around the globe in order to steal money as they see such things as an opportunity to earn money. **But that's not good you should not be using your skills in wrong direction**.<br>
Now such things are running paralelly across the globe, but we need some defense system too. Yeah we do have **Ethical Hackers** too who are working for some organization and also for the government, but when the attack happens the cyber security experts also need to know about what was the vulnerablity that got exploited, and also they need to trace the hacker also who did it, so that they can take some legal actions against him/her. Or if some crime happened regarding blackmailing where the criminal had some objectional photos or videos or any private data of victim and asking him to give ransom in return to get them deleted otherwise he/she would viral that thing to defame victim.<br>
Now the victim complaint to the police about the same and police went to the criminal in order to search the storage device where he/she had kept the data stored, This could be the hardisk or pendrive or memory card also. But when police reached to the cromonal's home they found no data in the storage device. But the victim knew that it was present there. So there is the complete chance of the criminal that he might have deleted the data that he was having, because of the fear of imprisonment. Here comes the use of **Cyber Forensic** team again, in order to scan the hard drive or any other storage device carefully and retreiving that data which was stored on that storage device. So they were able to retrieve the data which he/she was using to blackmail the victim and the criminal was imprisoned for his acts.
<br>

# <u>Another Scenario For The Use Of Cyber Forensics</u>
Let's see the another scenario where the need of **Cyber Forensics** will become more clear. Let's suppose you have a proprietry data which is very important to you and no other copy is present in the world. You have stored the data in a hard drive which consists of no other data, means the proprietry data is isolated from the other data. And now you are going to publish that thing in the form of software or research paper. But some mishappening occurs, in such a way that the hardisk was burnt or got damaged. In this case also the forensics team work on the storage device in order to retrieve the data back, they try assembling various sectrs together, means it is a very patienceful task. Yeah, the whole data will not be recovered now but yes much of it could be recovered. So such things also happen in real life.

# <u>Tools Needed for Cyber Forensics</u>
To understand the concept of cyber forensics, you need to install the following softwares and we will be using one by one:<br>
1. <a href="https://accessdata.com/product-download/ftk-imager-version-4-5">FTK Imager (Windows Version) </a>
2. <a href="https://www.autopsy.com/download/">Autopsy (Windows Version)</a>
3. <a href="https://hex-workshop.en.softonic.com/">Hex Workshop</a>
4. <a href="https://docs.microsoft.com/en-us/sysinternals/downloads/pstools">PS Tools</a>
5. <a href="https://docs.microsoft.com/en-us/sysinternals/downloads/listdlls">List DLLs</a>
6. <a href="https://accessdata.com/product-download/registry-viewer-1-8-0-5">Registry Viewer</a>
<br>

We will be using most of the tools that are mentioned above, surely these tools will give you a feel of being a forensic expert at the end as we will move forward in this series.<br>

**This blog was an introductory blog to tell you how cyber forensics come into action and I also discussed two cases, there are other applications also but never mind I will let you know all those things as we will further proceed. So in next blog I will show how and when to use the tools mentioned above.**