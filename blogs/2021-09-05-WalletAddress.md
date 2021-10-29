---
title: Cryptography Behind Bitcoin Wallet
author: Ansh Vaid
date: 2021-09-05 7:10:00 +0530
categories: [Blockchain And Cryptography]
tags: [blockchain, integrity, digital, wallet, python program, bitcoin, checksum, ecc, secp256k1, transactions, github]
---

<img src="/assets/Blockchain/banner7.jpg" alt="image1" height="400" width="900"/>
<caption>Image taken from <a href="https://miro.medium.com/max/1400/1*4tSEKx4KzavZZDAggIoJVA.png">here</a></caption>

---

In my last blog, I discussed about the concept of block headers, and how the hash of the block is calculated. The conceptual implementation could be found in the CTF challenge **Does A Second Matter**. If you missed the CTF then you can read the writeup at <a href="https://medium.com/vulnfreak/does-a-second-matter-10f5984e5061">https://medium.com/vulnfreak/does-a-second-matter-10f5984e5061</a>. In this blog, I am going to discuss how the wallet address in a Bitcoin blockchain could be calculated. This concept also involves a lot of cryptography.

# 1. <u>What Is Wallet Address?</u>
As we have an account number in respective banks, and if someone sends money to you, then he sends the money to your bank account number. This number is unique for you only and no one else in the world would have the same account number in the same bank. Similarly, in bitcoin transactions, if someone wants to send the bitcoins to any other person having a bitcoin account, then he has to send it to the person's wallet address. In bitcoin blockchain there is no concept of account number, rather the coins are sent to the address of a person's wallet. And since it is a digital concept, it has the implementations of public and private key. The wallet address is generated with the help of a private key, that is only known to the owner of that wallet. This private key is used to access the wallet, if it is lost by owner, then he can never spend the bitcoins present it that respective wallet. From private key, the public key is generated and from public key the wallet address is generated which is distributed to the parties who need to send you the coins. The important fact is, the process is one way only, i.e. you cannot get the private key from the public key and you cannot get the public key from the wallet address. This is the magic of mathematics.<br>

<br>
<br>

# 2. <u>How Your Wallet Address Is Calculated?</u>
Let's see the calculations step by step with the help of example:<br>
<ol>
<li>The process starts from generating a random private key of 256 bits: <b>010101010101001001010010101001010010001011101010101011010101010101010110101011010100101<br>010111010101010101010110101010101010110101010101010110101010101011010101010101010010101<br>0101001001001010101101010101010101101010101010101000101010101101010101010101010101</b></li><br>
<li>The private key is converted to hexadecimal format. In hexadecimal format, there is a pairing of 4 binary digits. Therefore, the 256 bits become 256/4 = 64 hexadecimal cahracters: <b>555252A522EAAD5556AD4ABAAAAD555AAAB555AAAA55492AD555AAAA2AB55555</b></li>
<li>This hexadecimal format is used as a private key and used to generate the public key using <b>Elliptic curve cryptography secp256k1</b> recommended parameters. To know more about this cryptography, follow the pdf (<a href="https://www.secg.org/sec2-v2.pdf">https://www.secg.org/sec2-v2.pdf</a>) which states the necessary parameters used by it during encryption.</li><br>
<li>The public key for the above private key is <b>04932867EA2D1685B4F645DD274F14677CD9F8CE7FB3B1C7A7787C661526FE39A6474481B2719C8EC95FE4A<br>920E297D83D5B4C08C83A55E69D1E2E98531EC78808</b> which contains both x and y coordinates. The prefix 04 denotes that it is uncompressed public key, therefore for further calculations the x-axis is taken, which is <b>02932867EA2D1685B4F645DD274F14677CD9F8CE7FB3B1C7A7787C661526FE39A6</b>,and the prefix 02 denotes it is compressed public key.</li><br>
<li>This public key undergoes lots of hashing, to get the wallet address. Now let's see various operations that would be done on it</li><br>
<li>Byte-wise SHA256 hashing is performed on public key. There is a difference between caracter-wise hashing and byte-wise hashing. Character wise hashig would give <b><del>b99e52a27e91ee74ad038d2d25f6821a974e34c55ba01482a55cbe2c8a50af2b</del></b> but bytewise hashing would give <b><ins>64936245d2412a249d02a35968fab260ef0ea2cb410ada695c158c09ee55d4b7</ins></b> as output.</li><br>
<li>The code to do the same is mentioned below:<br>
<script src="https://gist.github.com/AnshVaid4/a8d67c48d2e0f28fc0526913dc970757.js"></script>
</li><br>
<li>RIPEMD160 hash the output you got after byte-wise SHA256 hashing. Use the above code, and change the name of SHA256 hashing to RIPEMD160. Also change the input string in <b>pubkey</b> variable with the output of SHA256 hash. The output will come as: <b>568db6f20e28e415c8e788af37bbbd24c12d67e3</b></li><br>
<li>Now take the above output from RIPEMD160 hash and add two 0s in the beginning and then do byte-wise SHA256 hashing, and then again do byte-wise SHA256 hashing on the output you got from previous byte-wise SHA256 hashing. The output would come as: <b>3f75c800fe0be4be6a4b634797d661b580001e7b910bb4ad466bc4dc2492e019</b>.</li><br>
<li>Take the first 4 bytes from the beginning of the output you got from previous hash, i.e. <b>3f75c800</b>. Remeber it's in hexadecimal, therefore one character is a group of 4 binary numbers, that's why 8 hexadecimal characters are taken for 4 bytes.</li><br>
<li>These 8 bytes are the checksum, which are added to the end of RIPEMD160 hash having two 0s in the beginning. Therefore the hash now becomes <b>00568db6f20e28e415c8e788af37bbbd24c12d67e33f75c800</b>. This is known as 25-byte bitcoin wallet address. But this is not the actual wallet address.</li><br>
<li>Perform byte-wise Base58 encoding on it to get the wallet address. The output is: <b>18tet19jfTjbFc5NhXU8B1Cnb5Mjmoq4vs</b> which is the actual wallet address associated with the private key that we created randomly of 256 bits.</li>
</ol>

<br>
<br>

In this blog I discussed the concept behind how the wallet address in a bitcoin blockchain is created. The conceptual implementation could be found in the CTF challenge **What's My Wallet Address**. If you missed the CTF then you can read the writeup at <a href="https://medium.com/vulnfreak/whats-my-wallet-address-a8c25c8e32b1">https://medium.com/vulnfreak/whats-my-wallet-address-a8c25c8e32b1</a>. In the next blog I will discuss about some new concepts.