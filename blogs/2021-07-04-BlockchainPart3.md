---
title: Double Spending of Cryptocurrency
author: Ansh Vaid
date: 2021-07-04 7:10:00 +0530
categories: [Blockchain And Cryptography]
tags: [blockchain, cryptography, UTXO, unspent, spent, transaction, double spending, decentralized, address, public key, private key, binary, block, input, confirmed, unconfirmed, calculations]
---

<img src="/assets/Blockchain/banner3.jpg" alt="image1" height="400" width="900"/>
<caption>Image taken from <a href="https://www.tokens24.com/cryptopedia/basics/bitcoin-addresses-explained">here</a></caption>

---

In my last blog I had discussed about miners, why they do mining, what is unconfirmed transaction pool, saw different blocks and also how the block reward changes after the creation of some blocks. In this blog I am going to discuss about the concept of double spending, UTXOs, and the other concepts related to transaction in the blockchain.<br>

# 1.<u>What is Double Spending?</u>
When you have physical cash in your wallet and go to any store to buy grocery, clothes, any device etc. and after billing, the cashier gives you the total amount that you need to pay to buy that stuff. You give the whole payment in cash to the cashier and take away the stuff with you. But now is it possible that you pay the same cash, which you spent for the payment to buy stuffs, **again for buying the coke,chips etc. from the store or from any other store?** Yes, unless you steal the money from the cashier and trick him, but that's the illegal and you will surely be punnished for doing this crime. So you cannot spend the same money to buy other things which you have already spent.<br>

This is the scenario of double spending, where a person is using the same money to pay more than one parties. This problem in banking has to be resolved, otherwise the value of the money will decrease, and there would be no point of money, transactions, banking, account balance etc.<br>

In cryptocurrency, since the money is digital, so it would be more easy for a person to duplicate the transaction and do double spending. But Satoshi Nakamoto thought about this problem during the creation of bitcoin, and resolved it by introducing the concept of **verification and confirmation** of transaction and adding **timestamps** to the transaction. In bitcoin consensus (agreement followed by each node in respective blockchain), the transaction should have at least 6 confirmations to gain the trust that it is genuine. Suppose you have 3 BTCs, and you spent 2.5 BTCs to two different wallet addresses (wallet address is same as account number of the benificiary), the transactions will go to the unconfirmed transaction pool, which I discussed in last blog. The miner wil confirm the first transaction, and since it is valid it will be added to the block, and now it just needs 6 confirmations to make this transaction happen. The second transaction which was still present in unconfirmed transaction pool, suppose the second miner takes out for confirmation, but it will be found that the transaction is invalid this time.<br>

Why invalid this time? This is the main question. This is because every bitcoin when transferred from one bitcoin wallet (sender's account) to other bitcoin wallet (receiver's account), then the ownership of those certain bitcoins will change to the receiver's wallet. **Each cryptocurrency in blockchain is having a chain of ownership.** So in the second time the transaction of the sender trying to double spend the same amount to second party got invalid because during the transaction verifiaction it was found that the owner of those BTCs was someone else.<br>

The second case is, if both thetransactions are confirmed at the same time from the unconfirmed transaction pool, then in that case the two blocks will be formed in the blockchain. Yes, the blockchan splits for a while. So now the **longest chain rule** will apply, which says, among the two branches, the chain which will be the longest, i.e. the other blocks will keep on adding in blockchain, so they will also be added it one of the two branches. So one of the branch will be longer than other branch, and that longer branch will be permanent in the blockchain, and the shorter branch will be excluded. The branch should reach to the 6 blocks to become permanent. **It is not possible that both the branches will have same size**. The shorter branch is removed once the blockchain gets its permanent branch. The transactions of the removed branch again go to the unconfirmed pool of transactions or it depends on consensus what will happen.<br>
In last blog I told that as soon as miner confirms the transaction and adds it to block, the transaction happens from the sender's wallet to receiver's wallet. Just because I wanted to introduce the concept to you. But the actual transaction happens when it get minimum 6 confirmations, i.e. after the block in which the transaction is added, there must be at least 6 blocks to have a successfull and genuine transaction. Why? I just discussed in above paragraphs. Also sometimes it depends on wallet, how much confirmation it needs to have a successfull transaction<br>

The below snapshot shows the block numbers and their time of discovery in bitcoin blockchain. The block **689462** was found before the block **689467**. Hence the block **689462** has got the 6 confirmations, and since the block **689467** is the latest block, it has only one confirmation.<br>

