---
title: Let's Start With Blockchain
author: Ansh Vaid
date: 2021-06-19 7:10:00 +0530
categories: [Blockchain And Cryptography]
tags: [blockchain, nodes, cryptography, hash, hashing, bitcoin, ethereum, dogecoin, decentralized, centralized]
---

<img src="/assets/Blockchain/banner1.jpg" alt="image1" height="400" width="900"/>
<caption>Image taken from <a href="https://static.bangkokpost.com/media/content/20210430/c1_2108411_210430122446.jpg">here</a></caption>

---

Till now I have various concepts of ethical hacking such as **how to start with it**, different steps in ethical hacking like **footprinting, scanning, enumeration, breaking passwords, clearing logs** ; also I have discussed the attacks like **how hackers hack your android or pc or how they do MITM or DOS attack** and have also discussed various concepts of **Cyber Forensics** in last blogs.  <br>
But now since we have got the idea of cryptography and the use of encryption, we should start with the concept of blockchain, a field which has derived from the concept of cryptography. It is not at all difficult as it looks like. You should be familiar with the concept of cryptography.<br><br>


# 1.<u>Why Blockchain?</u>
This whole concept was discovered by a person named **Satoshi Nakamoto**, which he implemented in **Bitcoin**. In the present world(without blockchain) evrything is centralized. With the term **centralized**, I mean that the data is stored in one place, there is one body governing it which has some people who have the rights to access the database of banking transactions. Every time you make a transaction, the process will involve that central body where the money in front of your name/account number. Let's see this visually:<br>

``` code

     __________                          ____________                          _______________________________________                                                 
    |          |                        |            |    Request goes to     | Names     | Old Balance | New Balance |                                  
    | You want |     You open the       | You make a |    web server to do    |           |             |             |                       
    | to send  |  =================>    | payment of |  ===================>  | Ramesh    |   80$+20$   |    100$     |                                         
    |  20$ to  |    bank's website      |   20$ to   |    changes in both     | Nitin     |     60$     |     60$     |                                     
    |  Ramesh  |                        |   Ramesh   |       accounts         | Your name |   20$-20$   |     0$      |                                        
    |__________|                        |____________|                        |___________|_____________|_____________|  

    Your Motive                        Your Transaction                      Processing in database at centralized server                    

```

<br>

The database will get updated, which means the transaction is successfull. **If** the transaction was unsuccessfull due to some technical error, then that centralized body will be responsible to roll back to the old state. Or you can file a complain against the company who is providing the banking service. You are not responsible for the technical error that occured because there is a central body who is having the control on the service. It is the responsibility of the cenral body to provide the best services, to keep the data safe and to have a secured communicaton.<br>
But this is not the case in **Blockchain**. Blockchain is not controlled by any central body, infact there is no concept of centralized server. The nodes/computers which are the part of blockchain are itself the server, i.e. they have the information of all the customers who are using the service, stored in their devices in the form of ledger. Ledger is simply the database in blockchain. All the information related to the customer using the respective blockchain service is stored in a ledger, and the ledger is stored in all the nodes/computers that are the part of that blockchain service.<br>
So the difference is, the data that was being stored in a particular server, was now being distributed to all the nodes/computers that are the part of blockchain network. **The centralized data has shifted to decentralized data.** Let's discuss the concept of blockchain in terms of banking sector. The **cryptocurrencies** are the new currencies in blockcain network. Such as **Bitcoin, Ethereum, Dogecoin etc.**<br>
Now you would have a question that, in banking system, the companies providing the service first verify and validate whether the person doing a transaction is a genuine or not, how it is done in blockchain? The answer is simple, all the nodes that take part in blockchain, do the verification process, so that the person doing the transation is genuine and has sufficient balance for transaction. Every node don't have the sufficient hardware rsources to verify the transaction and create a block(this will be discussed later), so the nodes that can do this easily are called **MINERS**.<br>
<br>

# 2.<u>What Is Blockchain?</u>
As the name suggests, **A chain of blocks**. Similar to the concept of linked list data structure, where one node contains the address of second node and second node contains the address of third node, in the same way in blockchain, one block contains the address of another block, as well as the same block contains the address of previous block. It is not actually the address, you will find what is it in upcoming blogs of blockchain. The block as a whole contains the transactons that a person has done, it might be a single transaction or it might be 10,20,50,1000,20000..... transactions. The average size of block is 1MB and can grow upto 8MB. Every block in the blockchain has a block number and a hash of all the data that is stored in the block, including the transactions and the header.
<br>

## 2.1<u>How Is Blockchain Benificial</u>
The blockchain is in boost nowadays, and the blockchain can be of anything till the time it is decentralized. The blockchain of Bitcoin and blockchain of Ethereum are totally differet and so is with Dogecoin, though they use the same concept of blockchain. The nodes that partcipate in the blockchain of Bitcoin cannot access the ledgers of the Ethereum. It is another thing if you are a part of both the blockchains because you have a great hardware installation. The characteristics due to which it is in great demand are:
<ol>
<li><b><u>Immutability</u>:</b> The data ones entered in a block cannot be changed/altered/modified again.</li>
<li><b><u>Decentralized</u>:</b> It has no governing body, therefore no high charges to be withdrwn from people as a service charge. Infact the nodes maintain the whole network.</li>
<li><b><u>Secured</u>:</b> Each data in the blockchain is encrypted and due to the <b>immutability</b> characteristiic no one can change the data.</li>
<li><b><u>Transparancy</u>:</b> Everything is public in blockchain, if something malicious happens then everyone gets know the modified data, which is then restored with the help of copy of ledger of some other node.</li>
<li><b><u>Consensus</u>:</b> It is a protocol that all nodes have to fllow in a network, related to decision making in a scenario.</li>
<li><b><u>Fatster Settlements</u>:</b> In centralized scenario if something goes wrong in transaction then it takes lot of days to decide where the actual transaction is. But this is not there in blockchain, ones you made the transaction it will be received by other party.</li>
</ol>

<br>
<br>

I discussed the concept of blockchain in this blog, yeah it's not completed. There are many other concepts also that have to be discusse. I will be discussing them in upcoming blogs. This blog was just an introduction to the blockchain, surely there is lot more ahead.
