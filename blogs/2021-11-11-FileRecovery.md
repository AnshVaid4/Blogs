---
title: How Deleted Files Are Recovered In Windows OS?
author: Ansh Vaid
date: 2021-11-11 7:10:00 +0530
categories: [Cyber Forensics]
tags: [CHFI, CyberForensics, Cyber, Forensics, StrorageDevice, Data Recovery, MS DOS, hex]

---

![hack](/assets/CyberForensics/bannerRecovery.jpg)

Image taken from <a href="https://www.provendatarecovery.com/wp-content/uploads/2020/07/What-is-Digital-Forensics-and-Why-Is-It-Important.jpg">here</a>

---

This blog is on Cyber Forensics domain, where I will discuss how is it possible to retrieve the deleted data in Windows OS. Before this if you don't know much about Cyber Forensics, you can visit my profile to read them, or visit my website https://cybergeeks.website/ to get more relatable stuffs in Cyber Security domain.
To understand how the deleted files can be retrieved in Windows OS, let's start with the basics of Windows file system, FAT (File Allocation Table) file system (this file system used File Allocation Table, therefore it was named as FAT file system), which was used in floppy disks and other storage media in earlier Windows versions like Windows NT, DOS, Windows XP, Windows 2000 etc.. because the similar concept with little advancement is used in present file systems of Windows (like NTFS) is used, but the base concept is same.
Link for lab setup
Floppy disk file link: https://drive.google.com/file/d/1DN8aV2N2aPCQcE3RVpGkhTCeUJlb7cDj/view?usp=sharing
DOS OS VM file link: https://drive.google.com/file/d/1tg35dh1p3x_AOv7k9lZi3BqOhNdz1W-8/view?usp=sharing 
Credits for files: Udemy

---

Attach the floppy disk file Lab.vfd to DOS, and switch to A: drive using CMD. Then use dir command to list the files present in the disk. Right now it has only 2 files in the disk, as shown in below snap:

![hack](/assets/CyberForensics/DOS2.JPG)

Use diskedit command to launch the disk editor and start analyzing the files so that if there is any deleted file, then it could be recovered.
This DOS OS has the following configurations shown in the snap below:

![hack](/assets/CyberForensics/DOS1.JPG)

When a file is deleted from the FAT file system then, in the disk at the starting of the file, a hexadecimal character E5 is added and all the whole File Allocation Table(FAT) chain dedicated to that respective file is set to 0, but the data still is not deleted from the disk, just the entry from the File Allocation Table has been deleted (Refer File Allocation Table as the Index of the disk, used by the disk to refer where the file in the disk is present). 0xE5 is added to flag that file that it has been deleted and later if some new file is added on the disk, then it can replace the portion of that particular file (flagged with 0xE5). In many hex-editors 0xE5 is represented as σ (lowercase sigma).

![hack](/assets/CyberForensics/DOS3.JPG)

![hack](/assets/CyberForensics/DOS7.JPG)

σIMMYJ~1 is a deleted file in the floppy disk we attached to DOSSnap of File Allocation System of disk, showing 0s from beginning till 43, also known as FAT chainSomeone deleted the file σIMMYJ~1 as it has σ in the beginning of the filename. The size of the file is 20480 (Bytes), in short the data of the file is still not erased  because no new file have been added to the disk therefore starting cluster number of file is not 0. Other files highlighted in red are completely deleted ones because their content is not present on the disk (since their starting cluster number is 0). Let's try retrieving the content of the file manually to give you a sense how today's data retrieval tool find the deleted files on disk and help in retrieving. Following snap shows the hexadecimal representation of the deleted file.

![hack](/assets/CyberForensics/DOS5.JPG)

The name of the file is bit larger, but after deleting E5 was added to flag it a deleted fileTo start with, first I should rename the file from σIMMYJ~1 to JIMMYJ~1, i.e. removing σ from the filename. This will not retrieve the file but just a starting. Actually, σIMMYJ~1 is the short name created by file system because it cannot have the filename more than 8 bytes, and the actual name of file is JIMMY JULNGLE.

![hack](/assets/CyberForensics/DOS6.JPG)

Next step is to view the File Allocation Table of the disk. For that press Alt+O and then press 1, to view the 1st copy of FAT. There are two FAT copies, to fix the issues if one gets corrupted or to role-back. The following snap shows the FAT of the disk.

![hack](/assets/CyberForensics/DOS7.JPG)

There are two <EOF> visible, which refers to two non deleted files on the disk. Therefore I need to fit the third <EOF> somewhere before two <EOF> because the deleted file is present before the other two, as it can be seen in the snap above the previous snap.

![hack](/assets/CyberForensics/GFG.jpg)

Image taken from <a href="https://media.geeksforgeeks.org/wp-content/uploads/Contiguous-Allocation.jpg">here</a>

Earlier the files were not stored in fragmented manner, they were stored in continuous manner. Due to which the space of the disk was not utilized properly, as shown in above snap. The 5 files are stored on the disk, and File Allocation Table used to store the start and length of the file. For an example, file named mail shown in above snap is deleted, therefore the clusters numbers 19, 20, 21, 22, 23, 24 will be converted to 0, 0, 0, 0, 0, 0 in File Allocation Table, but still the data in mail is not deleted until it is overwritten. 
Same thing has to be done in our disk too, I need to recreate the index of the disk (File Allocation Table) by assigning proper cluster numbers in Sector 1 FAT for JIMMYJ~1 file. The size of the deleted file JIMMYJ~1 is 20480 bytes, sector size is 512 bytes. To get the number of clusters used by the file JIMMYJ~1 divide 20480/512 => 40. Therefore the file used 40 clusters. Till now the following information about the file which has to be retrieved is gathered:
Starting cluster of file is 2
File occupies 40 clusters

Therefore, find the cluster 2 in File Allocation Table. The below snap shows cluster 2 in File Allocation System.

![hack](/assets/CyberForensics/FAT chain.png)

![hack](/assets/CyberForensics/cluster 2.png)

The group of 0s is called FAT chain because the data of file still exist on diskSince I discussed earlier, the file is continuous, therefore the cluster 2 will link to cluster 3, cluster 3 to cluster 4, cluster 4 to cluster 5 ………….. cluster 40 to cluster 41 and then at the end <EOF>

![hack](/assets/CyberForensics/cluster 40.png)

![hack](/assets/CyberForensics/eof.png)

Cluster 40 (last cluster) pointing to cluster 41Cluster 41 is the End Of FileJust by doing this you have recovered your file, because now the clusters which were containing the data of file JIMMYJ~1 have now got their index in File Allocation Table. You just have to save the changes now.

![hack](/assets/CyberForensics/write.JPG)

Saving the changesNow exit the disk editor by using the shortcut Alt+O, then press X for exit.

![hack](/assets/CyberForensics/exit.JPG)

Alt+O, XNow I have returned back to command prompt of DOS. Again use dir command to list all the files present in the disk. And this time JIMMYJ~1 file is also displayed, i.e. the file is successfully recovered. The snap below shows the same:

![hack](/assets/CyberForensics/recovered.png)

File successfully recoveredThis blog was all about how the digital forensics can retrieve the data from any disk/drive/device. The complexity in steps varies, but that's the job of forensics experts to retrieve the deleted evidences from the devices. In my upcoming blogs on cyber forensics, I will use the same disk to show other techniques of digital forensics.
