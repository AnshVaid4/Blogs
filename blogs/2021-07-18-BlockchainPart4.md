---
title: Proof of Work
author: Ansh Vaid
date: 2021-07-18 7:10:00 +0530
categories: [Blockchain And Cryptography]
tags: [blockchain, cryptography, address, public key, private key, binary, block, probability, hash rate, difficulty, restriction, proof of work, nonce, miner, authenticity, calculations]
---

<img src="/assets/Blockchain/banner4.jpg" alt="image1" height="400" width="900"/>
<caption>Image taken from <a href="https://www.dittotrade.academy/wp-content/uploads/2019/09/Webp.net-resizeimage-640x360.jpg">here</a></caption>

---

In my last blog I discussed about the concept of double spending, UTXOs, and the other concepts related to transaction in the blockchain. In this blog I am going to discuss about the proof of work, difficulty level of the blockchain, what is it, what is its use and other questions related to it.<br>

# 1.<u>What is Proof of Work and Nonce?</u>
Blockchain has the concept in which the miners have to find the block, which contains the transactions they have confirmed. We have seen that the hash of block has some preceeding 0s in the hash. The hash is **SHA256** of the block header. SHA256 is the 256 bit hash, and in hexadecimal it is 64 characters long. Let's see the block number <a href="https://www.blockchain.com/btc/block/00000000000000000008abb7a22e8061ee620b4fc302574f3a13530e4c79a5ec">691384</a>. The hash of this block is **0x00000000000000000008abb7a22e8061ee620b4fc302574f3a13530e4c79a5ec**.<br>

![hack](/assets/Blockchain/blockhash.png)

<br>

The blockhash is having 19 preceeding 0s in the hash. To get the hash of this unique style such that it should start with 19 0s or any other depending upon the situation. This number keeps on increasing or decreasing and miners have to find the hash accordingly.<br>

This is what proof of work. The miners have to use their hardware resources like GPU, their time and electricity to find this single hash. Now you will wonder why, it's just a hash then why it will take time and hardaware resources? The answer is, when you create a hash then it take few microseconds to calculate, but when you apply such restrictions then it become somewaht difficult to calculate, and since it is a race, they have to find it as fast as possible to get the block reward.<br> 

Let's see an example:<br>
The SHA256 hash of word **Hello** is: **185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969**. And it did not take even a second to calculate.  <br>
The SHA256 hash of word **hello** is: **2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824**. This also didn't take even a second to calculate. <br>

## 1.1<u>What's The Drawback of Above Hashes?</u>
The drawback is, anyone can easily change the value in the block and find the hash quickly and then change it with newly found hash, and do the required changes in further blocks because we know that the every new block created has the hash value of previous block also, and if the hash of older block is changed the successive block hash will also change (Will discuss in detail in coming blogs). As we saw above, let's suppose that in the block **Hello** was some data in it, the hacker came and did a slight change to data and new data is **hello**. The attacker can find the new hash very quickly and add it to the block, and no one will get to know, and successive block hashes will also change automatically because the hash of this block got changed. **No one will ever get to know that an attacker changed something in any of the blocks, because there is no restriction**.<br>
Now let's add the restriction that the hash should start with atleast one 0. The hash of **Hello** is **185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969**, this will only change when we add some string or we change something in the string **Hello**. That some string which is added is called **nonce** which is the number. Yeah letters can also be used but blockchain concensus uses only the numeric values as nonce.<br>

|String|SHA256 Hash|
|-|-|
|0Hello|3573c6a611c56bfc80541dc4b3a8e631d4a014686f0c3d3cc6a74aabb177a9b9|
|1Hello|5d4934862b46d11597dd139a6948a3ef13d10cbffe8e40e0826bfcd826103a03|
|2Hello|**055e2022953918f07e9f915535d8d52795957f90a3b9680f6e198d93da74ce77**|

We found a hash starting with one 0 for the string **Hello**, the nonce is **2** in this case. This was easy because the restriction was only for one 0.<br><br>
Now let's add the restriction that the hash should start with atleast two 0s.

