---
title: Forensics with FTK Imager Part 2
author: Ansh Vaid
date: 2021-06-09 7:10:00 +0530
categories: [Cyber Forensics]
tags: [CHFI, CyberForensics, Cyber, Forensics, StrorageDevice, FTK, PSTools, hex]
---

<img src="/assets/CyberForensics/ftk2banner.jpg" alt="image1" height="400" width="900"/>
<caption>Image taken from <a href="https://drivesaversdatarecovery.com/wp-content/uploads/2017/06/df-process2.jpg.webp">here</a></caption>

---

In my last blog I discussed the interface of FTK Imager tool and talked about various files of NTFS, a widely used tool in terms of Cyber Forensics, and also why I
like this tool is because it has so many features and yet it is a free tool. If you don't have FTK Imager tool then you can download it
from this <a href="https://marketing.accessdata.com/l/46432/2020-09-24/8l45td">link</a>. <br><br>

In this blog I am going to show how the files are indexed in **MFT** file. The various important offset numbers in **$MFT** file. Also I will show how we can combine the fragments of the file(any file mp4,mp3,.exe,.apk,.txp,.ppt etc...) and combine them to form the source file again.<br>

# 1.<u>Various offset in $MFT file</u> 
<br>

**What is offset?**
Offset is just a position of the hexadecimal values in FTK Imager. Let's see an example:

![hack](/assets/CyberForensics/ftk2_1.PNG)

The ablove snapshot is the snapshot of 1st sector of the MFT file, which is of 512 bytes. The size of the sector is always 512 bytes. The size of the cluster changes, according to what you have chosen at the time of formatting the disk(min size of a cluster is 4096 bytes, also known as allocation unit size). That we have discussed in last blog. Above snap is the **$MFT** file's 1st sector, and it will be same in everyone's disk which is having NTFS file system.

**IMPORTANT:** The $MFT file is the index file, which stores the information regarding all the files and folders in the respective volume whose $MFT file it is. And the indexing is done in the form of records. Every file of that volume is having a record in $MFT file and these records are of 1024 bytes which are sequentially stored in the sectors of the volume. Remember that this $MFT is a file, stored sequentially and not broken into fragments unlike other files. Occupies all the clusters and doesn't leave any RAM slack. 1024 bytes (2 sectors) are used to store the records as a security for if the size of file present in record increases in future then the record could be extended. <br><br>
**Now your question would be if the file is of 2GB then how its record would fit in 1024 bytes?**<br>
The answer is simple, the record of the files are stored in hexadecimal form, which sotres the address of the cluster where that particular file is stored. So if in case that 2GB file is fragmented into 4 parts, and those 4 fragments are stored in different clusters, then the record will store the address of those 4 clusters in hexadecimal format. All this I will show practically in this blog.
<br>
<br>

![hack](/assets/CyberForensics/ftk2_1.PNG)
![hack](/assets/CyberForensics/ftk2_2.PNG)
<br>

The above two snapshots show the 1024 bytes(means 2 sectors) record of the $MFT file. In $MFT file the first record is always of $MFT file. The second sector is empty bcz the there are not many files in my logical volume to have more data in the records of $MFT. But yes the record will increase to another sector if I add more files in the volume that it is unable to map within 512 bytes.
<br>
<br>

# 2.<u>Let's see the record of another file in the volume</u>
![hack](/assets/CyberForensics/ftk2_3.PNG)
![hack](/assets/CyberForensics/ftk2_4.PNG)
<br>

The above two snapshots are showing the record of one of the tools of from Microsoft **pslist.exe**. If I search for this name in FTK imager like shown below:
![hack](/assets/CyberForensics/ftk2_5.PNG)
<br>

Then there might be more than one entries, depending if this file is present in any folder or not. If the file is in folder, then definitely when you search, you will find one of the entries in the folder, because the folder is also indexed in $MFT file. So, the same name could be present in that record. But we are finding the record for this file, so make sure that at the beginning of the record of this file, there is **File0** in the beginning. As you can see in the snapshot below:
![hack](/assets/CyberForensics/ftk2_6.PNG)
<br>
<br>

Now let's see the various offsets(the position), their hexadecimal values(what hexadecimal value is present at that position) and what does it means with respect to record:

**IMPORTANT:** Offset number always starts with 0 in a record and therefore goes till 511 in a sector. Also the Hexadecimal values might be changed in you device, so take the reference from the example I am using only for this blog and use it accordingly in your device. Also one more thing that the word **Attribute** will be used much in below table, which means that the information regarding the file is stored in various sections of record. Each section shows different information regarding the file. And these sections is known as **Attributes**.<br>


## Record begins

|Sno.|Offset|Hexadecimal Value (0x)|Interpretation| Description|
|-|-|-|-|-|
|1| 4-5 | 30 00 | ![hack](/assets/CyberForensics/ftk2_7.PNG) | This means that at offset 48 (value of signed integer) the details regarding the error handling is stored|
|2| 20 | 38 | ![hack](/assets/CyberForensics/ftk2_8.PNG) | This means that the length of the first attribute is 55 offsets. From 56th offset there is the beginning of the another attribute.|
|3| 48-49 | 0D 00 | This offset is the same that we discussed in Sno. 1 | These hexadecimal values are used as checksums, means the same two hexadecimal values would be present at the end of the sector to check if there is no error in the sector.|

## New attribute started

|Sno.|Offset|Hexadecimal Value (0x)|Interpretation| Description|
|-|-|-|-|-|
|4| 56 from beginning of record| 10 00 00 00 | From 56th offset you find six following 0s.| This is the new attribute that started. |
|5| 4 in this attribute | 60 | ![hack](/assets/CyberForensics/ftk2_9.PNG) | This displays the length of this attribute from the 56th offset, i.e. the new attribute will  start from 96th offset(value of unsigned integer) from the beginning of this attribute.|
|6| 20 in this attribute | 18 | ![hack](/assets/CyberForensics/ftk2_10.PNG) | This displays that the unsigned integer value 24, means the data of this attribute begins from 24th offset from the start of this attribute.|
|7| 24 in this attribute | 00 3D 68 EF 3F 5C D7 01 -  00 5C 6D C8 64 D1 D1 01 - 70 2F 1C FB 46 5C D7 01 - 17 0D 04 0F 47 5C D7 01 | These are 4 different timestamps of the file| 1st group timestamps the creation of file in the file system, 2nd group timestamps the last modification of the file in file system, 3rd group timestamps the last access of the file, 4th group timestamps the record update date and time|

## New attribute started

|Sno.|Offset|Hexadecimal Value (0x)|Interpretation| Description|
|-|-|-|-|-|
|8| 96 from beginning of last attribute | 30 00 00 00 | From 96th offset you find six following 0s. | This is the new attribute that started, having filename and other metadata. |
|9| 4 in this attribute | 70 | ![hack](/assets/CyberForensics/ftk2_11.PNG) | This displays the length of this attribute from the 96th offset, i.e. the new attribute will  start from 112th offset(value of unsigned integer) from the beginning of the attribute.|
|10| 20 in this attribute | 18 | ![hack](/assets/CyberForensics/ftk2_10.PNG) | This displays that the unsigned integer value 24, means the data of this attribute begins from 24th offset from the start of this attribute. This attribute has the filename.|

## New attribute started

|Sno.|Offset|Hexadecimal Value (0x)|Interpretation| Description|
|-|-|-|-|-|
|11| 112 from the beginning of last attribute | 80 00 00 00|  From 112th offset you find six following 0s. | This is the new attribute that started having information about the file fragments. |
|12| 4 in this attribute | 48 | ![hack](/assets/CyberForensics/ftk2_11.PNG) | his displays that the unsigned integer value 72, means the data of this attribute begins from 72nd offset from the start of this attribute. This attribute has the filename.|
|13| 8 in this attribute | 01 | Displays if the file is resident or not | Resident file is the file whose data is completely stored in MFT record, these files are smaller in size. If the file is resident then the offset 8th in this attribute has flag 00. Non-resident files are files whose data can't be fit in MFT record, these files are bigger in size. If the file is non-resident then the offset 8th in this attribute has flag 01.|
|14| 64 in this attribute| 41 | Hexadecimal value to retrievr the cluster number and fragment size of file. | This hexadecimal value displays that the 4+1=>5 hexadecimal values following this(41) hexadecimal value stores information related to the cluster where this file is present and the total offsets from that cluster where the file chunks are present. The 1st hexadecimal value after this i.e. 2C marks the total length of data related to file in the cluster and 4 hexadecimal values following 2C i.e. AB CA EC 04 is the starting address of the cluster from the beginning of the volume.

<br>

