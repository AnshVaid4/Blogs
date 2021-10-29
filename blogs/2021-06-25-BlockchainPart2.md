---
title: Understanding The Concepts Of Blockchain
author: Ansh Vaid
date: 2021-06-25 7:10:00 +0530
categories: [Blockchain And Cryptography]
tags: [blockchain, cryptography, hash, hashing, bitcoin, ethereum, dogecoin, decentralized, centralized, miners, fee, reward, block, block0, confirmed, unconfirmed]
---

<img src="/assets/Blockchain/banner2.jpg" alt="image1" height="400" width="900"/>
<caption>Image taken from <a href="https://www.finance-monthly.com/2019/08/the-top-3-cryptocurrencies-what-makes-them-a-success/">here</a></caption>

---

In my last blog I had discussed the idea of cryptography and the use of encryption, the concept of blockchain, a field which has derived from the concept of cryptography. Analogy of normal bank transaction and the bitcoin transaction, how it is different and why is it proposed to use a decentralized cryptocurrency instead of a centralized banking system.<br>
In this blog I am going to discuss other concepts of bitcoin blockchain. One important thing is, bitcoin blockchain is totally different from ethereum blockchain. Though the concept used is of blockchain but the implementation of transaction and verificaiton of that transaction is different. So firstly I will finish the discussion on bitcoin blockchain in this and upcoming blogs, then I will discuss the ethereum blockchain.<br>

# 1.<u>How Blockchain Is Transparent</u>
In blockchain everything which is being stored in the form of cryptographic methods. Cryptography involves hashing and encryption. These two terms are different from each other. Hashing is one way crytography and encryption involves both encryption and decryption. Blockchain uses asymytric type of encrption which involves two different keys, public and private key. All this is used to digitally prove your identity by digitally signing the transaction. That's why it is transparent. You can easily see all the transactions that are being validated in the blockchain explorer <a href="https://blockchain.com/explorer">here</a>. In future explanation I will be using this website to elaborate various examples, because you will be able to see each and everything happening in real time there.<br><br>

# 2.<u>What Is Unconfirmed Transaction Pool?</u>
In cryptocurrencies, when a sender sends the money to some merchant/recepient then the transaction takes some time to be confirmed before the currency is transeferred from sender's wallet to merchant's wallet. The confirmation is done by the miner on the grounds that the sender is having desired funds or not. By the time the transaction is not confirmed, the transaction is stored in a space known as **unconfirmed transaction pool**. So, the Bitcoin will have its own unconfirmed transaction pool, Ethereum will have its own unconfirmed transaction pool, Dogecoin will have its own unconfirmed transaction pool and so on.<br>
In this pool, all the transctions that are not conirmed and have to be confirmed by the miner are present. It may be 1 transaction, 10 transaction, 100 transactions or any number of transactions that are not yet confirmed by the miner. The miner basically selects those sets of transaction which provides him more **fee reward(I will discuss in future)**. So it totally depends on miner, your transaction will be completed once it is confirmed by miner, which means that till the time the sender's amount is in unconfirmed transaction pool the sender is only the owner of that amount, but once it gets confirmed the receiver becomes the owner of that amount. The time in confirmation of transaction can take 10 mins, 20 mins, 1 hour, 2hours, 12 hours, a week or more. Till the time miner don't confirms the transaction, the money is not transferred. **BUT** there is a time limit within which it has to be confirmed, after this if still the transaction is not confirmed then the transaction is removed from the unconfirmed pool and money is not transferred from your wallet. This limited time is of 14 days, within which your transaction has to get confirmed, otherwise your amount is added again in your wallet.<br><br>

