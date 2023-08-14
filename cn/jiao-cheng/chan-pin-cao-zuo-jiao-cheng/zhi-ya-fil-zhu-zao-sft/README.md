# 质押 FIL 到封装节点

&#x20;     SFT协议通过引入一种自动化的质押铸造机制，大大提升了资产管理的便利性。用户可以直接将FIL代币质押到指定节点，系统会自动以1:1的比例铸造出SFT。这一设计使SFT不仅是FIL持有者的算力凭证，也是收益权的象征。这种情况下，用户持有的SFT可以进行转移，收益权随之转移。同时，用户可以通过赎回界面随时进行实时赎回FIL操作，确保其资产流动性。

<figure><img src="../../../.gitbook/assets/SFT协议V2版本简介-2 (2).jpg" alt=""><figcaption></figcaption></figure>

#### 在Filecoin-FVM链上，在原来的铸造，质押功能基础上，新增以下功能：

1、FIL流动性池提供，流动池赎回；

2、FIL流动池订单借贷，还款；

3、SFT->FIL赎回池；

#### 在BSC链上，目前只能进行铸造SFT，农场SFT质押。

当前的V2版本，只支持FVM链的FIL赎回、FIL借贷、FIL提供等，BSC的用户想要参与到这些功能当中，需要进行跨链操作，用户需要将SFT从BSC跨链到FVM上面，来实现赎回，借贷等功能。

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>



#### SFT在FVM、BSC上，具有相同的收益权。FVM上的地址，获得的是FVM上的FIL奖励。BSC上，获得的是BSC上的FIL奖励。

\
