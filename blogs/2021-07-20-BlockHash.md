---
title: Block Hash
author: Ansh Vaid
date: 2021-07-20 7:10:00 +0530
categories: [Blockchain And Cryptography]
tags: [blockchain, integrity, merkle tree, root, block headers, timestamp, version, previous block hash, bits, nonce]
---

<img src="/assets/Blockchain/banner5.jpg" alt="image1" height="400" width="900"/>
<caption>Image taken from <a href="https://img.etimg.com/thumb/msid-81993233,width-650,imgsize-753834,,resizemode-4,quality-100/blockchain-getty.jpg">here</a></caption>

---

In my last blog, I discussed about the concept of proof of work, nonce, difficulty, range of hash values and some calculations which finalizes the difficulty level. In this blog I am going to discuss about the block hash, various block headers specifically about the Bitcoin Blockchain.<br>

# 1. <u>What is a Block Hash</u>
A block hash is a unique hash of the block to maintain the integrity of the data stored in the block. Yeah, you got it right, it is the one for which miners are competing to find a specific hash starting with 19 zeroes or 20 zeroes or any number of zeroes in the beginning of the hash, to get the block reward. The picture below is the <a href="https://www.blockchain.com/btc/block/00000000000000000008a89e854d57e5667df88f1cdef6fde2fbca1de5b639ad"><b>Block 691719</b></a> and its block hash is highlighted in red.<br>

![hack](/assets/Blockchain/hashblock.PNG)

<br>
<br>

# 2. <u>Block Headers</u>
To get the block hash the miners have to combine the block headers to get the particular hash starting with some zeroes. Actualy miners don't have to combine, all this is the backend process of mining software, but you should be knowing this. Following are the block headers which are combined to get a block hash:<br>
<ol>
<li><b>Block Version</b></li>
<li><b>Previous Block Hash</b></li>
<li><b>Merkle Root</b></li>
<li><b>Timestamp</b></li>
<li><b>Bits</b></li>
<li><b>Nonce</b></li>
</ol>
<br>

All the above six elements combine in order to get the block hash. **BUT** there is one header in the above list which is dynamic, which plays a ain role in finding the block hash, and that is **Nonce**. Nonce is the number (just a number) that miners add in the block header, in order to get the hash starting with specific number of 0s. Without this, it would be very easy for people to create a hash of the block, or also do some changes in the block and no one would have got to know that a change was done in the blockchain. I have discussed nonce in my previous blog. Here is the <a href="https://blog.vulnfreak.org/2021-07-18-BlockchainPart4/#:~:text=34d43fece89b4dff57cebb297e60d16477ad4c9f797036f07514d1a75afdc9c0-,138Hello,-00bb645c75727a5e63a9d91d1230dd314697673a66530c445081a1cc81b43219">highlighted link</a> for the nonce in the example of my last blog. Nonce, the word was originated from *Nonsense*, which has no meaning in the block, but was added to get a specific format hash. I will talk about the merkle root in this blog, and rest headers I will discuss in upcoming blog.<br>

# 3. <u>Merkle Root</u>
There is a concept of merkle tree, which is just a tree, as seen in the subject Data Structures And Algorithms. This concept is use to store the transactions hashes so that if any changes are done in the transaction in the block, the immediately the hash of the parent node corresponding to the leaf node storing the transaction hash, will chage, which will consequently change the hash of merkle root. This helps to identify in which transaction the change was done, rather than traversing the whole tree. There is one special thing in this is, there are always two children of parent node, if somehow there is a single child of a parent node then it gets replicated and this is how that parent gets its two children.<br>
**Now the question is, what data is stored in the leaves?** The answer is, all the hashes of a transaction are stored in the leaves of the merkle tree. Let's see with the below picture:<br>

![hack](/assets/Blockchain/tx1.png)
![hack](/assets/Blockchain/tx2.png)
![hack](/assets/Blockchain/tx3.png)

<br>

The above snaps are first few transactions of the <a href="https://www.blockchain.com/btc/block/00000000000000000008a89e854d57e5667df88f1cdef6fde2fbca1de5b639ad"><b>block 691719</b></a>, you can see the whole list of transactions there in the block. The highlighted hash is the transaction hash, which is stored in the leaves of merkle tree. The leaves have the transaction hash and their corresponding parent nodes store the hash calculated from the hashes of their children. Let's see with below diagram:<br>

![hack](/assets/Blockchain/merkletree.png)
<caption>Image taken from <a href="https://tutorialsdiary.com/wp-content/uploads/2018/10/Merkle_Tree_In_Blockchain.png">here</a></caption>

<br>

In the above picture, **T(A) T(B) T(C) T(D)** are the transaction stored in a block, **H(A) H(B) H(C) H(D)** are their respective hashes of transactions just like I have highlighted above for block 691719 transactions in red. **H(AB)** and **H(CD)** are the hashes calculated by combining the hashes of **H(A) H(B)** and **H(C) H(D)** respectively. And **H(ABCD)** is the hash found by combining the hashes of **H(AB)** and **H(CD)**, which is also the merkle root.<br>
If suppose you change something in transaction C or **T(C)**, then the hash **H(C)** will automatically change and therefore the hash **H(CD)** will change and therefore the hash **H(ABCD)** will get changed just like a chain reaction, and since the hash **H(ABCD)** is the merkle root, and used in the formation of block hash, the block hash will eventually change. On investigation, you can get the path of transaction whose value got changed with the help of another copy of ledger (blockchain database) which is stored with some other person, and you can revert that back. That's why this merkle root is being used in block header for the creation of the block hash.

# 4. <u>Closer Look at Block Headers</u>
Let's see the block headers with the help of snaps. The below snaps are from the <a href="https://www.blockchain.com/btc/block/2021"><b>block 2021</b></a> and the snap of **previous block hash** is from <a href="https://www.blockchain.com/btc/block/2020"><b>block 2020</b></a> because the previous block for block 2021 will be block 2020, and so is the block hash.<br>

## 4.1 <u>Block Version</u>
![hack](/assets/Blockchain/version.png)

<br>
<br>

## 4.2 <u>Previous Block Hash</u>
![hack](/assets/Blockchain/prevblockhash.png)

<br>
<br>

## 4.3 <u>Merkle Root</u>
![hack](/assets/Blockchain/merkleroot.png)

<br>
<br>

## 4.4 <u>Timestamp</u>
![hack](/assets/Blockchain/timestamp.png)

<br>
<br>

## 4.5 <u>Bits</u>
![hack](/assets/Blockchain/bits.png)

<br>
<br>

## 4.6 <u>Nonce</u>
![hack](/assets/Blockchain/nonce2.png)

<br>

In this blog I have discussed about the concept of block headers, need of block headers, concept of merkle tree, need of merkle root in block header and nonce again. In next blog I will be discussing other concepts related to block header and other block header parts which were not discussed in this blog.