# 3.<u>Who Is Miner?</u>
I have used a word **miner** in above paragraph. What does it mean? Is it a person or a machine? such questions arise at initial stage when learning about blockchain. A miner is a person who is responsible for confirming the transactions present in the unconfirmed transaction pool. He/she creates the block, and by saying "creates" it means that miner finds the hash of the block. All the transactions that are confirmed by the miner are added by his/her block. In bitcoin the size of the bolock is 1 Mb, and it is fixed for all the blocks which are the part of bitcoin blockchain. The size is mentioned in the consensus of bitcoin blockchain, if you want to increse the size of block then it can only be done through consensus. The consensus is just like a pact that every node in the blockchain have to agree. So bitcoin has its own consensus, eterum has its own consensus. In this way the hash, which is unique to every block is found by the hacker and add the transactions to it.

<br><br>

# 4.<u>What Miners Get In Return?</u>
It is an obvious question because miners are using there computer resources to validate the transactions and add them to the block. But why are they doing so? They are doing it to get the reward that every miner is getting to solve the puzzle(I will discuss in upcoming blog) and get the hash of the block. Currently the miner is getting 6.25 BTC(**block reward**) as a reward when he/she solves the puzzle to get the hash of the block. Also the miner gets the **fee reward** which is paid by the sender in order to make the transaction.<br>
**Block reward** is changed after every 210,000 blocks, i.e. approx 4 years and remain constant throughout the period, whereas the **fee reward** depends on the amount of transaction that the sender is sending to merchant. Satoshi Nakamoto who created the Bitcoin blockchain created the first block of this blockchain, and at that time the Block reward was of 50 BTC. Refer below snapshot, which is the **Block 0**.<br>

**IMPORTANT:** The first block is **block 0** therefore the second block is **block 1**, hence the 210000th block is **block 209999**, and after 210000 block we know what happens. If not then read the above content again.<br>

![hack](/assets/Blockchain/block0.PNG)

<br>
<br>

Right after this see the **Block 209999** in the below snapshot and see the block reward.

![hack](/assets/Blockchain/block209999.png)

<br>
<br>

Now see the **Block 210000** in the below snapshot and see the block reward, it should be halved as it is the 210001th block.

![hack](/assets/Blockchain/block210000.png)

<br>
<br>

Now see the **Block 420000** in the below snapshot and see the block reward.

![hack](/assets/Blockchain/block420000.png)

<br>
<br>

Similarly find the block from where th block reward started to be 6.25 BTCs. Now suppose you have 4 BTC in bitcoin wallet, and you want to send 4BTCs to a merchant, you will unable to make the payment because the "fee" that you need to pay has also have to be paid by you. Now suppose the fee for this transaction is 0.00090000 BTC, so you have to send 4.00090000 BTC, out of which 4 BTCs will automatically be transferred to the merchant and 0.00090000 BTC to the miner as a fee reward once the transaction is confirmed. But since we don't have 4.00090000 BTCs in wallet, the transaction cannot be initiated. You don't need to worry to calculate the extra fee that you need to pay during the transaction. The wallet automatically calculates the fee and adds to the total amount that you are paying to the merchant. Without fee you cannot make the transaction.<br>
We saw in above example that the transaction was unsuccessfull because we were not able to pay the fee. But now suppose instead of 4 BTC I want to make transaction of 2 BTCs. Now suppose the fee for the transaction is **0.000XXXXX** BTCs, where **X** is any number from the wallet that we have to pay as a fee for the transaction. Now the transaction will be initiated for 2.000XXXXX BTCs, and since I have sufficient funds(I have 4 BTCs in wallet), I can initiate the transaction, which will go to unconfirmed transaction pool, and if the miner confirms it then the merchant will receive the money. Below is the snapshot of transactions of <a href="https://www.blockchain.com/btc/block/0000000000000000000a2b3818afc6aa08a2490a693eff4e93c027163c6d5cec"><b>Block 688767</b></a> of Bitcoin, showng the transaction fee of every transaction that the sender had to send along with the money requested by merchant.<br><br>

![hack](/assets/Blockchain/fee.png)

<br>
<br>

In this blog I have discussed the concepts on why transaparancy is there in cryptocurrencies, what's unconfirmed transaction pool, we saw various blocks, their block reward, how does block reward gets affected, who are miners etc. I hope you got it. Now in next blog I am going to discuss the other interesting concepts of blockchains and cryptocurrencies. 
