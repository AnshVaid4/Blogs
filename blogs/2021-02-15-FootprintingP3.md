---
title: Footprinting and Reconnaissance using Linux OS
author: Ansh Vaid
date: 2021-02-15 7:10:00 +0530
categories: [Cyber Security and Ethical Hacking]
tags: [CEH, EthicalHacking, CyberSecurity , Footprinting, Information Gathering, recon-ng, theHarvester, maltego, Kali]
---

<img src="/assets/EthicalHacking/footprinting.jfif" alt="image1" height="400" width="900"/>
<caption>Image taken from <a href="https://www.lynda.com/Linux-tutorials/Ethical-Hacking-Footprinting-Reconnaissance/455717-2.html">here</a></caption>

---

This blog is in continuation previous blog on footprinting and reconnaissance. Previously you understood how to do
footprinting with the help of Windows OS. In this blog I am going to show how footprinting can be performed
with the help of Linux OS.

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

# Footprinting tools which uses Kali Terminal

## 1. Recon-ng
**Use:** The tool helps you to gather information about the websites resgistered with AIRIN (American Registry for Internet Numbers).
         So you cannot find the information of websites hosted in India. The information regarding the websites hosted in America 
         can be easily gathered.<br>
**Syntax:** recon-ng<br>
### Steps to use **recon-ng** tool
<ol type="1">
<li>Open linux terminal</li>
<li>Type <b>recon-ng</b> and press enter</li>
<ul>
<li>If using recon-ng first time then use following commands to install payloads.</li>
<li>Enter <b>marketplace install all</b> in recon shell.</li>
<li>It will automatically install its payloads, some will give error(marked with red colour) because they could only be installed with premium version.</li>
</ul>
<li>Create a new workspace or use the default workspace of recon-ng. For creating a new workspace use following commands otherwise 
to use with default workspace skip to next step. Advantage of using workspace is to separate different projects when you are gathering
information for more than one website simultaniously.</li>
<ul>
<li>Type <b>workspaces list</b> press enter </li>
<li>Type <b>workspaces create [any name you want to give to workspace]</b> press enter</li>
<li>New workspace started.</li>
</ul>
<li>Type <b>modules options</b> press enter. It will show you <b>[load|search]</b>. So accordingly we use option. Here we want to load a module
so we will type <b>load</b> after <b>modules</b>.</li>
<li>Now which module to load? This we can know by <b>modules load [press tab button 3 times]</b>. And you will get a list of modules.</li>
<li>Type <b>modules load recon/domains-contacts/whois-pocs</b> press enter. This payload is used for whois lookup.</li>
<li>Type <b>info</b> press enter to know what this payload needs(various settings to be done for payload). When you press enter then you
will be able to see an <b>Options</b> section, which will display 4 columns. 1st column shows the Name of the option you need to set
for the payload, 2nd column shows the current value of option which is set, 3rd column displays whther the particular option is required
to be set or not, 4th column shows the Description of the option so that you get idea what you need to set.</li>
<li>Type <b>options</b> and press enter if you are unable to recall what option to set now</li>
<li>It will show <b>[list|set|unset]</b>. In this case we need to set a SOURCE to the payload. So we will accordingly use the option.</li>
<li>Type <b>options set SOURCE [any website domain name]</b> and press enter</li>
<li>Now again type <b>info</b> and press enter. You will find that the 2nd column after SOURCE is now initialized with your target value.</li>
<li>Type <b>run</b> and enter to execute the payload. It will then show you the details it could find regarding the target website.</li>
<li>You can change the SOURCE value again for the same payload with <b>options set SOURCE [any website domain name]</b> and enter. </li>
<li>To change the payload refer to the 4th point.</li>
</ol>

**NOTE:** Whenever you are using command to set the options of payload(eg. setting SOURCE) then use the case(uppercase/lowercase) as specified
in the options when you run command **info**, if the case doesn't matches then it provides error. Also the command is **options**, not **option**.
<br>

### The screenshots below show the example of another module [profiler]

![recon-ng1](/assets/EthicalHacking/recon1.PNG)
<br>

![recon-ng1](/assets/EthicalHacking/recon2.PNG)
<br>

![recon-ng1](/assets/EthicalHacking/recon3.PNG)
In above snapshots, the SOURCE I have set is <a href="http://vulnweb.com/">vulnweb.com</a>. So it starts searching various social media websites
to find any account related to <a href="http://vulnweb.com/">vulnweb.com</a>. If any related account is found then that link is higlighted with
green colour, otherwise it is blue in colour. Sometimes error is geerated for any social media it is searching, so it is hihlighted in red colour
with error description.
<br>

## 2. Dmitry

**Use:** A vast command line tool to gather information.<br>
**Syntax:** dmitry -options [target website link] <br>

You can get the man page of dmitry by typing **dmitry** and press enter. If you want to perform whois lookup the use option **-w**, if you want
to scan the open ports of the target website then use option **-p**, if you want to scan the filtered ports of the website then use **-f**. Likewise
you can use various options in for performing information gathering through dmitry. The description is provided for all respective options.

![dmitry1](/assets/EthicalHacking/dmitry1.PNG)
<br>

*The above snapshot shows various options that could be used with this command, and description regarding the option is also provided.*

![dmitry2](/assets/EthicalHacking/dmitry2.PNG)

![dmitry3](/assets/EthicalHacking/dmitry3.PNG)
<br>

<i>I have killed the process in above snapshots in between, because it will give me a long list, so killed the process in between with **ctrl+c**.
You can carry on with the results that you are getting, no need for you all to kill in between, unless you wanna do.</i><br>
<br>

