---
title: Forensics with FTK Imager
author: Ansh Vaid
date: 2021-06-08 7:10:00 +0530
categories: [Cyber Forensics]
tags: [CHFI, CyberForensics, Cyber, Forensics, StrorageDevice, FTK, PSTools, hex]
---

<img src="/assets/CyberForensics/bannerftk.jpg" alt="image1" height="400" width="900"/>
<caption>Image taken from <a href="https://147146-880759-raikfcquaxqncofqfm.stackpathdns.com/wp-content/uploads/2019/07/computer-forensics-classes-in-dubai.jpg">here</a></caption>

---

In this blog I am going to show the interface of FTK Imager tool and talk about various files of NTFS, a widely used tool in terms of Cyber Forensics, and also why I
like this tool is because it has so many features and yet it is a free tool. If you don't have FTK Imager tool then you can download it
from this <a href="https://marketing.accessdata.com/l/46432/2020-09-24/8l45td">link</a>. 

![hack](/assets/CyberForensics/ftkhome.png)
<br>

This is the home screen of ftk imager. In this you can do the following:
1. Add evidence item
2. Create image of RAM
3. Create image of DISK
4. Various options of image available
5. Read an evidence item cluster by cluster
6. Search for suspecious keyword in evidence item
   
and the list goes on and on. That's why it is a vast and helpful tool in forensics.<br>

# 1.<u>Various files present in NTFS</u>
New Technology File System(NTFS) is a widely used file system in Windows operating system. This file system has some default files which it
creates for itself to keep a track of all the files in a disk, just like an index keeps all the track of all the pages of a book. Before moving
forward let me tell you basic architecture of a disk.

![hack](/assets/CyberForensics/disk.jpg)
<caption>Image taken from <a href="https://www.slashcam.de/images/news/g600/HDD-schema-14071_PIC2-600.jpg">here</a></caption>
<br>

The cluster is a smallest part of a disk of fixed size(512 bytes always) and a cluster is a group of sectors. Generally when you format a disk, you get an option
to choose the size of a cluster.<br>

### 1.1<u>Why is it asked?</u>
It is a good practice to keep the size of a cluster as small as you can, mostly recommended as **4096 bytes**. It is so because sometimes when you create
a file for example a text file as *test.txt*. Most of the times the text file are not so big, or even if they are big then their size wouldn't be the
multiple of the size of cluster(be it 4090 bytes in our case). Say the size of the cluster is 8192 bytes. The size of the file is less than the size of a cluster, the remaining 4102 bytes will be wasted of the cluster(*not exactly wasted but it will come in use untill the disk is almost full*). This free space is known as **slack space**. Some of the criminals take the advantage of this slack space to store some hidden data in the disk.<br>
**IMPORTANT:** Note the following things in above example:<br>
1. Size of sector is 512 bytes(always fixed) 
2. Size of 1 cluster is 8192 bytes i.e. 16 sectors
3. Size of file is 4090 bytes (Or 7 sectors and 506 bytes) 
4. Actual number of sectors used by file is 8 (7 fully and 8th partially)
5. Slack space calculated for above file will be 8192-4090=>4102 bytes.
6. The salck space of 4102 bytes is divided into two parts: **RAM Slack** and **File Slack**.
7. RAM slack is the number of bytes left in the sector. In this example the 512-506=>6 bytes is the RAM Slack. Why 512? Because the size of 1 sector is 512 bytes and the file is stored in only 7 sectors fully and 506 bytes of 8th sector. So the space which is left in 8th sector i.e. 512-506=>6 bytes is the RAM Slack.
8. We now know the RAM slack as 6 bytes. Therefore 4102-6=>4096 bytes is the File Slack, i.e 8 sectors. 8 sectors are wasted because of choosing 8192 bytes cluster. If we would have chosen 4096 bytes clusters then **this wastage would have reduced to only 6 bytes RAM slack, and no File Slack would be there at that time**.
9. RAM Slack is used by RAM as a dump.

<br>

I hope you have got from the example used above what is a sector, cluster, slack space and why it is necessary to choose small cluster size!!

<br>

Now one more thing, just an extra knowledge, that if the cluster size is more, then the fragments will be less which would enhance the reading and writing speed and also be feasible in indexing.

<br>
<br>

Remember in the last paragraph I wrote a statement **not exactly wasted but it will come in use untill the disk is almost full**. So how is this thing possible
in NTFS file system? we have various hidden files(note that this hidden file is not same as hidden file you create). These hidden files are created by default
as soon as the disk is formatted with the NTFS file system, and the name of these files start with **$**.<br><br>

# 2.<u>How to see these files?</u>
Follow the steps to see these files:
<ol>
<li>Go to <b>File > Add Evidence Item</b> <br><img src="/assets/CyberForensics/ftk1.PNG"></li>
<li>Select <b>Logical Drive</b> <br><img src="/assets/CyberForensics/ftk2.PNG"></li>
<li>Select <b>Logical Drive > Next</b></li>
<li>Select your volume, be it C, D, E or any other</li>
<li>Click on <b>Finish</b></li>
</ol>

<br>

The evidence i.e. the logical disk C in my case is added to the **Evidence Tree** panel of the window, and the window will look like the below snap:

![hack](/assets/CyberForensics/ftkevidence.PNG)

<br>

Click on + button to expand the tree to get root folder as shown in below snapshot:

![hack](/assets/CyberForensics/tree.PNG)

Click on **root** folder directory, and see the changes in **File List** pane of the window. Scroll down to see the files of NTFS file system, responsible to
maintain the records regarding the files directories, deleted fies, boot file, even the swap space file can also be seen, the ones marked with **$** symbol in the beginning. These files are the first files to be loaded in the beginning of the disk to map each and everything in the disk. The below snapshot shows such files:

![hack](/assets/CyberForensics/NTFSfiles.PNG)

| File Name | Description |
|-|-|
| **$AttrDef** | The file contains information related to the usable space in a volume |
| **$BadClus** | Contains information about bad clusters in a disk. You might have seen the notification when you plug in the USB drive about "Scan disk to repair bad clustes". The PC gets to know about bad clusters from this file only.|
| **$Bitmap** | It stores the flag relatd to the cluster if it is free or not. |
| **$Boot** | As the name suggests, this file contains the necessary information related to the device booting. So that's why it's present in the first cluster. Also have the addresses of $MFT and $MFTMirr.|
| **$LogFile** | File contains information about all the changes you do in the file system. |
| **$MFT** | Short form of **Master File Table**. The index of NTFS, having information of all the files that are present in the volume. Each volume has its own MFT, which is mapped to all the files in the volume with the location of cluster, starting point of the file, checksums etc. All this will be discussed in necxt blog.|
| **$MFTMirr** | Mirror file of $MFT first 4 records, like a backup of $MFT, $MFTMirr, $LogFile and $Volume.|
| **$Secure** | Each file has its own ACL in the file system, be it any mp4 file, mp3 file, image file, txt file or anything. The identical ACLs of the files are stored in this $Secure file to reduce the overhead.|
| **$UpCase**  | It's always of 128 KB in size. Having the uppercase letters. Basic purpose of this file is to sort the files according to filenames.|
| **$Volume** | Contains information related to the volume.|

These are the common NTFS files that get loaded first in the clusters to bring in the functionality of file system and maintain the record of each file that gets stored here.<br>

Why I discussed this? Because this will come handy in the discussion of next blog where I will show how we can stude the **$MFT** file and access the files from there, even we can restore the deleted file from there.