|String|SHA256 Hash|
|-|-|
|0Hello|3573c6a611c56bfc80541dc4b3a8e631d4a014686f0c3d3cc6a74aabb177a9b9|
|1Hello|5d4934862b46d11597dd139a6948a3ef13d10cbffe8e40e0826bfcd826103a03|
|2Hello|055e2022953918f07e9f915535d8d52795957f90a3b9680f6e198d93da74ce77|
|3Hello|d40a8767d2da3c7edcb423f4bb7968d797a86c730cbf6b41ff30cb54d950c6e9|
|4Hello|1bad8475e521834caab8defd97bfed44c88a0861aabe9bd26a613a9dbb1de37f|
|8Hello|ecc644a72b42d4fc39a514fca5c690656c601899077459c6d895f187abbc4d6f|
|11Hello|90959f88ac30994851bf9093e4b166b286efb8c919ed2ccf3111cc3e617a1119|
|16Hello|2111261f7bfa52deead0d6f6d144b0f2ba136cbad4825aec709981a82721c65c|
|25Hello|49dcd54dde9120b5ef8ff7a1fe06feccae9467213a5217ff02a3a6684293dae2|
|32Hello|6cd4815ffff13d84e1c274279ebc6b56df5cf8b3f53b626dcfe9d7dc65aae7c8|
|37Hello|652b59ca0026f68aab7d7f009e40704c6775a9d27e8efd4b6c85ca99ea82ef46|
|39Hello|43b76a5a14ea5efae78eb2e58e42984ce821846ba86a0ae3607fc2f2f1f50052|
|44Hello|118fd78c91c895f37ff0a342ddfb7f2856e279b0571bb729d3edfd6d6a05a81d|
|47Hello|07c2cec043a59669b8f634bcf53668fd332e0cb24f8dab8f505444fa7d0cbd8f|
|52Hello|45a4a26b4f09ad61116e05ad141f9f3076da1fd2595c53611c5644df27fa5a88|
|56Hello|210e653d1f8c7fc81115b65e9185eb3a15ec6f53c9069dbaefe2b667144387d1|
|58Hello|3b5902d144f1de20b5bdbf3716e3925e15b3299d6d511cc62fe979c69c9f7d6d|
|60Hello|36a13df5ef581a31f5f5b0a666277d0da00b8cc207234fcc31589d726095d39e|
|62Hello|1a6f452bf08ec1016d036b1d1ef7c3517106499b0ad3797c808a23644592b85a|
|66Hello|bd5aead4ac20f3c46f0e3a5f6ffc4d008f897baa3be2e5a34d87aa6a4d33be25|
|69Hello|d9991210cc0c2aa72c629a1b2b77debbb0f35d13b0b92af7d9b1c897eba71741|
|73Hello|5fb35fb73f1a22af478a7513f65b49fc6f35ed4e108d078dcc4c6953713206a6|
|75Hello|301474aaec58d407a7639c2c5f41315c19ab2ffbd7ef14846057b5973584869e|
|79Hello|269796e333567492368fb296466e8a30103561a96ada78878b75d2c8d8817163|
|82Hello|362978895d779a01fb0a0a71030a8cffe1d9fd6470bc2e6ea0105198d35b681c|
|84Hello|68934dd54f8fb39bbc40a2527c8de4c887b0b7168750d44bfc830394c3f06fd5|
|88Hello|2c9541f8255e7deb6ff56a695cf67c866984e43d8c4edb0b0a216f768520b2ba|
|94Hello|4e55008223bd88bf8df4642bd5bf6d8fcd4af3540125603209051b25a029c9c2|
|97Hello|9952f54ed1dc6ee6dc144798ce97cc28c7c1fdfd969f5262c6a937fc7fade53e|
|100Hello|fc420141671b9ec7a8e4995c8c55966cf389b567066600a17c064e29946d5d70|
|107Hello|5f2ce50647d48922896666caffe03fc706a37f659381832a83a106393bb8da67|
|111Hello|e7010833d041bdb0f12b808cc90c77a27e0a1d3b6ecfcfe97e93c02fa2f97bea|
|119Hello|140d9e7f2dc6f561df0a5114fc60115d27297015d7fe4d598599d0ad2f6d4149|
|122Hello|9be8d404067a3d17e8f895acdf1dc855d406d15249d6b5d61d37884b912d5fbb|
|126Hello|4f0a79beb31cf1c1bf28e346cc9b0c643e2fe154d86b9434d0a5274ab0b35845|
|128Hello|0969f2767879a5bc528987266532b0ef32679eff80a0aefac0895b0d88b27011|
|130Hello|1743d356db209a1caa5cf8c52fe5541099fdde88d31cebaec79682df364a34d5|
|136Hello|ea83e6c50dd3b464d679264300f810163651c7b3374e5158d8ddc4a4bab673f4|
|137Hello|34d43fece89b4dff57cebb297e60d16477ad4c9f797036f07514d1a75afdc9c0|
|138Hello|**00bb645c75727a5e63a9d91d1230dd314697673a66530c445081a1cc81b43219**|

<br>