## 3. Sublist3r
**Use:** This is a command line python based tool which is used for getting various subdomains about a target website from OSINT. Uses various search engines
which are added to its code.<br>
**Syntax:** sublist3r -option -d [target website link]

It might be possible that your Kali machine don't have it preinstalled, so use following command to install it- **apt-get install sublist3r** and
press enter. It will download and install it. Now to know various options for this tool, type **sublist3r -h** and press enter. You get its options
and their respective descriptions there. Option **-d [website link]** have to be mentioned always, otherwise tool will unable to find the target
website.

![sublister1](/assets/EthicalHacking/sublister1.PNG)
The above snapshot shows various options that could be used with this command, and description regarding the option is also provided.

![sublister2](/assets/EthicalHacking/sublister2.PNG)

![sublister3](/assets/EthicalHacking/sublister3.PNG)
The above snapshots show two of the options of sublist3r command. Try using other options on your own.
<br>
<br>

## 4. The Harvester
**Use:** This is again a python pased tool and works like sublist3r, used for gathering various information such as email, subdomains, open prts etc.<br>
**Syntax:** theHarvester -option -d [target website link]

Just like sublist3r, theHarvester also shows the available options that could be used for information gathering such as email id, subdomains etc.
To see the options type **theHarvester -h** and press enter to get the various options and its descriptions.  Latest Kali vesions might and might
not have it preinstalled. So type **apt-get install theHarvester** and press enter to install it. This is a command line tool and might not work
in latest versions of kali. The snapshot below shows various options vailable for theHarvester tool. Also the tool didn't work for me, you can try
it on your own maches, might be it works for you all.

![theHarvester1](/assets/EthicalHacking/theHarvester1.PNG)

![theHarvester2](/assets/EthicalHacking/theHarvester2.PNG)

## 5. Httrack
**Use:** This tool is used for website cloning/mirroring.<br>
**Syntax:** httrack [target website link]

**httrack** tool fully clones/mirrors a particular website, even you can get all the links with you, and the whole website is saved for you in offline
mode for you. With different pages/assets stored in various directories, you get a page index.html, which you need to open in firefox and go through other
pages. Basically the tool is used to get information how different pages are linked toeach other, architecture of the website. Type **httrack -h** to get
other details and options regarding the tool. When you mirror a website then the directory withe the name of website is created on the same directory where
you executed the command. You can explore that directory, it contains various subdirectories and assets.
![httrack](/assets/EthicalHacking/httrack.PNG)
In above snapshot I have terminated the execution of command because mirroring takes a long time. You can wait until the mirroring is completed.
<br>

## 6. WhatWeb
**Use:** Used for banner grabbing. This is also important in footprinting process.<br>
**Syntax:** whatweb [target website link]

Banner grabbing is the technique to get the information related to the website based on the banner available in the website. This is due to the 
misconfigurations of the website, we are able to get various sensitive information about the website. The output and reference regarding the tool,
you can take from is shown below:

```output 

root💀CyberWar)-[~]
└─# whatweb certifiedhacker.com
http://certifiedhacker.com [200 OK] Apache, Country[UNITED STATES][US], HTTPServer[Apache], IP[162.241.216.11], JQuery[1.4], Meta-Author[Parallelus], PasswordField[RevealPassword], Script[text/javascript], Title[Certfied Hacker], UncommonHeaders[upgrade,host-header]

```
<hr>

# GUI based footprinting tools
Till now we have used command line tools for footprinting. But there is one GUI based tool which helps in footprinting. There are other GUI based
footprinting tools, but this one is preinstalled in Kali, and provides maximum information about any website.

## Maltego
Steps to start maltego application:
<ul>
<li>Click on top left corner, on kali icon and search maltego.</li>
<li>Open maltego, and choose community edition.</li>
<li>Go on with simple registration step by step.</li>
<li>At last open a <i>new graph</i></li>
<li>If you are not getting <i>new graph</i> option then close maltego and open it again</li>
<li>There is a Maltego symbol or top-left side of window.</li>
<li>Just beside it, there is a <i>new graph</i> option beside it. Click on it.</li>
<li>From the left on <i>Entity Palette</i> drag company component to the workplace.</li> 
<li>Then edit the domain name for which you want to gather information by double clicking on <i>Patreva</i>. Then click enter.</li>
<li>Then right click on the company component and you will get various option, regarding information gathering <b>All Transformations</b> tab.</li>
<li>Choose one of the options, and the information will be displayed to you on graph. </li>
<li>Repeat same steps by clicking on various components, select various options and get information.</li>
<li>Discover various options.</li>
<li>At the end you can get the output in the form of PDF, from the <i>Import/Export</i> tab on top.</li>
</ul>

<br>

![maltego1](/assets/EthicalHacking/maltego1.PNG)
![maltego2](/assets/EthicalHacking/maltego2.PNG)
![maltego3](/assets/EthicalHacking/maltego3.PNG)
![maltego4](/assets/EthicalHacking/maltego4.PNG)

---

<br>
*This blog was all about the information gathering with the help of some commands on Linux and softwares. These commands are executed*
*in terminal which is present in Kali distro of Linux OS, so don't forget to open terminal. The footprinting and reconnaissance part*
*is over. Now we will move to next step for ethical hacking in upcoming blogs.*

<!--Credits for header pic https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.lynda.com%2FLinux-tutorials%2FFootprinting-reconnaissance%2F455717%2F5027599-4.html&psig=AOvVaw3a8Q0jqD8nFs_ch1h8rqJL&ust=1615481919393000&source=images&cd=vfe&ved=0CAIQjRxqFwoTCICK5aqZpu8CFQAAAAAdAAAAABAD -->