# 🔁 SFT赎回FIL机制详情说明

<figure><img src="../.gitbook/assets/2.png" alt="" width="563"><figcaption></figcaption></figure>

持有SFT代币的用户，可以通过Farm农场界面：[https://www.sftproject.io/#/farm](https://www.sftproject.io/#/farm) 赎回功能，进行赎回FIL操作。

## **赎回池：SFT协议下的智能合约机制，实现便捷的FIL赎回** <a href="#6bb7" id="6bb7"></a>

SFT协议下的赎回池机制，作为一个关键性的组成部分，借助Filecoin Virtual Machine（FVM）为用户提供了一种便捷的FIL赎回方案。本文将深入探讨赎回池的运作方式及其背后的核心机制。

<figure><img src="https://miro.medium.com/v2/resize:fit:700/1*khwpO9-AU98mHG9k4R16qw.jpeg" alt="" height="317" width="700"><figcaption></figcaption></figure>

## **赎回池机制简述** <a href="#f346" id="f346"></a>

赎回池机制是SFT协议的核心所在，当前基于FVM构建。其主旨在于创建一个智能合约池，以满足用户将FIL从合约中赎回至其个人地址的需求。赎回池内的FIL资金主要来源于两个渠道：

* **Filecoin节点到期释放：**根据Filecoin节点和官方规则，到期时间皆为540天。节点到期后，智能合约自动将节点内的FIL移至赎回池，满足需要将FIL赎回的用户的需求。
* **Pool流动性池：**当Pool流动性池的资金利用率低于80%时，将向赎回池提供FIL流动性支持。因此，在赎回池需求激增时，流动性池会临时提供FIL，满足用户的赎回需求。

## **赎回池机制中的优先级** <a href="#6c5c" id="6c5c"></a>

在赎回池机制中，以下优先级关系值得注意：

* **流动性池支持：** Pool流动性池为赎回池提供FIL流动性，这是一种借贷行为。赎回池中的SFT将被抵押到Pool流动性池，而流动性池将获得这些SFT所带来的收益权益。
* **还款的优先级：** 当Filecoin节点释放到期的FIL时，如果此时Pool流动性池的资金利用率超过80%，首先会归还给Pool流动性池，而剩余的FIL则会用于满足排队等待赎回的用户需求。

## **链上排队等待机制的解释** <a href="#888b" id="888b"></a>

某些赎回用户需要排队等待的原因有多个：

* **节点释放周期的差异：** 不同类型的Filecoin节点具有各自不同的释放周期，且每一批次的释放数量也有所不同。这些差异源自Filecoin公链的节点规则。
* **Pool流动性资金利用率：** 当Pool流动性资金利用率高于80%，并且当前释放批次的数量已耗尽时，后续用户的赎回请求需要在链上排队等待，直至有新的资金，将会立即赎回。

## **在BSC链上的赎回操作** <a href="#ddd4" id="ddd4"></a>

<figure><img src="https://miro.medium.com/v2/resize:fit:700/0*DsDYEuwk1bPlQnyq" alt="" height="206" width="700"><figcaption></figcaption></figure>

尽管目前SFT协议2.0的赎回网络位于Filecoin的FVM上，但未来将扩展至BSC网络。对于那些在BSC网络上拥有SFT地址的用户，他们需通过SFT跨链桥将SFT转移到FVM上，然后进行赎回操作。这样赎回的FIL将代表真实的FVM上的FIL。

综上所述，赎回池机制作为SFT协议的关键组成，旨在为FIL持有者提供高效的赎回机制。通过自动释放、流动性池支持以及优先级设定，该机制旨在提升FIL赎回体验，同时在跨链操作中维护用户的权益保障。

\