Finally got the hash starting with two 0s, with nonce **138** and hash **00bb645c75727a5e63a9d91d1230dd314697673a66530c445081a1cc81b43219**. On increasing the number of zeroes in the beginning of the hash you saw that I had to iterate more to get the desired hash, therefore the difficulty increased on increasing the number of zeroes. Now imagine the difficulty of nineteen 0s. To get the desired hash you use your resources, time and electricity; that's why it is called proof of work. I will discuss how it is secured enough to use in blockchain.

# 2.<u>Why it Becomes Difficult on Increasing 0s in the Beginning?</u>
SHA256 is of 256 bits OR 64 hexadecimal characters. In normal scenario when there is no restriction then the hash value lies in the range of **0000000000000000000000000000000000000000000000000000000000000000** and **ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff** in hexadecimal, i.e. from **0** to **115792089237316195423570985008687907853269984665640564039457584007913129639935** in decimal. You can see that it's a huge range and it will be easy task to find in this big range. <br>
When I applied the restriction that the hash should start with one 0, then the range lies in **0000000000000000000000000000000000000000000000000000000000000000** and **0fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff** (hash target) in hexadecimal, i.e. from **0** to **7237005577332262213973186563042994240829374041602535252466099000494570602495**, you can see that the range decreased.<br>
When I applied the restriction that the hash should start with two 0, then the range lies in **0000000000000000000000000000000000000000000000000000000000000000** and **00ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff** (hash target) in hexadecimal, i.e. from **0** to **452312848583266388373324160190187140051835877600158453279131187530910662655**, you can see that the range decreased again.<br>

## 2.1<u>What Did You Infer From Above Example?</u>
The outcome from the above scenarios is, as you aply the restriction and increase the number of 0s in the beginning of the hash, the range/band of values decrease, and you are working on more specific value within the range. As you decrease the range your time of finding that specific hash will increase because you are left with some specific hash values w.r.t. the nonce you choose. Also one more thing to note is, if the restriction is to find a hash with ten 0s in the beginning, and you found a hash with more number of zeroes (greater than 10) in the beginning of the hash, then alsoit is acceptable, because it will be lying in the same range that was defined by ten 0s in the beginning, but the chance are very less that this thing will happen. See the nonce of <a href="https://www.blockchain.com/btc/block/00000000000000000008abb7a22e8061ee620b4fc302574f3a13530e4c79a5ec">691384</a> block in below snapshot for generating a hash with nineteen 0s.<br>

![hack](/assets/Blockchain/nonce.png)

<br>

## 2.2<u>Calculation of Probability and Average Hashes Generated</u>
Let's take an example, the target hash is **0000ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff** in hexadecimal OR **1766847064778384329583297500742918515827483896875618958121606201292619775** (Favurable Outcme) in decimal. And we know that total hashes that could be generated are **ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff** in hexadecimal OR **115792089237316195423570985008687907853269984665640564039457584007913129639935** (Total Outcome) in decimal.<br>
Probability = (Favourable Outcomes)/(Total Outcomes)<br><br>
=>1766847064778384329583297500742918515827483896875618958121606201292619775/115792089237316195423<br>570985008687907853269984665640564039457584007913129639935<br>
=>0.000015<br>
=>1.5 x 10<sup>-5</sup><br><br>

**Average hashes to solve a block**<br>
=>115792089237316195423570985008687907853269984665640564039457584007913129639935/17668470647783843<br>29583297500742918515827483896875618958121606201292619775<br>
=>65,536 hashes to solve a block<br>
=>Now suppose your PC generates 1000 hashes/sec then solve 65536/1000 to get the time to solve a block by your PC<br>

# 3.<u>Rule and Formula of Difficulty</u>
The difficulty of the blockchain changes after every 2160 blocks, approx. 2 weeks. This is the rule that the new hash produced cannot be more than the 4 times of previous difficulty and cannot go down below 25% of previous difficulty. The concept of difficuly was introduced in the blockchain, so that the average time to find a block hash is 10 mins. If miners are taking more time to find the hash of the block (and this continues for most of the blocks out of 2160 blocks), then the new difficulty will be less than the present one, or if the miners are finding the block hash very frequently, less than 10 mins time (and this continues for most of the blocks out of 2160 blocks) then the new difficulty will be more than the present difficulty.<r>

**Formula for adjusting hash target:**<br>
*New Hash Target =  (Current Hash Target) x (Average time to generate last 2016 blocks)/10* <br>
If **Average time to generate last 2016 blocks** is less than 10 mins then the value of **New Hash Target** will be less that current other wise it will increase.

<br>
<br>

**Formula to find the difficulty:**<br>
*Difficulty = (Genesis block hash target)/(Current block hash target)*

<br>

In this blog I have discussed about the concept of proof of work, nonce, difficulty, range of hash values and some calculations. In my next blog I will discuss about the merkle tree and related concepts.