<br>

![hack](/assets/Blockchain/latestblocks.PNG)

<br>

The below snapshot shows the block **689462** which has got 6 confirmations, and is more trustworthy than **689467**.<br>


![hack](/assets/Blockchain/success.png)

<br>

The below snapshot shows the block **689467**. So it is not trustful, once it gets 6 more block added, the transactions of the block will be confirmed. It totally depends on wallets, some wallets need 3 confirmations, some needs 2 confirmations, and the transactions of large amounts sometimes need 15 confirmations also.<br>


![hack](/assets/Blockchain/unconfirmed.png)

# 2.<u>What is UTXO?</u>
UTXO is Unspent Transaction Output, a basic element of a blockchain. Suppose you go to the supermarket to buy some snacks. You will have some money in your physical wallet. You did a shopping of 30$. The cashier at the billing counter asks you for payment. You took out the wallet and see that you have one 50$ note. You gave that 50$ note to cashier and in return the cashier gives you the 20$ change which you keep in wallet. Fine? The total money you gave was 50$, in return you got 20$, so it can be interpreted as an equation 50$=30$+20$. 50$ you spent from your wallet, which lead to the creation of two hard cash, 30$ and 20$. LHS=RHS, the total amount created on left hand side is equal to total money created on right hand side. We can also say that 20$ were unspent. Why unspent? because you can still spend this 20$ from your wallet to buy other things, but the 30$ are spent, you cannot use them again. ALso the 50$ was your input for the transaction from your wallet, which resulted to 30$ and 20$ as output, from which you got 20$ back as another input to your wallet.<br>
Similarly in the cryptocurrency, when a transaction is done, the change you receive in return is known as **Unspent Transaction Output (UTXO)**. When you create a transaction in bitcoin, then suppose you have 0.6 BTC, 0.5 BTC,1.8 BTC, 1.5 BTC in your wallet(I have simplified the values of BTCs, in actual after decimal there are 8 digits). Yeah your wallet looks like this in backend, the bicoins from various transactions are not combined until you explicitly do it, because each of them has there own chain of owners. Your wallet hides this and displays the total to you. Now suppose you want to create the transaction of 2 BTCs, your wallet in the backend will automatically choose those **"UTXOs"** which will result to slightly more than the 2 BTCs, because transaction fees also has to be paid (all this is automatic, you just add the amount you want to pay and receiver's wallet address). So, the wallet suppose takes 1.8 BTC and 0.5 BTC for transaction, which amounts to 2.3 BTC. It will go to the unconfirmed transaction pool from which it will be added to block, the transaction fee will be given to miner and transaction will take 6 confirmations to be successfull. 2 BTCs had reached to receiver, suppose miner's fee was 0.1 BTC, so it will be paid to him automatically, now we are left with 0.2 BTC as change. If you claim then it will be reverted to your wallet, otherwise it is paid to miner. You don't need to explicitly claim because the wallet at the backend does it, these 0.2 BTCs are UTXO, which are reverted to your account, which you can use in future. Now your wallet will look like 0.6 BTC, 0.2 BTC, 1.5 BTC.<br><br>
The snapshot below shows a transaction from the sender in the left of arrow to the receivers' (receivers are marked with red boundary) addresses.<br>


![hack](/assets/Blockchain/tx.png)

<br>

In above snapshot the transaction of **2.37361032 BTC** is initiated by the sender on LHS. The transaction is splitted to 5 outputs, out of which the green boundaries addresses are the UTXO, which are reverted back to account, and the red boundaries are the actual spent, which the receiver will receive. Now have a look on blue boundary, in LHS and RHS, you will see that the actual input is not equal to the output because the transaction fee **(0.00061184)** is not subtracted in LHS. But when you subtract the transaction fee **(0.00061184)** from LHS **2.37361032 BTC**, then LHS will become equal to RHS. This concept I already discussed above, to keep track that the BTCs are not lost, LHS should be equal to RHS.<br>
<br>

# 3.<u>Will the Bitcoin Addresses Finish?</u>
Every time you do a transaction, a new wallet address of the sender as well as the receiver will get generated, this is done to provide the anonimity to the parties, and no one could track the transactions. You can still track but it will take a lot of time in mapping. So you will see that your wallet address changes every time you do a transaction, so this is the reason why it happens. In above transaction also you will see the wallet address of UTXO is not same, 1 is same and other one is different, but both are the addresses of the sender. So that's why the two UTXO have different address but ultimately going to sender. This does not means that you will not be able to use other bitcoins which you had in your wallet, because ultimately the owner of those addresses are you only. So, you have a lot of addresses in the backend but the wallet hides the complexity and shows you the recent address. Even if someone will send the bitcoin to older address, you will receive them, because you are only the owner.<br>
This arises these questions **Will the bitcoin addresses come to end soon? What if I get an address and that address is already taken? What if someone counters the same wallet address that I have and access the same coins?** Let's see some mathematical part of the bitcoin block chain.<br><br>
<ul>
<li>Each wallet address has a private key. So you generate new private keys everytime after the transaction. These are mapped in the backend of your wallet. Therefore having a new wallet address that hets generated after a transaction, and we discussed why is it done in above section.</li>
<li>Each private key is of 256 bits.</li><br>
<ul type="square">
<li>Therefore having <b>2<sup>256</sup></b> combinations.</li><br>
<li>This means you can flip a coin 256 times to get completely random private key. And people does it actually.</b><br>
<li>The private key is completely random, and is not checked whether it exists or not</li><br>
<li><b>Looks like:</b> 010101000100101000100101001001001111010101101010101010101001010000101010101010101010100<br>
10010010010010100101001010110101010100010101010100010010101001010101010100101010001001<br>
01000100101001001001111010101101010101010101001010000101011111101101001010010101101</li><br>
<li><b>2<sup>256</sup>=</b> 115792089237316195423570985008687907853269984665640564039457584007913129639936</li><br>
</ul>
<li>Each public key is of 160 bits.</li><br>
<ul type="square">
<li>Public key is generated from private key.</li><br>
<li>Public key is 160 bits</li><br>
<li>Therefore having <b>2<sup>160</sup></b> combinations, created from private key.</li><br>
<li><b>Looks like:</b> 010101000100101000100101001001001111010101101010101010101001010000101010101010101010100<br>
1001001001001010010100101011010101010001010101010001001010100101010101010</li><br>
<li><b>2<sup>160</sup>=</b> 1461501637330902918203684832716283019655932542976</li><br>
</ul>
<li>These 256 binary bits of private key and 160 binary bits of public key are converted to hexadecimal in order to process it<li><br>
<li>1 BTC = 10<sup>8</sup> satoshis. Satoshi is 0.00000001 BTC. To create 1 BTC we need 10<sup>8</sup> satoshis.</li><br>
<li>Number of blocks after which the block reward reduces is 210000</li><br>
<li>The block reward is halved every 210000 blocks, so it will be like 50+25+12.5+6.25+3.125+1.5625+.......~=100. This is done because the new bitcoins are introduced in the blockchain because of block reward.</li><br>
<li>Total reward will result to ~100</li><br>
<li>Total bitcoins ever created will be 210000 x 100 = 21 million. Total 21 million bitcoins can be created.</li><br>
<li>Therefore <b>21000000 x 10<sup>8</sup> =  2100000000000000 </b>satoshis are possible. Therefore we need maximum 2100000000000000 addresses.</li><br>
<li>But we have <b>1461501637330902918203684832716283019655932542976</b> pubic keys (which are the wallet addresses) corresponding to <b>115792089237316195423570985008687907853269984665640564039457584007913129639936</b> private keys</li><br>
<li>Probability of getting the same public key generated out of max it can be generated is N(A)/N(B), where N(A) is maximum addresses that are needed and N(B) is maximum public keys that could be generated.</li><br>
<li><b>2100000000000000/1461501637330902918203684832716283019655932542976   =  0.00000000000000000000000000000000143687830814556437936</b></li><br>
<li>Therefore probability is <b>1.436 x 10<sup>-33</sup></b> of generating the same address of bitcoin.</li><br>
<li>The probability of getting killed by a meteor for a person is <b>1.428 x 10<sup>-6</sup></b> (according to <a href="https://www.nationalgeographic.com/science/article/160209-meteorite-death-india-probability-odds">nationalgeographic.com</a>), which is much more than generating a same address of bitcoin.</li><br>
<li>Even if you keep on generating new address in your whole lifespan, still you will not reach near to the big number</li>
</ul>

<br>
<br>

In this blog I discussed the concept of double spending, UTXO, various concepts related to transactions, examples of transactions and their confirmatons, some more concepts of bitcoin and their wallets etc. I hope it was conceptual, and in easy language to explain the complex concepts. In upcoming blogs I will discuss some more concepts of blockchain and transactions.