---
title: Footprinting and Reconnaissance using Windows OS
author: Ansh Vaid
date: 2021-01-24 7:10:00 +0530
categories: [Cyber Security and Ethical Hacking]
tags: [CEH, EthicalHacking, CyberSecurity , Footprinting, Information Gathering, recon-ng, theHarvester]
---

<img src="/assets/EthicalHacking/footprinting.jfif" alt="image1" height="400" width="900"/>
<caption>Image taken from <a href="https://www.lynda.com/Linux-tutorials/Ethical-Hacking-Footprinting-Reconnaissance/455717-2.html">here</a></caption>

---

In this blog I am going to show different ways to perform footprinting. Now for doing this you should have
Linux and Windows operating systems. For Linux operating system there are some tools which run on CLI, and
on windows operating system, there are some commands on CMD(command prompt) by which footprinting could be
done. Also there are some websites through which information gathering can be done about the victim.
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

# Information Gathering By CMD Commands
_There are some commands in information gathering that you can try for other websites as well, but it is still adviced_
_not to try on them. Now let's start with practical concept of footprinting._

## 1. Tracert
**Use:** With this command you get the path(number of hops) to reach the website for which you are running this command.<br>
**Syntax:** tracert [URL of website]

![tracert](/assets/EthicalHacking/tracert.PNG)

In above snapshot you could see that my packet needed 14 hops to reach the destination, i.e. certifiedhacker.com website.
Also you can see the " *   *   * " pattern in some places. This is due to fact that the  response from the router exceeded
the ttl(time to live), therefore no information regarding the router could be found. The tracert sends three packets, and
the round trip time is displayed of each packet. Round trip time is just a time taken for the packet to reach the destination
router and come back to our device. Also the tracert command gives the IP address of the website for which you are finding
route.

## 2. Ping
**Use:** With this command you get the IP address of target. Also you can find the maximum size of frame that is accepted at
         the server side which can help attackers during DOS attack.<br>
**Syntax:** 
1. ping [URL of website]
2. ping -f -l {size of frame} [URL of website] <br>
The 1st syntax is normal pinging, where you will get the IP address of the website. In 2nd syntax "-f" "-l" are the options
which is used to specify the **frame** and **length** respectively and the **{size of frame}** is an integer which you can
change time to time until your frame gets discarded. By changing the values of the size of frame you get the boundry value
of the size of frame that is accepted at server side.

![ping](/assets/EthicalHacking/ping.PNG)

## 3. Nslookup
**Use:** With this command you can get the information regarding the Domain Name System(DNS). Just type **nslookup** in cmd and
         press enter key. You will get a shell with ">" symbol on left. Then you have to set various options depending upon the
         information you want. The options are-
<ul>
<li><b>A</b>: For getting IP address.</li>
<li><b>ptr</b>: For name from IP address.</li>
<li><b>ns</b>: For getting name server.</li>
<li><b>cname</b>: For getting alias name.</li>
<li><b>SOA</b>: For getting Start Of Authority.</li>
</ul>

These options are set in the shell in following manner-
**set type=[option name]** then press enter to set the option.
**Type URL** then press enter to get information regarding the option you set earlier.

**Syntax:** nslookup

![nslookup](/assets/EthicalHacking/nslookup.PNG)

## 4. Advanced Google Search
**Use:**Advanced google search, also known as _google hacking_ is another way to extract sensitive or hidden information with the
help of complex search queries. Query can find some valuable data about the target from google search engine. This type of google
search gives more specific result about what you have searched, unlike normal searching where you get lakhs of links.
The operators in the search query used are-
<ul>
<li><b>inurl:</b> This restricts the search results only to pages containing the word specified in the URL</li>
<li><b>intitle:</b> This operator restricts results to only those pages containing the specified term in the title</li>
<li><b>inanchor:</b> This operator results those pages containing query terms specified in the anchor text on link to the page</li>
<li><b>site:</b> Restricts search results to a specified site or domain</li>
<li><b>cache:</b> This operator displays google's cached version of a web page, instead of current version of the web page.</li>
<li><b>file by:</b> This operator provides the  search result with the specified file format specified by you after the operator.</li>
</ul>
These are few operators used during google search. There are more operators, but these are mostly used during search.

**Syntax:** operator:[link name or string depending on operator]
_You should not have spaces between **operator**, **:** and **search string**. Also carefully look the number search results found by_
_this method and normal google search._

![googlehacking](/assets/EthicalHacking/googlehacking.PNG)
---

# Websites That Help in Information Gathering
There are several good websites that help in providing information regarding the target, such as- IP address, website first seen, DNS,
website archtecture, location of the server, port numbers open etc. These sites are also used by general public for security reasons, 
so that they could not be fooled by anyone who is trying impersonate as someone else and trying to extract any information from them etc.

## 1. Netcraft
[https://www.netcraft.com/](https://www.netcraft.com/)<br>
This is an amazing website where you just have to put the URL of the target website about whose information you want to gather. Then 
automatically it will give you the information related to the website such as-
<ul>
<li>Rank of site</li>
<li>When was the site first seen</li>
<li>Any risk on site</li>
<li>Hosting company</li>
<li>IP address</li>
<li>Nameserver</li>
<li>Domain registrar</li>
<li>Location of server</li>
<li>Server side technologies</li>
<li>Languages used at client side scripting</li>
</ul>
Visit the site and try this website. Many other otions are also available. It is a vast website, with lots of information related to the target.

![netcraft](/assets/EthicalHacking/netcraft.PNG)

## 2. Shodan
[shodan.io](https://www.shodan.io/)<br>
This website also provides you with maximum information about the target website. But it could also show the various port numbers that
are open at the server side.

![shodan](/assets/EthicalHacking/shodan.PNG)

## 3. Archive
[archive.org](https://archive.org/)<br>
This website provides you the older versions of the websites. Sometimes the older versions of websites have some sensitive files, which
the organization forgets to remove and hide the links in their current versions. So those can be accessed from the older version of
websites.

![archive](/assets/EthicalHacking/archive.PNG)<br>

_There are other wesites also from which information gathering could be done. But most of the details about the target can be found_
_from above websites that are discussed. You may also refer following websites for information gathering-_
<ul>
<li><a href="https://www.yougetsignal.com/">yougetsignal.com</a></li>
<li><a href="https://in.godaddy.com/whois">godaddy.com</a></li>
<li><a href="https://whois.domaintools.com/">whois.domaintools.com</a></li>
</ul>
<br>
<hr>

*This blog was all about the information gathering with the help of some commands on CMD and websites. These commands are executed in CMD*
*which is present in Windows OS, so don't forget to open CMD as an administrator because some commands need administrative privileges also.*
*In next blog I will discuss how the information gahering can be done in Linux Operating System*

<!--Credits for header pic https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.lynda.com%2FLinux-tutorials%2FFootprinting-reconnaissance%2F455717%2F5027599-4.html&psig=AOvVaw3a8Q0jqD8nFs_ch1h8rqJL&ust=1615481919393000&source=images&cd=vfe&ved=0CAIQjRxqFwoTCICK5aqZpu8CFQAAAAAdAAAAABAD -->