![hack](/assets/CyberForensics/MFT.png)
![hack](/assets/CyberForensics/legends.png)

<br>
<br>

## Let's discuss the Sno. 14 of above table
```
64th offset of attribute 0x80 00 00 00 is 0x41 2C AB CA EC 04 00 00
41=> 4+1=>5 --> 5 offsets following 0x41 as the information related to cluster where
this file is present and the total offsets from that cluster where the file chunks are
present.

Which is 0x2C AB CA EC 04

Out of 0x2C AB CA EC 04
0x2C (the 1st part having group of 1 hexadecimal value)
AND
0xAB CA EC 04(2nd part having group of 4 hexadecimal values)

Remember it with this technique that if it is 0x41
then the 1st part will have only 1 hexadcimal value and 2nd part will have 4 hexadecimal values

OR if it is 0x23
then the 1st part will have only 3 hexadcimal value and 2nd part will have 3 hexadecimal values

OR if it is 0x34
then the 1st part will have only 4 hexadcimal value and 2nd part will have 3 hexadecimal values

```

<br>

In our case we have 0x41 then 1st part will have only 1 hexadcimal value(0x2C) and 2nd part will have 4 hexadecimal values(0xAB CA EC 04). From 1st part on interpretation we get 44 in unsigned integer.<br>

From 2nd part on interpretation we get 82627243 signed integer. We use signed integer for 2nd part because sometimes the file is fragmented, and the relative cluster position is given by the 2nd part. So if it is in negative then it means that the fragment of the file is present in those number of clusters before the current cluster position you are on.  If it is in positive then it means that the fragment of the file is present in those number of clusters after the current cluster position you are on.<br>

But this file is not fragmented, as it is not that large. So we have the position of only one cluster. If there were fragments, then you will again do the same step with the hexadecimal value, break the following hexadecimal values in 2 parts and so on.<br>
The value of first part is 44, but this is not the actual length, we have to convert this 44 in bytes. My cluster is of 4096 bytes. So I will multiply 4096 with 44, 4096x44=180224 bytes.<br>

From the 2nd part you infer that the starting cluster of the file is 82627243 from the beginning of the volume cluster and from 1st part you infer that 180224 bytes from that cluster position are of this file(pslist.exe).<br>

# By using the calculations how to find the file in the cluster?
Click on **NONAME[NTFS]** you will be able to see the 0th cluster and 0th sector. 
![hack](/assets/CyberForensics/ftk2_cluster0.PNG)

<br>

Click on 0th offset and press **Ctrl+S** to open **Go to sector/cluster** dialogue box. In the input box of cluster type 82627243 and press ok Then type 180224 as shown in below snapshot. Then your cursor will be positioned at the beginning of the cluster. 
![hack](/assets/CyberForensics/ftk2_cluster.PNG)

<br>
<br>

There press right click and select the option **Set selection length**. Then type 180224 as shown in below snapshot and press ok.
![hack](/assets/CyberForensics/ftk2_selectionsize.PNG)

<br>
<br>

Right Click on the selected part and select the option **Save Selection**. As shown in below snapshot:
![hack](/assets/CyberForensics/ftk2_saveselection.PNG)

<br>

Fill the **File Name** with extension. In this case I will write the name **pslist.exe** in filename, choose the path where you want to store. Press enter. The same file will be saved there. Now I can run the file through command prompt. There will be no error, cz the file is same. If your file is fragmented then save the fragments in one directory and then run the command **copy /b [fragments name separated by spaces] filename.extension**. The fragments will be combined together and the same file will be ready to use again there.


# 3.<u>Retrieving permanently deleted file from FTK Imager</u>
To retrieve the deleted file, do the following:

1. Attach the logical volume/image of any drive as evidence item.
2. From the **Evidence Tree**, open the directory from where the file got deleted.
3. Check the **File List**, you would be able to see the file marked with "cross" in front of it.
4. Right click on it and chose **Export Files** option.
5. Select the path where you want to save.
6. Click OK. The file is retrieved.

<br>
<br>

In the snapshot below the file **pslist.exe** is deleted permanently from my logical volume. Click on it and export it to retrieve.
![hack](/assets/CyberForensics/ftk2_deleted1.PNG)
![hack](/assets/CyberForensics/ftk2_deleted2.PNG)

<br>
<br>

The file can only be retrieved until you have not written anything in that volume, once you install anything in that volume the deleted file cannot be retrieved again from FTK Imager.

